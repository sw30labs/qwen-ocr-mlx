# 0008. Checkpoint after every frame and resume interrupted runs

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Local OCR of long recordings can take a long time and may be interrupted.

## Decision

After each keyframe, `process_video()` writes `<output>.checkpoint.json` with `next_idx` and the collected sections. On start, an existing checkpoint is loaded and frames up to `next_idx` are skipped. The checkpoint is deleted after the final output is written. `*.checkpoint.json` is git-ignored.

## Consequences

**Positive**

- Restarts do not redo finished frames.

**Negative**

- Resume assumes the same keyframes are produced again; changing thresholds or the input between runs silently misaligns the index.
- The checkpoint is rewritten in full each frame (grows with output).

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- No resume; per-frame output files.

## Evidence

- `src/run_ocr.py` (`process_video` checkpoint block)
- `.gitignore` (`*.checkpoint.json`)
- Commit 37686a7 message ('checkpoint/resume')
