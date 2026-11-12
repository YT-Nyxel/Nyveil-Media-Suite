# FFmpeg distribution notice

**Nyveil Media Suite 1.0.0**  
**Last updated:** 12 November 2026

Nyveil Media Suite bundles `ffmpeg/ffmpeg.exe` to merge media streams, convert local media, and remux live streams. This page records the exact binary, its licensing, and where to obtain the corresponding source.

---

## 1. Binary identification

The binary was inspected on 12 November 2026 and reports:

- **Version:** `9.0.1-full_build-www.gyan.dev`
- **Copyright banner:** `Copyright (c) 2000-2026 the FFmpeg developers`
- **Builder:** MSYS2 project
- **Supplier:** [Gyan.dev FFmpeg Builds](https://www.gyan.dev/ffmpeg/builds/)
- **License indicated by the supplier for this static build:** GPLv3
- **SHA-256:** `57C56E369D5B4873B4D93FC1A1D833CB7CD8BC9325C14B05C34CE60B22842D8A`
- **File size:** 222,229,504 bytes
- **Relevant configuration flags:** `--enable-gpl --enable-version3 --enable-static`
- **Recorded build information:** [ffmpeg/BUILD_INFO.txt](ffmpeg/BUILD_INFO.txt)

The full configuration includes many external libraries and is available from the binary with:

```powershell
.\ffmpeg\ffmpeg.exe -buildconf
```

The configuration includes GPL-only components such as:

```text
--enable-gpl --enable-version3
--enable-libx264 --enable-libx265
```

---

## 2. Why the binary is distributed separately

Nyveil invokes `ffmpeg.exe` as a separate process using `subprocess` for downloads, conversions, and live muxing. The application does not link this executable into its own address space. The executable and the Nyveil application are distributed together as separate programs, each under its own license.

This means the standalone FFmpeg binary does **not** by itself force the Nyveil application code to be GPL. However, the PyAV dependency used by `aiortc` loads FFmpeg libraries inside the application process, so the app as a whole is distributed under GPLv3. See [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md), section 3.2.

---

## 3. Source code and build information

- **FFmpeg 9.0.1 source:** https://ffmpeg.org/releases/ffmpeg-9.0.1.tar.xz
- **FFmpeg releases:** https://ffmpeg.org/releases/
- **Gyan.dev build scripts:** https://github.com/GyanD/codexffmpeg
- **Gyan.dev builds page:** https://www.gyan.dev/ffmpeg/builds/
- **FFmpeg legal information:** https://ffmpeg.org/legal.html
- **GPLv3 text:** [licenses/GPL-3.0.txt](licenses/GPL-3.0.txt)
- **GPLv2 text:** [licenses/GPL-2.0.txt](licenses/GPL-2.0.txt)
- **LGPL 2.1 text:** [licenses/LGPL-2.1.txt](licenses/LGPL-2.1.txt)

If you received the binary without this information, request the corresponding source at **Nyveil@web.de**. The offer is valid for at least three years from the date you received the binary. See [SOURCE_OFFER.md](SOURCE_OFFER.md).

---

## 4. Required release follow-up

Before distributing a release archive or installer:

- [ ] Include the complete GPLv3 text.
- [ ] Include this notice and [ffmpeg/BUILD_INFO.txt](ffmpeg/BUILD_INFO.txt).
- [ ] Include the source/build information above, or a written offer to provide it.
- [ ] Keep the binary, notices, and source/build information matched by version and SHA-256.
- [ ] Do not claim that FFmpeg, Gyan.dev, or the FFmpeg developers endorse Nyveil.
- [ ] If you modify the FFmpeg binary or build it yourself, update the version, checksum, configuration, and source offer.

FFmpeg's [legal page](https://ffmpeg.org/legal.html) explains the project's compliance guidance. Gyan.dev's builds page explains the licensing of its static builds.

---

## 5. Disclaimer

This notice records technical facts about the bundled binary and the release obligations that appear to apply. It is not legal advice. A qualified lawyer should review the final distribution model and all GPL compliance material before publication.
