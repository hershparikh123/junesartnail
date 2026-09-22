# June's Art Nail — Design System

The visual and interaction language of the June's Art Nail studio site. This is
the source of truth for the brand: extend the site by composing these tokens and
patterns rather than inventing new ones.

**Personality:** calm, warm, unhurried: the exhale after summer. One continuous
autumn sky, one low sun, leaves that turn as you scroll, and a maple-to-moss
palette. Almost all separation is done with hairlines and space rather than
boxes or background slabs. Nothing shouts; nothing moves fast.

---

## 1. The organising idea: one season, one scroll

The whole page shares a **single fixed canvas** (one sky) instead of a run of
separately decorated sections. A single scroll-progress value (0 → 1) drives:

- the **sky's** two gradient stops (`--sky-a` top, `--sky-b` bottom), from
  late-summer gold to deep persimmon,
- the **sun's** position along an arc, and its colour, and
- the **leaf colour** of every branch leaf (`--leaf-now` plus a per-leaf fill).

The top of the page is the last warm week of summer. By the bottom the leaves
have gone red and brown, and the footer is the first cold night. Scrolling the
site is one continuous story rather than a sequence of unrelated panels, and
that continuity *is* the design.

| Scroll | Sun x | Sun y | Moment |
|---|---|---|---|
| 0.00 | 8% | 82vh | late summer |
| 0.25 | 29% | 35vh | early fall |
| 0.50 | 50% | 16vh | peak colour |
| 0.75 | 71% | 35vh | turning |
| 1.00 | 92% | 82vh | late autumn → first cold night (footer) |

Arc: `x = 8 + p*84` (%), `y = 82 − sin(π·p)*66` (vh).

---

## 2. Brand foundations

| | |
|---|---|
| **Name** | June's Art Nail |
| **Location** | 441 Passaic Ave, Lodi, NJ 07644 |
| **Phone** | (973) 778-4494 · `tel:+19737784494` |
| **Services** | Manicures · Pedicures · Waxing |
| **Hours** | Mon–Fri 9:30 AM–7:00 PM · Sat 9:30 AM–6:00 PM · Sun closed |
| **Parking** | Own lot, plus street parking |
| **Descriptor** | "Full Service" |
| **Signature offer** | Free 10-minute massage with every Wednesday pedicure *(an add-on to pedicures — massage is not sold as a standalone service)* |
| **Voice** | Plain and warm — how the salon actually talks. Say the thing directly ("Prices depend on length, shape, and design"), not literarily ("the polish sets, the shoulders drop"). No marketing voice, no metaphor for its own sake. |

Section headings are plain statements — *What we do*, *Some of our recent work*,
*Come see us*. Because the headings now say what the section is, the repeated
uppercase eyebrow above each one was removed; only the hero keeps one.

---

## 3. Color

### The canvas

An autumn sky that deepens as you scroll. Every stop stays high-luminance
(see §7). Keyframes live in the `DAY` array in the script:

| p | Sky top | Sky bottom | Moment |
|---|---|---|---|
| 0.00 | `rgb(252,232,198)` | `rgb(250,219,180)` | late summer |
| 0.34 | `rgb(251,226,188)` | `rgb(249,214,172)` | early fall |
| 0.62 | `rgb(249,218,178)` | `rgb(247,206,165)` | peak colour |
| 1.00 | `rgb(246,204,160)` | `rgb(242,190,146)` | late autumn |

The footer is `--night #1E130D`: a cold bark-brown night, not neutral black.

### The autumn palette

**Graphic** colours: bars, dots, rules, leaves.

| Token | Hex | |
|---|---|---|
| `--maple` | `#B4441F` | the signature (accent) |
| `--pumpkin` | `#D9772B` | warm orange |
| `--cranberry` | `#8E2C3A` | deep red |
| `--moss` | `#6F7A3A` | the last green |
| `--gold` | `#D9A534` | ticker dots |
| `--bark` | `#6E3F24` | branch stems |
| `--harvest` | `#F2C48D` | type on the night footer |

### Text-safe partners

**Small text uses the `-ink` value; graphics use the plain one.**

| Token | Hex | On deepest sky |
|---|---|---|
| `--maple-ink` | `#8C3115` | 4.89:1 |
| `--cranberry-ink` | `#7C2433` | 5.82:1 |
| `--pumpkin-ink` | `#7E3D0D` | ≥4.5:1 |
| `--moss-ink` | `#4B5522` | 4.79:1 |
| `--bark-ink` | `#6E3F24` | 5.23:1 |

### Neutrals & roles

| Token | Hex | Role |
|---|---|---|
| `--ink` | `#2A1A12` | primary text |
| `--ink-soft` | `#4A362A` | secondary text |
| `--muted` | `#553F31` | tertiary text, deliberately dark (see §7) |
| `--line` | `rgba(58,32,18,.13)` | hairlines, the main separator |
| `--accent` | = `--maple` | large type, graphic marks |
| `--accent-deep` | = `--maple-ink` | interactive: fills, links, focus |

Surfaces (cards, gallery mats, nav, voucher) use a warm near-white
(`#FFFAF1` / `rgba(255,250,240,…)`), not pure white. Shadows are tinted toward
bark (`rgba(58,32,18,…)`).

**Categorical coding** (services and menu cards):
Manicures → cranberry · Pedicures → pumpkin · Gel & sets → maple · Waxing → moss.
The markup passes the `-ink` variants because those vars colour small labels.

### Usage rules

- The canvas is the sky; sections are **transparent** by default. Separation is a
  `1px var(--line)` rule, occasionally a translucent warm surface, never a
  coloured slab.
- `--accent-deep` signals interactivity: button fills, the phone link, focus
  rings, the progress bar.
- White text needs `--accent-deep` (8.19:1), never `--accent`.

---

## 4. Typography

| Token | Stack | Use |
|---|---|---|
| `--serif` | **Fraunces**, Georgia, serif | display headings, italic emphasis |
| `--sans` | **Instrument Sans**, Arial, sans-serif | body, UI, labels |

Fraunces is loaded as a **variable font with its `SOFT` and `WONK` axes**, not
the default instance. Display type is set at `"opsz" 144, "SOFT" 26` — the high
optical size gives a finer, higher-contrast cut; the softened terminals keep it
from turning brittle at scale. Italic emphasis adds `"WONK" 1` for the alternate
single-storey forms.

Display sits at **weights 290–340**. The rule is that display type earns its
scale by being set finely — light weight, tight tracking (`-.03em` at section
level, `-.035em` on the hero, never past the `-.04em` floor) — rather than by
being merely large.

**Numerals:** body prose uses `oldstyle-nums proportional-nums`, which sit on the
baseline like book type. Anything columnar — `.hours`, `.facts`, `.voucher dd`,
`.legal` — reverts to `lining-nums tabular-nums` so figures align.

| Role | Spec |
|---|---|
| Hero `h1` | `clamp(3rem, 8vw, 6rem)`, serif 330, `letter-spacing:-.025em` |
| Promo `h2` | `clamp(2.6rem, 5.6vw, 4.6rem)`, serif 340 |
| Section `h2.title` | `clamp(2rem, 4.6vw, 3.5rem)`, serif 380 |
| Body | `16.5px`, `line-height:1.72` |
| Label / meta | `9.5–11px`, `.22–.34em` tracking, uppercase, 700 |

`text-wrap: balance` on headings, `pretty` on long prose.

---

## 5. Spacing & layout

- **Container** `.wrap` — `max-width:1180px`, `padding:0 6vw`.
- **Section rhythm** — `clamp(5rem, 10vw, 8.5rem)` vertical.
- **Radii** — cards/pieces `4px`, buttons `2px`. The sun is the only round form.
- **Grids** — menu 4→2 (≤980)→1 (≤540); gallery/studio/visit
  2→1 (≤720–820); services 4-col→stacked (≤820).

---

## 6. Components

| Component | Notes |
|---|---|
| **Sky** `.sky` | Fixed, `z-index:-2`, full-viewport gradient of `--sky-a`/`--sky-b`. |
| **Sun** `.sun` | Fixed, `z-index:-1`, `clamp(76px,9vw,140px)`. A pale low autumn sun: a plain disc plus one faint amber halo. No rays, no corona, no pulse. |
| **Button** `.btn` | Uppercase 12px, `2px` radius. Primary (`.gold`) is solid `--accent-deep` with white text, wiping to ink on hover. Secondary (`.line`/`.bone`/`.ghostbone`) is an ink outline that fills on hover. |
| **Nav** | Fixed, ink-on-sky throughout (no light/dark inversion). Frosts to `rgba(255,255,255,.62)` + blur once scrolled. 2px accent progress bar. |
| **Service row** `.svc` | Editorial list; hover washes `--accent-wash`, indents, grows a colored left bar (`--a`). |
| **Menu card** `.mcard` | Hairline compartment with a 4px colored top bar (`--mc`). |
| **Gallery piece** `.piece` | White hairline mat, slight tilt that rights on hover, image scales `1.04`. |
| **Voucher** `.voucher` | Translucent white panel with a blur — the Wednesday offer's anchor. |
| **Hours** | A `.glass` panel. **`.glass` supplies no padding of its own** — the list must provide it (`.3rem clamp(1.15rem,2.2vw,1.6rem)`) or rows sit flush against the panel edge. |
| **Footer** | `--night`. The first cold night; the story's full stop. |
| **Branches** `.botanical` | Autumn branches whose leaves change colour with the season (§6b). |
| **Falling leaves** `.leaves` | A slow background drift; each leaf ripens as it falls (§6b). |

### 6b. Branches and falling leaves

**Branches** `.botanical`: two autumn branches framing the hero, a large
maple-leaf outline in the intro gutter, a leafy twig in the visit gutter, and
one small leaf on the footer's night edge. Leaf shapes (`#lf-maple`, `#lf-oak`,
`#lf-elm`) are `<symbol>`s in one sprite at the top of `<body>`.

- Stems use the painted-stroke idiom: **every path carries `pathLength="100"`**,
  so one `stroke-dasharray:100` draws them all, and `.d2–.d5` stagger the parts.
- Leaves (`.lf`) are filled `<use>`s. JS sets each one's fill from the
  **season ramp** (green `#8E9B3F` → gold → amber → pumpkin → maple red →
  crimson → brown `#7A4228`). Input is `ripen + scrollProgress` plus that
  leaf's own `data-o` offset, so a branch turns unevenly, like a real tree.
- On load, `ripen` eases from 0 to 0.24 over ~6s, so the hero leaves visibly
  turn from green to gold before anyone scrolls.

**Falling leaves** `.leaves`: a fixed layer at `z-index:-1`. JS builds 16 (9
on phones), each with its own speed (18–30s), sway, size and opacity (.4–.62).
Every leaf **ripens while it falls** through a `leaf-ripen` keyframe on
`fill`. Negative delays start them mid-fall. Transform-only animation. With
reduced motion the layer is never built and is `display:none`.

Two rules keep the branches from becoming clutter:

1. **They live in gutters, never over copy.** Below ~1240px there is no gutter,
   so `.b-intro` and `.b-visit` are `display:none`.
2. **They are armed by `.motion-ok`, not `.anim-ready`** (see §8). Unarmed,
   they render fully drawn and fully leafed, which is the correct fallback.

---

## 7. The legibility contract

The page is **dark ink on a permanently light sky**. That is a structural
decision, not a stylistic one: it means text contrast cannot break as the sun
moves, which was the failure mode of the earlier dark treatment.

Three rules keep it true:

1. **Every sky stop stays high-luminance.** The sky never darkens toward the
   text; it only shifts hue.
2. **The sun stays pale.** A saturated peach disc drops muted body text over it
   to ~3.2:1. Pale tints of the brand peach hold it at **6.21:1** at the worst
   point of the day. If the sun is ever re-saturated, this breaks.
3. **`--muted` is deliberately dark** (`#414A55`, not a light gray) so that even
   tertiary copy survives passing over the sun.

Measured worst cases across the whole scroll (all AA-passing):

| Pair | Worst |
|---|---|
| `--ink` on deepest sky | 10.01:1 |
| `--muted` on deepest sky | 5.86:1 |
| `--muted` directly over the sun | 7.15:1 |
| `--maple-ink` (accent text) on deepest sky | 4.89:1 |
| `--maple` (large display type only) on deepest sky | 3.32:1 |
| white on `--accent-deep` fill | 8.19:1 |
| white on the night footer | 18.19:1 |
| `--harvest` on the night footer | 11.31:1 |

Decorative layers are `aria-hidden`, `pointer-events:none`, and painted at
negative z-index beneath all content. Falling leaves stay small and at most 0.62
opacity so text they drift behind stays legible.

**Re-measure after any color change.** Both regressions found so far (a 4.17:1
note, a 2.44:1 paragraph over the sun) were caught by measuring, not by eye.

---

## 8. Motion

| Token | Curve | Use |
|---|---|---|
| `--ease-lux` | `cubic-bezier(.16,1,.3,1)` | the house curve (expo-out) |
| `--ease` | `cubic-bezier(.22,.7,.25,1)` | legacy / gentle |
| `--ease-inout` | `cubic-bezier(.62,.03,.21,1)` | symmetric moves |

Durations follow the 100/300/500 rule: **~90–120ms** for press feedback (under
the ~80ms perception threshold it reads as instant/mechanical), 300–500ms for
state changes, 500–1100ms for entrances. **Exits run ~75% of enter.** No bounce,
no elastic — nothing overshoots.

- **The day** — sky and sun update from one rAF-coalesced scroll handler: a
  single `scrollY` read per frame, then batched writes.
- **Section titles** — a **mask wipe**, not another fade-up: the words rise from
  behind their own baseline inside an `overflow:hidden` wrapper. Fade-and-rise on
  every section is the saturated default and reads as generic; this is the one
  signature reveal. The wrapper carries `padding-bottom:.16em` with matching
  negative margin so the clip never cuts descenders, and it uses **no gradient
  mask** — a static one would permanently fade the top of every heading.
- **Interaction layer** — every control has hover *and* press. The button wipe
  runs 520ms in / 260ms out with a separate 90ms press; cards lift on
  `--lift-1→2→3`; the nav rule wipes in from the left and out to the right.
- **Service rows** indent via `transform` on the children, **never animated
  padding** — padding drives layout and reflows the list on every hover. The
  title leads the rest by 0.3rem; that differential is what reads as considered.
- **Painted stroke / botanicals** — self-drawing SVG, the brand's hand mark.

### The motion gate (`.motion-ok`)

Anything animated by a **pure CSS transition** hides its start state behind
`.motion-ok`, and JS sets that class *only while `document.visibilityState` is
`"visible"`*.

CSS transitions do not advance in a hidden, backgrounded, or prerendered tab.
Gating on "script loaded" alone strands those elements in their start state
permanently — botanicals invisible, section headings displaced 105% and clipped
out of view. Both were caught by measuring the frozen state, not by eye.

Unarmed, everything renders in its final state. **Any new CSS-transition reveal
must sit behind `.motion-ok`.**

### The settle watchdog (anime.js content)

anime.js entrances animate `opacity:[0,1]`, so a stalled animation leaves content
at 0. The `settle` pass at 2.5s restores every registered end state.

**A running WAAPI animation outranks inline styles.** anime.js v4 is built on the
Web Animations API, so `utils.set()` — which writes inline styles — *cannot*
rescue an animation that started and then froze. Measured: inline style read
`opacity: 1` while the computed value stayed `0`. The watchdog was silently
ineffective for the whole page body.

`settle` therefore calls `finishAnims()` **before** `utils.set()`, explicitly
finishing stalled animations. Animations with `iterations === Infinity` (ticker,
gloss sweep) are skipped — `.finish()` throws on them and they are ambient, not
content-revealing.

**Two invariants for anyone adding an entrance:**

1. Every element the CSS hides must appear in the animation targets *and* in the
   watchdog's end state. The hero eyebrow was hidden by `.fade-up` but missing
   from the timeline, so it rendered at opacity 0 on every load.
2. Any new `settle.push` must `finishAnims(toEls(targets))` before setting styles.

`prefers-reduced-motion` is honored throughout: `anim-ready` and `motion-ok` are
both withheld, and CSS forces `.reveal`, `.fade-up` and `.w` visible.

---

## 9. Extending the system

1. New section → `<section>` + `.wrap`, transparent background, separated by a
   `--line` rule. Don't add a background slab.
2. New color only if it maps to a real category — add it as a `:root` token
   **with an `-ink` partner** if it will ever carry small text.
3. Any new decorative layer goes behind content and must not darken the sky.
4. Re-run the contrast table in §7 before shipping a color change.
5. The restraint is the brand: one sky, one sun, one season, hairlines, and space.


---

## 10. The harvest layer (fall, back to school)

The fall season runs the page as a series of distinct worlds, and each one is
deliberately different: a dark harvest dusk, a pumpkin band, a chalkboard, warm
paper and flannel, a notebook page, then night. The CSS sits in one block at
the end of the stylesheet (`HARVEST — the second fall layer`), so the season
can be lifted out later.

| Piece | What it is |
|---|---|
| **Hero dusk** `.hero-sky` | Its own sky: `#140807` → `#6E2911` with an ember glow at the horizon, a scatter of breathing stars, and a harvest `.moon`. Type turns cream (`--cream #FBEBD3`), the accent becomes `--glow #F29A4A`, and the nav gets `.on-dark` while it is over the hero. |
| **Hero leaves** `.hero-leaves` | A second falling-leaf layer inside the hero (14, or 8 on phones) at higher opacity with a soft glow. |
| **Handwritten note** `.hand-note` | "hello, sweater weather" in `--hand` (Homemade Apple), `aria-hidden`, pinned to the headline. It is the only new copy on the page. |
| **Pumpkin patch** `.patch` | A hill silhouette, a cluster of pumpkins, and a stack of schoolbooks with an apple and a pencil. |
| **Pumpkins** `#pk` | One symbol: five ribs share a radial gradient. `--pkf` swaps it for `#pkO` orange, `#pkW` white, `#pkR` red, or `#pkG` green gourd. They appear in the patch, the services header and the footer step. |
| **Pumpkin band** `.ticker` | Solid `--ember #E0702A` with dark type (5.49:1). |
| **Chalkboard** `.promo-in` | A slate board (`--board #1E2A24`) with chalk dust, a wood frame, a chalk ledge, and self-drawing chalk doodles (`.botanical.chalk`). |
| **Index card** `.voucher` | Ruled paper with a red margin line and striped tape. It uses the `rotate` property rather than `transform`, so anime.js entrances compose with it. |
| **Flannel** `.services` | A two-axis plaid at 6% over warm paper. |
| **Menu cards** `.mcard` | Index cards at slight alternating angles. The coloured `.bar` became a strip of tape. |
| **Polaroids** `.piece` | Plaid tape on top, with the caption in the handwritten face. |
| **Pumpkin spice latte** `.psl` | A cup beside "Plan your visit", with steam that rises (static when reduced motion is on). |
| **Notebook hours** `.hours` | Ruled lines, a red margin, three punched holes, today's row circled in red pencil, and an apple on the corner. |
| **Pencil** `.progress` | The scroll progress bar is a yellow pencil with an eraser and a sharpened tip. It is hidden at the top of the page. |

Legibility: cream on the hero dusk is at least 9.0:1 (at the horizon), chalk on the board is
12.96:1, dark ink on the `--glow` button is 7.57:1, and dark ink on the pumpkin band
is 5.49:1. The moon is placed clear of the copy at every width (on phones it
rises over the patch). Collisions are measured, not eyeballed.
