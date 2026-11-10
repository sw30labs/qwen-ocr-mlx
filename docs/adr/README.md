# Architecture Decision Records: sw30labs/qwen-ocr-mlx

A local-first OCR tool that turns screen recordings and screenshots into deduplicated Markdown using keyframe detection and a vision model (Qwen via MLX, a MiniMax server, or an external API module).

These ADRs are **retrospective**: they were reconstructed on 2026-11-10 from a full read of the repository at
commit `37686a7715885060405c462d4500b295ed94de52` (source, config, tests, docs and git history). They record decisions as they are visible in
the code. Where the *reason* behind a decision is not stated anywhere in the repo, the ADR says so, and the
inferred reason is logged as an assumption in [`../assumptions.md`](../assumptions.md) for the owner to confirm or correct.

Format: Title, Status, Context, Decision, Consequences (positive/negative), Alternatives considered, Evidence.
New ADRs should continue the numbering below.

| ADR | Title | Status |
|-----|-------|--------|
| [0001](0001-pivot-captioning-to-screen-ocr.md) | Replace the image-captioning CLI with a screen-recording OCR pipeline | Accepted (retrospective) |
| [0002](0002-hybrid-keyframe-extraction.md) | Select keyframes with a hybrid SSIM / pHash / HSV-histogram change detector | Accepted (retrospective) |
| [0003](0003-multi-stage-dedup.md) | Deduplicate OCR text across frames with selectable strategies | Accepted (retrospective) |
| [0004](0004-pluggable-ocr-backends.md) | Support three OCR backends: external API module, local Qwen (MLX), local MiniMax server | Accepted (retrospective) |
| [0005](0005-local-mlx-qwen-default-model.md) | Run local OCR with mlx-vlm and download weights on demand | Accepted (retrospective) |
| [0006](0006-strip-qwen3-thinking.md) | Strip Qwen3 reasoning blocks from model output | Accepted (retrospective) |
| [0007](0007-external-prompt-templates.md) | Keep prompts in prompts/<type>.md with built-in fallbacks | Accepted (retrospective) |
| [0008](0008-per-frame-checkpoint-resume.md) | Checkpoint after every frame and resume interrupted runs | Accepted (retrospective) |
| [0009](0009-output-formats-and-slide-breaks.md) | Write txt, json or md output with slide boundaries, defaulting to Markdown | Accepted (retrospective) |
| [0010](0010-images-as-keyframes.md) | Treat still images as pre-selected keyframes | Accepted (retrospective) |
| [0011](0011-single-script-no-packaging.md) | Ship as a single script with unpinned requirements, no tests and no CI | Accepted (retrospective) |
| [0012](0012-keep-user-content-out-of-git.md) | Keep inputs, outputs, checkpoints and assistant notes out of git | Accepted (retrospective) |
| [0013](0013-apache-2-license.md) | License the project under Apache-2.0 | Accepted (retrospective) |
