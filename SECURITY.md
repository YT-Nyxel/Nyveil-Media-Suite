# Security policy

## Supported versions

Security fixes are provided for the current release line:

| Version | Supported |
| --- | --- |
| 1.0.x | Yes |
| Older versions | Best effort; upgrade to the current release |

## Reporting a vulnerability

Please **do not open a public GitHub issue** for a security vulnerability.

Email **Nyveil@web.de** with the subject `Security report — Nyveil Media Suite` and include:

- the affected version and component (app, file sharing, signaling relay, build);
- a description of the issue and its potential impact;
- reproduction steps or a proof of concept;
- any relevant logs, screenshots, or files (please remove personal data and TURN credentials).

You will receive an acknowledgement on a best-effort basis. The publisher will investigate, keep you informed of the outcome, and credit you if you wish.

## Scope

In scope:

- the Nyveil application code in this repository;
- the file-sharing protocol, share-code handling, filename sanitisation, SHA-256 verification, and `.part` file handling;
- the included `tools/signaling_relay.py`;
- the packaged Windows release, where the issue is caused by Nyveil code.

Out of scope:

- vulnerabilities in `yt-dlp`, FFmpeg, VLC, PyAV, aiortc, cryptography, or other third-party components (report them upstream);
- vulnerabilities in media platforms, GitHub, STUN/TURN providers, or the user's network;
- social engineering, physical access, or issues that require an already-compromised device;
- denial-of-service attacks against third-party services;
- reports that only demonstrate that a user can share a malicious file (the receiver warning is deliberate).

## Safe harbour

The publisher will not pursue legal action for good-faith security research that:

- respects privacy and does not access, modify, or exfiltrate other people's data;
- does not disrupt the app, a relay, or a third-party service beyond what is necessary to demonstrate the issue;
- is reported privately and given reasonable time to fix before public disclosure.

This safe-harbour statement does not bind third parties or override applicable law.

## Security model and limitations

See [docs/FILE_SHARING.md](docs/FILE_SHARING.md) for the file-sharing security model. Key limitations:

- WebRTC/DTLS protects the connection, not the trustworthiness of the sender or file.
- Share codes are bearer credentials. Anyone with a code can attempt to connect while the share is active.
- TURN credentials are stored locally in plain text in `%APPDATA%\NyveilMediaSuite\sharing.json`.
- The included signaling relay speaks plain framed JSON over TCP. Put it behind TLS, a VPN, or another protected tunnel before using it across the internet.
- The receiver cannot verify the sender's identity. The app deliberately warns about unverified files and never opens them automatically.
