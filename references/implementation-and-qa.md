# Astro Implementation and QA

Read this reference while implementing the Astro site and during final browser verification.

## Suggested project shape

Use a simple static Astro structure unless the requested behavior needs a server:

```text
src/
  components/
  data/portfolio.ts
  layouts/Layout.astro
  pages/index.astro
  pages/404.astro
  scripts/site.ts
  styles/global.css
public/
  images/
  videos/
```

Use self-hosted fonts when practical. Add a title, description, language, theme color, favicon, Open Graph metadata, and canonical URL only when a real site URL is available. Do not bake `localhost` into canonical metadata.

Keep media paths root-relative (`/images/...`, `/videos/...`) so the static build can serve them consistently. Do not reference the user's Desktop paths from browser code.

## Responsive and interaction details

- Choose breakpoints from the supplied frames, not device-brand assumptions.
- Give wide visual portfolios a centered max width with deliberate full-bleed sections where the design uses them.
- Provide a portrait hero source for mobile when available. Use `muted`, `playsinline`, and a poster for ambient autoplay video; leave audio to user-initiated detail playback.
- Respect `prefers-reduced-motion` and data-saver signals. A poster must remain usable if autoplay is denied.
- Use native `<dialog>` for modal media when supported. Pause the hero while a detail is open, stop and release detail media on close, return focus to the trigger, and allow Escape.
- Use native `<details>` for independent FAQ/process disclosure when its behavior matches the design.
- Service tabs need selected state, roving keyboard focus, and matching content. If tab semantics are used, connect tabs to a labelled panel; otherwise use a clearly labelled button group.
- A horizontal gallery needs scroll snapping, reachable controls, accurate status text, and no page-level horizontal overflow.
- Clipboard actions need visible success/fallback feedback.
- Keep external social/tutorial links `noopener noreferrer`; do not test by posting, messaging, or submitting user data.

## Browser QA matrix

Start with the design frame widths, then cover edge sizes:

| Viewport | Purpose |
| --- | --- |
| 1440 × 900–1000 | primary desktop fidelity and full navigation |
| 768 × 1024 | transition/tablet layout and overflow |
| 390 × 844 | primary phone design and portrait media |
| 320 × 740 | long labels, buttons, and filter overflow |

At every width, compare `document.documentElement.scrollWidth` with `innerWidth`. Horizontal overflow is acceptable only inside intentional scroll containers.

Capture a viewport screenshot of the hero and a full-page screenshot for desktop and mobile. Inspect the screenshots, not just the DOM. Confirm that image orientation and EXIF handling are correct.

## Functional checks

Exercise at least these behaviors when present:

1. mobile menu open, close, Escape, and section navigation;
2. hero pause/play control and responsive source selection;
3. every service option, including keyboard arrows/Home/End when implemented as tabs;
4. every project filter and gallery previous/next control;
5. every project detail in video mode, plus still-image mode when offered;
6. showreel in desktop and mobile orientation;
7. process and FAQ disclosure behavior;
8. copy-to-clipboard feedback;
9. correct `href` values for mail, QR, tutorial, and social links without causing external side effects.

For every video, wait until the media has loaded enough to inspect:

```js
{
  src: video.currentSrc,
  duration: video.duration,
  width: video.videoWidth,
  height: video.videoHeight,
  paused: video.paused,
  error: video.error?.message
}
```

The duration must be finite and positive; dimensions must be non-zero; `error` must be absent. Confirm playback progresses for representative large files. For local serving, an HTTP request with `Range: bytes=0-1023` should normally return `206` and `video/mp4`.

Check visible images for `naturalWidth > 0` after they load. Ignore intentionally empty dialog placeholders before the dialog is used. Review console errors after the interactions.

## Build and local preview

Run the project's own checks and production build, for example:

```sh
npm run build
```

For local preview, start the documented development command in the project directory and verify the root URL returns HTTP 200. A loopback URL works only on the same computer. For a phone on the same Wi-Fi, use the server's network URL and keep the computer and dev server running. The network address may change after reconnecting or restarting.

Document how to stop the exact server process. Do not imply that a local preview is a deployed website.

## Handoff facts worth recording

- exact Node/Astro versions used;
- successful build result and number of diagnostics;
- tested desktop/mobile viewport sizes;
- decoded video durations and dimensions for notable cases;
- total image/video weight;
- static output directory;
- local start/stop commands;
- deployment work intentionally deferred;
- any remaining external-platform or real-device checks.
