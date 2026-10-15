# Video / Transcript Skill

Use for video metadata, transcript retrieval and AI results.

- Normalize URLs to provider + stable video ID.
- Use authorized APIs/captions; not all videos have accessible transcripts.
- Cache transcript by video ID, language, source and version.
- Cache AI results by transcript hash, model, prompt/config fingerprint.
- Support explicit refresh; distinguish stale metadata from transcript versions.
- Avoid repeated token use and unnecessary media storage.
- Handle private, deleted, restricted and failed videos safely.
