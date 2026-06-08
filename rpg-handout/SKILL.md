---
name: rpg-handout
description: >
  Create print-ready tabletop-RPG player handouts and props as self-contained HTML
  files (aged paper, letters, journals, official forms, typescripts, newspaper
  clippings, photo backs, book spreads, hand-drawn maps). Use when the user — a
  game master / Keeper / GM — wants a physical-looking handout for the table,
  whether they supply the finished in-fiction TEXT to typeset (primary case:
  reproduce verbatim, layout only) or just a brief to write from. Triggers on
  "make a handout", "typeset this letter/note/document", "format this as a prop",
  "player handout", "feelie", "draw a map for my scenario", Call of Cthulhu /
  D&D / any RPG handout requests.
---

# RPG handout maker

Produce **print-ready, self-contained HTML files** — one per handout — that the GM opens in a browser and prints. Everything (textures, drawings) is CSS/SVG; the only external dependency is Google Fonts via `<link>`.

## Step 0 — which mode?

**Format-only (PRIMARY, most common):** the user already has the final in-fiction text (their own, or transcribed from a published scenario) and wants the visual treatment. → Obey the **Golden Rule** below.

**Generate-from-brief:** the user gives a situation and wants you to write the in-fiction text too. → Write it in the requested language and an in-character voice; period-correct; subtle beats explicit (clinical/bureaucratic language that slides off-true is scarier than purple prose); end each handout on its hook (an annotation, an interrupted sentence, a name that shouldn't be there); never include information the players shouldn't have yet — ask if unsure.

If it's ambiguous which mode, ask one question.

## Golden Rule (format-only mode)

**Do NOT rewrite, expand, trim, "improve", or translate the user's text.** Reproduce it verbatim — including odd spelling, dialect, dates, or apparent errors: they may be deliberate (in-fiction voice, or fidelity to a published source). The only permitted changes are typographic (curly quotes, dashes, small caps) and only with the user's OK. If something looks like a mistake, **ask — don't fix**.

## Intake

Before building, make sure you know, per handout:
1. **Document type** (see `reference/techniques.md` for the recipe — journal, letter, official form, typescript, newspaper clipping, photo back, book/register spread, map, telegram…).
2. **Language** of the text.
3. **Period and country** (drives fonts, form layouts, stamps, paper, watermark brand).
4. **In-fiction author(s)** — how many distinct hands appear (each hand gets a different handwriting font, even within one document).
5. **Physical details** — water damage, torn edge, burned corner, fold creases, coffee ring, stamp present/absent, page number, missing pages. (Cheap to request, high payoff.)
6. **Spoiler boundary** — what must this reveal, and what must it NOT reveal yet? (Critical: handouts must never carry information the players shouldn't have. Ask if unclear.)

Ask only for what you're missing; don't interrogate.

## Technical requirements (every file)

- One **self-contained** `.html` per handout. A4 (`@page { size: A4; margin: 0 }`), portrait unless the type wants landscape (book spreads, maps, wide signs).
- A `.page`/`.sheet` div sized **21cm × 29.7cm** (swap for landscape).
- All CSS inline in a `<style>` block. Google Fonts via `<link>`. **No external images** — textures via layered CSS gradients, drawings via inline SVG.
- **Aged paper:** a warm parchment `linear-gradient` base (#efe5cc → #e3d5b6 range), 3–4 `radial-gradient` blotches in `rgba(150,110,60,…)` for foxing/water stains, `inset box-shadow` for edge darkening.
- **`@media print`:** white body, no drop-shadow; keep textures (tell the user to enable "background graphics" and set margins to none in the print dialog).
- **Keeper-only notes inside a file** go in a `.keeper-note` (small, grey) with `@media print { display:none }` so they never reach players.
- Use `reference/template.html` as the aged-paper starting point; copy and adapt rather than rebuilding from scratch.

## Document-type recipes

Load `reference/techniques.md` for the full set (fonts, layout, the stamp/torn-edge/two-map tricks, period-and-country guidance). Read it before building unless the type is trivial.

## Maps

For investigation maps, make **two versions**: a GM map (markings, location notes, secrets) and a **clean player map** (geography only — no scenario title, no spoiler labels; players annotate it during play). See the map recipe in `reference/techniques.md`.

## Output & delivery

- Write each handout to its own file (suggest `handout-<slug>.html`); if the user has a project folder, put them together (e.g. a `table-prep/` dir).
- For each handout, give a short **GM note in chat** (not in the printable file): where it's found in play, what clues it carries, and — for horror games — a suggested Sanity/stress cost.
- For photographic props you cannot render (a real photo's front face), describe the shot and offer both a real-photo shot-list and an AI-image-generator prompt.
- Remind the user once: open the files online at least once so the webfonts cache, then print with background graphics on and margins set to none.
