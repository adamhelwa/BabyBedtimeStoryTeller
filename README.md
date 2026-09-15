# BabyBedtimeStoryTeller — MVP

A front-end-only demo: enter a child's name and a theme, get a short, calming,
age-appropriate bedtime story generated and narrated aloud — with a replay button.

No backend. Calls the OpenAI API directly from the browser:

- `chat/completions` (gpt-4o-mini, JSON mode) — writes the story
- `moderations` (omni-moderation-latest) — checks it before narration; falls back to a
  curated pre-written story if it's ever flagged
- `audio/speech` (gpt-4o-mini-tts) — narrates it

## Running it

Open `index.html` directly, or serve the folder with any static server
(a real `http://` origin is required — `file://` blocks `fetch()` in most browsers):

```bash
python3 -m http.server 8000
```

On first load it asks for your OpenAI API key. The key is stored **only in your
browser's local storage** and sent directly from your device to OpenAI — it never
touches any server of ours, because there isn't one.

Design direction: Concept A — Calm & Minimal, from the BabyBedtimeStoryTeller PRD.
