# 0010. Treat still images as pre-selected keyframes

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The owner also wanted to OCR folders of screenshots, not only videos.

## Decision

`find_media()` walks `--input_dir` for videos (`.mp4 .mov .mkv`) and images (`.png .jpg .jpeg .bmp .tiff .webp`). Each video produces its own output; all images in the folder are sorted by path and processed together as one keyframe list, producing a single `<dir>_ocr.<type>` file. `--video` with an image path processes that one image. Keyframe detection is skipped for images, but dedupe still applies across them.

## Consequences

**Positive**

- One pipeline for both media types; a slide deck exported as images becomes one document.

**Negative**

- Images in different sub-folders are merged into one output.
- Cross-image dedupe can drop legitimately repeated content.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- One output per image (as the original captioner did).

## Evidence

- `src/run_ocr.py` (`find_media`, `load_images_as_keyframes`, `main`)
- Commit 37686a7 message ('image support')
