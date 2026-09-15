# BabyBedtimeStoryTeller — MVP

A front-end-only demo: enter a child's name and a theme, get a short, calming,
age-appropriate bedtime story generated and narrated aloud — with a replay button.

No backend. Calls the OpenAI API directly from the browser:

- `chat/completions` (gpt-4o-mini, JSON mode) — writes the story
- `chat/completions` again, as a safety judge — checks it before narration, retries up to
  twice, and falls back to a curated pre-written story if it's still flagged. (The dedicated
  `/v1/moderations` endpoint doesn't send CORS headers, so it can't be called from a
  browser at all — see [`docs/architecture.html`](docs/architecture.html) for why.)
- `audio/speech` (gpt-4o-mini-tts) — narrates it

Full architecture, data flow, design tradeoffs, and risk management:
[`docs/architecture.html`](docs/architecture.html) (or the [PDF](docs/architecture.pdf)).

New to the codebase? [`course/index.html`](course/index.html) is a five-module interactive
course that walks through how this app works — no coding background required. It covers
the user journey, the three OpenAI calls, the async request sequence, the CORS bug this
app actually hit (and how it was fixed), and the retry/fallback/error-handling patterns.

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
