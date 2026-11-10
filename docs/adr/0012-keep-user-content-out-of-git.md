# 0012. Keep inputs, outputs, checkpoints and assistant notes out of git

- **Status:** Accepted (retrospective, inferred 2026-11-10)
- **Date recorded:** 2026-11-10

## Context

Recordings and OCR output can be private or large.

## Decision

`.gitignore` excludes `input/`, `output/`, `*.checkpoint.json`, Python build/venv folders, IDE folders, `.DS_Store` and `CLAUDE.md` (added in 37686a7).

## Consequences

**Positive**

- User content and per-machine assistant notes do not get committed.

**Negative**

- Example inputs/outputs shown in the README cannot be reproduced from the repo.

## Alternatives considered

- No alternatives are recorded in the repository; the options below are inferred for comparison only and were not evidenced as considered.
- Commit a small sample input for testing.

## Evidence

- `.gitignore`
- Commit 37686a7
