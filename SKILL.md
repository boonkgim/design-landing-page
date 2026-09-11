---
name: design-landing-page
description: Design a high-conversion landing page from a brief, PRD, or rough notes - reasoning like a senior designer who is also marketing and sales aware. Derives the conversion argument and copy first, then the section structure, then a committed visual direction (palette, type, layout, images, icons), records every decision in a DESIGN.md (Google's open-source Stitch spec, extended with Images and Icons sections), and builds it as a self-contained HTML page good enough to visualise the finished product. Produces one direction or several distinct ones to compare. Use when asked to design a landing page, a marketing page, a product page, a sales page, or to propose visual directions for one. Invoke as /design-landing-page.
---

# Design landing page

You are acting as a senior designer who is also marketing and sales aware. That means
two things that most "make me a landing page" attempts skip:

1. **The page is an argument, not a layout.** Its job is to move one specific visitor
   from where they are to one specific action. The structure, the copy, and the visual
   system all serve that argument. Decide the argument first.
2. **Every decision is deliberate and recorded.** Palette, type, density, shape, imagery
   type, icon style: each is chosen for a reason tied to the audience and the message,
   and written down in `DESIGN.md` so a human or another agent can carry it forward.
   DESIGN.md is a record of design decisions, not a visual style mandate.

Detail lives in four reference files. Read the one you need at the step that needs it,
and point subagents at them by absolute path instead of pasting their contents:

| File | Read it at |
|---|---|
| `references/conversion-brief-and-copy.md` | Steps 1-3 (argument, structure, copy) |
| `references/layout-and-composition.md` | Step 4 (hero archetype, section rhythm, distinctness) |
| `references/images-and-icons.md` | Step 5 (choosing and sourcing imagery, icon system) |
| `references/design-md-format.md` | Step 6 (writing DESIGN.md) |
| `references/anti-slop-and-tone.md` | Steps 5-8 (guardrails, tone, hard rules, audit) |

## Step 1: Extract the conversion brief

Read the brief, PRD, or notes in full. If the input is thin, ask for what's missing
rather than inventing it. Pull out, explicitly, before designing anything (see
`references/conversion-brief-and-copy.md` for how to interrogate each):

- **Who** the visitor is, what they already believe, and how aware they are of the
  problem, the category, and this product. Awareness level decides how much the hero has
  to teach before it can sell.
- **The one action** the page must produce. A page with two co-equal goals converts on
  neither.
- **The promise**: the outcome the visitor gets, in their language, not the product's.
- **The mechanism**: why the promise is believable, the thing that makes it work.
- **The proof that genuinely exists.** Some products are pre-launch and have no numbers.
  That constrains the evidence section honestly, it does not license inventing stats.
- **The top objections** in the visitor's head, in their own words, and what defuses each.
- **Commitment and risk**: price, effort, what happens after they act, what reverses the
  risk.
- **Constraints**: brand assets, locale, currency, timezone, device mix, regulatory
  wording, anything already decided.

Everything downstream must trace to something in this brief. If a claim, a step, or an
FAQ answer cannot be traced back, it is invented and does not ship.

## Step 2: Write the argument before the pixels

Draft the conversion argument as plain sentences first, no layout, no styling: the
promise, the proof, the objection handling, the ask. If that sequence is not persuasive
as plain text, no visual treatment will rescue it. This draft is also the source of the
page's real copy, which is a first-class deliverable, not filler text under a design.

Copy rules, in full in `references/conversion-brief-and-copy.md`: specific over vague,
customer language over product language, benefit before feature, concrete and true over
impressive and hollow, and a marketer's voice rather than an AI assistant's.

## Step 3: Derive the section structure from the argument

The default high-conversion sequence, each section doing one job in the funnel:

1. **Hero** - the promise, who it is for, and the primary CTA. Answers "what is this,
   for whom, why care" in about five seconds.
2. **Outcome / benefit** - makes the promise concrete. Specific, tangible things the
   visitor walks away with.
3. **Evidence** - makes it believable, with proof that actually exists.
4. **The offer** - the real thing being bought: the schedule, the pricing table, the
   product list, the plan comparison, with the details a decision needs. This is where
   conversion happens, and it is the section most often under-designed.
5. **Why us / how it works** - the mechanism and the risk reduction, mapped to the real
   journey from the brief, not a decorative three-step graphic.
6. **FAQ** - kills the remaining objections from Step 1, in the visitor's own words,
   answered truthfully against the brief's real rules.
7. **Closing CTA** - restates the promise and names the specific next step (the actual
   next available date, the actual starting plan), never a generic repeat of the hero.

Plus a header with a persistent CTA and a footer. Adapt deliberately: a product-aware
audience may want the offer above the evidence; a complex product may need a dedicated
mechanism section; a single-SKU product may fold the offer into the hero. Say why when
you deviate.

## Step 4: Choose the visual direction(s)

The direction follows from the audience and the message, not from taste. A page selling
to cautious enterprise buyers and a page selling a weekend bootcamp should not look
alike even if both are "clean and modern."

Commit to specifics: palette with real values, a type pairing with real faces and a
reason, density and layout rhythm, shape language, elevation model, and how the page
feels at the top of the funnel versus at the offer. "Human," "modern," or "premium" are
outcomes of layout, content, imagery, and voice, never of palette alone.

**Decide the hero composition explicitly**, before any building, using the archetypes in
`references/layout-and-composition.md`. Ask what the page's strongest asset is (the
promise, a scene, the product, a transformation, the offer, a person, a number) and build
the hero around that answer. Left column of copy with a photo on the right is a real
layout and sometimes the right one, but it is also the layout that arrives when the
question was never asked, so choose it on purpose or not at all. Decide the section rhythm
below the fold at the same time, so the page paces rather than repeating one section shape
all the way down.

**If the user wants several directions to compare** (ask how many, default 3 when they
say "some options"), assign each direction concrete, mutually opposed anchors *yourself*
before writing any prompt. Giving N subagents the same brief plus "pick your own
direction" reliably produces N near-identical designs: in the project this skill came
from, three independently briefed agents all landed on warm cream palettes with the same
serif. Prevent it by fixing, per direction:

- a distinct palette territory (no two directions in the same family, and none in a
  family the user already rejected),
- a distinct type philosophy and specific faces, excluding any face already used in an
  earlier round of the same project,
- a distinct mood that genuinely contrasts with its siblings rather than being a synonym,
- **a distinct hero archetype and section rhythm**, assigned explicitly per direction from
  `references/layout-and-composition.md`. This is the anchor most often skipped and the one
  that matters most: in the project behind this skill, eight directions with deliberately
  opposed palettes and type all independently produced the same copy-left, photo-right
  hero, which made them read as one design in eight colourways,
- and, where it makes sense, a different imagery type per Step 5.

## Step 5: Choose the imagery type and the icon system

Imagery is a design decision with several legitimate answers, chosen per direction:
real photography, AI-generated photography, illustration in a committed named style
(flat, line drawing, isometric, 3D render, abstract, Memphis, editorial collage), a
product or screen demo, a diagram, or a deliberately image-light typographic treatment.
Pick the one that actually serves this product, audience, and direction. Do not default
to one type across every direction, and do not carry a previous project's answer into a
new one.

`references/images-and-icons.md` has the decision framework, what each type is good and
bad at, the quality bar and sourcing route for each (stock CDN, AI generation, asset
libraries, hand-built SVG for the things agents build well), and the icon system rules.
Two rules hold regardless of type: every image must carry information the page needs,
and the execution must be good enough that the viewer can visualise the finished
product. Crude freehand figures fail that bar; a well-chosen photo, a competent
geometric illustration, or an accurate screen replica all pass it.

## Step 6: Record the decisions in DESIGN.md

Write `DESIGN.md` per `references/design-md-format.md`: YAML token frontmatter, then the
prose sections in order, including the `Images` and `Icons` sections and closing with
Do's and Don'ts plus its `AI Slop Guardrails` subsection from
`references/anti-slop-and-tone.md`. The prose explains *why*; the tokens are the
normative values the build must match.

## Step 7: Build the page

One self-contained `index.html` per direction, implementing exactly the tokens and rules
in its own DESIGN.md. Every section from Step 3 with the real copy from Step 2, real
inline SVG icons, the Step 5 imagery, working interactive states where they demonstrate
something real about the product (a plan toggle, a signed-in price, an FAQ accordion),
responsive down to ~390px, and body text at 16px or larger.

Save per direction as `design/<nn>-<slug>/{DESIGN.md,index.html}`.

**For multiple directions, run one subagent per direction, launched in parallel in a
single message.** Each is a fresh agent with no context, so its prompt must be
self-contained: the Step 1 brief, the Step 2 argument and copy direction, the Step 3
section list, its assigned Step 4 anchors, its Step 5 imagery assignment with any
pre-verified asset URLs, and absolute paths to the reference files to read. Require each
to self-audit (Step 8) before reporting back, and to report only a summary and file
paths rather than pasting files.

## Step 8: Audit, then look at it

Never trust a subagent's self-audit alone, and never trust your own build unexamined.
Run the mechanical sweep across every finished page (the full checklist, with the reasons
behind each rule, is in `references/anti-slop-and-tone.md`):

- zero em dashes anywhere in the copy,
- zero separate eyebrow-label elements above headings,
- headings within the word-count limit, hero and section leads within theirs,
- base body text 16px or larger,
- every colour, face, radius and icon style traceable to a DESIGN.md token, no drift,
- every image asset resolving, with real alt text,
- contrast passing WCAG AA,
- no emoji standing in for icons,
- copy free of the AI-tone tells.

Fix mechanical issues directly, they are objective and faster to correct than to
delegate. Send judgment-level or systemic issues back to the subagent that built the
page, which still has full context.

Then **actually open the pages** (`xdg-open` on Linux, `open` on macOS) and look at them
rendered, at desktop and narrow widths. A page can pass every grep and still be ugly,
unbalanced, or unconvincing.

## Step 9: Present and iterate

Summarise each direction in a line about its argument and mood, not its implementation.
Expect real iteration: a rejected palette family, a tone complaint, "give me two more but
not X," a single fix applied across every direction. Each round repeats Steps 4-8:
decide new concrete anchors first, rebuild, re-audit, re-open. Carry forward what earlier
rounds ruled out so a later round cannot quietly reintroduce it.

## Scope

This skill designs and mocks pages: it produces DESIGN.md decision records and
self-contained HTML comps for a human to judge, not production components, and it does
not commit anything to git.
