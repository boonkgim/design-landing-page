# The DESIGN.md format

DESIGN.md is Google's open-source design-system spec (originated with the Stitch AI
design tool, `google-labs-code/design.md`, Apache 2.0). It is a self-contained,
plain-text representation of a design system: a YAML frontmatter block of
machine-readable design tokens, followed by a markdown body of human-readable design
rationale. Prose may use descriptive names ("Midnight Forest Green") that map to
systematic token names (`primary`); the tokens are the normative values, the prose is
context for how to apply them.

Every DESIGN.md produced by this skill extends the official 8-section spec with two
extra sections, `Imagery` and `Icons` (the spec explicitly allows and preserves
sections beyond its required list), and always ends its Do's and Don'ts with an
`### AI Slop Guardrails` subsection (see `anti-slop-and-tone.md`).

## Frontmatter schema

```yaml
---
name: <string>                     # the design system's name, e.g. "Deep Signal"
colors:
  <token-name>: <CSS color>        # at minimum a `primary` token; typically also
                                    # secondary, tertiary, neutral/surface, on-surface, error
typography:
  <token-name>:
    fontFamily: <string>
    fontSize: <px|rem>
    fontWeight: <number>
    lineHeight: <px|rem|unitless multiplier>
    letterSpacing: <px|em>         # optional
rounded:
  <scale-level>: <px>              # e.g. sm, md, lg, xl, full
spacing:
  <scale-level>: <px|number>       # e.g. an 8px-based scale
components:
  <component-name>:
    <token-name>: <literal | "{colors.primary}" reference>
---
```

Token references use `{path.to.token}` curly-brace syntax, e.g.
`backgroundColor: "{colors.primary-60}"`. Common recommended token names: colors
(`primary`, `secondary`, `tertiary`, `neutral`, `surface`, `on-surface`, `error`),
typography (`headline-lg`, `headline-md`, `body-lg`, `body-md`, `body-sm`, `label-lg`,
`label-md`, `label-sm`), rounded (`none`, `sm`, `md`, `lg`, `xl`, `full`). These are
non-normative naming conventions, not requirements, pick what fits the system.

## Section order (markdown body)

All `##` headings, in this exact order. None may be skipped for a landing page build
(the official spec allows omitting sections that don't apply, but a marketing landing
page needs all of them):

1. **Overview** — brand personality, target audience, the emotional response the UI
   should evoke (playful vs. professional, dense vs. spacious). Foundational context for
   every downstream stylistic decision not covered by an explicit token.
2. **Colors** — prose naming each color's role and referencing its token value, e.g.
   "**Primary (#1A1C1E):** a deep ink used for headlines...". At least `primary` must be
   covered.
3. **Typography** — prose on the type strategy: which faces, why, and the hierarchy
   (most systems have 9-15 typography levels).
4. **Layout** — the grid/spacing model (fixed-max-width grid, fluid grid, margin-driven,
   etc.) and the spacing rhythm (commonly an 8px base scale).
5. **Elevation & Depth** — how visual hierarchy is conveyed: real shadows and their
   exact values, tonal layering, or (for flat designs) borders/contrast instead.
6. **Shapes** — the corner-radius/shape language and its rationale.
7. **Imagery** *(extension)* — the one deliberate imagery style committed to (real
   photography with a specific treatment is the default choice this skill uses, see
   `photo-sourcing.md`; illustration or AI-generated photography are alternatives, never
   a mix of styles). Document exactly where images appear and what each one depicts.
   Imagery must communicate something real about the product; it is never decoration for
   empty space.
8. **Icons** *(extension)* — a real, consistent inline-SVG icon system: stroke width,
   size scale, filled vs. outline, and a concrete meaning table (what UI concept each
   icon represents). Never emoji, never an icon font.
9. **Components** — style guidance per component atom (buttons, cards, badges/chips,
   inputs, at minimum, plus whatever else the product needs). Note variants (hover,
   pressed, disabled) under related keys, e.g. `button-primary`, `button-primary-hover`.
10. **Do's and Don'ts** — concrete guardrails specific to this system (e.g. "the accent
    color is used for exactly one thing per screen"), ending with the
    `### AI Slop Guardrails` subsection from `anti-slop-and-tone.md`.

## Consistency is the whole point

Every color, font family, radius, spacing value, and icon style used in the
accompanying HTML must trace back to a token or a documented rule in that same
DESIGN.md. Before considering a design finished, diff the HTML's actual CSS values
against the DESIGN.md token list and fix any drift.
