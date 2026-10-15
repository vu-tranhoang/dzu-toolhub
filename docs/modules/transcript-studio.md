# Transcript Studio (planned)

Enter a supported video URL → normalize provider/video ID → look up saved transcript → fetch allowed captions or transcribe when needed → save transcript and history. Later summaries/scripts use their own cache.

Suggested entities:
- videos: platform, canonical ID, metadata, last checked
- transcripts: video ID, language, source, segments/timecodes, version/hash
- ai_results: transcript hash, task, model, prompt/config fingerprint, result
- processing_jobs: deduplication key, status, error, timestamps

URLs with tracking/time parameters should map to one canonical video. Support explicit refresh and missing/unavailable videos. Captions may be free; speech-to-text and summaries may incur costs. Respect platform terms and avoid storing unnecessary video/audio.
