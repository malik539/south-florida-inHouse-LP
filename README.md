# South Florida Dental Center — In-House Yearly Dental Plan (Google Ads LP)

Static, single-file Google Ads landing page. HTML5 + CSS3 + minimal vanilla JS.
No React/Vue/Next/Bootstrap/jQuery, no animation libraries, no build step, no
npm install. Serve the directory from any static host.

```
index.html
assets/images/      # authentic campaign assets (see assets/images/README.md)
CONTENT-SOURCE-NEEDED.md
```

## Current status

**Not launch-ready: content is unverified.**

The build environment's network egress policy blocks both
`smilehub.southfloridadentalcenter.com` and `southfloridadentalcenter.com`
(HTTP 403 at CONNECT), so the source campaign landing page could not be
audited. Per the brief's controlling rule — do not invent content — every
factual value is an explicit `[[VERIFY: ...]]` token rather than a guess.
There are zero invented prices, plan names, inclusions, exclusions, reviews,
ratings, credentials, savings claims, urgency or trust badges.

`CONTENT-SOURCE-NEEDED.md` lists every value required.

## Launch checklist

1. Replace every `[[VERIFY: ...]]` token (`grep -n 'VERIFY' index.html`) with
   the source LP's exact wording.
2. Replace `tel:[[VERIFY-PHONE-E164]]` on all seven phone CTAs with the real
   number in E.164 form, e.g. `tel:+19545551234`.
3. Point `#enroll-form`'s `action` at the practice's real booking/enrollment
   endpoint, or swap the card for the existing scheduling widget, then delete
   the placeholder guard at the bottom of the inline script. Reduce the field
   set to exactly what the existing form collects.
4. Drop the real assets into `assets/images/`.
5. Confirm the brand hex values in `:root` against the live LP's CSS — the
   current values were sampled from the supplied logo artwork and are marked
   UNCONFIRMED.
6. Delete any section the source LP does not support: reviews, FAQ, and the
   plan-vs-insurance comparison (already omitted, per the brief's instruction
   to skip it unless every cell is factually supported).
7. Delete the `.build-notice` banner block and the `.verify` CSS rule.
8. Remove `<meta name="robots" content="noindex">` if the campaign wants the
   page indexed.
9. Paste the GTM / Google Ads / GA4 container into the marked slot in `<head>`.

## Tracking

Every conversion element carries a stable id plus `data-conversion-type`
(`phone`, `plan`, `form`), and plan CTAs carry `data-plan` so GTM can attribute
which plan was clicked:

`header-phone-cta`, `header-plan-cta`, `hero-plan-cta`, `hero-phone-cta`,
`hero-card-plan-cta`, `plan-1-cta`, `plan-2-cta`, `mid-plan-cta`,
`mid-phone-cta`, `trust-plan-cta`, `contact-phone-cta`, `form-submit-cta`,
`final-plan-cta`, `final-phone-cta`, `footer-phone-cta`, `sticky-mobile-call`,
`sticky-mobile-plan`.

Rename the plan CTA ids/`data-plan` values to the real plan names once known.

## Implementation notes

- **CRO order:** minimal PPC header (no site nav) -> hero with offer card ->
  quick benefits -> plan pricing -> how it works -> why an in-house plan ->
  mid CTA -> practice trust -> reviews -> important plan details -> FAQ ->
  form + location -> final CTA. Exclusions live in a visible bordered panel
  inside each plan card, not in small grey footnotes.
- **Mobile:** hero reflows to headline -> offer/pricing card -> CTAs -> visual
  via flex `order`. Plan cards always stack. Sticky bottom bar (call + primary
  CTA) is mobile-only, respects `env(safe-area-inset-bottom)`, and `body` gets
  matching bottom padding so it never covers content.
- **Performance:** all CSS inline, one small inline script at end of body,
  system font stack (zero font requests), no render-blocking resources, hero
  preloaded with `fetchpriority="high"`, everything below fold lazy-loaded
  with explicit dimensions to hold CLS at zero.
- **Glass:** applied only to the header, hero offer card and sticky bar, each
  with an opaque `rgba` fallback declared before the `@supports` block that
  adds `backdrop-filter`.
- **Accessibility:** semantic landmarks, single H1, ordered heading levels,
  skip link, visible focus rings, accordion buttons with
  `aria-expanded`/`aria-controls` and regions labelled by their trigger,
  labelled form fields (labels, not placeholders), `type="tel"`/`type="email"`
  with autocomplete, `aria-live` status, and a `prefers-reduced-motion` block
  that disables all reveals and transitions. A `.no-js` class on `<body>` is
  removed by the script so reveal content is never hidden without JS.
