# Images and icons

Imagery is a design decision with several legitimate answers. Choose the type that
serves this product, this audience, and this direction, then execute it to a standard
where the viewer can visualise the finished product. Record the choice and its reasoning
in the DESIGN.md `Images` section, and the icon system in `Icons`.

Two rules hold whatever type is chosen:

- **Every image carries information.** It shows what the product is, what using it looks
  like, what the outcome is, who is behind it, or how something works. An image that
  could be deleted without the page losing meaning should be deleted.
- **Execution quality is the gate, not the medium.** A well-chosen photo, a competent
  geometric illustration and an accurate product replica all let a viewer see the
  finished thing. A crude freehand figure does not, whatever the concept behind it was.

## Choosing the type

| Type | Strongest when | Weak when | Watch out for |
|---|---|---|---|
| **Real photography** | trust and human context matter, the experience is physical or social, the audience is conservative | the subject is abstract, or no honest photo of the real thing exists | stock clichés: handshakes, high-fives, laughing-with-salad, generic "team celebrating" |
| **AI-generated photography** | you need a specific scene no stock library has, or full control of casting, setting and grade | the shot must depict a real, verifiable person, place or result | hands, text in-image, uncanny faces, over-glossy lighting that reads as synthetic |
| **Illustration, committed style** (flat, line, isometric, 3D render, abstract, Memphis, collage) | the value is abstract or systemic, the brand is playful or distinctive, photography would look generic | the audience needs literal proof the thing exists | style drift between assets; half-committed styles that read as clip art |
| **Product / screen demo** | the product is visual and the UI is the value; often the single highest-converting image on a software page | the product is a service or the UI is not yet designed | fake-looking UI, illegible at mobile widths, showing a screen that does not match the real product |
| **Diagram / data visualisation** | the value is a process, a comparison, or a number worth seeing | it is decorative, or the data is invented | diagrams that restate the adjacent paragraph without adding clarity |
| **Typographic / textural / image-light** | premium editorial positioning where type and space carry the page | the visitor needs to see the thing before believing it | mistaking "no images" for restraint when the page actually needs proof |

Notes on choosing well:

- Match the type to the *argument*, not to fashion. A page whose proof is "this is a real
  room with real people in it" wants photography. A page whose proof is "look at what the
  tool does" wants a product demo. A page selling an abstract system wants a diagram or a
  committed illustration style.
- **Vary the type across competing directions.** If you are producing several directions
  to compare, giving them all the same imagery type wastes the comparison, they will
  read as the same design in different colours.
- Mixing types on one page is allowed only when each has a clear role (for example,
  photography for the human proof and a screen replica for the product section). Two
  illustration styles on one page is style drift, not variety.
- A prior project's answer is not this project's answer. Photography was the right call
  on one project because hand-drawn figures had failed there; that is not a rule.

## Getting the assets

**Real photography.** Source from a stock CDN that allows hotlinking (Unsplash's
`images.unsplash.com/photo-<id>` pattern works without an API key). Do this yourself
before briefing any subagent: build the URL with explicit width and quality parameters,
confirm it returns HTTP 200, then **look at it** by downloading a small preview and
opening it with the Read tool, which renders images. Never pass along a photo you have
not seen. Reject clichés and anything that contradicts the audience (a screen full of
code on a page for non-technical buyers). Hand each direction its own vetted set with a
one-line description of what each image shows, and give different directions different
anchor images.

**AI-generated photography or illustration.** Legitimate and often better than stock when
you need a specific scene. Check for an available image-generation skill (for example a
Cloudflare Workers AI generator) and its credentials before promising this route. Prompt
deliberately and concretely for the scene the page actually needs, describing subject,
setting, composition, lighting and mood, then review the output and regenerate rather
than shipping a flawed frame. Generation cost is real, so confirm with the user before
committing to a route that generates many assets.

**Illustration from a library.** When a committed style is wanted and generation is not
available, use one consistent open-licensed illustration set rather than assembling
mismatched assets. One source, one style, one palette treatment.

**Hand-built SVG.** Agents build *geometric, diagrammatic and interface* SVG well:
abstract shape compositions, isometric blocks, charts, annotated diagrams, and accurate
replicas of product UI built from HTML and CSS. Agents build *organic freehand figures*
badly. Use hand-built SVG for the former and never for the latter.

**Product / screen demos.** Usually best built as real HTML and CSS rather than an image:
a faithful, styled replica of the product's interface, using the page's own tokens,
readable at mobile widths. This is often the most convincing "image" on the page and it
stays crisp at any resolution.

## Treatment and documentation

Whatever the type, document in the `Images` section: the chosen type and why it fits this
direction, the treatment (crop ratios, colour grade or duotone, framing, border or
shadow, how images sit against the palette), where each image appears, and what each one
depicts. A consistent treatment is what makes assets from different sources read as one
system.

Practical requirements: meaningful `alt` text on every image, responsive sizing that does
not overflow at ~390px, an aspect-ratio box so layout does not jump while loading, and
sensible file weight. If images are hotlinked, the page depends on network access, which
is acceptable for a design comp and should be stated.

## Icons

Icons are a system, not decoration, and are documented in the `Icons` section.

- **Real inline SVG only.** Never emoji, which render inconsistently and read as
  unfinished, and never an icon font.
- **One family, one set of mechanics**: a fixed stroke width, a consistent corner and
  terminal treatment, filled or outline as a deliberate choice, and a small size scale
  (for example 16 / 20 / 24 px) used consistently.
- **A meaning table.** List the concepts that get an icon in this product (date,
  location or delivery mode, capacity, price, notification, account, credit, status) and
  fix one icon per concept. An icon that appears once with no repeated meaning is
  usually decoration.
- **Icons support labels; they rarely replace them.** An icon-only control needs an
  accessible name.
- Keep icons subordinate to content: they clarify scanning, they are not the visual
  interest of a section. Rows of large decorative icons over generic headings are a
  known slop pattern (see `anti-slop-and-tone.md`).
