# House manual

A single-page guide for friends staying at the flat with Fred and Luna. Two tabs: the cats and their timetable, then how the flat works.

One page per tab, read top to bottom. Each section puts its heading in a left rail with the content alongside, separated by hairline rules. The Flat covers WiFi, front door, windows, bins, kitchen and living room. The Cats opens with a live line naming the next feed, then feeding, Fred, Luna, living with them, and the vet.

Design follows the Strand Labs site rather than the palette tokens: white grounds, `gray-50` cards with a `gray-200` border and a soft shadow, bold Playfair headings in navy, Inter for body, a navy band for the vet details, and green used only on the next-feed marker. No cream, and light only.

Installable as a PWA and works offline once opened, so a sitter can add it to their home screen and still read it if the WiFi drops.

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

Content lives directly in `index.html`. The meal rows carry `data-feed="HH:MM"`, `data-name` and `data-food`, which drive the navy panel and the timeline: change a time in the visible cell and in `data-feed`, and everything above follows.

A new section is a `<section>` holding an `<h2>` and a `.content`, which in turn holds `.entry` blocks (an uppercase label plus prose). Use `.two` inside `.content` for a pair of short entries side by side. Below 820px the rail collapses and headings sit above their content.

Bump `CACHE` in `sw.js` when changing anything other than `index.html`, so old assets are dropped.

## A note on privacy

The repository is public, because GitHub Pages on a free account cannot serve a private one. `robots.txt` and a `noindex` meta tag keep it out of search results, and the page carries no home address. It does carry the WiFi password. If that stops being acceptable, the options are a paid GitHub plan with a private Pages site, or a client-side passphrase gate over the Flat tab.
