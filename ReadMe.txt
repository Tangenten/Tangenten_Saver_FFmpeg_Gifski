Tangenten Saver (FFmpeg & Gifski)
=================================

Saver (FFmpeg & Gifski) is a Fusion fuse that exports animation sequences to
video and GIF formats using FFmpeg and Gifski on the system PATH. It provides
a comprehensive UI for codec selection, rate control, palette tuning, and
per-codec encoder choice without writing command-line arguments.

Requirements
------------

- **FFmpeg** — required for all formats except Gifski GIFs.
  Install via your package manager (apt, brew, etc.) or from https://ffmpeg.org.
- **gifski** — required only for the "GIF (Gifski)" preset.
  Install via your package manager or from https://github.com/ImageOptim/gifski.

Both tools must be discoverable on the system PATH.

Install
-------

Copy this folder into your Fusion Fuses directory:

    DaVinci Resolve
    — Windows: C:\ProgramData\Blackmagic Design\DaVinci Resolve\Support\Fusion\Fuses
    — macOS:   ~/Library/Application Support/Blackmagic Design/DaVinci Resolve/Support/Fusion/Fuses
    — Linux:   ~/.local/share/DaVinciResolve/Fusion/Fuses

    Fusion Studio
    — Windows: C:\ProgramData\Blackmagic Design\Fusion\Fuses
    — macOS:   ~/Library/Application Support/Blackmagic Design/Fusion/Fuses
    — Linux:   ~/.fusion/BlackmagicDesign/Fusion/Fuses

2. Restart DaVinci Resolve or Fusion Studio.

Supported Formats
-----------------

| Format              | Codec    | Extension | Notes                              |
|---------------------|----------|-----------|------------------------------------|
| MP4 (H.264)         | h264     | .mp4      | libx264, faststart support         |
| MP4 (H.265/HEVC)    | h265     | .mp4      | libx265, hvc1 tag                  |
| MP4 (AV1)           | av1      | .mp4      | libaom-av1 / libsvtav1 / librav1e  |
| WebM (VP9)          | vp9      | .webm     | VP9 alpha channel support          |
| GIF                 | gif      | .gif      | FFmpeg palettegen pipeline         |
| GIF (Gifski)        | gif_gifski | .gif    | High-quality GIF via gifski        |
| WebP (Animated)     | webp     | .webp     | Lossy/lossless, alpha              |
| APNG (Animated PNG) | apng     | .png      | Compression & prediction options   |
| AVIF                | avif     | .avif     | libaom-av1 / libsvtav1 / librav1e  |
| ProRes              | prores   | .mov      | 422 Proxy through 4444 XQ          |
| PNG Sequence        | png_seq  | .png      | Direct frame export, no encode     |

Features
--------

- **Per-codec encoder selection** — auto-detects available encoders from
  `ffmpeg -encoders` and lets you choose (e.g. libsvtav1 vs libaom-av1).
- **Rate control** — CRF, ABR, or CBR with VBV buffer/maxrate for H.26x.
- **Two-pass encoding** — for H.264, H.265, VP9, AV1, AVIF.
- **GIF palette tuning** — palette mode, max colors, dither, two-pass palette
  for higher quality.
- **Alpha handling** — automatic alpha flattening for codecs without alpha
  support; VP9 alpha, WebP alpha, ProRes 4444 alpha.
- **Frame resolution** — auto-scale from input or manual width/height.
- **Frame output rate** — override composition frame rate.
- **Custom command template** — advanced users can edit the generated FFmpeg
  command directly.
- **Keep/reuse frames** — skip re-rendering when only the encode step changes.
- **Progress bar & cancel** — real-time feedback with cancel button.
- **Output size display** — shows rendered file size after export.

Quick Start
-----------

1. Add the node (right-click → Add Tool → Tangenten → Saver (FFmpeg Gifski)).
2. Connect your render output to the yellow input.
3. Set the output path in the Path field (use Fusion path maps like `Comp:/`).
4. Choose a format from the Format dropdown.
5. Adjust encoder settings (speed, profile, rate control) as needed.
6. Click Export and wait for the progress bar to finish.

License
-------

This project is licensed under LGPL-2.1-or-later. See License.txt for full
terms and the third-party compliance notice.

In short:
- The fuse script (Saver_FFmpeg_Gifski.fuse) never links against or includes
  FFmpeg or gifski; it spawns them as subprocesses. It is independent Lua
  software licensed under LGPL-2.1-or-later.
- FFmpeg and gifski are separate projects with their own licenses (LGPL/GPL
  and AGPLv3 respectively). You must install them separately and comply with
  their terms.

---
Repository: https://github.com/Tangenten/Tangenten_Saver_FFmpeg_Gifski
