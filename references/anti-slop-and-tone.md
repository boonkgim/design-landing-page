# Anti-slop guardrails and copy tone

Every design direction this skill produces must be audited against this checklist
before it's considered done, both by the subagent that built it (self-audit) and by a
mechanical re-check afterward (see `SKILL.md` step 6). These rules exist because they
are exactly the tells that make an AI-generated design or AI-written copy read as
generic, and because a real client rejected earlier rounds for them.

## The 10 AI-generated-UI tells (visual)

Ban all of these, worded in the specific design system's own vocabulary, not just
copy-pasted:

1. Generic purple-to-cyan or lavender "AI startup" gradients used as decoration rather
   than a documented brand color.
2. Glassmorphism plus a neon glow or colored box-shadow halo, added for decoration
   rather than tied to a documented elevation model. A saturated or dark-surface system
   is exactly where this creeps in, watch it closely there.
3. Rows of 3 or 6 identical icon-over-heading "feature cards" carrying generic,
   interchangeable copy that isn't real product content.
4. Reflexive use of Inter, Space Grotesk, or Geist (or an italic-serif-accent-word
   cliché) as an unexamined default rather than a deliberate, documented type choice.
5. A meaningless badge or pill sitting above a hero headline ("✨ New", "AI-Powered")
   that carries no real information.
6. **Any separate "eyebrow" label element above a heading, at any size.** This is banned
   outright, not just discouraged, regardless of whether it's all-caps or not, regardless
   of size. If a heading's supporting context is genuinely important, fold it directly
   into the heading itself, either as a smaller lead-in line inside the same `<h1>`/`<h2>`
   element, or as a colon-joined clause ("Who's teaching this: two instructors, no filler
   bios"). Never a separate labeled tag element.
7. Emoji used as icons anywhere in the UI, instead of the documented inline-SVG icon
   system.
8. Fake or unsourced stat banners and trust numbers ("10,000+ learners", "99%
   satisfaction") that the product doesn't actually have. See "Evidence for pre-launch
   products" below.
9. A generic numbered "Step 1 / Step 2 / Step 3, how it works" graphic added reflexively
   when the real flow doesn't need explaining, or where the steps are decorative filler
   rather than the product's actual, specific flow.
10. Decorative-only imagery that cannot be tied to a real page purpose (a random
    handshake photo, an unrelated abstract 3D blob), and low-contrast dark-mode-by-default
    body text that fails WCAG AA. This does **not** mean stock or AI-generated photography
    is banned: well-chosen, deliberately-treated real photography that depicts something
    true about the product is encouraged. The ban is specifically on generic filler with
    no connection to the section's content.

State the system's own governing rule too: every element on the page must serve a real
purpose tied to actual product data or a real user action described in the source brief,
never a purely decorative element that could be deleted without losing information or
function.

## Hard rules, not style preferences

- **No em dash anywhere, in any copy.** Not in headlines, body copy, captions, alt text,
  quotes, footers, anything. Use a comma, a period (new sentence), or parentheses
  instead. Grep the finished HTML and DESIGN.md for `—` and confirm zero before calling
  the work done.
- **Base body paragraph text is 16px or larger, everywhere.** This is a modern-web
  accessibility baseline, not a style choice. Small text is fine for genuine micro-UI (a
  badge, a timestamp label) but never for the primary reading copy of a paragraph.
- **Headlines stay at or under ~12 words; subheads (leads) stay at or under ~25-30
  words.** These are the empirically-supported ranges for landing page conversion copy.
  If a headline or subhead you drafted runs longer, cut it, don't just let it wrap.

## Writing tone: like a marketer, not like an AI assistant

Concretely avoid, anywhere in the copy:

- The "not just X, it's Y" / "not only X, but Y" construction, the single most-cited AI
  writing tell.
- Reflexive use of **"actually," "real," "genuinely," "truly"** as authenticity-signaling
  filler. Do not write "the real, bookable schedule" or "who's actually teaching this,"
  just write "the bookable schedule" / "who's teaching this." If a sentence still reads
  fine with the word deleted, delete it.
- Corporate-consultant words: "delve," "leverage," "seamless," "robust," "unlock,"
  "elevate," "underscore," "holistic," "game-changing," "cutting-edge," "at the end of
  the day," "it's worth noting," "pave the way," "foster."
- Reflexive rule-of-three lists used purely for rhythm rather than because there are
  really three things.
- Signposting phrases: "let's dive in," "here's the thing," "here's where it gets
  interesting," "moving on to."

Write like an experienced marketer who has shipped real landing page copy: plain,
specific, varied-length sentences, a little informal confidence, no hedging or
throat-clearing. Every claim should be something concretely, specifically true about
this product, never vague ("boost productivity," "AI-powered efficiency").

## Evidence for pre-launch products

Many products this skill will be used for have no track record yet. Never invent fake
customer counts, star ratings, or "X,000 users served" vanity stats to fill an evidence
section, that's dishonest, and it's banned tell #8 above regardless. Instead build
evidence from what an early, real offering can honestly have:

- A specific, plausible bio for whoever's behind the product (real-sounding company
  names/roles as illustrative sample content are fine, e.g. "spent six years building
  automation tooling at a logistics company," never a vague "expert").
- A concrete breakdown of what's actually delivered (a curriculum, a feature list, a
  process), not a marketing summary of it.
- Tangible before/after artifacts specific to the product.
- A testimonial-style quote, if used, is illustrative sample content the same way
  placeholder product names and prices are elsewhere in the mock, never presented as if
  it is real collected feedback.

## How-it-works and FAQ must be real

Steps in a "how it works" section must map to the actual user journey described in the
source brief/PRD, not generic decorative "Step 1: Discover, Step 2: Engage, Step 3:
Grow" filler. FAQ entries must address real objections grounded in the actual product's
real business rules (pull them from the brief), never invented answers that contradict
what the brief actually says.
