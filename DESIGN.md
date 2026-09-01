---
title: michaelXmachina — design system
created: 2026-09-01_05-11 WEST
provider: claude-code
psid: 7c96f5cc-5521-4c11-8d35-dd76d491a9f2
model: claude-opus-5
tags: [mxm-site, design-system, tokens]
---

# michaelXmachina — design system

Extracted from the built `/work` page, not invented. Every value below is what actually
ships. When this file and the CSS disagree, the CSS is wrong — fix it here first, then there.

Purpose: stop re-deciding the same things each session. Without a fixed target, output drifts
toward the generic average every time (see `design-research.md` §1).

---

## Named direction

**Quiet editorial, near-black, type-led.** Not a tech-agency page and not a design portfolio.
The work is shown at full width and the writing around it stays small and calm. Confidence
comes from restraint and scale contrast, never from ornament.

What this direction forbids: gradients, glassmorphism, rounded cards with soft shadows, icon
rows, uppercase letterspaced micro-labels, three-up feature grids, emoji.

## Color

| Token | Value | Use |
|---|---|---|
| `--paper` | `#070707` | Page ground |
| `--raised` | `#0b0b0a` | Section band — one step up, deliberately barely visible |
| `--ink` | `#eceae4` | Headings, client names, anything that must read first |
| `--body` | `#a3a29c` | Body copy |
| `--dim` | `#6a6963` | Notes, credits, component lists |
| `--line` | `#1e1e1c` | Hairlines and borders |

Warm-neutral, not blue-black. No accent color: the client logos and screenshots supply all
the color on the page, so the chrome stays out of their way. If an accent is ever added it
should be a single hue used once, not a palette.

## Type

Two families. Contrast comes from **weight and width**, not from serif-vs-sans — a serif
(Instrument Serif) was tried in v1 and rejected as too curvy and tall.

- `--display` — **Archivo** 500/600, tight tracking (`-0.02em` to `-0.035em`). Headings only.
- `--sans` — **Work Sans** 300 body, 400 for emphasis. Never bold body copy.

### Scale (all fluid)

| Element | Size |
|---|---|
| `h1` | `clamp(2.3rem, 6.4vw, 4.5rem)` |
| Section head `h2` | `clamp(1.7rem, 4vw, 2.6rem)` |
| Column head `h2` | `clamp(1.6rem, 3.4vw, 2.3rem)` |
| Lead case `h3` | `clamp(1.6rem, 3.4vw, 2.4rem)` |
| Case `h3` | `clamp(1.35rem, 2.6vw, 1.8rem)` |
| Lede / clarify | `clamp(1.05rem, 1.6vw, 1.22rem)` |
| Body | `1.02rem` / line-height `1.6` |
| Notes, credits | `0.93rem` / line-height `1.9` |
| Component lists | `0.9rem` / line-height `1.85` |

The h1-to-body jump is roughly **4.4×** at desktop. Keep large jumps; adjacent sizes read as
indecision.

## Layout

- Text column: `--max` **1080px**, gutter `2.5rem`, via `.wrap`.
- Breakpoints: **520** (component lists to one column), **640** (Also grid to one column),
  **700** (lead case stops bleeding), **800** (Brand/Content stack).
- `html, body { overflow-x: clip }` — `clip`, never `hidden`, so body never becomes a scroll
  container and `position: sticky` keeps working.
- Full-bleed pattern: `width: 100vw; margin-left: calc(50% - 50vw)`, reverted below 700px.

## Motion

One orchestrated reveal. Not scattered micro-interactions.

- Reveal: opacity + `translateY(18px)`, `0.7s cubic-bezier(0.2, 0.6, 0.2, 1)`.
- Stagger delays: **90 / 110 / 120 / 180 / 270ms** via `--d`. Never more than ~300ms.
- IntersectionObserver: threshold `0.08`, rootMargin `0px 0px -8% 0px`, unobserve after firing.
- Marquee: `0.45px` per frame, pauses on hover/focus/scroll.
- Hover fades: `0.25s ease`.

**Three non-negotiable safety layers**, because motion that fails must fail visible:
1. Hidden state gated behind a `.js` class set by an inline pre-paint script — no JS means
   nothing is ever hidden.
2. A 2s timeout reveals anything the observer missed.
3. `prefers-reduced-motion` short-circuits in both CSS and JS.

## Images

- Screenshots: full container width, natural height. **Never** `object-fit: cover` in a fixed
  ratio box — it crops headlines — and never `contain`, which letterboxes. Let the image be
  its own height.
- Compress to under ~200KB, ~1600–1800px wide, JPEG q72–80.
- Client logos: forced white via `filter: brightness(0) invert(1)` at `0.62` opacity, `1` on
  hover. Uniform white is a decision, not a limitation — two logos (Meritech, Braze) ship
  dark-only, so it is also what keeps them visible.
- Logo heights are **hand-tuned per mark** (15–42px), because the aspect ratios run 2:1 to
  11:1. A single fixed height would make the wide wordmarks enormous.

## Accessibility floors

- Touch targets **≥44px**. Icon-only links get `min-height: 44px` via flex, which grows the
  hit area without resizing the mark.
- Every image carries real `alt`; duplicated marquee rows are `aria-hidden` with `tabindex="-1"`.
- No horizontal page scroll at any width. Verified at 375 / 768 / 1440.

## Writing rules

Learned the hard way on this page — these are content rules, and they were the difference
between the first draft and the current one.

- **Present, don't argue.** State what the work was. No invented conceptual framing
  ("the problem" / "the move"), no thesis dressed up as insight.
- **No hedging or explanatory prose** telling the reader what the page is doing.
- **Title Case** for anything that is not a sentence.
- **Facts only.** Funding figures and dates get a source link. Adjacency is never causation:
  say when a round closed, never imply the work caused it.
- **Unknowns stay marked**, never filled with a plausible guess.
- Agent-written lines get flagged for M, never passed off as his voice.

## Process

1. Fix the direction before writing code. Ambiguity collapses toward the generic mean.
2. One deliberate change per pass; snapshot to `work/versions/` so directions stay comparable.
3. Verify by measurement, not by screenshot alone — and know the artifacts: a hidden browser
   pane suspends `requestAnimationFrame` and reports `clientWidth: 0`, so motion cannot be
   observed and computed styles freeze mid-transition. Emulate a viewport to force real layout.
4. Read the page as a stranger would before calling it done.
