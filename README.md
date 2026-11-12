# Nyveil Media Suite

Nyveil Media Suite is a compact Windows desktop utility for downloading publicly accessible media as MP4 or MP3 with `yt-dlp` and converting local audio/video files with FFmpeg. It is designed for legitimate creator workflows where you have the right or permission to download and use the media.

**Version:** 1.0.0  
**License:** [GPL-3.0-or-later](LICENSE) (application code)  
**Publisher:** Jason Bruns — Nyveil@web.de

## Download

Download the Windows release ZIP from the **Releases** page. The ZIP contains the executable and all legal/license notices; a bare EXE may also be provided for convenience. Every release also includes a complete source archive so the GPLv3 source-availability requirement is met. See [SOURCE_OFFER.md](SOURCE_OFFER.md) and [PUBLISHING.md](PUBLISHING.md) for the release layout.

No media files are hosted here. Nyveil is a tool; it does not provide or endorse content.

## Features

- Dark, compact desktop interface with media title and thumbnail preview
- Automatic source detection for public links
- MP4 video or MP3 audio output
- Local file converter for MP4, MKV, MOV, WebM, MP3, WAV, M4A, AAC, FLAC, and OGG
- Peer-to-peer file sharing over encrypted WebRTC data channels (share code, no account, SHA-256 verification)
- User-selected local download folder, progress, background processing, and clear errors
- Curated links for YouTube, TikTok, Instagram, SoundCloud, Vimeo, X / Twitter, Twitch, and Reddit
- No accounts, cloud storage, advertising, analytics, or telemetry

The curated list is not a compatibility guarantee. Source support depends on `yt-dlp`, public access, the platform, region, and the link itself. See the [official yt-dlp supported-sites reference](https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md).

## File sharing

The **File Sharing** tab sends a single local file directly to another
installation. A sender chooses a file and a validity period, then shares the
generated `NVF1-…` code. The receiver connects with that code, inspects the
preview, chooses a save folder and starts the download explicitly. Files are
encrypted in transit by WebRTC/DTLS, hashed with SHA-256 on both sides, and are
never opened automatically. An always-visible warning reminds the receiver that
the file is unverified.

Direct connections work on a LAN without external infrastructure. Cross-network
signaling can use the included `tools/signaling_relay.py`. Optional TURN
fallback, STUN servers, relay and advertised host can be configured in the tab's
settings or through `%APPDATA%\NyveilMediaSuite\sharing.json` and `NYVEIL_*`
environment variables. No TURN credentials or Nyveil servers are bundled. The
default STUN entry is the public `stun.l.google.com:19302` service and can be
disabled.

See [docs/FILE_SHARING.md](docs/FILE_SHARING.md) for the user flow, security
model, configuration, limits, and the exact test coverage.

## Portable Windows use

`dist\Nyveil Media Suite.exe` is a single-file, windowed build. Copy that EXE to the target machine; no separate `_internal` folder is required. No console window is shown. Windows may show SmartScreen warnings until a publisher reputation/signing process is established.

## Build from source

The complete source is in the release source archive: download `Nyveil-Media-Suite-<version>-source.zip` from the Releases page (or use this repository if you publish the source layout). Install Python 3.10+ and dependencies:

```powershell
py -m pip install -r requirements.txt
py main.py
```

The source run uses `ffmpeg/ffmpeg.exe` when present and otherwise looks for `ffmpeg` on `PATH`. The repository does not commit the 222 MB FFmpeg binary; for a release build, download the Gyan.dev 9.0.1 full build and place it at `ffmpeg/ffmpeg.exe`, or install FFmpeg on `PATH` for a source run. Build the portable executable with:

```powershell
py -m PyInstaller --noconfirm --clean main.spec
```

The output is `dist\Nyveil Media Suite.exe`. The application icon is taken from `assets/nyveil.ico`.

Run the test suite (standard library `unittest`, no extra test dependency) with:

```powershell
py -m unittest discover -s tests -v
```

The integration tests open real WebRTC connections on loopback and therefore
exercise the aiortc stack installed in the environment.

## Dependencies and licenses

The project uses yt-dlp, curl-cffi, CustomTkinter, Pillow, aiortc (with aioice, PyAV, cryptography and pylibsrtp), python-vlc, PyInstaller, and a bundled FFmpeg binary. See [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md) and [FFMPEG_NOTICE.md](FFMPEG_NOTICE.md) before distributing a release.

**GPLv3 note:** the bundled FFmpeg 9.0.1 binary is a Gyan.dev GPLv3 build. The PyAV wheel used by aiortc also bundles FFmpeg 8.1.2 libraries with GPL codecs (`libx264`, `libx265`). The application code is therefore licensed under **GPL-3.0-or-later**, and every binary release must make the complete corresponding source available. Attach the source ZIP to the same GitHub release. If you cannot do that, do not distribute the current build; replace the GPL-linked components first.

## Privacy and responsible use

The app is local-first. When you inspect or download a pasted URL, it contacts that source through yt-dlp and may load the public thumbnail returned by the source. Downloaded files are saved only to your chosen folder. Source sites and network providers may process connection data under their own policies. The app has no Nyveil server and does not intentionally write app log files.

File sharing connects two installations directly. Share codes, connection
metadata and the selected file are exchanged between the two peers; no file is
uploaded to Nyveil. Signaling is either a direct TCP connection or the relay you
configure yourself. If STUN is enabled (the default), the app contacts the
configured STUN server, which by default is `stun.l.google.com`. Disable STUN in
the connection settings if that is not acceptable. TURN, when configured, is
operated by whoever supplies its credentials. TURN credentials are stored locally in plain text in `%APPDATA%\NyveilMediaSuite\sharing.json`; use a dedicated credential.

Only download media you are allowed to download and use. Private, login-only, paywalled, access-restricted, and DRM-protected media are not supported. The app does not grant permission to infringe copyright, and platform terms can impose additional restrictions. Some platforms prohibit downloading even public content. You are responsible for complying with their terms.

Nyveil is not affiliated with, endorsed by, or sponsored by YouTube, Google, TikTok, Instagram, Meta, SoundCloud, Vimeo, X/Twitter, Twitch, Reddit, VideoLAN/VLC, FFmpeg, Gyan.dev, GitHub, or their maintainers. All names and trademarks belong to their respective owners. See [LEGAL.md](LEGAL.md) and [TRADEMARKS.md](TRADEMARKS.md).

## Legal documents

- [LEGAL.md](LEGAL.md) — publisher information, German § 5 DDG note, copyright/trademark notices, source availability, takedown contact
- [NOTICE](NOTICE) — project copyright and third-party notice summary
- [PRIVACY.md](PRIVACY.md) — privacy notice / Datenschutzhinweis
- [TERMS.md](TERMS.md) — terms of use, disclaimer, liability
- [SECURITY.md](SECURITY.md) — vulnerability reporting and security model
- [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md) — dependency licenses and release obligations
- [FFMPEG_NOTICE.md](FFMPEG_NOTICE.md) — bundled FFmpeg details and source information
- [SOURCE_OFFER.md](SOURCE_OFFER.md) — GPLv3 source availability
- [TRADEMARKS.md](TRADEMARKS.md) — name, icon, and fork policy
- [PUBLISHING.md](PUBLISHING.md) — GitHub release layout, source ZIP, and publishing steps
- [licenses/](licenses/) — full license texts
- [RELEASE_CHECKLIST.md](RELEASE_CHECKLIST.md) — release and legal checks

## Support and release contact

Bug reports, privacy requests, security reports, and takedown notices: **Nyveil@web.de**.

Do not post TURN credentials, personal data, or confidential information in a public GitHub issue. For security issues, follow [SECURITY.md](SECURITY.md).
