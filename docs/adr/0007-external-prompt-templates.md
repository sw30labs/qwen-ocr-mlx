# 0007. Keep prompts in prompts/<type>.md with built-in fallbacks

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Code screenshots, slides and general documents need different extraction instructions.

## Decision

`--type {auto,code,slides}` selects `prompts/<type>.md`. The file holds the system prompt, a line `---`, then the user prompt. If the type file is missing it falls back to `auto.md`, then to built-in `DEFAULT_SYSTEM_PROMPT` / `DEFAULT_USER_PROMPT`. Prompts ask for raw Markdown, Mermaid for diagrams, quoted Mermaid labels, and no guessing at cut-off content.

## Consequences

**Positive**

- Prompts can be edited without touching code.

**Negative**

- The built-in default user prompt duplicates `prompts/auto.md`, so the two can drift.
- The external API backend ignores these prompts (it calls `extract_text_from_image` without them).

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Prompts hard-coded in Python only.

## Evidence

- `prompts/auto.md`, `prompts/code.md`, `prompts/slides.md`
- `src/run_ocr.py` (`load_prompts`, `DEFAULT_*_PROMPT`)
- Commit 37686a7
