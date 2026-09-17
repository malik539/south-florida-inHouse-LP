# Image assets

These files are referenced by `index.html` but are **not yet present**: the
source campaign landing page (and the practice site) are blocked by this
environment's network egress policy, so the authentic assets could not be
downloaded. See `../../CONTENT-SOURCE-NEEDED.md`.

Required, taken from the source campaign LP — no stock substitutes, no
generated dentists, patients, offices or before/after results:

| File | Used for | Notes |
|---|---|---|
| `logo.svg` | header + footer | SVG preferred; PNG at 2x acceptable |
| `hero.webp` | hero visual (LCP) | authentic practice/team photo, 880x660 or larger, 4:3 |
| `doctor.webp` | trust section | authentic doctor photo, square crop |
| `og-image.jpg` | social share preview | 1200x630 |
| `favicon.png` | browser tab | 48x48 |

Optimisation expected before launch: WebP/AVIF, correct intrinsic dimensions
matching the `width`/`height` attributes in the markup, and compression to
roughly 100-200 KB for the hero. The hero image is preloaded with
`fetchpriority="high"` and is deliberately **not** lazy-loaded; everything
below the fold is `loading="lazy" decoding="async"`.

Alt text must describe the real photo and, for the doctor image, use the name
and role exactly as the source LP states them.
