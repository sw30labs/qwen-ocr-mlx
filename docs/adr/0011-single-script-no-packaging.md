# 0011. Ship as a single script with unpinned requirements, no tests and no CI

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The project is a personal utility.

## Decision

All logic is in `src/run_ocr.py`, run as `python src/run_ocr.py`. `requirements.txt` lists unpinned packages (mlx, mlx-lm, mlx-vlm, pillow/Pillow twice, huggingface-hub, torch, torchvision, opencv-python, numpy, json5, requests, psutil, scikit-image, openai). There is no pyproject, test suite or GitHub workflow.

## Consequences

**Positive**

- Easy to copy and run.

**Negative**

- Nothing checks that changes keep working; behaviour shifts with upstream releases (open VulnOps PRs #1 pin versions and #2 bumps certifi, observed 2026-11-10).
- Unused requirements (`json5`, `psutil`, `openai`, `mlx-lm`, `torch`/`torchvision` in the current script) add install weight.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- A packaged CLI with tests on the pure functions (dedupe, prompt loading, thinking strip).

## Evidence

- Repository tree @ 37686a7 (9 files)
- `requirements.txt`
- Open PRs sw30labs/qwen-ocr-mlx#1, #2
