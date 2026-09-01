---
title: Design Research — Anti-Slop Web Design with Claude
created: 2026-08-31
provider: claude-code
model: claude-sonnet-5
tags: [research, design, claude-workflows]
---

# Design Research — Anti-Slop Web Design with Claude

Research for a non-coder brand/narrative strategist building a portfolio site with Claude Code, whose complaint is generic AI-website feel (uniform sections, no scale contrast, uppercase mono micro-labels, invented conceptual framing, hedging prose). Goal: act as a curator reacting to visual work, not a prompt engineer.

## 1. Anti-slop techniques

**Anthropic's own cookbook** — "Prompting for frontend aesthetics" ([platform.claude.com/cookbook/coding-prompting-for-frontend-aesthetics](https://platform.claude.com/cookbook/coding-prompting-for-frontend-aesthetics)) — names the failure directly: *"You tend to converge toward generic, 'on distribution' outputs... it is critical that you think outside the box!"* Pasteable fragments: Typography — *"Avoid generic fonts like Arial and Inter... High contrast = interesting. Display + monospace, serif + geometric sans."* Scale — *"Use extremes: 100/200 weight vs 800/900, not 400 vs 600. Size jumps of 3x+, not 1.5x."* Color — *"Dominant colors with sharp accents outperform timid, evenly-distributed palettes."* Motion — *"One well-orchestrated page load with staggered reveals... creates more delight than scattered micro-interactions."* Notably absent: reference images, multi-direction generation, critique loops — those come only from the practitioner ecosystem below.

**Design-token-first ("DESIGN.md").** Write a persistent design-tokens doc — colors, type stack, spacing scale, named aesthetic family — *before* asking for UI, so Claude has a fixed target instead of re-sampling the average each session. Catalogued at scale in [awesome-claude-design](https://github.com/rohitg00/awesome-claude-design): 30+ example files across nine named aesthetic families, plus a "remix recipe" pattern (e.g. "Linear's typography + a terracotta accent") for combining two references into a third.

**Commit to one extreme, named.** Recurring advice (Adpharm, MindStudio, superdesign.dev) is a single named direction with 3–5 defining moves — "brutalist editorial," not "make it look nice" — with a confirm step before code. Ambiguity is what collapses toward the generic mean.

**Visual critique loop.** [design-loop](https://github.com/tonymfer/design-loop) is a Claude Code plugin that screenshots the live page section-by-section, scores each 1–5 against five fixed criteria (composition, typography, color/contrast, visual identity — explicitly the "portfolio test," polish), fixes the top three offenders, repeats until two consecutive 4/5+ passes. This is close to literal "curator, not prompt engineer": the human (or the loop, standing in) reacts to screenshots rather than writing prompts.

**Detect/rewrite existing slop.** [avoid-ai-design](https://github.com/funboy322/avoid-ai-design) audits already-generated frontend, prioritized P0 (obvious tells) → P2 (cosmetic) — a finishing pass, not a generation-time technique. Its tell catalogue is folded into Section 2.

**Source caveat:** most secondary writeups (MindStudio, superdesign.dev, aidesigner.ai) repackage the same Anthropic cookbook language rather than reporting independently. The two GitHub repos are stronger evidence — they encode technique as executable logic, not marketing prose.

## 2. Recognizable markers of AI-generated design, paired with counters

| Marker (the tell) | Counter |
|---|---|
| Inter/Roboto/Arial, no display face | Typeface with a point of view; pair contrasting families — "display + monospace, serif + geometric sans" ([cookbook](https://platform.claude.com/cookbook/coding-prompting-for-frontend-aesthetics)) |
| Indigo→purple gradient, gradient `bg-clip-text` headlines — traced to Tailwind's `indigo-500` overrepresentation in training data | Dominant color + one sharp accent; palette "drawn from something true about the product" ([925studios](https://www.925studios.co/blog/ai-slop-design-tells)) |
| Three/four-up card grid (rounded-2xl, soft shadow, top icon) — hero+cards+CTA template | Break the triptych: asymmetry, alternating rows, a marquee ([alexlavaee.me](https://alexlavaee.me/blog/lessons-learned-designing-with-ai/)) |
| Bento grid as default layout, not a choice | Reserve tile-grids for genuinely heterogeneous content |
| Uppercase letterspaced mono micro-labels on every section | If it's everywhere it's decoration — drop it, or use once where it earns meaning |
| Uniform section rhythm (same padding/pattern repeated) | Vary deliberately — full-bleed vs. contained, density shifts — "sections have rhythm" ([design-loop](https://github.com/tonymfer/design-loop)) |
| Glassmorphism/backdrop-blur by reflex, `rounded-2xl shadow-lg` everywhere | Reserve blur/radius for where it does representational work; flat sharp edges are a legitimate default |
| Nested cards within cards | Cap nesting at two levels; use a rule/divider instead |
| Weightless hedging copy ("Elevate," "Seamless," "Powerful yet simple") | Copy that "says something only your product could say" ([925studios](https://www.925studios.co/blog/ai-slop-design-tells)) |
| Worn default icons (Lucide Sparkles/ArrowRight/Zap) | Commit to one icon family, or drop icons for type-only markers |
| Timid even palettes, no scale contrast | Extremes not middles: weight 100/200 vs 800/900; size jumps 3x+, not 1.5x |
| Invented conceptual framing dressed as insight | No design-literature counter found — this is an "AI writing" tell (see `avoid-ai-writing`, sibling to `avoid-ai-design`), not a visual one. Flagging as a gap rather than inventing an answer. |

## 3. Claude Design / the `design` skill in Claude Code

Research preview, `v2.1.234+`, Pro/Max/Team/Enterprise ([Claude Code changelog, week 34 2026](https://code.claude.com/docs/en/whats-new/2026-w34)). Invoke with a brief, not a spec — changelog example: `/design redesign the composer based on what people actually use it for`. Claude drafts multiple `.dc.html` **artboards** on one pan/zoom **canvas**, published as an Artifact. Where saving is enabled, the canvas is a real visual editor — **click-to-select, properties panel, inline text editing, undo/redo**; otherwise it's **view-and-export (PNG/PDF)** only ([blakecrosley.com](https://blakecrosley.com/blog/claude-code-design-skill)). **Save publishes a new version for everyone.** Workflow: open canvas, pick one artboard, tell Claude which to implement — the curator motion, applied to N drafted directions instead of one.

**Good for:** UI mockups/screen flows, landing pages, marketing/social graphics, single-artboard print pieces. Fits the "generate several directions, then commit to one" pattern from Section 1.

**Limits:** research preview — no documented artboard-count cap, unclear re-seeding mechanics, editing-gate conditions unstated ([blakecrosley.com](https://blakecrosley.com/blog/claude-code-design-skill)). It drafts artboards, not the live site — the implementation step is still code generation, so final fidelity depends on that translation. It's a front-end for drafting/picking directions, not a substitute for stating an aesthetic direction explicitly.

## 4. Motion in single-file HTML (no build step, no CDN, strict CSP)

All native browser APIs — zero external scripts, CSP-safe, degrade gracefully. Scroll-driven animations (`animation-timeline: scroll()`/`view()`) ship in Chrome/Edge 115+, Firefox 132+, Safari 18+ (~84% global support); cross-document View Transitions ship in Chrome 126+, Firefox 128+, Safari 18+ ([MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Scroll-driven_animations/Timelines), [Chrome for Developers](https://developer.chrome.com/docs/web-platform/view-transitions/)).

**Scroll-triggered reveal — IntersectionObserver (universal support):**
```html
<style>
  .reveal { opacity: 0; transform: translateY(24px); transition: opacity .6s ease, transform .6s ease; }
  .reveal.is-visible { opacity: 1; transform: none; }
</style>
<script>
  const io = new IntersectionObserver((entries) => {
    for (const e of entries) if (e.isIntersecting) { e.target.classList.add('is-visible'); io.unobserve(e.target); }
  }, { threshold: 0.15 });
  document.querySelectorAll('.reveal').forEach(el => io.observe(el));
</script>
```

**SVG line-drawing — stroke-dashoffset (pair with the observer above):**
```css
.draw path { stroke-dasharray: 1000; stroke-dashoffset: 1000; transition: stroke-dashoffset 1.4s ease; }
.draw.is-visible path { stroke-dashoffset: 0; }
```
Use `path.getTotalLength()` at runtime instead of `1000` when precision matters.

**Staggered reveal — CSS-only:**
```css
.stagger > * { opacity: 0; animation: rise .5s ease forwards; animation-delay: calc(var(--i) * 90ms); }
@keyframes rise { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: none; } }
```
Set `style="--i:2"` etc. per child instead of hand-writing `nth-child` rules.

**CSS scroll-driven animation — no JS, tied directly to scroll position:**
```css
@supports (animation-timeline: view()) {
  .scroll-reveal { animation: fade-in linear both; animation-timeline: view(); animation-range: entry 0% cover 30%; }
  @keyframes fade-in { from { opacity: 0; transform: translateY(40px); } to { opacity: 1; transform: none; } }
}
.scroll-reveal { opacity: 1; } /* fallback outside @supports */
```

**View Transitions — progressive enhancement:**
```js
function updateView(renderFn) {
  if (!document.startViewTransition) return renderFn();
  document.startViewTransition(() => renderFn());
}
```
Cross-document (real page navigations) needs only CSS, no JS: `@view-transition { navigation: auto; }` on both pages.

All patterns stack — IntersectionObserver for broadest compatibility, `animation-timeline` behind `@supports`, View Transitions for page/state swaps. None require a bundler or CDN tag; `script-src 'self'` is enough.

## 5. The video question — "motion graphics for every line" from a Drive link

Claude does not natively watch or listen to video — it reads text: a transcript, timestamps, a description ([vomo.ai](https://vomo.ai/guide/can-claude-analyze-video)). Plausible pipeline: (1) transcription (Whisper or similar) produces a word/line-level timestamped transcript from the talking-head video; (2) Claude reads it and writes HTML/CSS/JS compositions, one motion-graphics treatment per line, keyed to timestamps; (3) a renderer turns that HTML into actual video frames over the source footage.

Step 3's tool is real: [HyperFrames](https://github.com/heygen-com/hyperframes), open-sourced by HeyGen (Apache 2.0, ~April 2026) — "write HTML, render video, built for agents." Agents write plain HTML with `data-start`/`data-duration` timing attributes; the CLI renders deterministically to MP4 via headless browser + FFmpeg, usable directly from Claude Code.

**Verdict:** plausible, no exotic capability required — Claude writes motion-graphics code driven by transcript timing, a separate deterministic renderer (HyperFrames, or similarly Remotion) produces the video. It is *not* Claude generating video directly or "watching" the Drive video — the link most likely supplied a transcript, or one was produced from it first. Treat "excellent results from just a Drive link" as plausibly embellished in the retelling; the real version still needs a transcription step and a renderer in the loop.
