# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A two-page static CV/portfolio site, deployed via GitHub Pages: plain HTML and CSS, no build
step, no JavaScript, no package manager. Built from an "Industry" design system export from
Claude Design. All current content (name, employer, project names, stats) is placeholder text
to be replaced. Files must live at the repository root (not a subfolder) since Pages serves
directly from there.

## Commands

Preview locally — no build step needed:

```bash
python3 -m http.server
```

Then open `http://localhost:8000`. Opening `index.html` directly from the filesystem also
works.

There is no lint, test, or build command — there is no tooling in this repo at all.

## Deployment

Pushing to `main` is what publishes the site — GitHub Pages is configured (Settings → Pages)
to deploy from that branch, root folder. For the URL to be `https://<username>.github.io`
(no path suffix), the repository itself must be named exactly `<username>.github.io`.

## Structure

- `index.html` — CV home page (hero, experience, selected projects, stack, talks, contact)
- `projects.html` — all six projects in full detail
- `assets/styles.css` — the design system: colors, type, component classes (buttons, cards,
  tags). Treat as generated/foundational; avoid casual edits.
- `assets/site.css` — page layout and responsive rules; this is where layout changes belong
- `assets/portrait.svg` — placeholder portrait
- `.nojekyll` — tells GitHub Pages to serve files as-is (no Jekyll processing)

## Architecture notes

- **Projects are triple-linked.** Each project lives in three places: a summary card in
  `index.html`'s `card-grid`, a full `<article>` in `projects.html`, and an entry in the
  `proj-index` nav strip at the top of `projects.html`. They're tied together by ids
  `#p1`–`#p6`. Adding, removing, or reordering a project means updating all three.
- **Styling is token-driven.** Colors, spacing, and type come from CSS variables at the top
  of `assets/styles.css` (e.g. `--color-accent` recolors buttons, rules, numerals, and the
  duotone photo treatment everywhere at once). Don't hard-code hex values or font names
  outside that file.
- **The visual system is deliberate and load-bearing:** square corners (never round them),
  hairline borders, no fills on cards, and `+` registration marks (`<i class="corner tl/tr/bl/br">`
  elements) at the corners of cards and buttons — keep these four elements when copying a
  block. The primary button's solid accent fill is the one intentionally filled object in
  the system.
- Fonts (Barlow, Barlow Condensed) load via `@import` from Google Fonts at the top of
  `styles.css`.
