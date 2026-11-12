# GPLv3 source availability / Quellcodeangebot

**Nyveil Media Suite 1.0.0**  
**Last updated:** 12 November 2026

Nyveil Media Suite is distributed as a Windows executable and includes GPLv3-licensed software. Under the GNU General Public License version 3, everyone who receives the binary is entitled to the **complete corresponding source code** for the exact version they received.

This page explains where to get it. It is part of the distribution and must be included with every release.

---

## 1. Nyveil Media Suite source

The complete source archive for a release is attached to the **same GitHub release** as the EXE:

- Asset name: `Nyveil-Media-Suite-<version>-source.zip`
- Example: `Nyveil-Media-Suite-1.0.0-source.zip`
- It contains the application source, `main.spec`, `requirements.txt`, build instructions, this notice, the GPLv3 text, and the third-party notices.

If the source asset is missing, inaccessible, or you received the EXE from somewhere else, request the source by email:

**Nyveil@web.de** — subject `Source request — Nyveil Media Suite <version>`

The publisher will provide the corresponding source for the version you received. The offer is valid for at least **three years** from the date you received the binary. A charge may be made only to cover the reasonable cost of physically performing the source distribution, if a physical medium is requested.

### What the source archive does not contain

- your personal data, TURN credentials, or local settings;
- downloaded or shared media;
- third-party binaries that are not part of the source (for example, the prebuilt `ffmpeg.exe`); their source is identified below.

---

## 2. Bundled FFmpeg 9.0.1 binary

The release bundles `ffmpeg/ffmpeg.exe`, identified as:

- **Version:** `9.0.1-full_build-www.gyan.dev`
- **Supplier:** [Gyan.dev FFmpeg Builds](https://www.gyan.dev/ffmpeg/builds/)
- **Builder:** MSYS2 project
- **License indicated by the supplier for this static build:** GPLv3
- **SHA-256:** `57C56E369D5B4873B4D93FC1A1D833CB7CD8BC9325C14B05C34CE60B22842D8A`
- **Relevant configuration flags:** `--enable-gpl --enable-version3 --enable-static`

### FFmpeg source

- **Upstream source:** https://ffmpeg.org/releases/ffmpeg-9.0.1.tar.xz
- **Upstream releases directory:** https://ffmpeg.org/releases/
- **Gyan.dev build scripts:** https://github.com/GyanD/codexffmpeg
- **Build information recorded for this binary:** [ffmpeg/BUILD_INFO.txt](ffmpeg/BUILD_INFO.txt)
- **GPLv3 text:** [licenses/GPL-3.0.txt](licenses/GPL-3.0.txt)

The exact configuration is available from the binary with:

```powershell
.\ffmpeg\ffmpeg.exe -buildconf
```

The configuration includes GPL-only components such as `--enable-libx264` and `--enable-libx265`. Their source and license notices are part of the FFmpeg build. Keep the binary, the build information, and the source references matched by version and checksum.

### Why this binary is separate

Nyveil invokes `ffmpeg.exe` as a separate process for merging and conversion. The application does not link this executable into its own address space. The executable and the Nyveil application are therefore distributed together as separate programs, each under its own license. This does not reduce the GPLv3 obligations for the FFmpeg binary itself.

---

## 3. PyAV 18.1.0 and its bundled FFmpeg 8.1.2 libraries

The `aiortc` dependency uses **PyAV 18.1.0**, whose Windows wheel bundles FFmpeg 8.1.2 native libraries. The installed package reports:

```text
av.__version__            = 18.1.0
av.ffmpeg_version_info    = 8.1.2
library_versions          = libavutil 60.26.102, libavcodec 62.28.102,
                            libavformat 62.12.102, libavdevice 62.3.102,
                            libavfilter 11.14.102, libswscale 9.5.102,
                            libswresample 6.3.102
```

The wheel contains GPL codec libraries including `libx264` and `libx265`. Because these libraries are loaded in the application process, the distributed application includes GPL-linked components. This is why the Nyveil application code is licensed under GPLv3.

### PyAV source

- **PyAV 18.1.0 source:** https://github.com/PyAV-Org/PyAV/tree/v18.1.0
- **PyAV release:** https://github.com/PyAV-Org/PyAV/releases/tag/v18.1.0
- **PyAV license:** [licenses/pyav-18.1.0-LICENSE.txt](licenses/pyav-18.1.0-LICENSE.txt)
- **PyAV build documentation:** https://pyav.basswood.io/developers/building.html

### FFmpeg 8.1.2 source used by PyAV

- **Upstream source:** https://ffmpeg.org/releases/ffmpeg-8.1.2.tar.xz
- **FFmpeg license information:** https://ffmpeg.org/legal.html
- **GPLv2 text:** [licenses/GPL-2.0.txt](licenses/GPL-2.0.txt)
- **GPLv3 text:** [licenses/GPL-3.0.txt](licenses/GPL-3.0.txt)
- **LGPL 2.1 text:** [licenses/LGPL-2.1.txt](licenses/LGPL-2.1.txt)

The exact PyAV wheel contents can be inspected in the installed environment:

```powershell
python -c "import av, os; print(av.__version__, av.ffmpeg_version_info); print(os.path.dirname(av.__file__))"
```

If you need the exact build configuration or the corresponding source for the PyAV wheel you received, request it at **Nyveil@web.de** or obtain it from the PyAV project's release/source materials. Keep the request and the response with your release records.

**Compatibility caveat:** x264 and x265 are commonly licensed under GPLv2, and GPLv2-only components can be incompatible with GPLv3. The Gyan.dev FFmpeg build is supplied as GPLv3 and the PyAV wheel is supplied by PyAV as a whole, but this specific combination should be reviewed by a qualified lawyer before publication. If it cannot be confirmed, replace the PyAV wheel with an LGPL-only FFmpeg build or remove the PyAV dependency.

---

## 4. Other third-party components

The complete list of Python dependencies, versions, licenses, and source links is in [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md). Exact license texts are in the [licenses](licenses/) directory.

Notable components:

- **yt-dlp 2026.10.26** — Unlicense — https://github.com/yt-dlp/yt-dlp
- **aiortc 1.16.0** — BSD-3-Clause — https://github.com/aiortc/aiortc
- **aioice 0.13.0** — BSD-3-Clause — https://github.com/aiortc/aioice
- **pylibsrtp 1.0.0** — BSD-3-Clause — https://github.com/aiortc/pylibsrtp
- **cryptography 50.0.2** — Apache-2.0 OR BSD-3-Clause — https://github.com/pyca/cryptography
- **python-vlc 3.0.21203** — LGPL-2.1-or-later — https://github.com/oaubert/python-vlc
- **CustomTkinter 6.0.0** — MIT (wheel metadata says CC0; included LICENSE is MIT) — https://github.com/TomSchimansky/CustomTkinter
- **Pillow 12.3.0** — MIT-CMU — https://github.com/python-pillow/Pillow
- **curl-cffi 0.17.0** — MIT (bundles libcurl-impersonate with its own third-party notices) — https://github.com/lexiforest/curl_cffi
- **PyInstaller 6.22.3** — GPL-2.0-or-later with the PyInstaller bootloader exception — https://pyinstaller.org/

---

## 5. Release checklist for source compliance

Before publishing a release:

- [ ] Build the EXE from the tagged source.
- [ ] Create `Nyveil-Media-Suite-<version>-source.zip` from the same commit.
- [ ] Attach the source ZIP to the **same** GitHub release as the EXE.
- [ ] Include `LICENSE`, `NOTICE`, `THIRD_PARTY_LICENSES.md`, `FFMPEG_NOTICE.md`, `ffmpeg/BUILD_INFO.txt`, `SOURCE_OFFER.md`, `PRIVACY.md`, `TERMS.md`, `LEGAL.md`, `SECURITY.md`, `TRADEMARKS.md`, and the `licenses/` directory in the release.
- [ ] Verify the FFmpeg SHA-256 matches the value above.
- [ ] Confirm no TURN password, personal data, or downloaded media is in the source ZIP.
- [ ] Keep the release assets online for at least three years.

If you cannot publish the corresponding source, do not distribute the current build. Remove or replace the GPL-linked components first.

---

**Source contact:** Jason Bruns — **Nyveil@web.de**
