# Image assets

All assets are in place, derived from the two files the practice supplied
(the logo artwork and Dr. Cohen's portrait).

| File | Size | Used for |
|---|---|---|
| `logo.png` | 12 KB | header + footer |
| `doctor.webp` | 12 KB | hero portrait (LCP) |
| `doctor.jpg` | 21 KB | `<picture>` fallback for the portrait |
| `og-image.jpg` | 54 KB | social share card, 1200×630 |
| `favicon.png` | 5 KB | browser tab, 64×64 |

## What was done to them

- **`logo.png`** — the supplied artwork sat on a flat `#e5e5e5` backdrop,
  which showed as a grey box against the white header. That backdrop is keyed
  out to transparency with a narrow feathered band so the edges stay clean,
  the artwork is trimmed to its bounding box, resized to 560px wide (roughly
  3× its 46px display height) and quantised to a 48-colour palette. The result
  is visually identical at 12 KB, down from 62 KB truecolour. It renders on
  white, on glass and on the dark footer chip.
- **`doctor.webp` / `.jpg`** — the portrait at its native 364×362, encoded
  as WebP at q86 with a progressive JPEG fallback. It is the LCP element, so
  it is preloaded and not lazy-loaded. `object-position: 50% 22%` keeps the
  face centred in the square crop.
- **`og-image.jpg`** — composed at 1200×630: the portrait on brand navy
  (`#124f7f`) with the logo on a white chip.
- **`favicon.png`** — the tooth glyph from the left of the logo mark,
  flattened onto white at 64×64.

Nothing is stock, generated, or a stand-in: no invented dentists, patients,
office interiors or before/after results.

## If you want to add more

An authentic **office interior** shot is the one gap. With it, the merged
"practice & dentist" block can split back into two image-led sections the way
the source page had them. Drop it in as `office.webp` (square crop, ~720px)
plus a `.jpg` fallback and it can be wired in.

A **second portrait or team shot** would also let the hero and the Dr. Cohen
section each carry their own photo instead of sharing one.
