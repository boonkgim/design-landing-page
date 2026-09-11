# The DESIGN.md format

DESIGN.md is **a record of design decisions**, not a style mandate and not a framework.
It is Google's open-source design-system spec (originated with the Stitch AI design tool,
`google-labs-code/design.md`, Apache 2.0): a self-contained plain-text file with a YAML
frontmatter block of machine-readable design tokens followed by a markdown body of
human-readable rationale.

The division of labour matters. **The tokens are the normative values** the build must
match exactly. **The prose explains why**, so that a human or another agent picking this
up later can extend the system without guessing. Prose may use descriptive names
("Midnight Forest Green") that correspond to systematic token names (`primary`).

This skill uses the official section list extended with two sections, `Images` and
`Icons`. The spec explicitly preserves sections beyond its own list, so this is a
sanctioned extension rather than a deviation.

## Frontmatter schema

```yaml
---
name: <string>                     # the design system's name, e.g. "Deep Signal"
description: <string>              # optional, one line on the direction
colors:
  <token-name>: <CSS color>        # at minimum `primary`; typically also secondary,
                                    # tertiary, neutral/surface, on-surface, outline, error
typography:
  <token-name>:
    fontFamily: <string>
    fontSize: <px|rem>
    fontWeight: <number>
    lineHeight: <px|rem|unitless multiplier>
    letterSpacing: <px|em>         # optional
rounded:
  <scale-level>: <px>              # e.g. none, sm, md, lg, xl, full
spacing:
  <scale-level>: <px|number>       # e.g. an 8px-based scale, plus gutters/margins
components:
  <component-name>:
    <property>: <literal | "{colors.primary}" reference>
---
```

Token references use `{path.to.token}` syntax, e.g. `backgroundColor: "{colors.primary}"`.
Component variants live under related keys: `button-primary`, `button-primary-hover`,
`button-primary-disabled`. Common component properties: `backgroundColor`, `textColor`,
`typography`, `rounded`, `padding`, `height`, `size`.

Recommended (non-normative) token names: colors `primary`, `secondary`, `tertiary`,
`neutral`, `surface`, `on-surface`, `outline`, `error`; typography `display-lg`,
`headline-lg`, `headline-md`, `body-lg`, `body-md`, `body-sm`, `label-lg`, `label-md`,
`label-sm`; rounded `none`, `sm`, `md`, `lg`, `xl`, `full`. Use whatever naming is
consistent; most systems carry 9 to 15 typography levels.

## Section order

All `##` headings, in this order. A landing page build should carry all of them.

1. **Overview** (also valid as "Brand & Style") - the holistic description: brand
   personality, who the page is for, and the emotional response it should produce
   (playful or serious, dense or spacious, loud or restrained). This is the context an
   agent falls back on for any decision the tokens do not cover, so make it specific
   enough to actually decide things.
2. **Colors** - each colour's role and where it is allowed, referencing token values:
   "**Tertiary (#B8422E):** the sole driver of interaction, used only for the primary
   action and critical highlights." **Write the accent's scarcity rule explicitly**, as a
   short list of where it may appear and where it may not. Accent colour leaks into
   decoration (quote rules, card edges, icon tiles) whenever that list is missing.
3. **Typography** - the type strategy: which faces, chosen *why*, and how the hierarchy
   works. Name any face reserved for a specific job (data, labels, quotes). If a widely
   defaulted face is used, say what it was chosen over and why, so it reads as a decision.
4. **Layout** - the grid and spacing model (fixed max-width, fluid, asymmetric editorial),
   the spacing rhythm, container widths, and how density changes between sections. **Record
   the hero composition here**: which archetype (type-led, full-bleed, product-first,
   before-and-after, offer-as-hero, portrait-led, statement figure, collage, editorial
   opener, split), and why it follows from this page's strongest asset. **Record the
   section rhythm too**: how the page paces, which section deliberately breaks the pattern,
   and how the offer's treatment differs from the supporting sections. See
   `layout-and-composition.md`.
5. **Elevation & Depth** - how separation and hierarchy are conveyed, stated as a
   deliberate order of escalation rather than one default: whitespace, surface tone shift,
   soft elevation, border. Give the real values (shadow definitions, surface steps) and say
   which method defines a card in this system, and which is reserved to make the offer
   outrank supporting content. Flat systems say so explicitly and name what does the work
   instead.
6. **Shapes** - the corner-radius language and its rationale, plus any other shape
   signature (cuts, seams, framing, how images are cropped or masked).
7. **Images** *(extension)* - the imagery type chosen for this direction and why it fits
   (real photography, AI-generated photography, illustration in a named style, product or
   screen demo, diagram, or a deliberately image-light treatment), the treatment that makes
   assets read as one system (crop ratios, colour grade, framing), where images appear, and
   what each one depicts and tells the reader. See `images-and-icons.md`.
8. **Icons** *(extension)* - the icon system: style, stroke width, size scale, filled or
   outline, and a meaning table mapping product concepts to icons. Inline SVG only, never
   emoji. State where icons are *not* used, since the common failure is decorative icon
   tiles filling a slot rather than carrying meaning.
9. **Components** - per-component guidance: buttons and their variants, cards, badges and
   status chips, form inputs, accordions, navigation, plus whatever this product needs.
   Cover states, not just resting appearance. **For every container type, say what defines
   it** (fill, elevation, border, spacing alone) rather than assuming a border, and say how
   the offer's container is deliberately distinguished from supporting ones.
10. **Do's and Don'ts** - concrete guardrails for this system ("the accent colour appears
    once per screen"), ending with the `### AI Slop Guardrails` subsection from
    `anti-slop-and-tone.md`.

## Writing it as a decision record, not a description

A DESIGN.md that only describes what the page looks like is a style sheet in prose. What
makes it worth keeping is the reasoning, so that the next person or agent extends the
system instead of guessing at it. Three habits do most of the work:

- **Say what was chosen over what.** One clause is enough: the faces considered and why
  this pairing won, the hero archetypes that did not fit this product's strongest asset,
  the separation method rejected as redundant. A rule with a reason survives contact with
  a new screen; a rule without one gets overridden the first time it is inconvenient.
- **Record constraints and exclusions carried in from review.** Palettes already rejected,
  typefaces used by a sibling direction, patterns the client called out. These are the
  decisions most likely to be silently reintroduced in a later round.
- **Write rules that can be checked.** "Generous whitespace" cannot be verified;
  "sections use 96px vertical padding, 64px under 640px, and the offer section alone gets
  128px" can. Prefer the checkable form wherever a real value exists.

## Fidelity between the document and the build

The point of the format is that the document and the implementation agree. Before calling
a design finished, diff the actual CSS values in the HTML against the token list: every
colour, face, radius, spacing step and icon style used must trace to a token or a
documented rule. Undocumented values are drift and get fixed in one direction or the
other, either the token list gains the value deliberately, or the build is corrected.
