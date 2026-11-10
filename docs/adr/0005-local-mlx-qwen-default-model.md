# 0005. Run local OCR with mlx-vlm and download weights on demand

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Local inference on Apple silicon was a goal from the first commit (README prerequisites: macOS with Apple silicon).

## Decision

Local mode uses `mlx_vlm.load(..., lazy=True)` and `generate`. Default repo is `mlx-community/Qwen3.5-27B-bf16` (the original captioner used `lmstudio-community/Qwen3-VL-30B-A3B-Instruct-MLX-8bit`). `resolve_model_path()` maps a repo id to `HUGGINGFACE_HUB_CACHE/models--<org>--<name>`; `ensure_model_available()` downloads with `snapshot_download(repo_id, local_dir=...)` if neither `params.json` nor `config.json` sits at the top of that folder. Defaults: `--qwen-max-tokens 8192`, temperature 0.0.

## Consequences

**Positive**

- Private, offline OCR after first download.
- Weights path can be overridden with `--qwen-model-path`.

**Negative**

- A normal HF cache entry keeps files under `snapshots/<sha>/`, not at the top of `models--...`, so an already cached model is not detected and is downloaded again into the cache folder as a flat copy.
- A missing mlx-vlm raises at runtime rather than at start-up.
- Each frame is written to a temporary PNG before inference.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Use `snapshot_download` without `local_dir` and load from the returned snapshot path; mlx-lm only.

## Evidence

- `src/run_ocr.py` (`DEFAULT_QWEN_REPO_ID`, `resolve_model_path`, `ensure_model_available`, `ocr_with_qwen`)
- `git show 78a3070:src/main.py` (`DEFAULT_REPO_ID`)
- README Prerequisites
