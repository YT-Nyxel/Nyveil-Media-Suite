# License texts

This directory contains the license texts and notices shipped with the pinned dependency versions used for Nyveil Media Suite 1.0.0, plus the GPL/LGPL texts required for the bundled FFmpeg components.

The files were copied from the installed Python packages on 12 November 2026. The GPLv2, GPLv3, LGPL-2.1, MPL-2.0, and curl texts were obtained from their official/SPDX sources.

## Core licenses

| File | Component |
| --- | --- |
| `GPL-3.0.txt` | GNU GPL v3 — Nyveil application code, Gyan.dev FFmpeg build, GPL-linked FFmpeg libraries |
| `GPL-2.0.txt` | GNU GPL v2 — PyInstaller, some FFmpeg/PyAV codec components |
| `LGPL-2.1.txt` | GNU LGPL v2.1 — python-vlc, FFmpeg libraries where applicable |
| `MPL-2.0.txt` | Mozilla Public License 2.0 — certifi |
| `curl.txt` | curl license — libcurl-impersonate bundled by curl-cffi |

## Dependency notices

| File | Package |
| --- | --- |
| `aioice-0.13.0-LICENSE.txt` | aioice 0.13.0 — BSD-3-Clause |
| `aiortc-1.16.0-LICENSE.txt` | aiortc 1.16.0 — BSD-3-Clause |
| `altgraph-0.17.5-LICENSE.txt` | altgraph 0.17.5 — MIT |
| `certifi-2026.10.23-LICENSE.txt` | certifi 2026.10.23 — MPL-2.0 notice |
| `cffi-2.1.1-LICENSE.txt` | cffi 2.1.1 — MIT-0 |
| `cryptography-50.0.2-LICENSE.txt` | cryptography 50.0.2 — dual-license notice |
| `cryptography-50.0.2-LICENSE.APACHE.txt` | cryptography — Apache-2.0 text |
| `cryptography-50.0.2-LICENSE.BSD.txt` | cryptography — BSD-3-Clause text |
| `curl-cffi-0.17.0-LICENSE.txt` | curl-cffi 0.17.0 — MIT |
| `customtkinter-6.0.0-LICENSE.txt` | CustomTkinter 6.0.0 — MIT |
| `darkdetect-0.8.0-LICENSE.txt` | darkdetect 0.8.0 — BSD-3-Clause |
| `dnspython-2.9.2-LICENSE.txt` | dnspython 2.9.2 — ISC |
| `google-crc32c-1.9.0-LICENSE.txt` | google-crc32c 1.9.0 — Apache-2.0 |
| `ifaddr-0.2.0-LICENSE.txt` | ifaddr 0.2.0 — MIT |
| `packaging-26.3-LICENSE.txt` | packaging 26.3 — dual-license notice |
| `packaging-26.3-LICENSE.APACHE.txt` | packaging — Apache-2.0 text |
| `packaging-26.3-LICENSE.BSD.txt` | packaging — BSD-2-Clause text |
| `pefile-2024.8.26-LICENSE.txt` | pefile 2024.8.26 — MIT |
| `pillow-12.3.0-LICENSE.txt` | Pillow 12.3.0 — MIT-CMU/HPND |
| `pyav-18.1.0-LICENSE.txt` | PyAV 18.1.0 — BSD-3-Clause (does not cover bundled FFmpeg) |
| `pycparser-3.12-LICENSE.txt` | pycparser 3.12 — BSD-3-Clause |
| `pyee-13.0.1-LICENSE.txt` | pyee 13.0.1 — MIT |
| `pyinstaller-6.22.3-COPYING.txt` | PyInstaller 6.22.3 — GPL-2.0-or-later with bootloader exception |
| `pyinstaller-hooks-contrib-2026.7-LICENSE.txt` | pyinstaller-hooks-contrib 2026.7 — bundled notices |
| `pylibsrtp-1.0.0-LICENSE.txt` | pylibsrtp 1.0.0 — BSD-3-Clause |
| `pyopenssl-26.4.0-LICENSE.txt` | pyOpenSSL 26.4.0 — Apache-2.0 |
| `python-vlc-3.0.21203-COPYING.txt` | python-vlc 3.0.21203 — LGPL-2.1-or-later |
| `pywin32-ctypes-0.2.3-LICENSE.txt` | pywin32-ctypes 0.2.3 — BSD-3-Clause |
| `setuptools-65.5.0-LICENSE.txt` | setuptools 65.5.0 — MIT |
| `typing-extensions-4.16.0-LICENSE.txt` | typing-extensions 4.16.0 — PSF-2.0 |
| `yt-dlp-2026.10.26-LICENSE.txt` | yt-dlp 2026.10.26 — Unlicense |

## Not included here

Some wheels bundle native libraries whose notices are not shipped as separate files in the Python package. These include:

- FFmpeg 8.1.2 codec libraries inside the PyAV wheel (x264, x265, lame, vpx, dav1d, SVT-AV1, WebP, and others);
- libcurl-impersonate's statically linked TLS/HTTP/compression libraries;
- libsrtp and OpenSSL dependencies used by pylibsrtp/cryptography.

Before publishing a release, inspect the wheels and add the missing upstream notices. This is part of the release checklist. When in doubt, include the upstream project's license text and a link to its source.

## Note

These files are provided for compliance and identification. They do not change the license terms of the components. If a license text here conflicts with the upstream project's official text, the upstream text controls.
