# South Florida Dental Center — In-House Yearly Dental Plan (Google Ads LP)

Static, single-file Google Ads landing page. HTML5 + inline CSS3 + one small
vanilla JS block. No React/Vue/Next/Bootstrap/jQuery, no animation libraries,
no build step, no npm install. Serve the directory from any static host.

```
index.html          60 KB, self-contained
assets/images/      authentic campaign assets (see assets/images/README.md)
```

Source of truth:
`https://smilehub.southfloridadentalcenter.com/in-house-yearly-dental-plan-campaign`

All copy, pricing, inclusions, exclusions, credentials and reviews are
reproduced from that page. Nothing is invented: no savings calculations, no
insurance comparison, no urgency or scarcity, no trust badges, no awards, no
ratings or review counts beyond the 4.9 (333) the source itself displays.

## Before launch

1. **Confirm the Periodontal Plan disclaimer** — see *Open question* below.
   This is the one blocking item.
2. Drop the real assets into `assets/images/` (`logo.svg`, `hero.webp`,
   `office.webp`, `doctor.webp`, `og-image.jpg`, `favicon.png`). Until then
   the page hides missing images rather than showing broken ones.
3. Paste the GTM / Google Ads / GA4 container into the marked slot in `<head>`.
4. Confirm the brand hex values in `:root` against the live LP's CSS. They
   were sampled from the logo artwork, not read from the source stylesheet
   (the host was unreachable from the build environment).

## Open question — needs the practice to confirm

On the source page the **Periodontal Plan** carries the same disclaimer as the
Silver Plan:

> Does not include deep cleanings (scaling & root planing). Not available to
> patients with periodontal disease.

That contradicts the Periodontal Plan's own listed benefits — *20% off deep
cleanings (scaling & planing)* and *4 periodontal procedures per year* — and
would exclude exactly the patients the plan exists for. It reads like a
copy-paste error on the source.

The offer has **not** been altered: the disclaimer is reproduced verbatim on
both cards, with an HTML comment at the Periodontal card flagging it. Get the
correct wording from the practice and replace that block before spending on
clicks — as written it will suppress conversions on the higher-priced plan.

## Three other judgement calls

- **Booking URL.** The source's Book Appointment links carry a stale
  `?_ga=2.196331813.840105407.1656953681-1891242693.1655136567` cross-domain
  linker parameter captured in 2022. The destination is preserved
  (`https://app.nexhealth.com/appt/southfloridadentalcenter`); the dead `_ga`
  value is dropped, since replaying a fixed four-year-old client ID corrupts
  GA4 session stitching. Restore it if the practice wants the URL byte-identical.
- **Review dates.** The source's Google widget shows relative timestamps
  ("6 days ago"). A static page cannot carry those truthfully, so they are
  omitted. Review wording, reviewer names and the Google attribution are
  unchanged. Re-adding the live widget would restore the dates at the cost of
  third-party JS on the LP.
- **Review permalinks.** Each review on the source deep-links to its Google
  Maps entry. Those URLs are ~400 characters of opaque base64 and were not
  hand-transcribed; the "Posted on Google" attribution is kept as text. Wire
  the real permalinks in if you want them clickable.

## No lead form — by design

The source campaign page has no lead form. Its conversion flow is exactly two
actions: **Book Appointment** (NexHealth) and **Call 954-710-0383**. Adding a
form would have meant inventing a destination, so the page ships with those
two real actions only. If the practice wants a form, point it at a real
endpoint first.

## Tracking

Every conversion element has a stable id plus `data-conversion-type`
(`phone`, `book`, `directions`, `navigate`), and plan CTAs carry `data-plan`
so GTM can attribute which plan was clicked.

| id | type | plan |
|---|---|---|
| `header-phone-cta` | phone | — |
| `header-book-cta` | book | — |
| `hero-phone-cta` | phone | — |
| `hero-book-cta` | book | — |
| `hero-card-compare-cta` | navigate | — |
| `silver-plan-cta` | phone | silver |
| `silver-plan-book-cta` | book | silver |
| `periodontal-plan-cta` | phone | periodontal |
| `periodontal-plan-book-cta` | book | periodontal |
| `plan-help-phone-cta` | phone | — |
| `mid-phone-cta` | phone | — |
| `mid-book-cta` | book | — |
| `doctor-book-cta` | book | — |
| `final-phone-cta` | phone | — |
| `final-book-cta` | book | — |
| `location-phone-cta` | phone | — |
| `directions-cta` | directions | — |
| `footer-phone-cta` | phone | — |
| `sticky-mobile-call` | phone | — |
| `sticky-mobile-book` | book | — |

## Structure

Minimal PPC header (no site nav) → hero with glass Silver-pricing card →
trust strip → what the plan is → **plans & pricing** → how it works → why
choose → an investment in your health → mid CTA → about the practice → meet
Dr. Cohen → reviews → important plan details → final CTA → location → footer
→ mobile sticky bar.

Pricing sits high: the Silver Plan's adult and child prices are in the hero
card, and the full two-plan comparison is the fourth block on the page.
Exclusions get a bordered amber panel inside each plan card, not grey
footnotes, plus a consolidated *Important plan details* section.

**Sections deliberately not built:** plan-vs-traditional-insurance (the source
gives no factual comparison data, so per brief the section is skipped
entirely — the six "No Deductibles / No Annual Maximum Benefit / …" points are
presented as the practice's own commitments instead) and FAQ (the source has
none, and inventing questions was not an option). The accessible
expand/collapse requirement is met instead by the long reviews, mirroring the
source's own "Read more" behaviour.

## Implementation notes

- **Mobile:** hero reflows to headline → offer/pricing → CTAs → visual via
  flex `order`. Plan cards always stack. Sticky bottom bar (Call Now + Book
  Appointment) is mobile-only, respects `env(safe-area-inset-bottom)`, and
  `body` carries matching bottom padding so it never covers content.
- **Performance:** all CSS inline, one small script at end of body, system
  font stack (zero font requests), no render-blocking resources, hero
  preloaded with `fetchpriority="high"`, everything below the fold
  `loading="lazy" decoding="async"` with explicit dimensions to hold CLS at
  zero. Single ~60 KB document, no external requests at all.
- **Glass:** header, hero offer card and sticky bar only, each with an opaque
  `rgba` fallback declared *before* the `@supports backdrop-filter` block.
- **Accessibility:** semantic landmarks, one H1, no skipped heading levels,
  skip link, visible focus rings, `aria-expanded`/`aria-controls` on the
  review toggles, `role="img"` + `aria-label` on star ratings, `<address>`
  for the address, `<time>` for hours, and a `prefers-reduced-motion` block
  that disables every reveal and transition. A `no-js` class on `<body>` is
  removed by the script, so review text is never clamped without JS and
  reveal content is never hidden.
- **SEO:** descriptive title and meta description drawn from source copy,
  canonical pointing at the campaign URL, Open Graph basics, and `Dentist`
  JSON-LD carrying only verified name/phone/address/hours. `aggregateRating`
  is deliberately omitted from the markup — the 4.9 (333) is Google's own
  third-party rating and self-serving review markup risks a manual action.
