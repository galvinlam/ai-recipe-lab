# AI Recipe Lab

<p>
  <a href="https://galvinlam.github.io/ai-recipe-lab/" target="_blank" rel="noopener">
    Open AI Recipe Lab
  </a>
</p>

AI Recipe Lab started from a practical problem: cooking videos are easy to watch once and hard to use later.

A useful recipe might be buried inside a twenty-minute YouTube video, split across narration, subtitles, camera shots, pinned comments, and casual phrases like "a splash," "a little bit," or `少許`. Playlists make the problem bigger. They are great for discovery, but not great when you want to compare recipes, search ingredients, or cook from them without replaying the video.

This project explores how AI can turn that messy media into something structured. The idea is to capture a video or playlist, read the transcript-like text, detect the language, pull out ingredients, normalize rough quantities, build a cooking timeline, and leave uncertainty visible for human review.

The useful endpoint is not just a recipe card on screen. The useful endpoint is a structured markdown note that can be copied or downloaded, dropped into LLM Wiki's ingest inbox, searched later, compared with other recipes, and queried in plain language.

![AI Recipe Lab screenshot](docs/assets/ai-recipe-lab-main.png)

## Workflow

```text
YouTube video / playlist
        |
        v
Transcript + metadata capture
        |
        v
Language detection
  EN / 繁體中文 / 日本語 / mixed subtitles
        |
        v
Ingredient extraction
        |
        v
Quantity normalization
  "a splash" / 少許 / visual-only amounts
        |
        v
Cooking method timeline
        |
        v
Recipe card
        |
        v
Confidence notes + review gaps
        |
        v
Copy / download markdown
        |
        v
Drop into LLM Wiki raw inbox
        |
        v
Indexed LLM Wiki note
```

## How AI Fits In

AI is useful here because the input is not clean data. It has narration, incomplete subtitles, visual context, multilingual phrasing, and vague cooking language. The workflow uses AI as a translator between messy source material and a recipe card that a person can actually use.

The important part is not pretending the extraction is perfect. The interface keeps confidence and review gaps visible, so a human can quickly check uncertain quantities, missing temperatures, or steps that were shown on camera but not spoken clearly.

## LLM Wiki Tie-In

Without the ingest workflow, this project is mainly a prototype of the user experience and output format. It becomes useful when the generated card is exported into LLM Wiki as markdown.

The page now includes two static handoff actions:

- `Copy Markdown`: copies the selected recipe note.
- `Download .md`: downloads an ingest-ready markdown file.

That file can be dropped into an LLM Wiki raw inbox, for example `raw/inbox/recipes/`, where the normal ingest process can pick it up.

Example note shape:

```markdown
---
source: https://youtube.com/watch?v=...
language: Japanese + English
tags: [recipes, cooking-video, udon, miso, weeknight]
confidence: 88
ingest_target: llm-wiki/raw/inbox/recipes
review_gaps:
  - Miso type inferred from video color and subtitles
  - Heat level translated from "weak flame"
---

# Miso Butter Udon

Summary, ingredients, cooking timeline, source notes, and uncertainty checks.
```

Once saved this way, LLM Wiki can answer questions like:

- "Which recipes use miso and take under 20 minutes?"
- "Show me Traditional Chinese congee recipes with ginger."
- "Which recipe cards still have low-confidence quantities?"
- "Compare the udon recipes I saved from Japanese cooking videos."

## AI Prompt

Short Codex prompt sequence used to shape the project:

```text
Create a static GitHub Pages app called AI Recipe Lab.
Show how AI turns YouTube cooking videos into recipe cards.
Make the first screen screenshotable with a workflow graphic and recipe preview.
Include multilingual examples: English, Traditional Chinese, and Japanese.
Add clickable sample recipes, ingredients, cooking steps, and confidence gaps.
Add copy/download actions that export the selected recipe as markdown for LLM Wiki ingest.
Write a README that explains the problem, the AI workflow, and demo limits.
```

## Usage

Open `index.html` directly in a browser, or serve the folder with any simple static server.

Example:

```powershell
cd "~/projects/ai-recipe-lab"
python -m http.server 8000
```

Then open `http://localhost:8000`.

## What It Demonstrates

- Capturing a YouTube video or playlist URL as source material.
- Extracting transcript-like text from noisy cooking narration.
- Detecting language, including English, Traditional Chinese, Japanese, and mixed-language examples.
- Identifying ingredients from casual speech.
- Normalizing quantities such as "a splash," `少許`, and low-confidence inferred amounts.
- Building a timed cooking method timeline from video moments.
- Creating a clean recipe card with ingredients, summary, method, confidence, and review gaps.
- Copying or downloading the structured output as an LLM Wiki markdown note.

## Demo Data

This is a static demo. The example recipes and outputs are hand-authored to show the user interface and product idea. The page does not call YouTube, scrape transcripts, run AI extraction, or store data.

Included sample cards:

- Miso Butter Udon: Japanese plus English subtitle fragments.
- 薑絲雞粥 / Ginger Chicken Congee: Traditional Chinese cooking phrasing.
- Sheet Pan Fish Tacos: English narration with loose quantities and visual timing.

## Why It Exists

The goal is to make cooking videos easier to reuse. Instead of leaving good recipes trapped inside video timelines, AI Recipe Lab shows a path from unstructured media to organized LLM Wiki notes: ingredients, method, timing, language context, and places where the AI needs a person to double-check.

## Files

- `index.html`: Single-page static app with embedded CSS and JavaScript.
- `README.md`: Project purpose, usage, and demo explanation.
- `.gitignore`: Local files to ignore if the parent process initializes git.
