# Architecture

## V0.1
React + TypeScript + Vite dashboard. No API, database, authentication, cloud service or user-file persistence. Tool cards are placeholders, not functional processors.

## Later, only when needed
Browser dashboard → optional Spring Boot API → PostgreSQL for transcript/history/cache + filesystem for large binary assets. Background jobs for slow video/AI tasks. Keep boundaries between modules and do not tie ToolHub to mini-shipper.

## Data lifecycle
- Asset drafts: working data, optional autosave when persistence is built, export then user-confirmed cleanup with recovery window.
- Transcript: normalize provider + video ID, language and version. Reuse valid saved transcripts. Metadata may need refresh independently.
- AI results: reuse only with matching input version/hash, model, prompt version and parameters.
- Large files: avoid database blobs unless justified; no user assets in git.

## Remote access (deferred)
Home PC hosting via HTTPS tunnel/reverse proxy and access controls, backup and recovery. Do not expose Vite dev server or database publicly.
