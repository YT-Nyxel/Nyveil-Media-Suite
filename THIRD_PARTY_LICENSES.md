# Third-party licenses and distribution notes

**Nyveil Media Suite 1.0.0**  
**Last updated:** 12 November 2026

This file lists the software used to build and run Nyveil Media Suite, the licenses declared for the pinned versions, and the distribution obligations that apply to the Windows release. It is a summary; the full license texts are in the [licenses](licenses/) directory and in the installed packages.

---

## 1. Nyveil Media Suite

Nyveil Media Suite application code is Copyright © 2026 **Jason Bruns** and is licensed under the **GNU General Public License, version 3 or later (GPL-3.0-or-later)**.

- Full license: [LICENSE](LICENSE)
- GPLv3 text: [licenses/GPL-3.0.txt](licenses/GPL-3.0.txt)
- Source availability: [SOURCE_OFFER.md](SOURCE_OFFER.md)

The app is distributed as object code. The complete corresponding source for each release must be made available to recipients under GPLv3. The recommended method is to attach the source ZIP to the same GitHub release as the EXE.

---

## 2. Python dependencies

Versions are pinned in [requirements.txt](requirements.txt) and were verified in the build environment. The table includes direct and bundled transitive dependencies.

| Component | Version | Role | License / source | Distribution note |
| --- | --- | --- | --- | --- |
| [yt-dlp](https://github.com/yt-dlp/yt-dlp) | 2026.10.26 | Public media extraction/download | Unlicense | Installed wheel includes the Unlicense text. Preserve it. yt-dlp notes that some of its other release artifacts bundle components under other licenses; check the exact installed wheel if you change the version. |
| [curl-cffi](https://github.com/lexiforest/curl_cffi) | 0.17.0 | HTTP stack used by yt-dlp | MIT | Wheel bundles `libcurl-impersonate`, which includes third-party libraries (curl, TLS, HTTP/2, compression). Retain the bundled notices and the `curl_cffi.libs` license information. curl license text: [licenses/curl.txt](licenses/curl.txt). |
| [CustomTkinter](https://github.com/TomSchimansky/CustomTkinter) | 6.0.0 | Desktop widgets | MIT (wheel metadata says CC0; included `LICENSE` is MIT) | Retain the included MIT notice. Re-check if the version changes. |
| [Pillow](https://github.com/python-pillow/Pillow) | 12.3.0 | Thumbnail image handling | MIT-CMU (HPND-style) | Full text: [licenses/pillow-12.3.0-LICENSE.txt](licenses/pillow-12.3.0-LICENSE.txt). |
| [aiortc](https://github.com/aiortc/aiortc) | 1.16.0 | WebRTC peer connections and data channels | BSD-3-Clause | Full text: [licenses/aiortc-1.16.0-LICENSE.txt](licenses/aiortc-1.16.0-LICENSE.txt). |
| [PyAV](https://github.com/PyAV-Org/PyAV) / `av` | 18.1.0 | Native media bindings required by aiortc | BSD-3-Clause for PyAV itself | **The wheel bundles FFmpeg 8.1.2 libraries, including GPL `libx264` and `libx265`.** See section 3. |
| [aioice](https://github.com/aiortc/aioice) | 0.13.0 | ICE/STUN/TURN implementation | BSD-3-Clause | Full text: [licenses/aioice-0.13.0-LICENSE.txt](licenses/aioice-0.13.0-LICENSE.txt). |
| [pylibsrtp](https://github.com/aiortc/pylibsrtp) | 1.0.0 | SRTP bindings | BSD-3-Clause | Full text: [licenses/pylibsrtp-1.0.0-LICENSE.txt](licenses/pylibsrtp-1.0.0-LICENSE.txt). |
| [cryptography](https://github.com/pyca/cryptography) | 50.0.2 | DTLS/TLS primitives | Apache-2.0 OR BSD-3-Clause | Dual-licensed. Include both texts: [Apache](licenses/cryptography-50.0.2-LICENSE.APACHE.txt), [BSD](licenses/cryptography-50.0.2-LICENSE.BSD.txt). |
| [pyOpenSSL](https://github.com/pyca/pyopenssl) | 26.4.0 | TLS helper dependency of aiortc | Apache-2.0 | Full text: [licenses/pyopenssl-26.4.0-LICENSE.txt](licenses/pyopenssl-26.4.0-LICENSE.txt). |
| [pyee](https://github.com/jfhbrook/pyee) | 13.0.1 | Event emitter used by aiortc | MIT | Full text: [licenses/pyee-13.0.1-LICENSE.txt](licenses/pyee-13.0.1-LICENSE.txt). |
| [dnspython](https://github.com/rthalley/dnspython) | 2.9.2 | DNS resolution for aioice | ISC | Full text: [licenses/dnspython-2.9.2-LICENSE.txt](licenses/dnspython-2.9.2-LICENSE.txt). |
| [ifaddr](https://github.com/pydron/ifaddr) | 0.2.0 | Network interface discovery | MIT | Full text: [licenses/ifaddr-0.2.0-LICENSE.txt](licenses/ifaddr-0.2.0-LICENSE.txt). |
| [google-crc32c](https://github.com/googleapis/python-crc32c) | 1.9.0 | CRC32C native module used by aiortc | Apache-2.0 | Full text: [licenses/google-crc32c-1.9.0-LICENSE.txt](licenses/google-crc32c-1.9.0-LICENSE.txt). |
| [cffi](https://github.com/python-cffi/cffi) | 2.1.1 | C foreign-function interface | MIT-0 | Full text: [licenses/cffi-2.1.1-LICENSE.txt](licenses/cffi-2.1.1-LICENSE.txt). |
| [pycparser](https://github.com/eliben/pycparser) | 3.12 | C parser used by cffi | BSD-3-Clause | Full text: [licenses/pycparser-3.12-LICENSE.txt](licenses/pycparser-3.12-LICENSE.txt). |
| [typing-extensions](https://github.com/python/typing_extensions) | 4.16.0 | Typing backports | PSF-2.0 | Full text: [licenses/typing-extensions-4.16.0-LICENSE.txt](licenses/typing-extensions-4.16.0-LICENSE.txt). |
| [python-vlc](https://github.com/oaubert/python-vlc) | 3.0.21203 | Python bindings for the locally installed VLC runtime | LGPL-2.1-or-later | Full text: [licenses/python-vlc-3.0.21203-COPYING.txt](licenses/python-vlc-3.0.21203-COPYING.txt). VLC itself is not bundled; the user installs it separately. |
| [PyInstaller](https://pyinstaller.org/) | 6.22.3 | Build tool / bootloader | GPL-2.0-or-later with a special exception | The exception allows building and distributing non-free programs. Changes to PyInstaller itself remain subject to the GPL. Full text: [licenses/pyinstaller-6.22.3-COPYING.txt](licenses/pyinstaller-6.22.3-COPYING.txt). |
| [certifi](https://github.com/certifi/python-certifi) | 2026.10.23 | CA bundle | MPL-2.0 | Package notice: [licenses/certifi-2026.10.23-LICENSE.txt](licenses/certifi-2026.10.23-LICENSE.txt). Full MPL-2.0 text: [licenses/MPL-2.0.txt](licenses/MPL-2.0.txt). |
| [altgraph](https://github.com/altgraph/altgraph) | 0.17.5 | PyInstaller dependency | MIT | Full text: [licenses/altgraph-0.17.5-LICENSE.txt](licenses/altgraph-0.17.5-LICENSE.txt). |
| [packaging](https://github.com/pypa/packaging) | 26.3 | Version parsing | Apache-2.0 OR BSD-2-Clause | Texts: [Apache](licenses/packaging-26.3-LICENSE.APACHE.txt), [BSD](licenses/packaging-26.3-LICENSE.BSD.txt). |
| [pefile](https://github.com/erocarrera/pefile) | 2024.8.26 | PE parsing used by PyInstaller | MIT | Full text: [licenses/pefile-2024.8.26-LICENSE.txt](licenses/pefile-2024.8.26-LICENSE.txt). |
| [pywin32-ctypes](https://github.com/enthought/pywin32-ctypes) | 0.2.3 | Windows API bindings | BSD-3-Clause | Full text: [licenses/pywin32-ctypes-0.2.3-LICENSE.txt](licenses/pywin32-ctypes-0.2.3-LICENSE.txt). |
| [setuptools](https://github.com/pypa/setuptools) | 65.5.0 | Packaging runtime | MIT | Full text: [licenses/setuptools-65.5.0-LICENSE.txt](licenses/setuptools-65.5.0-LICENSE.txt). |
| [darkdetect](https://github.com/albertosottile/darkdetect) | 0.8.0 | Theme detection for CustomTkinter | BSD-3-Clause | Full text: [licenses/darkdetect-0.8.0-LICENSE.txt](licenses/darkdetect-0.8.0-LICENSE.txt). |
| [pyinstaller-hooks-contrib](https://github.com/pyinstaller/pyinstaller-hooks-contrib) | 2026.7 | PyInstaller hooks | See included license details | Full text: [licenses/pyinstaller-hooks-contrib-2026.7-LICENSE.txt](licenses/pyinstaller-hooks-contrib-2026.7-LICENSE.txt). |

If a dependency or its bundled native libraries change, re-check the licenses and update this file and the `licenses/` directory.

---

## 3. Bundled FFmpeg binaries

### 3.1 `ffmpeg/ffmpeg.exe` — FFmpeg 9.0.1 (Gyan.dev full build)

The release bundles the standalone FFmpeg executable used for merging and conversion:

- **Version:** `9.0.1-full_build-www.gyan.dev`
- **Supplier:** [Gyan.dev FFmpeg Builds](https://www.gyan.dev/ffmpeg/builds/)
- **Builder:** MSYS2 project
- **License indicated by the supplier for static builds:** GPLv3
- **SHA-256:** `57C56E369D5B4873B4D93FC1A1D833CB7CD8BC9325C14B05C34CE60B22842D8A`
- **Relevant flags:** `--enable-gpl --enable-version3 --enable-static`
- **Source:** https://ffmpeg.org/releases/ffmpeg-9.0.1.tar.xz
- **Build scripts:** https://github.com/GyanD/codexffmpeg
- **Recorded build info:** [ffmpeg/BUILD_INFO.txt](ffmpeg/BUILD_INFO.txt)

The binary is invoked as a separate process. It is not linked into the Nyveil application. It is distributed alongside the app as a separate program. The GPLv3 text and the source/build information must accompany the release. See [FFMPEG_NOTICE.md](FFMPEG_NOTICE.md) and [SOURCE_OFFER.md](SOURCE_OFFER.md).

### 3.2 PyAV wheel — FFmpeg 8.1.2 libraries (GPL codecs)

PyAV 18.1.0's Windows wheel bundles FFmpeg 8.1.2 native libraries, including:

- `libx264` (GPL)
- `libx265` (GPL)
- `libmp3lame`, `libvpx`, `libdav1d`, `libSvtAv1Enc`, `libwebp`, and others

The installed package reports:

```text
av.__version__         = 18.1.0
av.ffmpeg_version_info = 8.1.2
```

Because these libraries are loaded in the application process, the distributed app includes GPL-linked components. This is why the Nyveil application code is licensed under GPLv3. The PyAV wheel's own metadata declares BSD-3-Clause for PyAV, but that does not override the licenses of the bundled FFmpeg libraries.

- **PyAV source:** https://github.com/PyAV-Org/PyAV/tree/v18.1.0
- **PyAV license:** [licenses/pyav-18.1.0-LICENSE.txt](licenses/pyav-18.1.0-LICENSE.txt)
- **FFmpeg 8.1.2 source:** https://ffmpeg.org/releases/ffmpeg-8.1.2.tar.xz
- **FFmpeg legal information:** https://ffmpeg.org/legal.html
- **GPLv2 text:** [licenses/GPL-2.0.txt](licenses/GPL-2.0.txt)
- **GPLv3 text:** [licenses/GPL-3.0.txt](licenses/GPL-3.0.txt)
- **LGPL 2.1 text:** [licenses/LGPL-2.1.txt](licenses/LGPL-2.1.txt)

**Important:** the bundled GPL codecs may create a licensing conflict if the app were distributed under a permissive license such as MIT. Do not change the app license to MIT/Apache while the current PyAV wheel is bundled. Either keep the GPLv3 distribution and provide corresponding source, or replace PyAV with a build that uses LGPL-compatible FFmpeg libraries. Get qualified legal advice before changing this arrangement.

**GPLv2/GPLv3 compatibility caveat:** some FFmpeg codec components, including x264 and x265, are commonly offered under GPLv2 terms. GPLv2-only code can be incompatible with GPLv3 code. The Gyan.dev FFmpeg build is supplied as GPLv3, and the PyAV wheel is supplied by PyAV as a whole; nevertheless, before publishing, have a qualified lawyer confirm that the exact bundled build is GPLv3-compatible, or replace the PyAV wheel with an LGPL-only build. Do not rely on this file as a legal opinion.

---

## 4. VLC

The app's streaming tab requires a locally installed **64-bit VLC** runtime and the `python-vlc` bindings. VLC is not bundled in the Nyveil EXE; the user installs it separately.

- **python-vlc** is LGPL-2.1-or-later. Its full text is in [licenses/python-vlc-3.0.21203-COPYING.txt](licenses/python-vlc-3.0.21203-COPYING.txt).
- **VLC** itself is distributed by VideoLAN under its own licenses (LGPL-2.1-or-later for most of the core, with some components under other licenses). If you ever bundle VLC, you must include its notices and comply with its source/relinking obligations.
- Do not imply that VideoLAN endorses Nyveil.

---

## 5. Bundled native libraries and notices

The PyInstaller build bundles native libraries from PyAV, aiortc, pylibsrtp, cryptography, curl-cffi, and PyInstaller. Their Python package licenses are listed above. Some wheels also bundle third-party native code:

- **PyAV:** FFmpeg 8.1.2 and its codec libraries (see section 3.2).
- **curl-cffi:** `libcurl-impersonate` and its statically linked TLS/HTTP/compression libraries. Retain the notices shipped in the wheel; the `curl_cffi.libs` directory contains the native library.
- **pylibsrtp:** libsrtp and its dependencies.
- **cryptography:** OpenSSL and its dependencies.
- **PyInstaller:** bootloader and its notices.

The `licenses/` directory contains the exact license files shipped by the installed Python packages. It does not contain every upstream native library notice. Before publishing, inspect the wheel contents and add any missing notices. This is part of the release checklist.

---

## 6. Release procedure

1. Pin dependency versions after testing and save the dependency metadata/notices for those exact versions.
2. Include this file, [LICENSE](LICENSE), [NOTICE](NOTICE), [FFMPEG_NOTICE.md](FFMPEG_NOTICE.md), [SOURCE_OFFER.md](SOURCE_OFFER.md), [PRIVACY.md](PRIVACY.md), [TERMS.md](TERMS.md), [LEGAL.md](LEGAL.md), [SECURITY.md](SECURITY.md), [TRADEMARKS.md](TRADEMARKS.md), and the [licenses](licenses/) directory in the release archive.
3. Include the GPLv3 text, the FFmpeg source/build information, and the complete corresponding source for the app in the same release.
4. Re-check notices whenever dependencies, the FFmpeg binary, or the PyAV wheel changes.
5. Do not publish TURN credentials, personal data, or downloaded media in the source archive or repository.

---

## 7. Disclaimer

This file records technical licensing facts and release obligations. It is not legal advice. The GPL/FFmpeg/PyAV distribution model should be reviewed by a qualified lawyer before publication, especially if you change the license, bundle additional binaries, or monetise the project.
