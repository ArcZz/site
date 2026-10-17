# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Zhi Zhang's personal academic homepage, served by GitHub Pages from the `main` branch root at `https://arczz.github.io/site/`. It is a single self-contained static page: no framework, no build step, no package.json, no external fonts, icons, or scripts.

- `index.html`: the whole site. HTML, CSS, 12 inline SVG Pokémon sprites, and the Poké Ball / `use FLY` script all live in this one file.
- `Zhi-Zhang-CV.pdf`: public CV, opened by the `resume` text link (relative `./Zhi-Zhang-CV.pdf`, no `download` attribute). Never commit a CV with a private phone number.
- `favicon*`, `android-chrome-*`, `apple-touch-icon.png`, `site.webmanifest`: favicon set generated from the Leckerli One font (see `about.txt`). `index.html` does not currently link them.
- `robots.txt`, `sitemap.xml`: single-URL SEO files pointing at the `/site/` base.

Before 2026-10-17 this repo held Hugo 0.98 build output; that is gone, see git history if an old page is needed. `blog-sources/` and the `zhi-cactus-site-final.zip` package are git-ignored.

## Hard constraints

- **Keep the URL**: the site lives at `https://arczz.github.io/site/`, a project page under the `/site/` subpath. Keep all asset links relative (`./file`), never `/file`. No `CNAME` (one was tried and removed).
- **Deploy = push to `main`**. The repo root is what GitHub Pages serves; there is no Actions workflow.
- **Design is frozen** to the approved Cactus-style package: Menlo / Meslo LG monospace, white background, 39rem column, teal `#2CBC89` headings and nav, blue `#2B90BD` hover, blush `#FFB6A6` Pokémon accent. Do not add frameworks, decorations, Pokédex counters, or redraw the sprites.
- **Contact order is fixed**: `Find me on` GitHub icon, Google Scholar icon, Email icon, `and resume.` (plain text link, last). Icon links keep their `aria-label`.

## Behavior to preserve when editing `index.html`

- Shuffle-bag sampling in the inline script: all 12 Pokémon appear once per cycle (Fisher–Yates), no repeat straddling cycles, a new draw only on closed → open, not on hover while pinned.
- Poké Ball opens on hover (mouse) or tap/click (pinned), closes on leave, outside pointerdown, or Escape. Beam flash, pop-out, cry bubble, and recall animations are CSS keyframes keyed off `.is-open` / `.is-closing`.
- Footer `use FLY` is a real `#top` anchor; the header ball plays `fly-land` once scrolling reaches the top. `prefers-reduced-motion` disables all of it.

## Local preview and checks

Links are relative, so either open `index.html` directly or serve from the repo root:

```bash
cd /Users/zhangzhi/Studio/blog/site && python3 -m http.server 8000   # http://localhost:8000/
```

Headless Chrome clamps `--window-size` to a 500px minimum, so for 390px / 320px layout checks wrap the page in an `<iframe>` of that width rather than trusting `--screenshot` at small sizes. The shuffle logic can be unit-checked in Node by extracting the inline `<script>` and stubbing `document` (see git history of the 2026-10-17 migration for the approach).
