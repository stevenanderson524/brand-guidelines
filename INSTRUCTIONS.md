# INSTRUCTIONS.md

Project conventions for the Experience Modernization Agent. **Read this on warm-up before any task.** When in doubt, follow these rules over your defaults. Ask clarifying questions rather than guess.

---

## Project overview

- **Site type:** Brand guidelines / brand portal
- **Source of truth:** Figma template. Frames define design intent, not pixel-perfect targets.
- **Delivery:** Edge Delivery Services + Document Authoring (DA)
- **Audience:** Internal brand teams, agencies, partners — not consumer marketing
- **Tone:** Reference-style. Clear, scannable, instructional. Not promotional.

---

## Authoring philosophy

- **Default content first (David's Model).** Before creating a block, ask: *can an author produce this with normal typing — headings, paragraphs, lists, inline images?* If yes, do not create a block.
- Brand sites lean roughly 70% default content / 30% blocks. Resist over-blocking.
- A block is justified only when content is one of:
  - Repeating-structured (cards, swatches, comparison rows)
  - Interactive (carousel, accordion, tabs)
  - Requires decoration logic an author cannot express in plain typing

---

## Block reuse rules

- Always check the existing block library in this repo and the [Block Collection](https://www.aem.live/developer/block-collection) before creating anything new.
- Apply the 70% similarity threshold: if a new Figma frame is ≥70% similar to an existing migrated block, create a **variant**, not a new block.
- Prefer variants over config cells for styling differences.
- When creating a variant, add it to the block's metadata so future migrations can reuse it.

---

## Brand-portal block patterns

Search for existing implementations before building. These are the patterns this site type typically needs:

| Pattern | Recommended approach |
|---|---|
| Typography specimens | Default content + section metadata. Block only if showing live HTML + code pairing. |
| Color swatch grid | `swatch-grid` block, collection model. One row per color (name, hex, usage notes). |
| Logo gallery | `cards` block variant. |
| Logo do/don't grid | `cards` block with two-column variant and clear visual markers (✓ / ✗ icons). |
| Spacing/scale specimens | Default content; add a small `spec` block only where labeling is required. |
| Voice and tone examples | Default content. Blockquotes for examples, lists for guidelines. |
| Brand asset downloads | Default content list with links. Block only if file metadata (size, format) is required inline. |
| Component preview embed | `embed` or `iframe` block. |

---

## Naming conventions

- **Page slugs:** lowercase, hyphenated, no `.html`. Examples: `/foundations/color`, `/components/buttons`, `/voice/principles`.
- **Section folders in DA:** `foundations/`, `components/`, `voice/`, `assets/`, `guidelines/`. Adjust per project but document any deviation here.
- **Block names:** lowercase, hyphenated, structural — not content-descriptive. `swatch-grid` not `brand-colors`. `comparison` not `dos-and-donts`.
- **Image filenames:** lowercase, hyphenated, no spaces. Sanitize Figma layer names on download.

---

## Design tokens

- Tokens live in `styles/styles.css` as CSS custom properties.
- **Phase 1 (site-wide design) must complete before any block-specific styling.**
- Token seed: run design migration against the Figma frame named `Design Tokens`, `Style Guide`, or the richest available frame containing type ramp + full color palette + spacing scale. If unclear which frame to use, **ask before proceeding** rather than picking one.
- Block CSS must reference global tokens. Do not hardcode hex values, font sizes, or spacing values inside block CSS.

---

## Navigation

- Three-section structure (Brand / Sections / Tools) enforced by `header.js`.
- `nav.md` lives in the repo root.
- Typical brand-portal top-level: Foundations, Components, Voice, Assets, Guidelines.
- Tools section for this site type is usually empty or a single "Download brand kit" link.
- If `nav.md` is empty or ambiguous, ask before generating structure.

---

## Critique standards

- Visual fidelity target: 85% similarity to the Figma frame (block critique) or to the source page (page critique).
- Run block critique on every migrated block.
- Run page critique on at minimum: home, one foundations index page, one component detail page.
- Figma intent is the ceiling, not the floor. Do not pursue pixel-perfection at the cost of EDS performance characteristics.

---

## Performance and accessibility (non-negotiable)

- Target near-100 Lighthouse scores across Performance, SEO, Accessibility, Best Practices.
- No client-side framework imports in blocks unless explicitly approved.
- All images must go through `createOptimizedPicture`.
- All interactive blocks must be keyboard-navigable and have screen-reader labels.
- Color swatches and do/don't examples must maintain WCAG AA contrast for surrounding text and labels.

---

## What NOT to do

- Do not migrate a full Figma file in one prompt. Migrate global design first, then blocks one `node-id` at a time.
- Do not create new blocks when default content suffices.
- Do not hardcode brand colors or type values into block CSS — reference tokens.
- Do not invent navigation structure when `nav.md` is empty — ask.
- Do not push directly to `main`. Open a feature branch and PR.

---

## Workflow checkpoints

**Starting a new task, confirm:**
1. Project documentation has been read (warm-up complete).
2. Phase 1 design migration is complete (tokens exist in `styles/styles.css`).
3. The relevant Figma `node-id` is known for any block migration request.

**Ending a session, confirm:**
1. All migrated blocks have passed block critique.
2. Any new variants are documented with metadata.
3. Code changes are pushed to a feature branch (not `main`).

---

## Project-specific notes

<!-- Use this section for anything specific to the current Figma source, account, or demo target. -->
<!-- Examples: -->
<!-- - Figma file key: {fileKey} -->
<!-- - Tokens seed frame node-id: {nodeId} -->
<!-- - Account / demo target: e.g., NFL, CenturyLink, Boost -->
<!-- - Any custom block names that override the defaults above -->
