# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file, mobile-first trip guide (`index.html`) published via GitHub Pages at `https://dkasprzak.github.io/travel-guide/`. No build step, no dependencies, no tests, no package manager. Pushing `index.html` to `main` is the deploy (the owner often uploads it from a phone via the GitHub web UI). To preview locally, open `index.html` in a browser.

All page copy is in Polish; code identifiers and comments are in English. `README.md` (Polish) is the owner's manual for reusing the template for a new trip — keep it in sync when changing structure, class names, or the checklist key.

## Structure of `index.html`

- **CSS tokens** live in `:root` at the top of the second `<style>` block. Every color is defined three times: light default, `@media (prefers-color-scheme: dark)` under `:root:not([data-theme="light"])`, and `:root[data-theme="dark"]`. Change all three together. Themeable per trip: `--accent` (highlighted times, focus ring), `--green` (transit line color), `--stripe-a`/`--stripe-b` (top stripe band, e.g. club colors).
- **Sections** are `<section id="...">` with manually numbered `<h2><span class="n">01</span>…`. The sticky `<nav class="jump">` chips link to these ids — adding/removing/renaming a section means updating the nav and renumbering.
- **Reusable markup patterns** (place item in `ul.places`, timeline item in `ol.tl` with optional `class="key"`, checklist `label`, metro stop in `ol.stops` with `mid`/`end` variants) are documented as copy-paste snippets in `README.md`.
- **Inline script** at the bottom (ES5, no dependencies):
  - "Kopiuj adres" button copies a hardcoded `var text=` string, with a select-text fallback.
  - Checklist state persists in `localStorage` under the prefix `'ncl-'` + input `id`. For a new trip the prefix must change, and every checkbox needs a unique `id`. The progress counter is recomputed from the DOM.
  - Scroll spy adds `.active` + `aria-current` to the `nav.jump` chip whose section is under the sticky nav; it derives sections from the chips' `href`s, so it needs no changes when sections change.

## Things that are easy to miss

- The accommodation address is duplicated in four places: the `#addr` text, the "Nawiguj do noclegu" maps link, the `origin=` of the stadium walking-route link, and `var text=` in the script.
- Map links use `https://maps.google.com/?q=...` (pins) and `https://www.google.com/maps/dir/?api=1&origin=...&destination=...&travelmode=walking` (routes), spaces as `+`.
- The repo and page are public: never add door codes, booking numbers, or phone numbers.
- Wrap any `localStorage` access in `try/catch` (existing code does) — the page must work when storage is unavailable.
