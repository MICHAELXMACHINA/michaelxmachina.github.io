---
title: /work page — iteration log
created: 2026-09-01_01-55 WEST
provider: claude-code
psid: 7c96f5cc-5521-4c11-8d35-dd76d491a9f2
model: claude-opus-5
tags: [mxm-site, portfolio, iteration-log]
---

# /work — iteration log

Live preview: `http://localhost:8123/work/` (python http.server on 8123, run from repo root)
Snapshots: `work/versions/` — open any of them directly to compare.

## Versions

| File | What it was |
|---|---|
| `versions/v1-serif-tabs.html` | Instrument Serif display, Brand/Content stacked, tab row under each heading, name+one-liner above image |
| `versions/v2-sidebyside-archivo.html` | Archivo display, Brand Strategy \| Content side by side, image-first with title below, scrollable marquee |

## Decisions locked

- **Audience:** people M is already in conversation with, or fellowship/grant/job applications. The page confirms, it doesn't convince.
- **One belief:** he's done this work for serious companies and the work was good.
- **No argument apparatus.** Present the work, let it speak. Killed: "the problem / the move", "same job higher stakes", the milestones caveat.
- **Not "Symantic Studio"** at the top — company renaming to michaelXmachina eventually. No header for now.
- **Title Case** everywhere except sentences.
- **Featured Projects** (not Featured Work).
- **Client order:** Astroscale, Matter, Everyday Dose, Ursa Major featured; Meritech, OfferFit, Merlyn Mind, Veryfi in Also; Otoy in marquee only.

## Open — needs M

- [ ] **Headline.** Current: "Authentic branding and content for purpose-driven companies." M is chewing on branding+content vs strategy+storytelling, and on having two modifier pairs. See analysis below.
- [ ] **Hero subline.** Five options drafted; option 1 is live.
- [ ] **Astroscale years** — the only remaining `.ask` marker on the page.
- [ ] **Matter one-liner** — M wants their thesis described beyond "backed by Kleiner Perkins". Needs their portfolio checked.
- [ ] **Font** — Archivo is the current pick after Instrument Serif was rejected as "too curvy and tall". Alternates: Newsreader, Bricolage Grotesque, Work Sans at extreme weights.

## The naming problem (M's open question)

Current headline stacks two pairs: *authentic* + *purpose-driven* (modifiers), *branding* + *content* (deliverables). Four slots, and the modifiers compete.

- **"Content" is the weak word.** It's a commodity term — content mills, content marketing — and it undersells strategy work. "Storytelling" matches his own vocabulary and the mXm identity.
- **Cleanest fix:** drop one modifier, keep one pair of deliverables.
  - `Brand strategy and storytelling for purpose-driven companies.` — one modifier, two deliverables, uses his own section names
  - `Branding and content for purpose-driven companies.` — plainest, no adjective stack
- **The more interesting pair** underneath all of this is substance vs expression — what a company *is* vs how it *says it*. That's the actual two-part thing he keeps circling:
  - `What a company stands for, and how it says it.`

## Known issues

- **Marquee auto-scroll unverified.** Rebuilt as a real scroll container (drag/scroll left-right, no hover snap-back). Could not confirm motion — the browser pane was hidden, which suspends `requestAnimationFrame` and reports zero width. **Check this first.**
- Braze logo is the only raster (PNG); soft if the band ever scales up.
- Meritech + Braze ship dark-only logos, so the whole band is forced white via CSS filter. Ursa Major's orange and Matter's green are flattened as a side effect.

## Overnight queue (work top-down, one item per pass)

Ordered by value. Do ONE per pass, snapshot, log, commit. Do not redesign wholesale.

1. ~~**Verify the marquee actually scrolls**~~ — code hardened and bug fixed (pass 02-11). **Still needs M's eyes on actual motion**, since rAF cannot run while the pane is hidden. If it does not move for him, the remaining suspects are: `mask-image` on the scroll container, or `overflow-x: auto` being overridden at his viewport width.
2. **Responsive pass** — check 390px, 768px, 1440px. Fix anything that breaks. Mobile is likely where this is weakest.
3. **Scroll reveals** — one orchestrated staggered reveal using IntersectionObserver (pattern in `design-research.md` §4). Understated: opacity + small translate, once, no loops. Must respect `prefers-reduced-motion`.
4. **Headline variants** — build 3 full-page snapshots into `versions/` with different headline+subline combinations so M can compare them side by side rather than imagining them.
5. **Section rhythm** — the four featured cases are currently identical blocks. Vary deliberately (full-bleed vs contained, or a density shift) per `design-research.md` §2.
6. **Landing page** (`/index.html`) — M said to consider it. Do NOT change its content or tagline. Only candidate change: restore the commented-out `past-work` block to link `/work`. Snapshot before touching, and flag it rather than assuming.
7. **A DESIGN.md** — tokens, type scale, spacing, named direction. This is the durable artifact; it feeds every later session and M's own service offering.

## Pass log

| Time | Pass | What changed |
|---|---|---|
| 01-55 | — | Queue established; v1 and v2 snapshotted |
| 03-11 | 3 — scroll reveals | One orchestrated reveal pass, 15 blocks, each revealed once then unobserved: h1 → clarify (110ms) → Brand/Content columns (0/120ms) → marquee → section heads → the four cases → the four Also tiles (0/90/180/270ms). Opacity + 18px rise, 0.7s, custom easing. IntersectionObserver at 0.08 threshold with -8% bottom rootMargin. **Three safety layers, all verified:** (a) the hidden state is gated behind a `.js` class set by an inline pre-paint script — removing the class returns every element to opacity 1, so a failed or blocked script can never hide content; (b) a 2s failsafe reveals anything the observer missed; (c) `prefers-reduced-motion` rule confirmed present in the stylesheet and the JS short-circuits to show-all when it matches. Verified the CSS resolves correctly by disabling transitions and re-reading: all 15 settle to opacity 1 / transform none. **Not verified: the animation playing visually** — with the pane hidden the compositor is suspended, so `getComputedStyle` returns frozen mid-transition values (this is why an unpatched read shows opacity 0 despite `.in` being applied; it is an artifact, not a bug). Snapshot: `versions/v5-scroll-reveals.html` |
| 02-41 | 2 — responsive | Tested 375 / 768 / 1440. **No horizontal page scroll at any width** (the only elements exceeding the viewport are inside the marquee, which is a deliberate scroll container). Two real defects found and fixed: (a) marquee logo links were 15–42px tall — below the 44px touch minimum — now `min-height:44px` via flex, logo sizes unchanged; (b) "Positioning Recommendation" and "Positioning Statement" wrapped to ragged two-liners in the 155px mobile column — component lists now collapse to one column under 520px. Re-verified at 375px: 0 wrapped items, all 9 tap targets exactly 44px. 768px: lists 2-col, grid 2-col, clean. 1440px: offering side-by-side 535/465, h1 72px, wrap capped 1080, clean. Note: the offering stacks below 800px, so iPad portrait gets Brand and Content stacked — deliberate, side-by-side at 768 would be cramped. **Still NOT verified: marquee visible motion** — retested at 1440 where layout does compute (`clientWidth` 1080, `scrollWidth` 3176, so it is genuinely scrollable), but `document.hidden` stays true and rAF reports 0 frames regardless of viewport size. The zero-width guard behaves correctly (scrollLeft holds at 1, no slam). Snapshot: `versions/v4-responsive.html` |
| 02-11 | 1 — marquee | Proved rAF is fully suspended while the browser pane is hidden (0 frames in 600ms) — that alone explains the unobservable motion; the scroll math dry-ran clean (wraps correctly, position stays in [0, half)). Found and fixed a real latent bug: with no layout box, writing `scrollLeft` silently fails, so `pos` drifted ahead of reality and the seam-rebase would slam the band to its end on first paint or on pane reveal. Now guarded on `clientWidth`, seam-rebase only fires during user scrolling, and a `visibilitychange` handler resyncs so it resumes instead of jumping. Verified: no slam while hidden, all 18 logos load. **NOT verified: visible motion** — needs the pane displayed. Snapshot: `versions/v3-marquee-hardened.html` |
