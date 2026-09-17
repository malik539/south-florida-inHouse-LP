# Image assets

All assets are authentic practice photography supplied by South Florida Dental
Center. Nothing is stock, generated, or a stand-in — no invented dentists,
patients, office interiors or before/after results.

| File | Size | Used for |
|---|---|---|
| `logo.png` | 12 KB | header + footer |
| `chairside-440.webp` | 18 KB | hero (LCP), phones |
| `chairside-800.webp` | 39 KB | hero (LCP), desktop |
| `chairside.jpg` | 81 KB | `<picture>` fallback for the hero |
| `office-720.webp` | 50 KB | "Trusted Care in Coral Springs" |
| `office.jpg` | 89 KB | `<picture>` fallback |
| `doctor.webp` | 13 KB | "Meet Dr. Daniel Cohen" |
| `doctor.jpg` | 22 KB | `<picture>` fallback |
| `og-image.jpg` | 54 KB | social share card, 1200×630 |
| `favicon.png` | 5 KB | browser tab, 64×64 |

First render pulls the HTML plus `logo.png`, one `chairside-*.webp` and the
favicon — roughly 93 KB on a phone, 114 KB on desktop. Everything below the
fold is lazy.

## Where each photograph is used, and why

- **Chairside (Dr. Cohen showing a dental model to a patient)** leads the
  hero. It is the highest-resolution source (1080×1080), it shows the dentist
  and a relaxed patient rather than a posed solo shot, and it carries a glass
  caption naming him and his title. It is the LCP element: preloaded with
  `imagesrcset`/`imagesizes` so phones fetch the 440px file and desktops the
  800px one, `fetchpriority="high"`, never lazy-loaded.
- **Front desk (patient checking in with the team)** illustrates "Trusted Care
  in Coral Springs", matching that section's own copy about a welcoming
  environment and friendly staff.
- **Portrait** heads "Meet Dr. Daniel Cohen", where a portrait belongs. It is
  364×362 native, so `.trust-media-sm` caps its column at 400px to stop the
  browser upscaling it.

## Processing applied

- **`logo.png`** — the supplied artwork sat on a flat `#e5e5e5` backdrop,
  which showed as a grey box against the white header. That backdrop is keyed
  out to transparency with a narrow feathered band so edges stay clean, the
  artwork is trimmed to its bounding box, resized to 560px wide (~3× its 46px
  display height) and quantised to a 48-colour palette. Visually identical at
  12 KB, down from 62 KB truecolour. Renders on white, on glass and on the
  dark footer chip.
- **Photographs** — resized from 1080×1080 with Lanczos, encoded as WebP
  (q74–76) with progressive JPEG fallbacks behind `<picture>`.
- **`og-image.jpg`** — composed at 1200×630: the portrait on brand navy
  (`#124f7f`) with the logo on a white chip.
- **`favicon.png`** — the tooth glyph from the left of the logo mark,
  flattened onto white at 64×64.

Every `<img>` carries explicit `width`/`height`, so CLS stays at zero. If any
image fails to load the page hides its wrapper rather than showing a broken
placeholder, and the logo falls back to the practice name as styled text.
