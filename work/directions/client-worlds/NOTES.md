---
title: Direction A, Client Worlds
created: 2026-10-10 WEST
provider: claude-code
model: claude-sonnet-5-5
tags: [mxm-site, design, directions]
---

# Direction A: Client Worlds

**Idea.** The Matter treatment becomes the system: the page chrome is neutral near-black, and every project is its own tinted panel whose background, ink and accent come from that client's screenshot. All four featured cases share one template (head, screenshot, body), the screenshot alternating sides on desktop and stacking on mobile; the five smaller collaborations use the same language at card scale.

## Tokens
- Chrome: paper `#0f1011`, ink `#f4f4f0`, body `#c9cbc6`, dim `#9b9e98`, line `#2b2d2e`. No lime; nothing in the chrome carries colour.
- Panels (bg / ink / accent): Astroscale `#080d18` / `#f6efe9` / `#f28b3d`; Matter `#e9ecdf` / `#20291c` / `#405d22`; Everyday Dose `#f2e6ee` / `#271a25` / `#5a34c2`; Ursa Major `#e6d3b9` / `#2b1a10` / `#8f3913`. Small panels: Meritech `#111b21`, OfferFit `#2c0f4d`, Merlyn Mind `#2a211c`, Veryfi `#141a35`, Civic `#f1eeee`, each with its own accent. Sampled from the edges and dominant tones of the screenshots (Astroscale navy and flare orange, Ursa tan and rust, OfferFit purple, Veryfi navy and green).
- One accent job per panel: the case number and the single call-to-action button. The hero thumbnails reuse the panel colours as mini previews.
- Type: Archivo with width axis 112% (104-106% on mobile) for headings, Work Sans for text. Section titles clamp 2.25-5.25rem and are always larger than project titles (max 3.5rem). Three small sizes only: 14, 16, 18px.
- Services: both offerings fully expanded as rows: title left, three tiers as columns with hairline lists (one column on mobile).
- Motion: hover and focus transitions only (button fill, image scale 1.015). No entrance animation. The screenshot on a desktop panel is `position:sticky` so a tall copy column (Everyday Dose) does not leave dead space beside it.

## Verified
- Visible text, alt text and link targets compared programmatically with `/work/index.html`: identical. The only difference is the Google Fonts URL (adds the width axis). Added `meta robots noindex` (not visible).
- WCAG AA computed for every panel: ink, body, dim and accent against background all at least 5.18:1 (worst case is the dim text on Dose); the button text uses the panel background on the accent colour, so the same figure applies.
- Headless Chrome at 1440 and 500, plus 390 via a temporary iframe wrapper (removed): no horizontal overflow, nav keeps the email link visible at 390, hero fits.
- Final screenshots in `shots/` were taken with lazy loading temporarily switched to eager so below-the-fold images show; the shipped file keeps `loading="lazy"`.

## Known issues
- In the DOM the Matter caption ("Brand and Content for Matter Venture Partners") sits before "My Role", because the screenshot cell precedes the body cell. It still appears under the screenshot. Text content is otherwise in original order.
- Everyday Dose still shows empty panel space beside its list when scrolled to the panel top; the sticky screenshot fills it as you scroll.
- 1920 and 768 were not rendered; the layout relies on the 1000px and 700px breakpoints and a 1360px wrap cap above 1500px.
- "Get in Touch" button at 390 is tight (about 125px) but fits on one line.
