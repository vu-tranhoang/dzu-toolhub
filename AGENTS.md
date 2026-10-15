# Dzũ ToolHub — Agent Instructions

Read this document and the relevant skill before coding.

## Product intent
A modular, personal, local-first creative toolkit. The MVP runs on one PC with no login, database or cloud requirement. Future self-hosting must remain possible but is not in scope yet.

## Rules
1. Read docs and current code first. Do not implement speculative infrastructure.
2. Keep tools modular, typed, accessible, and responsive.
3. Never commit secrets, user-generated images, transcripts or downloaded media.
4. Prefer deterministic browser-side processing for tilemaps/sprites; add an API only when necessary.
5. Asset export must complete before optional cleanup; never destroy drafts on a mere Export click.
6. Cache transcripts by platform/video ID, language and version; cache AI outputs by input hash, model, prompt and configuration.
7. Require HTTPS and authentication before any future public exposure.
8. Check license and terms before copying third-party code or extracting video content.
9. Run typecheck/build when available, report verification truthfully.
10. Keep scope small; record decisions in docs/decisions.md.

## Skills
- UI: skills/frontend/SKILL.md
- API: skills/backend/SKILL.md
- Pixel assets: skills/asset-processing/SKILL.md
- Video/transcript: skills/video-transcript/SKILL.md
- Testing: skills/quality/SKILL.md
- Storage/deployment: skills/deployment-storage/SKILL.md
