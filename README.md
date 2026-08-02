# House manual

A single-page guide for friends staying at the flat with Fred and Luna. Two tabs: the cats and their timetable, then how the flat works.

Built for lookup rather than reading. The Cats tab opens on a live panel naming the next feed and what to serve, with the day's four feeds as a timeline. The Flat tab opens on the three things every guest asks for. Everything below that sits in labelled rows, each showing a one-line answer and opening for the detail, so neither tab runs longer than a couple of screens.

Light only, matching the Strand Labs site. Installable as a PWA and works offline once opened, so a sitter can add it to their home screen and still read it if the WiFi drops.

## Hosting

Static site on GitHub Pages, served from `main` at the repository root. Push to `main` and the change is live in about a minute.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole manual: markup, styles and scripts inline |
| `manifest.json` | PWA metadata, name and icons |
| `sw.js` | Service worker. Network-first for the page so edits land immediately, cache-first for assets |
| `robots.txt` | Blocks search indexing |
| `icon-*.png`, `apple-touch-icon.png` | Home-screen icons, generated from Georgia Bold on cream |

## Editing

Content lives directly in `index.html`. The feed rows in the schedule table carry `data-feed="HH:MM"`, `data-name` and `data-food`, which drive both the now panel and the timeline: change a time in the visible cell and in `data-feed`, and everything above follows.

A collapsible row is a `<details>` holding a `.label` (what it is) and a `.hint` (the answer in one line, truncated if it runs long, so keep hints short). Add `open` to the tag for anything that should start expanded.

Bump `CACHE` in `sw.js` when changing anything other than `index.html`, so old assets are dropped.

## A note on privacy

The repository is public, because GitHub Pages on a free account cannot serve a private one. `robots.txt` and a `noindex` meta tag keep it out of search results, and the page carries no home address. It does carry the WiFi password. If that stops being acceptable, the options are a paid GitHub plan with a private Pages site, or a client-side passphrase gate over the Flat tab.
