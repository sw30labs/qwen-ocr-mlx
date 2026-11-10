# 0004. Support three OCR backends: external API module, local Qwen (MLX), local MiniMax server

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

The owner wanted both local and hosted OCR options.

## Decision

`process_video()` picks one backend per run: `--use-local-minimax` (OpenAI-compatible `/v1/chat/completions` at `--minimax-url`, default `http://127.0.0.1:8000`), `--use-local-qwen` (mlx-vlm), or by default an API path that dynamically loads `direct_ocr.py` from the same directory and calls its `load_api_config` / `extract_text_from_image` (default `--model gpt-5-mini`). The two local flags are mutually exclusive.

## Consequences

**Positive**

- Same keyframe/dedupe pipeline regardless of model.

**Negative**

- `src/direct_ocr.py` is not in the repository and never has been (git history checked), so the default API path fails unless the user supplies that file.
- The MiniMax backend sends only text (`[Image: WxH pixels]` plus the prompt) and no image, so it cannot read the frame content; the code comment says MiniMax is text-only.
- `--private` is parsed and passed through but never used.
- `openai` is in requirements.txt but not imported.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- A single backend; a vision-capable OpenAI-compatible client for every backend.

## Evidence

- `src/run_ocr.py` (`process_video`, `ocr_with_minimax`, `ocr_with_qwen`, `SourceFileLoader(... 'direct_ocr.py')`)
- `git log --all -- src/direct_ocr.py` → no commits (2026-11-10)
- `requirements.txt`
