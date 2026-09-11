# Layout and composition

Palette and typeface are the easy half of a direction. Composition is what actually makes
two designs feel different, and it is where generated pages converge hardest: given the
same brief, independent attempts reliably produce the same page with different colours.

Evidence from the project this skill came from: eight landing pages, built by eight
separately briefed agents with deliberately opposed palettes, type pairings and moods.
Every single one produced the same hero, copy in a left column, a rounded photo in a right
column, at ratios between 1.05:1 and 1.2:1. The directions were distinct everywhere except
the part of the page a visitor sees first.

## The hero is a decision, not a template

The split hero (copy left, media right, vertically centred, two CTAs, a meta line under
them) is the default that arrives when nobody asked what the hero should be. It is a
perfectly good layout, and it is the right answer often enough that it keeps getting
chosen, which is exactly why choosing it by reflex is invisible until you see four of them
in a row.

Ask first: **what is the strongest asset this page has?** The hero should be built around
the answer.

| If the strongest asset is | Consider |
|---|---|
| the promise itself, stated well | a **type-led hero**: large headline, no media, generous space, one CTA. Works when the sentence is genuinely good and the brand can carry restraint |
| a scene or atmosphere | a **full-bleed image or video** with overlaid copy, or a wide image band under a short copy block. Needs contrast discipline to stay AA |
| the product or its output | a **product-first hero**: the interface, a real screen, or a sample of actual output at large scale, with copy sized as support above or beside it |
| a transformation | a **before and after** composition: the two states side by side or stacked, the copy naming the change |
| the offer itself (a date, a price, availability) | a **hero that is the offer**: the bookable thing surfaced immediately, copy compressed to a line or two above it |
| a person (a founder, an instructor, a practitioner) | a **portrait-led hero**, often full-height on one side or as a large bleed, with the copy in their voice |
| a number or a proof point | a **statement hero** built around that figure at display scale |
| variety and energy | a **collage or layered composition**: several images at different scales, overlapping the type, breaking the grid |
| the sheer quality of the writing | an **editorial opener**: asymmetric measure, oversized drop line, the media entering below the fold rather than beside the headline |

Other structural variables worth moving, independent of the archetype: whether the hero
is full-viewport-height or short and dense; whether media bleeds off an edge or sits
inside the container; whether the copy is left, centred, or offset into a narrow column;
whether the CTA sits inline with the copy or in a band below; whether the section ends on
a hard edge, a diagonal, or a colour change.

## The rest of the page needs rhythm too

The same convergence happens below the fold: every section becomes a centred heading, a
lead paragraph, and a grid of equal cards. A page built that way has no pacing, and the
visitor's eye has no reason to slow down anywhere in particular.

Vary deliberately:

- **Alternate the shape of sections**: a full-bleed band, then a two-column asymmetric
  split, then a simple centred column, then a wide table-like list.
- **Vary density**: put air around the sections that matter most and let supporting
  material sit tighter. Uniform padding everywhere flattens importance.
- **Change the container**: a narrow measure for reading, a wide one for the offer, edge
  to edge for imagery.
- **Give the offer a different treatment from everything else.** It is the section you
  want people to stop at, so it should not share a recipe with the FAQ.
- **Let one section break the pattern.** A single deliberate departure (an oversized
  quote, a full-width image, a dark band in a light page) creates a landmark and makes the
  page memorable.

## The moves you have to ask for

Everything in a spacing, radius and colour scale describes a rectangle sitting straight.
No scale has a step for character, so an agent left to itself ships a plain rounded
rectangle every time. If a direction is supposed to have edge, the expressive moves have
to be named explicitly in the DESIGN.md, with values, or they will not appear:

- **Rotation.** A slight `transform: rotate(-2deg)` on a card, photo or badge, so an
  element sits like something placed by hand rather than laid out by a grid.
- **Hard shadow.** An offset solid shadow (`box-shadow: 4px 4px 0` in an ink colour)
  instead of a soft blur. Reads as print, sticker or poster rather than as elevation.
- **Slanted section edges.** A `clip-path` polygon that ends a band on a diagonal rather
  than a horizontal, so sections interlock instead of stacking.
- **Wobble.** An asymmetric multi-value radius
  (`border-radius: 255px 15px 225px 15px / 15px 225px 15px 255px`) for a hand-drawn,
  marker-outline feel.
- **Directional shapes.** `clip-path` arrows, notches and tabs, so a step, a callout or a
  price tag has a direction rather than being a box.

Use them sparingly and systematically: pick one or two, apply them consistently to the
same kind of element, and record the exact values as component tokens. Sprinkled at random
they read as noise; applied consistently they become the thing that makes a direction
recognisable.

## Composition is part of a direction's distinctness

When producing several directions to compare, assign each a **different hero archetype
and a different section rhythm**, the same way you assign each a different palette and
type pairing. If two directions share a composition, they will read as the same design
twice no matter how far apart their colours are, and the comparison gives the user nothing
to choose between.

Record the decision in the DESIGN.md `Layout` section: which hero archetype, why it suits
this product's strongest asset, and how the section rhythm is meant to pace the page.
