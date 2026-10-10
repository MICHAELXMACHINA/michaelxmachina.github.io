---
title: Direction C, Index, notes
created: 2026-10-10 WEST
provider: claude-code
model: claude-sonnet-5-5
tags: [mxm-site, design, directions]
---

# Direction C: Index

**Idea.** A dark, type-led studio index: the hero's four thumbnails become a huge condensed-Archivo project list (hover or keyboard focus reveals a screenshot preview, CSS only), and each featured case is a full-bleed client-tinted band with a monumental title, the screenshot straddling the band edge, then a caption. Lime appears only on actions (nav contact, case buttons, link hover/focus on dark).

## Tokens
- Page: paper `#0e100d`, surface `#161914`, ink `#f2f1ea`, body `#cfd2c7`, dim `#9da295`, rule `#2e332a`, accent `#d7ef9b` (actions only).
- Client tints (band / lower area), sampled with PIL from the screenshots: Astroscale `#0a0e17` / `#05070c`; Matter `#d1d2ce` / `#e1e3dd` (ink `#162528`); Everyday Dose `#f3cdd7` / `#fbe4ea` (ink `#271a25`); Ursa Major `#2a1d16` / `#1a110c`.
- Collaboration panels: Meritech `#0c151d`, OfferFit `#3f126d`, Merlyn Mind `#4d3429`, Veryfi `#181d39`, Civic `#f3ede5`.
- Type: Archivo `wdth 62`, weight 800 for display (h1 up to 15rem, h2 8.5rem, case and index names 6.5rem, service names 4rem, tier and collaboration names 2.4rem); Work Sans for text. Only three text sizes: 0.875rem, 1.0625rem, 1.375rem.
- Light cases (Matter, Dose) use an ink button with lime text so lime stays the action colour and passes contrast.

## Structure notes (text unchanged)
- Services is no longer collapsible: `<details>` replaced by an always-open two-column specification (service names h3, tiers h4; the section h2 stays "How I Can Help").
- Each case follows one template: band (number, sector, title), screenshot, caption (role, copy, link). In the Matter case the line "Brand and Content for Matter Venture Partners" sits directly under the screenshot, as in the source order of that case.
- Added `<meta name="robots" content="noindex">` (draft). No other head changes.

## Verified
- Headless Chrome screenshots at 1440 and 500 (`shots/index-1440.png`, `shots/index-500.png`), hover state (`shots/index-hover-1440.png`, forced via a temporary class in a test copy; the real rule is `:hover` / `:focus-visible` inside `@media (hover:hover) and (pointer:fine) and (min-width:900px)`). Below that, or on touch, the index is a plain large list with small inline thumbnails.
- 390px checked through a 390px iframe; no horizontal overflow measured (element right edges and scrollWidth) at 390, 768, 1440, 1920.
- WCAG AA computed for every text/background pair (all pass, minimum 4.90 on the dimmed non-hovered index rows; most are above 7). Full table was generated in a scratch script.
- Focus ring is lime on dark sections and ink on light bands. `prefers-reduced-motion` disables transitions. Buttons and links are at least 44px tall.

## Known issues
- Hover preview and focus preview were verified only through the forced-class test copy, not by a real mouse; keyboard focus uses the same rule.
- The dimmed non-hovered rows are 4.90:1, only while another row is hovered.
- Services right column is shorter than the left, leaving empty space under "Video" on desktop.
- The line break in "Matter Venture<br>Partners" is kept from the source, so that title is two lines while the others are one.
- Tier rows were not tested with browsers lacking `:has()`; the dimming just doesn't happen there.
- Lazy images below the fold are blank in plain headless screenshots; final shots were taken from a temporary eager copy (deleted).
- 768px was measured for overflow but not visually inspected.
