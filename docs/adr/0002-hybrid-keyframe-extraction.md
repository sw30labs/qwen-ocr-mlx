# 0002. Select keyframes with a hybrid SSIM / pHash / HSV-histogram change detector

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Screen recordings contain many near-identical frames; OCR on every frame would be slow and repetitive, while naive sampling misses slow scrolls.

## Decision

`extract_keyframes_hybrid()` emits the first frame, then a new keyframe when at least `min_interval_seconds` (0.5) has passed **and** any of: SSIM below 0.97 with at least 2% changed area, pHash Hamming distance ≥ 8, or HSV histogram correlation ≤ 0.90. A frame is forced every `max_interval_seconds` (4.0). Frames are compared on a grayscale, blurred, ≤640 px copy. All thresholds are CLI flags.

## Consequences

**Positive**

- Fewer model calls; ignores cursor blinks; still catches slow scrolls (docstring rationale).
- Tunable without code changes.

**Negative**

- Every frame is decoded and scored on CPU, so long recordings take time before any OCR starts.
- All keyframes are held in memory as full-resolution BGR arrays.
- The `area_thresh` parameter of `_ssim_and_changed_area` is unused; the per-pixel delta threshold (0.15) is hard-coded.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Fixed-rate sampling; scene-detection libraries such as PySceneDetect.

## Evidence

- `src/run_ocr.py` (`extract_keyframes_hybrid`, `_to_gray_small`, `_phash`, `_hsv_hist_corr`, `_ssim_and_changed_area`)
- Module docstring point 1
