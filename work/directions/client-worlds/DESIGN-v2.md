---
title: Client Worlds v2 — design plan
created: 2026-10-10 WEST
provider: claude-code
model: claude-opus-5-5 (plan); implementation by Sonnet
tags: [mxm-site, design, client-worlds]
---

# Client Worlds v2 — design plan

Michael chose Client Worlds on 2026-10-10 and found v1 unpolished: unicode arrows as icons, services as a wall of text on mobile, a "More Collaborations" heading that isn't needed, and a Civic card that spans the full width as if it were more important. This plan applies the web-design process in `/Users/mac/cortex/ops/skills/web-design/SKILL.md`.

## Brief

- **Subject:** Michael Ketigian, brand strategist and writer, trading as Symantic Studio.
- **Audience:** founders and executive teams he is already talking to, plus applications. They look on a laptop or a phone, often from a link in a message.
- **Job:** confirm, within a minute, that he has done brand strategy and writing for serious companies and that the work is good.
- **Mode:** Experience (a portfolio). Let the client work lead; the interface recedes.
- **The one memorable move:** every featured client lives in its own world, a panel whose colour is drawn from that client's own site. Everything else stays quiet.

## Tells this plan refuses

Source: the Anthropic `frontend-design` skill and the Impeccable craft floor (see `ops/skills/web-design/SKILL.md`).

- A near-black ground with one acid-green accent (v1 and the live site). **The lime accent is removed.** Client colour is the only colour.
- Numbered markers such as "01 / Astroscale" and "01 ↘" on content that is not a sequence. **Removed.**
- An eyebrow label above a heading. **Removed.**
- Meta strings joined with middle dots. Role and service lists render as real lists with spacing. Same words; the dot separator was presentation.
- Unicode glyphs as icons. **Replaced** with one inline SVG set (Lucide geometry, 1.5px stroke, 1em box).
- Same-size card soup. Featured work gets panels; further work becomes a compact strip at lower prominence.

## Tokens

| Token | Value | Use |
|---|---|---|
| `--ground` | `#121314` | Page ground, neutral graphite (not a tinted green-black) |
| `--ground-2` | `#1a1b1d` | Services band, card backgrounds |
| `--ink` | `#f2f2ef` | Headings and primary text on the ground |
| `--body` | `#c9cac6` | Body on the ground |
| `--dim` | `#9a9b97` | Secondary on the ground (≥4.5:1 on `--ground`) |
| `--line` | `#2c2d30` | Hairlines on the ground |
| Panel tokens | per client | `--p-bg`, `--p-ink`, `--p-body`, `--p-dim`, `--p-line`, `--p-accent`, kept from v1 where they passed AA |

**Type.**
- Display: Archivo, width 112, weight 600, tracking −0.03em.
- Text: Work Sans 400/500.
- **Scale:** hero `clamp(3rem, 7vw, 6rem)`; section `clamp(2.25rem, 4.5vw, 3.75rem)`; panel title `clamp(2rem, 3.4vw, 3rem)`; strip title 1.25rem; lead 1.125rem; body 1rem; small 0.875rem. There are no other sizes.
- **Setting:** `text-wrap: balance` on headings and `pretty` on paragraphs. The body measure stays at or below 68ch.

**Space.** 4, 8, 12, 16, 24, 32, 48, 64, 96 and 128px only. Leave more space above a heading than below it.

**Icons.** Inline SVG, `stroke: currentColor`, 1.5px, `width/height: 1em`, and `vertical-align: -0.125em` or flex-centred. There are only three icons:
- arrow-up-right, for external links
- chevron-down, for disclosures; it rotates 180° when open
- arrow-down-right, for in-page jumps from the hero cards; it is optional and quiet

## Information architecture

1. **Nav:** the Symantic Studio wordmark (a white mark, not lime); then Services, Work and a Get in Touch button. On phones it shows Work and Get in Touch.
2. **Hero:** h1, then the clarify paragraph, then four client mini-panels linking to each project. Each mini-panel shows only the screenshot and the client name.
3. **How I Can Help.** There are two disclosures, **collapsed by default**.
   - The summary shows the service name and its three tier names as a quiet inline list, with a chevron on the right.
   - The open state shows the tiers as a grid: three columns on desktop, one on mobile.
   - The full row is the 56px+ hit target.
   - It is a native `details`/`summary`, with height animated through `interpolate-size: allow-keywords` plus `::details-content` where supported. Elsewhere it is instant, and reduced motion is honoured.
4. **Selected Projects.** There are four panels with one template, and the screenshot alternates sides on desktop.
   - **Always visible:** the client title, the sector or years line where the source has one, the role list, the screenshot and the single primary action (a client-accent button with an arrow-up-right icon).
   - **Behind a "Project Details" disclosure:** the description paragraph or paragraphs, the Everyday Dose bullet list, the collaboration credit and the Matter caption. "Project Details" is the only new UI label.
   - On mobile a panel is: title, meta, role, screenshot, action, then the disclosure.
5. **Further work.** There is no heading or subtitle; the section is named only by `aria-label="More client projects"`.
   - **Layout by width:**
     - Desktop at 1100px and up: a row of five equal columns.
     - Narrower: a horizontal scroll-snap rail in which each card is 78% of the viewport wide and the next card peeks in, so that more work is visible.
   - **No card ever spans the row.**
   - **Card contents:** screenshot, name (linked), role list, credit, and "Project Case Study" with the external icon. Each card gets a quiet tint from its own screenshot, as in v1.
   - **Prominence:** the strip is visibly lower in hierarchy than the featured panels.

## Craft floor applied

- Theme the browser surfaces: `::selection` using the panel accent or ink, `scrollbar-color`, `caret-color`, `text-underline-offset: .2em` and `text-decoration-thickness: 1px`.
- Focus rings use `--ink` on the ground and `--p-ink` in panels.
- Touch targets are 44px or larger.
- No horizontal page scroll; the rail scrolls inside its own container.
- Motion is limited to the disclosure open and close, a chevron rotation and a slight screenshot hover. There is no entrance animation.
- Images keep their width and height attributes.
