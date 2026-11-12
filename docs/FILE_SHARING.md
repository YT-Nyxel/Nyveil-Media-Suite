# Nyveil File Sharing

Nyveil File Sharing sends one local file directly from one installation to
another. It uses WebRTC data channels for the file bytes and a small framed
JSON handshake for signaling. There are no accounts, no upload to a Nyveil
server, and no automatic opening of received files.

The page is available through the **File Sharing** navigation item and offers
two actions:

- **Datei freigeben** — share a file, display its share code and transfer status.
- **Datei empfangen** — enter a share code, inspect the preview and download.

## User flow

### Sending

1. Open **File Sharing → Datei freigeben**.
2. Choose a file and a validity period (15, 30, 60 or 120 minutes).
3. Start the share. The app hashes the file with SHA-256 first; for large files
   this can take a moment.
4. Copy the generated `NVF1-…` share code and send it to the receiver through a
   channel you trust.
5. The window shows the connection route, the number of connected receivers,
   progress and speed for each transfer. One receiver is served at a time;
   after a successful transfer the sender returns to waiting and the same code
   can be used again until it expires or is stopped.
6. **Freigabe beenden** ends the share immediately. Closing the window with
   **X** asks “Möchtest du die Freigabe wirklich beenden?” with the options
   **Freigabe beenden** and **Abbrechen**.

### Receiving

1. Open **File Sharing → Datei empfangen**.
2. Paste the share code and connect.
3. Inspect the preview: filename, extension, size, detected type and the
   SHA-256-based readiness status. The warning
   **Nicht geprüfte Datei – Download auf eigene Gefahr** is always visible.
4. Choose the save folder and press **Datei herunterladen**. Nothing is written
   before this explicit action.
5. The file is written to a hidden `.nyveil-*.part` file, verified and only then
   renamed to its final name. The success message shows the saved path. The
   file is never opened automatically.

## Security model

- **Transport encryption:** WebRTC data channels run over DTLS/SCTP. The
  application does not add its own encryption layer on top.
- **Share code as bearer credential:** the code contains a random 64-bit session
  id, a random 128-bit authorization token, the expiry time, the signaling
  endpoint and a checksum. Anyone with the code can attempt to connect while
  the share is active, so treat it like a password. It contains no file bytes.
- **Authorization:** the sender's signaling endpoint checks the session id and
  token in constant time. Unknown or modified codes receive an `unauthorized`
  error. A second simultaneous receiver is rejected as `busy`.
- **Time limit:** every share has an expiry timestamp. The sender enforces it;
  the code is also rejected if it is clearly stale. Stopping a share closes the
  listener and invalidates the code.
- **Integrity:** the SHA-256 digest is computed incrementally before sending and
  again while receiving. The transfer also carries an explicit byte count. A
  size mismatch, extra data, a missing end frame or a different digest causes
  the partial file to be deleted and the transfer to fail.
- **Filename safety:** incoming names must be a plain basename. Path separators,
  control characters, Windows device names (`CON`, `NUL`, …), trailing dots and
  spaces are rejected or sanitized. Files are always created below the selected
  destination folder; existing files are never overwritten (`name (1).ext`).
- **No auto-open:** received files are only saved.

The preview and warning exist because the receiver cannot verify the identity
or intent of the sender. WebRTC encryption protects the connection, not the
trustworthiness of the file.

## Transfer design

- 32 KiB binary messages per chunk.
- Sender-side flow control through the SCTP `bufferedAmount` (high-water 4 MiB,
  low-water 1 MiB), so a whole file is never held in memory.
- The receiver writes chunks to disk as they arrive and hashes them
  incrementally. aiortc delivers data channel messages as events; the receive
  queue has a hard 4096-message safety ceiling, after which the transfer is
  aborted instead of exhausting memory.
- A final `done`/`ack` exchange makes sure the sender knows the receiver saved
  and verified the file before the channel is closed.
- Transfer cancellation (`cancel`, `bye`) is handled as a normal control frame.

## Architecture

| Module | Responsibility |
| --- | --- |
| `app/sharing/models.py` | States, metadata, progress, user-facing errors, formatting |
| `app/sharing/share_code.py` | Base32 share code format, strict parsing, expiry checks |
| `app/sharing/security.py` | Filename sanitizing, metadata validation, SHA-256, part files |
| `app/sharing/config.py` | STUN/TURN/relay settings, environment overrides, LAN host detection |
| `app/sharing/signaling.py` | Direct TCP signaling, optional relay client and relay server |
| `app/sharing/webrtc.py` | Peer connection, data channel wait, route label, cleanup |
| `app/sharing/transfer.py` | Chunked send/receive, backpressure, control frames, verification |
| `app/sharing/sender.py` | Outgoing share lifecycle and sequential receivers |
| `app/sharing/receiver.py` | Connect, preview, explicit download |
| `app/sharing/service.py` | Dedicated asyncio thread and thread-safe event facade |
| `app/sharing_panel.py` | CustomTkinter page, sender/receiver windows, dialogs |
| `tools/signaling_relay.py` | Optional relay process for cross-network signaling |

All networking, hashing and file IO runs on a dedicated asyncio thread. The GUI
only consumes plain event dictionaries through a `queue.Queue`; it never blocks
Tk's main loop.

## Signaling and NAT traversal

### Direct mode (default)

The sender opens a TCP listener on a random port and puts its detected LAN
address and that port into the share code. This works without any external
infrastructure when both machines are on the same network and the firewall
allows the connection. For connections across the internet, the operator must
forward that port or use the relay mode.

### Relay mode

Both peers connect to a relay and exchange their SDP offer/answer through it.
The relay is included in this repository at `tools/signaling_relay.py`:

```powershell
python tools/signaling_relay.py --host 0.0.0.0 --port 8765
```

Configure both installations with the same `host:port` (UI settings,
`sharing.json`, or `NYVEIL_SIGNALING_RELAY`). The relay forwards only signaling
messages; file bytes still travel through WebRTC. It is **not** a TURN server.
The relay speaks plain framed JSON over TCP, so for internet deployment put it
behind TLS (reverse proxy), a VPN, or another protected tunnel. It stores no
rooms after both peers disconnect.

### STUN and TURN

- **STUN** is enabled by default with the public server
  `stun:stun.l.google.com:19302`. It is used to discover the public address for
  direct peer-to-peer connections. Using it contacts Google's infrastructure;
  it can be disabled in the settings, and the app works without it on a LAN.
- **TURN** is supported but **not configured by default**, because no TURN
  server or credentials are included or invented. TURN is the fallback when
  both peers are behind restrictive NAT/firewalls and no direct path exists.
  Supply your own TURN service (for example Coturn) via the connection settings
  or environment variables.

No server, domain or credential in this repository is a Nyveil-provided
service. The default STUN entry is a public third-party service.

## Configuration

Settings are stored per user:
`%APPDATA%\NyveilMediaSuite\sharing.json`

Environment variables override the file:

| Variable | Meaning |
| --- | --- |
| `NYVEIL_STUN` | Comma-separated STUN/STUNS URLs; empty disables STUN |
| `NYVEIL_TURN` | TURN/TURNS URL, e.g. `turn:turn.example.org:3478` |
| `NYVEIL_TURN_USERNAME` | TURN username |
| `NYVEIL_TURN_PASSWORD` | TURN credential |
| `NYVEIL_SIGNALING_RELAY` | Relay endpoint `host:port` |
| `NYVEIL_SHARE_HOST` | Host/IP written into the share code |

## Limits

- One active sender share and one active receiver connection per installation.
- One receiver at a time; after completion the sender accepts the next one.
- No resume/partial download support (`offset` must be 0).
- Single files only, up to 1 TiB (safety ceiling).
- No contact list, accounts, discovery, or permanent download links.
- The receiver does not verify the sender's identity; the warning is deliberate.

## Testing status

What was actually executed during development:

- `python -m unittest discover -s tests -v` — 40 tests, all passing:
  share-code round trips and tamper/truncation rejection, filename sanitizing,
  metadata validation, SHA-256 verification, part-file cleanup, chunked
  send/receive, bounded receive queue, flow-control cancellation, config
  round trips and environment overrides.
- Real WebRTC loopback integration tests on one Windows machine:
  direct TCP signaling, 1 MiB file transfer with hash equality, two sequential
  receivers, tampered same-size file rejected with no leftovers, forged token
  rejected, locally expired code rejected, relay-server signaling mode,
  stopping a share, stopping during hashing, and stopping a sender during an
  active transfer (clean teardown, error on the receiver, no `.part` file).
- An automated GUI smoke test: sender window → share code → receiver window →
  preview → explicit download → verified file, plus the X-close confirmation
  with both **Abbrechen** and **Freigabe beenden**.
- A PyInstaller build (onefile, windowed) including the aiortc/av/cryptography
  native modules; the build completed and the executable was launched for a
  startup smoke test on this Windows machine.

Not covered by automated tests, and therefore requiring a second installation
or external infrastructure before release:

- Two physical machines over a real LAN and Windows Firewall prompts.
- Internet connectivity through NAT with the default STUN server.
- An actual TURN deployment (no TURN credentials were available).
- `tools/signaling_relay.py` across two networks, including TLS/VPN setup.
- Very large files, slow disks, antivirus scanning, sleep/network changes.
- macOS/Linux behavior (the app targets Windows).
- A full sharing transfer from the packaged executable (the startup smoke test
  only proves that the bundled native modules load).

## Privacy and legal notes

- File sharing is peer-to-peer. The publisher does not operate a relay, TURN
  server, or storage service for shared files.
- The share code is a bearer credential. Anyone who has it can attempt to
  connect while the share is active; treat it like a password.
- A signaling relay or TURN server that you configure may see connection
  metadata, including IP addresses. If you operate one, you are responsible for
  securing it and for complying with applicable law.
- TURN credentials are stored locally in plain text in
  `%APPDATA%\NyveilMediaSuite\sharing.json`. Use a dedicated credential.
- Do not share files you are not allowed to share. The receiver is warned that
  files are unverified and must choose to download them; files are never opened
  automatically.
- See [PRIVACY.md](../PRIVACY.md), [TERMS.md](../TERMS.md), and
  [LEGAL.md](../LEGAL.md) for the full notices.

## Troubleshooting

- **“Der Sender ist nicht erreichbar”** — check the code, that the share is
  still active, the LAN/firewall path, and whether a relay is needed.
- **“Zeitüberschreitung beim Aufbau der Peer-Verbindung”** — a direct path could
  not be established. Configure TURN or use a reachable relay.
- **“Der SHA-256-Hash stimmt nicht überein”** — the file changed during transfer
  or was corrupted; it was deleted and must be sent again.
- **“Die Datei konnte nicht gespeichert werden”** — close programs that lock the
  target folder (antivirus, indexer, Explorer preview) and retry.
