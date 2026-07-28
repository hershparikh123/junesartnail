# June's Art Nail — Design System

The visual and interaction language of the June's Art Nail studio site. This is
the source of truth for the brand: extend the site by composing these tokens and
patterns rather than inventing new ones.

**Personality:** bright, minimal, modern. One continuous sky, one small sun, and
a warm rose-to-magenta palette. Almost all separation is done with hairlines and
space rather than boxes or background slabs. Nothing shouts.

---

## 1. The organising idea: one day, one scroll

The whole page shares a **single fixed canvas** — one sky — instead of a run of
separately decorated sections. A single scroll-progress value (0 → 1) drives:

- the **sky's** two gradient stops (`--sky-a` top, `--sky-b` bottom), and
- the **sun's** position along an arc, and its colour.

The sun rises low-left at the top of the page, is overhead at the midpoint, and
sets low-right at the bottom. The footer is the one dark surface: night, after
the sun has gone. Scrolling the site is therefore one continuous story rather
than a sequence of unrelated panels — that continuity *is* the design.

| Scroll | Sun x | Sun y | Moment |
|---|---|---|---|
| 0.00 | 8% | 82vh | first light |
| 0.25 | 29% | 35vh | mid-morning |
| 0.50 | 50% | 16vh | overhead |
| 0.75 | 71% | 35vh | afternoon |
| 1.00 | 92% | 82vh | golden hour → night (footer) |

Arc: `x = 8 + p*84` (%), `y = 82 − sin(π·p)*66` (vh).

---

## 2. Brand foundations

| | |
|---|---|
| **Name** | June's Art Nail |
| **Location** | 441 Passaic Ave, Lodi, NJ 07644 |
| **Phone** | (973) 778-4494 · `tel:+19737784494` |
| **Services** | Manicures · Pedicures · Waxing · Permanent make-up |
| **Hours** | Mon–Fri 9:30 AM–7:30 PM · Sat 9:30 AM–6:30 PM · Sun closed *(per business card)* |
| **Descriptor** | "Full Service" |
| **Signature offer** | Free 10-minute massage with every Wednesday pedicure *(an add-on to pedicures — massage is not sold as a standalone service)* |
| **Voice** | Plain and warm — how the salon actually talks. Say the thing directly ("Prices depend on length, shape, and design"), not literarily ("the polish sets, the shoulders drop"). No marketing voice, no metaphor for its own sake. |

Section headings are plain statements — *What we do*, *Some of our recent work*,
*Come see us*. Because the headings now say what the section is, the repeated
uppercase eyebrow above each one was removed; only the hero keeps one.

---

## 3. Color

### The canvas pink

The business card is pink — that is the real brand color, and it is now the
canvas. `--pink #F4A6C0` · `--pink-soft #FBDCE7` · `--pink-deep #C43D6E`.
The sky ramps through it (see §1), the footer is a deep plum-pink night
(`--night #25101E`) rather than neutral black, and surfaces carry a hint of it
instead of plain white.

### The brand palette

The four brand swatches. These are **graphic** colors — bars, dots, rules, the
sun, the swatch wall.

| Token | Hex | |
|---|---|---|
| `--brick` | `#A2574F` | warm rosewood |
| `--peach` | `#E68057` | soft apricot |
| `--rose` | `#BF7587` | dusty rose |
| `--magenta` | `#993A8B` | the signature |

### Text-safe partners

Only `--magenta` is dark enough to carry small text on the sky unaided, so each
brand color has an `-ink` partner for type. **Small text uses the `-ink` value;
graphics use the plain one.**

| Token | Hex | On darkest sky |
|---|---|---|
| `--magenta-ink` | `#7E2E73` | 6.27:1 |
| `--brick-ink` | `#8A453E` | 5.28:1 |
| `--peach-ink` | `#9A4523` | 4.88:1 |
| `--rose-ink` | `#8E4A5C` | 4.82:1 |

### Neutrals & roles

| Token | Hex | Role |
|---|---|---|
| `--ink` | `#15191E` | primary text |
| `--ink-soft` | `#333C45` | secondary text |
| `--muted` | `#414A55` | tertiary text — deliberately dark (see §7) |
| `--line` | `rgba(21,25,30,.13)` | hairlines, the main separator |
| `--night` | `#14181D` | the footer only |
| `--accent` | = `--magenta` | large type, graphic marks |
| `--accent-deep` | = `--magenta-ink` | interactive: fills, links, focus |

**Categorical coding** (services and menu cards) maps onto the palette:
Manicures → magenta · Pedicures → peach · Waxing → brick ·
Permanent make-up → magenta. Because those vars color small labels, the markup
passes the `-ink` variants.

### Usage rules

- The canvas is the sky; sections are **transparent** by default. Separation is a
  `1px var(--line)` rule, occasionally a translucent white surface
  (`rgba(255,255,255,.5)`), never a colored slab.
- `--accent-deep` signals interactivity: button fills, the phone link, focus
  rings, the progress bar.
- White text needs `--accent-deep`, never `--accent`: white on the lighter
  magenta is 3.9:1 and fails; on the deep magenta it is 8.32:1.
- Focus ring: `2px solid var(--brass)` (→ accent), `outline-offset:3px`. Never remove.

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
- **Radii** — cards/pieces `4px`, buttons `2px`. The sun and swatch chips are the
  only round forms.
- **Grids** — menu 4→2 (≤980)→1 (≤540); wall 3→2 (≤920); gallery/studio/visit
  2→1 (≤720–820); services 4-col→stacked (≤820).

---

## 6. Components

| Component | Notes |
|---|---|
| **Sky** `.sky` | Fixed, `z-index:-2`, full-viewport gradient of `--sky-a`/`--sky-b`. |
| **Sun** `.sun` | Fixed, `z-index:-1`, `clamp(76px,9vw,140px)`. A plain disc plus one faint halo — no rays, no corona, no pulse. |
| **Button** `.btn` | Uppercase 12px, `2px` radius. Primary (`.gold`) is solid `--accent-deep` with white text, wiping to ink on hover. Secondary (`.line`/`.bone`/`.ghostbone`) is an ink outline that fills on hover. |
| **Nav** | Fixed, ink-on-sky throughout (no light/dark inversion). Frosts to `rgba(255,255,255,.62)` + blur once scrolled. 2px accent progress bar. |
| **Service row** `.svc` | Editorial list; hover washes `--accent-wash`, indents, grows a colored left bar (`--a`). |
| **Menu card** `.mcard` | Hairline compartment with a 4px colored top bar (`--mc`). |
| **Swatch chip** `.chip` | The one place with saturated color and glass: full-bleed polish gradient, gloss highlight, and a dark glass label that refracts it. |
| **Gallery piece** `.piece` | White hairline mat, slight tilt that rights on hover, image scales `1.04`. |
| **Voucher** `.voucher` | Translucent white panel with a blur — the Wednesday offer's anchor. |
| **Hours** | A `.glass` panel. **`.glass` supplies no padding of its own** — the list must provide it (`.3rem clamp(1.15rem,2.2vw,1.6rem)`) or rows sit flush against the panel edge. |
| **Footer** | `--night`. The story's full stop. |
| **Botanicals** `.botanical` | Line-art sprigs, blooms and a flowering branch. |

### 6b. Botanicals

Six inline SVG line drawings — sprigs framing the hero, a bloom in the intro, a
flowering branch over the shade wall, a sprig in the visit gutter, and a small
bloom on the footer's night edge.

They use the same idiom as the painted stroke: **every path carries
`pathLength="100"`**, so a single `stroke-dasharray:100` draws them all
uniformly regardless of their real length, and `.d2/.d3/.d4` stagger the parts so
a sprig unfurls stem → leaves → bloom. Stroke color comes from `--bot`, size from
`--bot-w`, opacity from `--bot-o` (0.3–0.5).

Two rules keep them from becoming clutter:

1. **They live in gutters, never over copy.** The content column caps at 1180px,
   so below ~1240px there is no gutter and `.b-intro`, `.b-wall` and `.b-visit`
   are `display:none`. Collision with real text nodes is measured at 375 / 885 /
   1425px, not eyeballed.
2. **They are armed by `.bot-anim`, not `.anim-ready`.** JS adds `.bot-anim` only
   while `document.visibilityState === "visible"`. CSS transitions do not advance
   in a hidden or prerendered tab, so gating on script-loaded alone would ship the
   flowers permanently invisible. Unarmed, they render fully drawn — the correct
   fallback.

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
| `--ink` on darkest sky | 13.32:1 |
| `--ink` directly over the sun | 12.18:1 |
| `--muted` on darkest sky | 6.78:1 |
| **`--muted` directly over the sun** | **6.21:1** |
| `--magenta-ink` (accent text) on sky | 6.27:1 |
| white on `--accent-deep` fill | 8.32:1 |
| white on the night footer | 17.82:1 |

Decorative layers are `aria-hidden`, `pointer-events:none`, and painted at
negative z-index beneath all content.

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
5. The restraint is the brand: one sky, one sun, hairlines, and space.
