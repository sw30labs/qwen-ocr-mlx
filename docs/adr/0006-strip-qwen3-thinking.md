# 0006. Strip Qwen3 reasoning blocks from model output

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Qwen3 chat templates can put `<think>` into the prompt, so generated text starts mid-reasoning.

## Decision

`_strip_thinking()` removes full `<think>...</think>` blocks, drops everything before a lone `</think>`, and drops a trailing unclosed `<think>`. Its docstring says that if neither tag appears the model hit the token limit while thinking and the frame is skipped, but the code returns the stripped text in that case rather than an empty string.

## Consequences

**Positive**

- OCR output contains only the answer.

**Negative**

- The docstring's case 3 ('return empty string') does not match the code when no tags are present; reasoning text with no tags would be kept.
- Applied only to the Qwen backend.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Disable thinking in the chat template.

## Evidence

- `src/run_ocr.py` (`_strip_thinking`, `ocr_with_qwen`)
- Commit 37686a7 message ('thinking-strip for Qwen3')
