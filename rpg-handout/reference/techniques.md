# Document-type recipes

Match fonts, layout, stamps, paper, and watermarks to the **period and country** of the fiction. The recipes below are starting points — adapt.

Good Google Fonts to reach for:
- **Handwriting:** La Belle Aurore, Homemade Apple, Shadows Into Light Two, Caveat, Tangerine (ornate/old), Dancing Script (florid).
- **Typewriter:** Special Elite.
- **Serif print / forms:** Libre Baskerville, EB Garamond, Playfair Display (display headlines).
- **Condensed news:** Oswald, Playfair Display (heads) over a serif body.

Core principle: **different in-fiction writers get different fonts**, even across decades of the same document. Vary ink colour too (#2e3a55 faded blue, #3a3326 sepia, near-black for typewriter).

---

## Handwritten journal / letter

- Handwriting font sized 15–17pt, `line-height` ~1.7.
- Faded ink colour; slight `transform: rotate(-0.6deg)` varied per paragraph for an unruled hand.
- Uneven margins; `text-indent` on paragraphs.
- Underline key phrases with a translucent stroke (`text-decoration-color: rgba(...,.6)`).
- For a letter: add a date line, a salutation, a signature in a slightly larger/looser hand.

## Lined notebook page

- Background = stacked `repeating-linear-gradient` for the ruling (one line every ~27–28px) plus the parchment gradients; set `background-origin` so the rule aligns to the content box.
- A vertical red margin line via an absolutely-positioned 1px element.
- Set the handwriting `line-height` to the ruling pitch so text sits on the lines.

## Official form (certificate, police report, registry act)

- Pre-printed parts in a serif (Libre Baskerville); **filled-in fields in Special Elite** (typewriter) or a handwriting font for hand-completed forms.
- Double-rule header (`border-bottom: double`), a crest/`✠` glyph, institution name in letter-spaced caps.
- A faux **round stamp**: a `border-radius:50%` element, `border: 2.5px solid rgba(violet,.42)`, `transform: rotate(-12deg)`, low opacity, text curved or stacked inside — overlap it slightly over a signature for authenticity.
- Signature lines: a bottom-bordered box with a handwriting-font name sitting on it, rotated ~-1.5deg.
- A pencil annotation (different from the typed fields) sells a secret: faint grey handwriting font, rotated.

## Typescript / manuscript page

- Special Elite, justified, page number centred at top.
- **Fountain-pen corrections:** a struck word (`text-decoration: line-through` in ink-blue) with the replacement as a `<sup>` in a handwriting font.
- A margin note: absolutely-positioned handwriting block rotated ~2°.
- **Torn edge:** a full-width element with `clip-path: polygon(...)` using many small alternating points to fake a ragged tear; background matches the page-behind colour (or print white).

## Newspaper clipping

- Narrow justified columns (`column-count` or fixed-width `.col` divs), condensed serif **headline** (Playfair Display, heavy), serif body ~8.5pt.
- Slightly grey ink on off-white newsprint (cooler, less warm than parchment).
- Ragged torn edges via `clip-path`; optional yellowing via a faint sepia overlay gradient.
- A dateline / paper name in small caps. A subhead. Maybe a "continued on…" cut-off.

## Photo back

- A photo-paper rectangle scaled up ~1.5–1.7× from real (e.g. 9×12cm → ~15×20cm) for table legibility.
- Water-damaged corners: corner `radial-gradient` stains.
- Two hands (an inscription + a later annotation), a faint period **brand watermark** at the foot (FERRANIA for mid-century Italy, Kodak Velox / AZO for the US, AGFA for Germany).
- You can't render the photo FRONT — below the prop, give a GM card describing the image, a real-photo shot-list, and an AI-image prompt.

## Book / family register spread

- **A4 landscape**, rendered as an open two-page spread.
- Dark leather binding via the outer `linear-gradient`; inner-spine shadow on each leaf with `inset box-shadow` on the spine side.
- Entries across generations in **different hands** (ornate Tangerine for the oldest, La Belle Aurore for the middle, Caveat/biro for the most recent).
- Page numbers at the outer bottom corners.

## Telegram

- Monospace or Special Elite, ALL CAPS, "STOP" for full stops.
- A printed form header (POST OFFICE / company), strips of "tape" feel via thin horizontal rules, a received-stamp.

## Hand-drawn map

- Inline **SVG** on parchment.
- Waterways/coasts: wobbly `Q`-curve paths, `stroke-linecap: round`, width by importance.
- Roads: dashed strokes. Terrain: small tick-mark glyphs (marsh, hills). Settlement dots + handwriting labels (Caveat).
- A **cartouche** (double-ruled box, small-caps serif title), a **compass rose**, a **scale bar**.
- **Two versions for investigations:** a GM map (red POI marks + location notes + secrets named) and a clean **player map** (geography + public place names only — NO scenario title, NO spoiler labels; leave discovery sites unmarked so players annotate them). Keep both visually identical in style so a marked-up player copy matches the GM's.

---

## Aging & finishing (physical, optional — tell the user)

- Print on cream / ivory 90–100gsm for forms and letters; heavier stock for maps.
- Real aging after printing: sponge edges with cold tea, dry flat under a book; a candle-singed edge for burned documents (do this safely, outdoors).
- Fold a letter in three; add a coffee-cup ring with an actual cup of coffee on scrap first to test.

## Print dialog reminder (give once)

Open each file online at least once so Google Fonts cache. Then: browser print → **margins: none**, **enable "background graphics"**, correct paper orientation per file.

## Heavy / slow-to-open PDFs

If a Chrome "Print to PDF" handout opens sluggishly (especially in macOS Preview), the cause is almost always a **`mix-blend-mode` or CSS `filter`** in the stylesheet: it makes Chrome flatten the page into a full-page lossless bitmap that the viewer must decode on every open. The fix is in the **source**, not post-processing — remove the blend mode / filter and reproduce the effect with a normal-composited translucent gradient (see "Keep backgrounds vector" in SKILL.md). Re-export from Chrome; the text should now be selectable in the PDF.

**Do not reach for Ghostscript** (`gs -dPDFSETTINGS=/ebook …`) to shrink these: it only re-compresses the same bitmap (so open-time barely improves) and it strips the embedded colour profile, which makes the parchment render noticeably **darker** vs the black text. It's the wrong tool for this symptom.
