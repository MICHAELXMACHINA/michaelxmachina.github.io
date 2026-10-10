# Direction B: Journal

**Idea.** A light, printed-matter page tied to the CV: warm paper, near-black ink, hairline rules and one 12-column grid, with terracotta reserved for links and actions. The four projects share one monograph layout (metadata in a narrow left margin, title, then the screenshot as a plate in a ruled mat tinted from the client's palette), and the two section heads are the loudest type on the page.

## Tokens

| Token | Value | Contrast on paper `#f8f6f0` |
|---|---|---|
| Paper | `#f8f6f0` (CV paper) | |
| Ink | `#202721` | 14.2 |
| Body | `#343b35` | 10.7 |
| Dim (labels, credits) | `#5d655d` | 5.6 |
| Terracotta (links, actions only) | `#a74832` (CV accent) | 5.4 (AA for small text) |
| Hairline / strong rule | `#cfd3c8` / ink | decorative |
| Plate mats | Astroscale `#e6e9ee`, Matter `#e4e9db`, Everyday Dose `#f1e4ec`, Ursa Major `#eee3d3`, collaborations `#efece3` | no text on mats |

Type: Archivo 700 (display, tracking -0.05em; the hero's second line is weight 300) and Work Sans 400/500. Scale: hero up to 9.6rem; section heads up to 6rem; project titles up to 4rem; lead 1.25 to 1.5rem; text 1.0625rem; small sizes limited to three (0.8125, 0.9375 and 1.0625rem).

Grid: 12 columns. Left margin column (cols 1-3) for case numbers, role and credit; content from col 4. Services use the same split: service name left, three tiers as a ruled table-like grid on the right. More Collaborations: three plates, then two wider ones (6-col scheme).

## Decisions

- Services render fully expanded (no `<details>`), tiers as columns with ruled lists. Service names became h3 and tiers h4 for correct outline; text unchanged.
- Hero's lime span became a weight contrast (700 versus 300) instead of a color.
- The mat tint is the carry-over of the Matter and Everyday Dose treatment, kept calm and light so the page stays one system.
- Only motion: hover underline and border changes. No entrance animation (tried one; removed because it was captured mid-fade and the page does not need it).

## Verified

- Word multiset, alt text, image src/width/height and link hrefs are identical to `/work/index.html` (scripted comparison).
- No horizontal overflow at 390, 768, 1440 and 1920 (iframe scrollWidth check).
- Screenshots at 1440 and 500 in `shots/` reviewed section by section; mobile stacks name, plate, role, copy.
- Contrast pairs computed (table above). Touch targets: nav links, index links, case links and credit links are at least 44px tall. `:focus-visible` outline in terracotta; `prefers-reduced-motion` honored; no JavaScript.

## Known issues

- DOM order within Matter changed slightly: the screenshot now precedes the role and copy (as in the other three) and the caption "Brand and Content for Matter Venture Partners" sits under the plate. The same words are present; only Matter's source order differs from the original.
- Credit lines moved next to "My Role" for Matter and Ursa Major (Matter's was after the copy).
- Lazy images below the fold were captured after loading in the final screenshots; headless may show blanks elsewhere.
- Civic's source screenshot is pale, so its plate looks washed out; that is the asset, not the layout.
- Google Fonts needs network; fallback is Arial.
