# Craft values

Concrete numbers for the decisions that otherwise get made by adjective. A DESIGN.md rule
that can be checked against a value survives review; "generous spacing" and "soft shadows"
do not. Use these as defaults to depart from deliberately, not as a house style: a
direction that refuses them for a stated reason is fine, a direction that never named them
is unfinished.

## Type scale

Nine roles, as size / weight / line-height. Drawn from published design systems and a
structured review of 100 landing pages.

| Role | px | Weight | Line-height |
|---|---|---|---|
| Page title | 30 | 600 | 1.2 |
| Section heading | 20 | 500 | 1.4 |
| Lead | 18 | 400 | 1.45 |
| Body | 16 | 400 | 1.55 |
| Card body | 16 | 400 | 1.55 |
| Button label | 16 | 500 | 1.2 |
| Table cell | 14 | 400 | 1.45 |
| Caption | 14 | 400 | 1.45 |
| Label | 12 | 500 | 1.4 |

**This is a product UI scale**, and the 30px page title is a UI page title, not a marketing
hero. On a landing page the display end runs far larger, commonly `clamp(32px, 5vw, 56px)`
and up for a hero, with a section heading around 28 to 40px. Everything from the lead
downward holds as given: **body is 16px**, captions and table cells are 14px, and the 12px
label is the floor. What transfers exactly is the discipline, a real step between each
level rather than a smear of near-identical sizes, and line-height rising as size falls
(1.2 for display, around 1.55 for body).

## Measure, spacing, breakpoints

- **Measure**: cap line length at **65 to 75 characters** (`max-width: 65ch`). Reading
  degrades past 80. This applies to every paragraph, including ones inside cards.
- **Spacing scale**: a fixed set, `4, 8, 12, 16, 24, 32, 48, 64`. Values outside the scale
  are how rhythm decays. An 8px grid is the common alternative.
- **Breakpoints**: `sm 640`, `md 768`, `lg 1024`, `xl 1280`. A card grid typically runs 1
  across at sm, 2 at md, 3 at lg.

Most systems ship near-identical numbers here, so the point is not which set you pick, it
is naming yours in the DESIGN.md instead of improvising per section.

## Density

Two settings, chosen per surface rather than per page. A marketing page is almost always
comfortable; a dense schedule or comparison table may be compact.

| | Row | Control | Padding | Gap | Input padding | Button padding |
|---|---|---|---|---|---|---|
| Comfortable | 48px | 44px | 16px | 16px | 14px | 18px |
| Compact | 32px | 32px | 8px | 8px | 10px | 12px |

## Borders

Six kinds, each with a job. The point of the list is that "border" is not one decision.

| Kind | Job | CSS |
|---|---|---|
| None | A block that needs no edge | `border: none` |
| Hairline | A card boundary, kept quiet | `border: 1px solid rgba(0,0,0,.08)` |
| Solid | An input the eye can find | `border-color: #a3a3a3` |
| Thick | The selected item in a set | `border-width: 2px` |
| Divider | One rule, not a box each | `border-top: 1px solid #e2e2e2` |
| Focus ring | Drawn outside the edge | `outline: 2px solid #1565c0; outline-offset: 2px` |

**Every control needs a visible focus ring.** In a review of 100 pages only 64 percent had
one. It is the single most skipped accessibility affordance and it costs one declaration.

Note the divider row: when a set of items each get their own box, one rule between them is
usually the better answer (see the boxing tell in `anti-slop-and-tone.md`).

## Shadows

`box-shadow: <x> <y> <blur> <spread> <colour>`, where x and y move it, blur softens it,
spread resizes it.

| Step | For | Value |
|---|---|---|
| None | A page section | `none` |
| Small | A resting card | `0 1px 2px rgba(0,0,0,.06)` |
| Medium | A card on hover | `0 3px 8px rgba(0,0,0,.10)` |
| Large | A dropdown | `0 6px 16px -2px rgba(0,0,0,.12)` |
| Extra large | A modal | `0 8px 20px -4px rgba(0,0,0,.16)` |

Elevation should map to how far an element is from the page, not to how important its
content is. Importance is a job for size, space and position.

## Radius

| Value | Reads as |
|---|---|
| 0px | Square and technical |
| 2px | Barely softened |
| 4px | The neutral default |
| 8px | Clearly rounded |
| 16px | Friendly and soft |
| 9999px | A pill |

Pick one base radius and derive the rest. Pills are for tags and chips. Match the radius
to the element: 24px on a small card rounds it into a soft blob, and cards generally want
12 to 16px.

## Colour

**Work in OKLCH.** Its three axes are perceptual: lightness 0 to 1 (black to white), chroma
0 to about 0.32 (sRGB's ceiling, reached only around magenta), and hue 0 to 360. The reason
it matters: `hsl(60 100% 50%)` is a blinding yellow and `hsl(240 100% 50%)` is a near-black
blue, and both claim 50 percent lightness. OKLCH reads them 0.97 and 0.45. Lightness in
OKLCH can be compared across hues, which is what makes a palette tunable rather than
guessed.

**The vocabulary maps onto the axes**, which turns adjectives into edits:

| Word | Axis |
|---|---|
| saturated, muted | chroma |
| deep, dark, bright, vibrant | lightness |
| warm, cool | hue |
| tint, shade, tone | mixed with white, black, grey |

**A palette is a shape**: how many hues you spend and how much chroma you allow. Name the
shape rather than listing hex codes. Six that cover most products, five swatches each:

| Shape | Swatches `oklch(L C H)` | Suits |
|---|---|---|
| Neutral plus one accent | `0.98 0.002 250`, `0.92 0.004 250`, `0.72 0.006 250`, `0.32 0.008 250`, `0.55 0.14 250` | dashboards, admin, dense data |
| Warm and earthy | `0.95 0.012 85`, `0.84 0.04 80`, `0.66 0.07 60`, `0.55 0.09 40`, `0.42 0.05 120` | craft, wellness, hospitality |
| Cool and corporate | `0.97 0.005 250`, `0.88 0.02 245`, `0.62 0.11 250`, `0.45 0.13 255`, `0.3 0.05 250` | fintech, business software, health |
| Dark ground, one bright | `0.18 0.01 265`, `0.26 0.012 265`, `0.38 0.015 265`, `0.8 0.02 265`, `0.78 0.17 150` | developer tools, media, night use |
| Saturated flats | `0.55 0.22 27`, `0.82 0.15 88`, `0.45 0.2 265`, `0.2 0.01 90`, `0.97 0.003 90` | education, children, a point of view |
| Pastel tints | `0.9 0.045 25`, `0.9 0.045 90`, `0.9 0.045 160`, `0.9 0.045 240`, `0.9 0.045 320` | onboarding, calm consumer apps |

Roles to fill: primary (required), secondary, accent, neutral, surface and on-surface, and
destructive. Note how the palettes differ in kind, not just hue: the pastel set holds L and
C fixed and moves only hue, the dark set spends almost no chroma until the single bright.

## Motion

**Five kinds**: micro-interaction (hover, focus, active), state change (idle, loading,
done), enter and exit (modal, toast), loading (skeleton, spinner, progress), and
scroll-linked (reveal, sticky header).

**Four primitives**, and almost everything is a combination of two:

| Primitive | Value | Used for |
|---|---|---|
| Fade | `opacity: 0 → 1` | every enter and exit; skeletons pulse it alone |
| Slide | `translateY(16px) → 0` | toasts, dropdowns, scroll reveals; travel of 8 to 16px |
| Zoom | `scale(0.95) → 1` | modals from 95 percent; buttons to 97 percent on press |
| Spin | `rotate(360deg)` | the only one that loops |

**Timing**: 100ms reads as too fast, 200ms is about right, 500ms is too slow. Easing:
`linear` is machine-like, `ease-out` is the default to use, bounce reads as a toy.

```css
--motion-fast: 120ms;
--motion-base: 180ms;
--motion-ease: cubic-bezier(0.2, 0, 0, 1);
transition: transform 180ms, opacity 180ms;
@keyframes spin { to { transform: rotate(360deg); } }
```

The working recipe is **a fade plus one small move**: 8 to 16px of travel, or a scale
between 94 and 97 percent. And `prefers-reduced-motion` has to be asked for by name or it
will not appear.

## Six principles, and what each looks like in a DESIGN.md

| Principle | Written as |
|---|---|
| Hierarchy | a real step between each type size |
| Contrast | 4.5:1 for body text, 3:1 for large text |
| Alignment | one grid, and nothing placed by eye |
| Proximity | tight inside a group, loose between groups |
| Repetition | one accent and one radius, reused |
| Restraint | two font families, not five |
