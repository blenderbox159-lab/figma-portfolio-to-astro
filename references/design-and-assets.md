# Design and Asset Intake

Read this reference after the Figma structure is approved, or when replacing design placeholders with the user's real files.

## Figma evidence to capture

For each primary desktop and mobile frame, record:

- frame node ID and exact dimensions;
- section order and approximate section heights;
- max content width, page gutters, column widths, gaps, and corner radii;
- background, surface, text, muted, border, and accent colors;
- heading/body sizes and line heights;
- image aspect ratios, crops, and object positioning;
- every visible heading, label, project title, metadata line, CTA, and link;
- intended desktop/mobile differences rather than assuming the mobile frame is a simple stack.

Always obtain at least one screenshot of each main frame. Structured design output is useful for exact values; the screenshot reveals composition, visual balance, and crops. If context is large, inspect the main frames first, then fetch only the detail nodes that materially affect implementation.

Use the exact approved frame/version, not whichever frame happens to be first in the file.

When the available Figma tooling returns asset URLs, download exact assets into the project while the URLs are valid. Keep the downloaded files as the site's runtime assets. Do not embed temporary Figma MCP URLs in source code.

## Source-to-slot manifest

Build a small inventory before copying anything:

| Site slot | Source file | Destination | Format / ratio | Notes |
| --- | --- | --- | --- | --- |
| Logo | supplied transparent logo | `public/images/logo.png` | transparent PNG/SVG | verify legibility on dark background |
| Hero desktop | Figma export or showreel poster | `hero-desktop.*` | usually 16:9 | preserve focal point |
| Hero mobile | mobile frame export/poster | `hero-mobile.*` | portrait | do not crop the desktop poster blindly |
| Showreel desktop/mobile | approved master outputs | `showreel-desktop.mp4`, `showreel-mobile.mp4` | landscape/portrait | real MP4, not GIF |
| Project card/detail | latest case still and video | stable semantic filename | recorded ratio | latest user-stated output wins |
| Portrait, tutorial, QR | supplied originals | stable semantic filename | preserve content | QR must remain scannable |

Use semantic filenames that do not expose temporary export names. Prefer site-owned copies to symlinks so the project stays portable. Preserve originals.

Before copying, inspect video metadata with a local media tool when available: codec, duration, pixel dimensions, orientation, and file size. Do not assume extension or filename proves the file is browser-decodable. Keep the original high-quality masters untouched.

## Content decisions

- Extract actual copy from Figma, but apply newer user-provided revisions.
- Keep contact details and social/tutorial URLs in one data module.
- Write missing biography or project copy conservatively from supplied facts. Do not add client names, performance claims, or unverified roles.
- If process material is absent and the user says it is not needed, do not create a fake behind-the-scenes gallery; a truthful process accordion is enough.
- Label self-initiated work accurately.

## Media performance note

High-resolution masters may be appropriate for local visual review but expensive on the public web. Record total video size. For deployment, recommend separate web encodes, poster images, CDN/object storage, caching, and region-specific delivery only when that stage is requested. Do not silently reduce or overwrite the user's masters during design implementation.
