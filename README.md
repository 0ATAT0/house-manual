# House manual

A single-page guide for friends staying at the flat with Fred and Luna. Two tabs: the cats and their timetable, then how the flat works.

Two levels. Each tab opens on a grid of tiles, one per area, and tapping a tile opens that area on its own page. The Flat has WiFi, front door, bins, windows, kitchen and living room. The Cats leads with a navy tile naming the next feed and what to serve, then Fred, Luna, saying hello, sleep and play, and the litter tray.

Tiles carry a status badge where there's something live to say: the next feed on the navy tile, `TUE` on bins, `10–5` on sleep.

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

Navigation is hash routing, so the phone's back gesture works and any area can be linked directly (`#kitchen`, `#feeding`). A tile is a `<button data-go="key">`; its page is an `<article class="detail" id="d-key" data-tab="flat|cats">`. Add both and it wires itself up.

The tile grid is two columns on a phone, three from 700px and four from 1000px. The navy tile spans two.

Bump `CACHE` in `sw.js` when changing anything other than `index.html`, so old assets are dropped.

## A note on privacy

The repository is public, because GitHub Pages on a free account cannot serve a private one. `robots.txt` and a `noindex` meta tag keep it out of search results, and the page carries no home address. It does carry the WiFi password. If that stops being acceptable, the options are a paid GitHub plan with a private Pages site, or a client-side passphrase gate over the Flat tab.
