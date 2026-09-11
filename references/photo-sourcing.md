# Sourcing imagery: real photography over illustration

A landing page mock needs to let the viewer visualize the actual finished product.
Hand-coded SVG illustrations of people, drawn by an agent with no real illustration
skill, read as crude and amateurish and undermine that goal, even when the rest of the
system is well executed. Default to real photography unless the user specifically asks
for an illustration style and accepts that tradeoff.

Two ways to get real photography into a self-contained mock:

## Option A: curated stock photography (default)

Source real photos from Unsplash's direct CDN (`images.unsplash.com/photo-<id>`,
current, stable, no API key needed for hotlinking) and reference them with plain `<img>`
tags. This makes the mock's images dependent on network access when opened, which is an
acceptable, explicit tradeoff for a design comp, not a production page.

**Curation process, do this yourself before handing URLs to any subagent, do not let a
subagent pick blind:**

1. Search for candidate photos matching the product's real context (e.g. for a training
   product: "business meeting laptops," "presenter small audience," "team collaboration
   workshop"). Think about what the page's sections actually need: a hero scene, an
   evidence/testimonial-style portrait, a few supporting shots.
2. For each candidate, build the URL as
   `https://images.unsplash.com/photo-<id>?auto=format&fit=crop&w=<width>&q=<quality>`
   and verify it resolves with `curl -s -o /dev/null -w "%{http_code}" <url>`, expect 200.
3. **Visually review every candidate before using it.** Download a small preview
   (`curl -o preview.jpg "...&w=400&q=50"`) and open it with the Read tool (it renders
   images). Do not trust a filename or a search-result title as a stand-in for actually
   looking at the photo.
4. Reject anything that reads as a stock-photo cliché or is wrong for the audience:
   people high-fiving, a hand-shake close-up, an oversized conference-stage shot when the
   real product is small-scale, a screen full of code when the actual audience is
   non-technical, generic "team celebrating" shots with no connection to the product.
   Prefer photos that depict something specifically true about the product's real
   experience (a small session in progress, someone doing focused work, a plausible
   instructor/founder portrait).
5. Hand each subagent the exact, already-verified URLs to use (with a one-line
   description of what each shows), not a search instruction, fresh subagents have no
   way to verify reachability or content themselves without repeating this whole process.
6. Every design direction should get its own photo assignments (a suggested hero anchor
   plus a supporting set), not the identical shared pool used identically by every
   sibling, or the designs will look like siblings regardless of palette differences.

## Option B: AI-generated photography

If the user is open to it and Cloudflare Workers AI credentials
(`CLOUDFLARE_ACCOUNT_ID`, `CLOUDFLARE_API_TOKEN`) are available (check `ToolSearch` for
the `generate-image-cf` skill; see its own setup docs if credentials are missing), a
subagent can generate bespoke photography instead of sourcing stock. This gives full
control over composition and lets every direction have genuinely unique imagery. The
same rule applies: generate with a specific, deliberate prompt tied to real page content
("a small group of business professionals in a bright meeting room watching one person
present on a laptop, candid, natural light"), never a vague prompt that produces generic
filler. Do not default to this path without asking, image generation has a real cost and
the user may prefer to review the curated-stock option first.

## Option C: illustration (discouraged, last resort)

Only if the user explicitly wants an illustrated look and understands the risk: commit
to one specific, named illustration style (flat/geometric, isometric, hand-drawn line,
Memphis, etc.) and hold every image to that one style rigidly. Never let a subagent
freehand SVG people without a concrete style reference, that is what produces the
"ugly illustration" outcome this skill exists to avoid.

## Whichever option is used

Document the choice and its treatment (crop ratios, color grading/duotone, where each
image appears and what it depicts) in the DESIGN.md `Imagery` section. Every image must
tie to something real the page is saying, never decoration for empty space.
