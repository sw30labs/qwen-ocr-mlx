# 0003. Deduplicate OCR text across frames with selectable strategies

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Consecutive keyframes often show overlapping content, so raw OCR output repeats.

## Decision

`dedupe_sections()` splits text on blank lines and supports `auto` (line-number-aware merge when line numbers are detected, then fuzzy), `exact`, `fuzzy` (difflib ratio ≥ `--similarity`, default 0.95), `lines` and `ngram` (Jaccard of line n-grams), plus an optional unique-lines pass. New sections from each frame are separated by a `---SLIDE_BREAK---` marker.

## Consequences

**Positive**

- Readable output without repeated blocks; strategy can match content type (code vs slides).

**Negative**

- Fuzzy matching compares each section to every earlier section, so cost grows quadratically with document length.
- `process_video()` defaults `unique_lines=True`, but the CLI flag is `store_true` (default False), so CLI runs have it off; the two defaults disagree.
- With `--dedupe-strategy lines`, sections go through line-number merging but then match neither the fuzzy nor the ngram branch, so nothing is added to `new_sections`; the unique-lines pass only runs on a non-empty list, so every frame is reported as a duplicate and the output stays empty.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Single exact-match dedupe; embedding-based similarity.

## Evidence

- `src/run_ocr.py` (`dedupe_sections`, `dedupe_by_line_numbers`, `fuzzy_section_is_dup`, `ngram_signature`)
- `main()` argparse (`--unique-lines` store_true)
- Module docstring point 2
