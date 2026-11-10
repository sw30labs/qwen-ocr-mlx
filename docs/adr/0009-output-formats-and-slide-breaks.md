# 0009. Write txt, json or md output with slide boundaries, defaulting to Markdown

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Users want either a readable document or structured data.

## Decision

`--output-type {txt,json,md}` (default `md`). Markdown joins sections and turns slide breaks into `---` rules; JSON groups sections into `[{"slide": n, "sections": [...]}]`; text uses a 40-character `=` rule. Output path is `<output_dir>/<stem>.<type>`; per-video relative sub-folders are preserved.

## Consequences

**Positive**

- Markdown output matches the Markdown-first prompts.

**Negative**

- `process_video`'s own default `output_type` is `txt` while the CLI default is `md`.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- One file per keyframe.

## Evidence

- `src/run_ocr.py` (`process_video` output block, `main()` path logic)
