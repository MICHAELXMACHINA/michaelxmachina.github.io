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
