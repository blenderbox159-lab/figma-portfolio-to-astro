# Figma MCP Website Design Workflow

Read this reference before creating or materially updating the portfolio design in Figma.

## Connection and target

Use the Figma MCP tools for canvas work. A browser-open Figma tab alone is not evidence that MCP access or the target file is available.

- For a new file, load the available `figma-create-new-file` skill, resolve the correct plan with the supported identity/plan tool, create a Design file, and reuse the returned `file_key` for all later calls.
- For an existing file, use the exact Figma URL/file key and requested node/page. Do not assume the currently open file is the target.
- If the user requests a new version, create a new file/page or clearly separated frames. Do not change the earlier approved draft.

Before every Figma write, load and obey the current `figma-use` skill. For a composed full-page view, also load `figma-generate-design`; if the work creates reusable components or variants, load the Figma component/library skill too. Those skills are the source of truth for current tool schemas, `skillNames`, font loading, Auto Layout, page switching, variables, component properties, IDs, screenshots, and error recovery.

## File organization

A practical portfolio file can contain:

- `00 Brief & Reference` — direction summary, reference principles, content map, and missing assets;
- `01 Foundations` — colors, type scale, spacing/radius roles, button/card/accordion patterns;
- `02 Desktop` — primary long-page frame;
- `03 Mobile` — primary mobile long-page frame;
- `04 Archive` — earlier explorations only when the user wants them retained in the same file.

Match existing file conventions when they already exist. Do not create extra pages merely to satisfy this example.

## Build order

1. Inspect pages, top-level nodes, components, variables, styles, fonts, naming, and clear canvas space with a read-only call.
2. Convert the approved content architecture into named sections and determine target frame widths. Use the actual brief/reference; do not default every desktop to 1440 or every mobile to 390 when another size is specified.
3. Create desktop and mobile wrapper frames first. Build sections directly inside their wrapper; do not build loose top-level sections and reparent them later.
4. Establish or reuse semantic variables/styles for background, surface, text, muted text, borders, accent, spacing, radii, typography, and effects.
5. Create only the needed reusable local components when the linked design system has no suitable component. Repeated navigation, buttons, chips/tabs, project cards, accordion rows, and media frames should not remain duplicated one-off groups.
6. Build a top-down skeleton with named placeholders, then fill related sections in retry-safe batches. Remove all shimmer/placeholders when complete.
7. Use editable text, frames, components, vector icons, and image fills. A full-page screenshot may be used only as a reference, never as the finished design.
8. Place real content images using supported image hashes/capture transfer when needed. Do not leave final media frames blank when approved assets exist.
9. Return every created/mutated node ID and meaningful structural evidence from each write.

## Portfolio-specific decisions

- Hero: define the intended media crop, readable text zone, primary CTA, and mobile alternative.
- Services: make the relationship between selector and featured case explicit.
- Work: specify whether cards scroll horizontally, filter by category, or open a detail/video state.
- Process/FAQ: show open and closed states at least once when interaction matters.
- About/tutorial/contact: design for real portrait/cover/QR ratios rather than generic boxes.
- Long-page rhythm: vary density deliberately; avoid stacking equally sized sections with identical spacing.
- Mobile: redesign navigation, hero crop, action layout, cards, long text, and modal proportions. Do not simply scale down desktop.

## Validation and checkpoint

After composition, inspect structural metadata and take one desktop and one mobile full-composition screenshot. Verify:

- all text uses the intended font family/style and is not clipped;
- no overlaps, unintended absolute positioning, empty frames, or unfinished placeholders;
- images use the intended crop and orientation;
- repeated elements are consistent and componentized where appropriate;
- desktop and mobile contain the same required content with intentional responsive differences;
- previous drafts remain intact;
- frame names clearly indicate version and viewport.

Apply targeted fixes, then capture one post-fix screenshot only when something changed.

Present the Figma link plus desktop/mobile long previews and the remaining asset list. Ask for design confirmation before code when the user has not pre-authorized continuous end-to-end execution.

## Handoff to Astro

Once approved, record the exact desktop/mobile frame node IDs and final asset slots. The code stage must read those approved nodes with the current Figma design-to-code workflow; do not implement from memory or from an obsolete draft.
