# AI Recipe Lab

<p>
  <a href="https://galvinlam.github.io/ai-recipe-lab/" target="_blank" rel="noopener">
    Open AI Recipe Lab
  </a>
</p>

AI Recipe Lab is a static GitHub Pages portfolio demo for Galvin Lam. It shows how an AI-assisted tool could transform messy real-world cooking media, such as YouTube videos and playlists, into structured recipe cards that are easier to review, cook from, and save.

![AI Recipe Lab screenshot](docs/assets/ai-recipe-lab-main.png)

## Purpose

The project demonstrates a practical AI workflow without needing a backend, API key, build step, or external dependencies. It is designed to be screenshotable for a college portfolio and clear enough for a reviewer to understand in one browser view.

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
- Saving the structured output to a future knowledge base concept.

## Demo Data

This is a static demo. The example recipes and outputs are hand-authored to show the user interface and product idea. The page does not call YouTube, scrape transcripts, run AI extraction, or store data.

Included sample cards:

- Miso Butter Udon: Japanese plus English subtitle fragments.
- 薑絲雞粥 / Ginger Chicken Congee: Traditional Chinese cooking phrasing.
- Sheet Pan Fish Tacos: English narration with loose quantities and visual timing.

## Why It Exists

Cooking videos are useful but hard to search, compare, translate, or cook from later. AI Recipe Lab presents a portfolio-friendly example of using AI to convert unstructured media into a useful structured artifact while keeping uncertainty visible for human review.

## Files

- `index.html`: Single-page static app with embedded CSS and JavaScript.
- `README.md`: Project purpose, usage, and demo explanation.
- `.gitignore`: Local files to ignore if the parent process initializes git.
