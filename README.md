# AI Recipe Lab

<p>
  <a href="https://galvinlam.github.io/ai-recipe-lab/" target="_blank" rel="noopener">
    Open AI Recipe Lab
  </a>
</p>

AI Recipe Lab is a URL-to-card prototype for turning YouTube cooking videos into recipe notes that can be ingested by LLM Wiki.

Paste a YouTube link, click `Process Link`, review the generated card, then copy or download an LLM Wiki-ready markdown file. The app tries public captions first, then falls back to YouTube page text through Jina Reader. If online text is unavailable, it falls back to a clearly marked review card.

![AI Recipe Lab screenshot](docs/assets/ai-recipe-lab-main.png)

## Workflow

```text
YouTube link
  -> transcript + metadata
  -> language detection
  -> ingredients + quantities
  -> cooking timeline
  -> recipe card
  -> copy/download markdown
  -> LLM Wiki raw inbox
```

## LLM Wiki Handoff

The generated markdown includes source URL, language, tags, confidence, ingredients, steps, and review gaps. It is meant to be dropped into an LLM Wiki ingest folder such as:

```text
raw/inbox/recipes/
```

## Current Scope

This public GitHub Pages version is frontend-only. It can attempt public caption and page-text lookup from the browser, but it does not run `yt-dlp`, call an LLM, download video files, or write directly into LLM Wiki.

A real connected version would need a backend worker:

```text
URL -> captions/yt-dlp -> LLM synthesis -> markdown -> LLM Wiki ingest
```

## AI Prompt

```text
Create a static app where a user pastes a YouTube cooking link.
Try public captions first, then fall back when captions are unavailable.
Extract likely ingredients, method steps, confidence gaps, and a recipe card.
Export the selected recipe as markdown for LLM Wiki ingest.
Keep the UI screenshotable and multilingual.
```

## Run Locally

```powershell
cd "~/projects/ai-recipe-lab"
python -m http.server 8000
```

Then open `http://localhost:8000`.
