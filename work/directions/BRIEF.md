---
title: /work — three visual directions brief
created: 2026-10-10 WEST
provider: claude-code
model: claude-opus-5-5 (supervisor); implementation by Sonnet workers
tags: [mxm-site, design, directions]
---

# /work — three visual directions

Michael's request, 2026-10-10: make the site look and feel much better without superfluous bells and whistles. Explore three distinct directions. **Do not change any narrative content**, only how it looks and feels.

Source of truth for content: `/work/index.html` at commit `6b8f423`. Each direction is a standalone page at `/work/directions/<slug>/index.html` and must not modify the live `/work/index.html`.

## Shared rules (every direction)

- **Text is frozen.** Every visible string, link target, alt text and section order (hero → How I Can Help → Selected Projects → More Collaborations) stays identical. Do not add taglines, labels, numbers, years, quotes or any new words. You may remove purely decorative duplicates only if listed under your direction. Title Case for non-sentences is already applied; keep it.
- **What Michael liked:** the Matter Venture Partners treatment, where the section background is tinted to pair with that client's screenshot, and it holds up on mobile. Everyday Dose now uses the same treatment in pink.
- **What Michael asked against:** a basic-looking site, inconsistent treatments, lack of personality. Also no gimmicks: no parallax, no cursor effects, no auto-playing motion, no scroll-jacking, no gradients for decoration, no glassmorphism, no emoji, no icon rows.
- **Known weaknesses to fix:** section headings are smaller than project titles (inverted hierarchy); about ten near-identical small text sizes (use at most three small sizes); the lime accent is used for too many jobs; four featured cases use mismatched layouts; the services section is two collapsed bars that say little (it is now the second thing a visitor sees).
- **Tech:** single static HTML file with inline CSS. Images from `/assets/work/*.jpg` with absolute paths. Google Fonts allowed (Archivo is a variable font with a width axis: `Archivo:wdth,wght@62..125,100..900`). JavaScript optional and only as progressive enhancement; all content visible and usable without it. Native `<details>` is fine.
- **Quality floor:** WCAG AA contrast; 44px minimum touch targets; visible `:focus-visible`; `prefers-reduced-motion` honored; no horizontal scroll at 390, 768, 1440 and 1920; images keep `width`/`height` attributes; the mobile nav keeps the email link visible.
- **Motion budget:** at most hover/focus transitions and one subtle entrance. Nothing that delays reading.

## Direction A: Client Worlds (`/work/directions/client-worlds/`)

Extend the treatment Michael likes into the system. The page stays dark; each featured project becomes its own tinted panel whose background, ink and accent are sampled from that client's screenshot (Astroscale: deep space navy/black with warm orange accent; Matter: existing sage; Everyday Dose: existing pink; Ursa Major: warm dusk/rust tan). All four use one consistent panel template (copy column + screenshot), alternating screenshot side on desktop, stacking cleanly on mobile. More Collaborations become smaller panels in the same language, each with a quiet tint from its own screenshot. The site chrome (hero, services, nav) goes neutral so client color carries the page. Services: show all tiers expanded as a clear grid, not collapsed bars. Display type: Archivo with a slightly expanded width for headings for character.

## Direction B: Journal (`/work/directions/journal/`)

A light, editorial, printed-matter direction that ties the site to Michael's CV (white pages, terracotta `#a74832`, Archivo/Work Sans). Warm paper ground, near-black ink, terracotta as the single accent used for links and actions only. Strict Swiss-style grid with hairline rules, generous margins and large scale contrast. The four featured projects use one consistent layout; screenshots sit in thin-ruled frames like plates in a monograph. Services become a typographic table-like grid of the three tiers. More Collaborations become a disciplined two- or three-column grid. Feels like a well-set studio monograph: calm, precise, confident.

## Direction C: Index (`/work/directions/index-studio/`)

A dark, type-led, cinematic direction. The hero's four thumbnails become a large typographic project index: client names set big in condensed Archivo (narrow width axis), one per row with hairline rules, each linking to its project; on hover/focus with a fine pointer a small preview of the screenshot appears; on touch the index is a plain, large list (thumbnails may show inline small). Featured projects are monumental: screenshot near full-bleed with the title in a strong band, one consistent template for all four, with client-tinted bands echoing the Matter idea subtly. A single accent (keep lime `#d7ef9b` but use it for one job only). Services as a stark two-column specification. Feels like a studio's index page: bold, graphic, confident.

## Deliverables per direction

1. `/work/directions/<slug>/index.html`.
2. Screenshots in `/work/directions/<slug>/shots/` at 1440 and 500 widths (headless Chrome cannot go below 500px).
3. A short `NOTES.md` in the folder: the idea in two sentences, key tokens (colors, type scale), what was verified, and known issues.
