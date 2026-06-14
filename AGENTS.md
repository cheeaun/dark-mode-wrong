# AGENTS.md

Guidance for AI agents (and humans) working in this repo.

## What this is

A one-page site arguing that theme toggles need **three** states — Light / Dark /
Auto, with Auto as the default. The page implements the pattern it describes, so
it is its own live demonstration.

- **No build step, no dependencies.** `index.html` is the whole site: vanilla
  HTML/CSS/JS plus self-hosted fonts in `fonts/`. Open it in a browser to run it.
- **Make no external network requests.** Everything (fonts included) is
  self-hosted on purpose. Don't add CDN links, analytics, or third-party scripts.

## ⚠️ When you edit the content: bump the modified date everywhere

The "last modified" date is duplicated across files and has **no build step to
keep it in sync** — so you must update each copy by hand. Whenever you change the
page's content or code, set every location below to **today's date** (the
`UserPromptSubmit` context line gives you today's date; format `YYYY-MM-DD`):

| File | What to update |
| --- | --- |
| `index.html` | `dateModified` in the `TechArticle` JSON-LD (`<script type="application/ld+json">`) |
| `index.html` | `<meta property="article:modified_time" content="…">` |
| `sitemap.xml` | `<lastmod>` |
| `llms-full.txt` | the `*Last updated: …*` line near the top |

**Do not** change the *published* dates — `datePublished` in the JSON-LD and
`<meta property="article:published_time">` are fixed at first publication
(2026-06-12).

## Keep the parallel copies in sync

The argument exists in three places. A change to the substance in one must be
mirrored in the others (then bump the dates above):

- `index.html` — the canonical, rendered version.
- `llms-full.txt` — the full article as plain markdown, for LLMs/agents.
- `llms.txt` — the short summary + links.

Two more mirrors inside `index.html` itself:

- The **`FAQPage` JSON-LD** mirrors the `<details class="objection">` Q&A in the
  body. Edit an objection → update its question/answer in the JSON-LD too.
- The **`og:`/`twitter:` description** tags echo the hero copy. Keep them aligned.

## Verifying

There are no tests. To check a change, serve the folder (e.g.
`python3 -m http.server`) and load `index.html`. After touching structured data,
confirm both JSON-LD blocks still parse as valid JSON.
