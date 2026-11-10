# 0001. Replace the image-captioning CLI with a screen-recording OCR pipeline

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The first version (78a3070, 2025-10-24) was `src/main.py`, which captioned every image in `input/` with `lmstudio-community/Qwen3-VL-30B-A3B-Instruct-MLX-8bit` and wrote one JSON per image plus `captions.json`. Commit 52373ff (2026-02-25, message 'update') deleted `src/main.py` and added `src/run_ocr.py`.

## Decision

The project's working entry point is `src/run_ocr.py`: it turns screen recordings (and images) into deduplicated Markdown/text/JSON via keyframes plus a vision model. The README and the GitHub repo description were **not** updated and still describe `src/main.py` captioning, its flags and its JSON output.

## Consequences

**Positive**

- One tool now covers videos and images and produces readable documents rather than captions.

**Negative**

- The README is stale: its usage (`python src/main.py --input-dir ...`), flags (`--repo-id`, `--model` as a path, `--user-prompt`) and outputs no longer exist.
- The module docstring still calls the script `drun_ocr.py` and refers to `direct_ocr.py`.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Keep captioning as a separate entry point next to OCR.

## Evidence

- git log: 78a3070 'initial Commit' (adds src/main.py), 52373ff 'update' (deletes src/main.py, adds src/run_ocr.py)
- README.md @ 37686a7
- `src/run_ocr.py` module docstring
- GitHub repo description (fetched 2026-11-10)
