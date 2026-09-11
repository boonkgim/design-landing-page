# Guardrails: visual slop, copy tone, and the hard rules

Every design this skill produces is audited against this file, first by whoever built it,
then independently. These are not stylistic opinions; each one is a specific tell that
makes a design or its copy read as machine-generated, and each was caught in real review.

## The governing rule

**No element that serves no purpose.** Every element on the page must carry information
tied to the product's real content, or enable a real user action. If an element can be
deleted and the page loses neither meaning nor function, it was decoration and it goes.
Apply this to imagery, icons, badges, dividers, labels, stat rows, and whole sections.

Every DESIGN.md ends its Do's and Don'ts with an `### AI Slop Guardrails` subsection
restating this rule and the bans below in that system's own vocabulary, not copied
verbatim.

## The visual tells

These are patterns to recognise, not properties to ban on sight. Nearly every one of them
has a legitimate use in the hands of someone who chose it deliberately and can say why;
what marks them out is being reached for by default, as filler, or as a substitute for a
decision. Judge the specific combination in context. The genuinely non-negotiable items
are in **Hard rules** below.

1. **Generic purple-to-cyan or lavender "AI startup" gradients** used as decoration
   rather than as a documented brand colour.
2. **Glassmorphism plus neon glow or coloured box-shadow halos** applied for atmosphere
   rather than following a documented elevation model. Dark and saturated surfaces are
   where this creeps in hardest.
3. **Rows of three or six identical icon-over-heading cards** carrying generic,
   interchangeable copy. The pattern is not banned; the interchangeable filler content in
   it is. If the four cards could belong to any product, they belong to none.
4. **Reflexive default typefaces.** Inter, Space Grotesk and Geist chosen because they
   are the obvious answer, or the italic-serif-accent-word cliché. Any of these is fine
   when actually chosen and justified in the Typography section.
5. **A meaningless badge or pill above the hero headline** ("✨ New", "AI-Powered") that
   carries no information.
6. **The rounded card with a coloured left-edge stripe.** The specific combination is the
   tell: a rounded-corner card, a hairline border or tinted fill, and a 3-4px coloured bar
   down its left edge, used for a quote, callout or feature. It is one of the most
   recognisable auto-generated card treatments, it usually spends the brand's accent
   colour on decoration rather than on an action, and it tends to stand in for a card that
   was not actually designed. Reach for type, space, a surface shift or a full border
   instead.

   Do not over-apply this. A coloured or neutral left rule is not banned in itself: a
   plain blockquote with a left rule and no card around it is a long-standing typographic
   convention and is fine; so is a sharp-edged callout, and so is an edge colour that
   encodes real state across a set (error, warning, success) when documented as doing so.
   Judge the combination, not the single property.
7. **Defining every card with a 1px hairline border.** Cards are fine. Grouping content
   into cards is often the right call, especially for the offer. The tell is the reflex
   that a card *is* `surface + 1px border + radius`, applied to every group on the page,
   in any border colour, not just grey. When the recipe never varies, the offer, a bio, a
   list of outcomes and a footnote all carry identical visual weight and the layout stops
   expressing any hierarchy.

   A card can be defined by several things, and the hairline should not be the automatic
   answer: a **surface tone shift** (a white card on a tinted page, or a sunken fill on a
   light one) often separates on its own and makes an added border redundant; **soft
   elevation** does it while signalling interactivity; **spacing and type hierarchy** alone
   are frequently enough; a **solid colour block** does it emphatically. A border is one
   legitimate option among these, not the default, and it works best when the system has
   deliberately committed to a hairline language throughout, or when it is carrying real
   meaning such as a selected or error state.

   Two practical checks. If a card sits on a differently-toned background *and* has a
   hairline, the hairline is usually doing nothing: delete it and see. And if every card
   on the page shares one recipe, vary it deliberately so that the section you most want
   chosen reads as the most prominent.
8. **Any separate eyebrow-label element above a heading, at any size.** Banned outright,
   not merely discouraged, regardless of case or size. If the supporting context matters,
   fold it into the heading itself, either as a smaller lead-in line inside the same
   heading element or as a colon-joined clause ("Who's teaching this: two instructors, no
   filler bios"). The pattern is doubly bad when the label is set too small to read
   comfortably, which is the usual case.
9. **Emoji standing in for icons**, instead of the documented inline-SVG icon system.
10. **Fabricated stat banners and trust numbers** the product does not have. See the
    evidence guidance in `conversion-brief-and-copy.md`.
11. **A decorative numbered "Step 1 / 2 / 3" graphic** that does not depict the product's
    real flow, or that exists where nothing needed explaining.
12. **Decoration with no informational job**, in any medium, plus low-contrast text that
    fails WCAG AA. This is explicitly *not* a ban on any imagery type: real photography,
    AI-generated photography, illustration and product demos are all legitimate and
    encouraged when chosen deliberately (see `images-and-icons.md`). What is banned is the
    unrelated handshake photo, the abstract blob behind the headline, the stock scene that
    contradicts the audience, and imagery so crudely executed that it stops the viewer
    believing in the finished product.

## Hard rules

- **No em dash anywhere in any copy.** Not in headlines, body, captions, alt text,
  quotes or the footer. Use a comma, a full stop, or parentheses. Grep for `—` and expect
  zero before shipping.
- **Body text at 16px or larger** for all real reading copy. Smaller sizes are for
  genuine micro-UI only (badges, timestamps, table labels), never for paragraphs. This is
  a modern-web accessibility baseline.
- **Headlines at or under about 12 words; hero subheads and section leads at or under
  about 25 to 30 words.** Trim, do not wrap.
- **Contrast passes WCAG AA** for every text-on-background pair, checked rather than
  assumed, especially on saturated and dark surfaces.
- **Responsive to ~390px** without horizontal overflow.

## Copy tone: a marketer, not an AI assistant

Avoid, specifically:

- **"Not just X, it's Y"** and its variants ("not only X, but Y", "this isn't about X,
  it's about Y"), the single most recognisable AI writing structure.
- **Reflexive "actually", "real", "genuinely", "truly"** used as authenticity signals.
  "The real, bookable schedule" and "who's actually teaching this" both improve by simply
  deleting the word. If the sentence survives the deletion, delete it.
- **Consultant vocabulary**: delve, leverage, seamless, robust, unlock, elevate,
  underscore, holistic, game-changing, cutting-edge, at the end of the day, it's worth
  noting, pave the way, foster, navigate (figurative), landscape (figurative).
- **Rule-of-three lists** written for rhythm when there are really two or five things.
- **Signposting**: "let's dive in", "here's the thing", "here's where it gets
  interesting", "moving on to".
- **Throat-clearing openers**: "In today's fast-moving world", "When it comes to", "At
  its core".

Write plainly and specifically, vary sentence length, and let a declarative sentence land
without hedging it. Confidence without exaggeration is the register.

## The audit

Mechanical, run across every finished page:

```
grep -o '—' index.html | wc -l                  # em dashes, expect 0
grep -c 'class="eyebrow' index.html             # eyebrow labels, expect 0 (check equivalents too)
grep -n 'border-left:[[:space:]]*[2-9]' index.html   # edge stripes: review each hit, see tell #6
grep -c 'border:1px solid' index.html                # hairline-defined cards: see tell #7
```

The first two are pass/fail. The last two only surface candidates for judgment: check
whether each stripe hit is the rounded-card-plus-accent-stripe pattern or a legitimate
plain left rule, and whether a high hairline count means cards are being defined by border
reflexively (especially where a tone shift already separates them) or reflects a system
deliberately committed to a hairline language. Leave the legitimate ones alone.

plus: extract every `<h1>`/`<h2>` and the paragraph after the hero heading and word-count
them; confirm base body font size; diff every colour, face and radius in the CSS against
the DESIGN.md tokens; confirm every image asset resolves and has alt text; check contrast
pairs; grep the copy for the tone list above.

Then open the page and look at it, at desktop and at ~390px. Every rule here can pass
while the page is still unbalanced or unconvincing, which is a judgment only looking can
catch.
