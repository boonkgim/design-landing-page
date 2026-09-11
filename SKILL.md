---
name: design-landing-page
description: Generate multiple distinct, high-conversion landing page designs for a product from its PRD or brief - each documented as a DESIGN.md (Google's open-source Stitch spec) and built as a self-contained HTML mock with real photography, run through a shared anti-AI-slop and anti-Claudish-tone audit before being handed back. Use when the user asks to design a landing page, mock up landing page options, create marketing page designs, or wants several visual directions to compare for a product's main marketing page. Invoke as /design-landing-page.
---

# Design landing page

Produce several genuinely distinct landing page design directions for a product, each
a real `DESIGN.md` plus a self-contained `index.html`, good enough that the user can
actually visualize the finished product rather than a wireframe. This skill exists
because plain "design me 3 versions" attempts converge on the same palette, lean on
crude hand-drawn illustration, and read as AI-written both visually (gradients, glow,
eyebrow labels, emoji icons) and in copy (em dashes, "not just X, it's Y," reflexive
"actually/real," corporate-consultant words). Every step below exists to prevent one of
those specific, previously-observed failures.

Two reference files carry the detail so this file stays a workflow, not a spec dump:

- `references/design-md-format.md` - the exact DESIGN.md schema and section order.
- `references/anti-slop-and-tone.md` - the visual and copy guardrail checklist, and the
  word-count/accessibility rules.
- `references/photo-sourcing.md` - how to source real imagery instead of illustration.

Point subagents at these files by path (they're plain files on disk) rather than
pasting their contents into every prompt.

## Step 1: Read the source material

Read the PRD or brief in full before doing anything else. Everything downstream, the
outcome section's specific claims, the evidence section's honest framing, the
how-it-works steps, the FAQ answers, must be traceable to something this document
actually says. Note in particular:

- The real user journey (how someone actually goes from landing on the page to
  completing the core action), for the "how it works" section.
- The real business rules (cancellation policy, pricing rules, what's in vs. out of
  scope), for the FAQ.
- Whether the product is pre-launch with no track record yet (affects the Evidence
  section, see `anti-slop-and-tone.md`).
- The target audience's technical comfort level and device mix (affects tone and
  mobile-responsiveness priority).

## Step 2: Confirm scope with the user

Don't assume. Ask (a single `AskUserQuestion` call covers this in one round-trip):

- **Which page(s)?** Default assumption, absent other instruction: one full landing
  page containing, in this order: **Hero** (benefit-first, not feature-first), **Outcome
  / Benefit** (concrete, specific things a user gets, not vague claims), **Evidence**,
  **the product's core functional section** (a schedule, a feature grid, a pricing
  table, whatever the product's main "here's the actual thing" content is),
  **Why us / How it works** (mapped to the real journey from step 1), **FAQ** (real
  objections from step 1), **Closing CTA** (specific, not a repeat of the hero CTA). If
  the user only wants one specific screen (e.g. just a dashboard mock), confirm that
  instead of building the full seven-section structure.
- **How many directions?** Default to 3 if unspecified. More than 4-5 in one batch
  makes the convergence problem in Step 4 harder to avoid and burns a lot of tokens for
  marginal comparison value.
- **Imagery approach.** Offer the options in `photo-sourcing.md` (curated stock,
  AI-generated, illustration) and let the user pick; default to curated stock
  photography if they have no preference, it's the most reliable path to something that
  looks like a real, finished product.
- **Any hard constraints?** Palette exclusions (e.g. "not cream," "not dark mode"),
  brand colors that must appear, anything the user already knows they don't want.

## Step 3: Assign genuinely distinct creative directions

This is the step that fails silently if rushed. Giving N subagents an identical brief
plus "pick your own creative direction" reliably produces N designs that converge on
the same palette family and type pairing (observed failure: three separate agents told
to pick their own direction all independently landed on warm terracotta/cream tones
with a serif display face). Prevent this by deciding the directions yourself, up front,
before writing any subagent prompt, with concrete, mutually opposed anchors:

- A specific palette **territory** per direction (not just "your choice"): e.g. one
  direction anchored on a fully saturated dominant color, one on a cool neutral
  crisp-white base, one on a warm editorial cream, one on a dark ink surface. Never let
  two directions in the same batch share a palette family.
- A specific type **pairing philosophy** per direction: e.g. one condensed bold display
  face, one elegant high-contrast serif, one single geometric sans across all weights.
  Explicitly forbid whichever faces already got used in a prior round of this same
  project (track this across sessions if redoing a rejected batch).
- A specific **mood/energy** word per direction that's a real contrast to its siblings
  (bold and energetic vs. restrained and premium vs. calm and minimal), not near-synonyms.
- If this is a redo after a rejected batch, name the earlier rejection explicitly in
  each new prompt (what was tried, what the client said was wrong) so the new batch
  doesn't quietly repeat it.

## Step 4: Source imagery

Follow `references/photo-sourcing.md` for whichever option was chosen in Step 2. If
using curated stock, do the search-and-visual-review yourself (or via a `fork` if you
want to keep the raw search noise out of your own context) **before** writing subagent
prompts, then hand each subagent its own pre-verified, pre-vetted URL set. Give each
direction a different suggested hero image where plausible, identical photo pools
across siblings undercut the "genuinely distinct" goal from Step 3 even when the
palette differs.

## Step 5: Launch one subagent per direction, in parallel

Use the `Agent` tool, one call per direction, all in a single message so they run
concurrently. Each is a **fresh agent with zero context of this conversation**, so its
prompt must be fully self-contained: the product summary from Step 1, the exact section
list from Step 2, its assigned concrete direction from Step 3, its photo assignment
from Step 4, and explicit pointers (by absolute path) to
`references/design-md-format.md` and `references/anti-slop-and-tone.md` for it to read
and follow. Ask each subagent to:

1. Read the two reference files and the source PRD/brief.
2. Write `DESIGN.md` in the assigned direction, following the reference format exactly,
   including the `Imagery`, `Icons`, and `AI Slop Guardrails` sections.
3. Build `index.html`: one self-contained file, every section from Step 2, real inline
   SVG icons (never emoji), the assigned photography, a working sign-in/state toggle if
   the product has a personalization concept worth demonstrating, mobile-responsive to
   ~390px.
4. **Self-audit before finishing**: grep its own HTML for em dashes and confirm zero,
   confirm no separate eyebrow-label element exists anywhere, check every heading and
   hero subhead against the word-count limits in `anti-slop-and-tone.md`, diff every
   color/font/radius value used against the DESIGN.md token list and fix any drift,
   verify every image URL still returns 200, check text contrast against its background
   for WCAG AA.
5. Save both files under a per-direction folder, e.g.
   `design/<nn>-<short-slug>/{DESIGN.md,index.html}`.
6. Report back concisely: what was built, the two file paths, and explicit confirmation
   of the self-audit results (should not paste full file contents).

## Step 6: Independently re-audit every direction yourself

Don't trust the self-audit report alone, subagents miss things, especially when the
prompt itself introduced repeated phrasing (if you wrote "the real schedule" in three
separate prompts, expect three separate designs to independently produce "the real,
actually bookable schedule"). After all subagents report back, run a mechanical sweep
across every finished `index.html`:

- Em dash count (`grep -o '—' file | wc -l`), must be zero.
- Eyebrow markup count (`grep -c 'class="eyebrow"' file` or similar), must be zero.
- Extract every `<h1>`/`<h2>` and the paragraph immediately after the hero `<h1>`,
  word-count them, flag anything over the limits in `anti-slop-and-tone.md`.
- Re-verify every image URL still returns 200.
- Spot-check a handful of headlines and body copy against the Claudish-tone list.

Fix mechanical, unambiguous issues yourself directly (em dash replacement, eyebrow
folding, trimming an over-long headline) rather than round-tripping through a subagent
for every small thing, it's faster and the changes are objective. For anything requiring
real design judgment across the whole batch (a systemic issue like every direction
having the same problem), send one message per affected subagent (resume it by name/id,
it has full context of what it built) rather than starting fresh agents, unless the
change is substantial enough that a fresh, focused brief is clearer.

## Step 7: Hand it back

Open every finished `index.html` for the user (`xdg-open` on Linux, `open` on macOS) so
they can review real rendered pages, not just a file listing. Summarize each direction
in one line (palette/mood, not implementation detail). Expect iteration: palette
rejections, tone complaints, requests for more directions with a specific constraint
(as happened when a client asked for "2 more, just not cream"), a request to fix one
specific issue across the whole batch. Treat each round the same way as Steps 3-6:
decide concrete new anchors before dispatching, re-run the same audit on the result.

## What this skill does not do

It does not decide the product's information architecture beyond the standard landing
page section list in Step 2, and it does not commit anything to git. It builds
throwaway-but-real design comps for the user to compare and choose from, not production
code.
