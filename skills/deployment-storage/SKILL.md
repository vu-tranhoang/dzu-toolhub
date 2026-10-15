# Deployment / Storage Skill

- Local-first; no required cloud infrastructure in MVP.
- Distinguish drafts, finalized exports, transcript history and AI caches.
- Never delete work until export is confirmed; provide retention/recovery settings.
- Plan backups, restoration tests, disk quotas and database migrations when persistence is added.
- If exposed remotely: HTTPS, authentication, secrets protection and rate limiting.
- Never publicly expose Vite development server or raw database ports.
