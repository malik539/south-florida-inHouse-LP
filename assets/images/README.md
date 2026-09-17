# Image assets

`index.html` references the files below. They are the authentic South Florida
Dental Center assets from the source campaign landing page and are **not yet
in the repo** — the source host was unreachable from the build environment, so
they could not be downloaded.

Until they are added, the page hides each missing image wrapper via a small
`onerror` handler rather than rendering broken-image placeholders, so the
layout stays clean.

| File | Used for | Target size |
|---|---|---|
| `logo.svg` | header + footer | SVG, or PNG at 2x |
| `hero.webp` | hero visual (LCP) | 880×660 or larger, 4:3 |
| `office.webp` | about-the-practice section | square crop |
| `doctor.webp` | Meet Dr. Daniel Cohen | square crop |
| `og-image.jpg` | social share preview | 1200×630 |
| `favicon.png` | browser tab | 48×48 |

No stock substitutes, no generated dentists, patients, offices or
before/after results.

Optimisation before launch: WebP/AVIF, intrinsic dimensions matching the
`width`/`height` attributes in the markup, hero compressed to roughly
100–200 KB. The hero is preloaded with `fetchpriority="high"` and deliberately
**not** lazy-loaded; everything below the fold is lazy.

Alt text is already written against the source page's own image descriptions
("Welcoming modern dental office interior", "Dr. Daniel Cohen — General &
Cosmetic Dentist"). Adjust only if the actual photo differs.
