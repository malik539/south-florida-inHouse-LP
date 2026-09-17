# Content still required from the source campaign landing page

**Status:** the build is blocked from verifying offer facts.

This session's network egress policy denies access to both:

- `https://smilehub.southfloridadentalcenter.com/in-house-yearly-dental-plan-campaign` (primary source of truth)
- `https://southfloridadentalcenter.com/dental-plan/` (secondary verification source)

Both return `403` at the CONNECT stage of the organization's egress proxy
(`connect_rejected`). Text-extraction relays (`r.jina.ai`, CORS proxies,
Google cache) are blocked as well. Nothing was routed around.

Because the brief's controlling rule is **DO NOT INVENT CONTENT**, no price,
plan name, inclusion, exclusion, testimonial, disclaimer or credential has
been written into `index.html`. Every such value is an explicit
`[[VERIFY: ... ]]` token. The page renders, is fully responsive, accessible
and tracking-ready — it is simply not yet truthful, and must not be published
until the tokens are replaced.

## How to unblock

Either:

1. Allowlist the two hosts above for this environment's network policy, or
2. Paste the page's content into the session (view-source dump, a text copy,
   or a screenshot set is enough).

## Exact values needed

Search `index.html` for `[[VERIFY` to find every one in place. The inventory:

### Branding
- [ ] Logo file (and a 2x/WebP version if available)
- [ ] Exact brand hex values as used on the LP (current CSS variables were
      sampled from the supplied logo artwork and are marked as unconfirmed)
- [ ] Font family used on the LP
- [ ] Button styling / shape / colour used on the LP

### Offer
- [ ] Plan name(s) — exact wording
- [ ] Price per plan and the price frequency wording
- [ ] Adult price
- [ ] Child price
- [ ] Additional-member price
- [ ] Number of exams included
- [ ] Number of cleanings included
- [ ] X-ray inclusions (which x-rays, how many)
- [ ] Discount percentage(s) and which procedures they apply to
- [ ] Cosmetic dentistry references
- [ ] Implant references
- [ ] Membership duration wording
- [ ] Eligibility requirements
- [ ] Exclusions — clear aligners, periodontal restrictions, deep cleaning
      restrictions, member restrictions, anything else stated
- [ ] Terms / disclaimers, verbatim

### Conversion
- [ ] Primary CTA wording, exactly as the campaign uses it
- [ ] Primary CTA destination URL (booking / enrollment system)
- [ ] Secondary CTA wording
- [ ] Phone number(s) — and whether new-patient and existing-patient numbers
      are distinguished, plus which one the campaign points PPC traffic to
- [ ] Lead form: every field, which are required, the form `action`, and the
      thank-you / confirmation flow

### Trust
- [ ] Doctor name(s) and any credentials stated on the LP
- [ ] Testimonials / reviews — verbatim wording, reviewer name, rating and
      source exactly as shown
- [ ] Any trust indicators actually present

### Contact
- [ ] Address as written on the LP
- [ ] Office hours if the LP shows them
- [ ] Email if present

### Assets
- [ ] Logo
- [ ] Doctor / team photography
- [ ] Office photography
- [ ] Any other campaign imagery, with the alt text used

### FAQ
- [ ] Every question and answer present on the LP. If the LP has no FAQ, the
      FAQ section is deleted rather than filled in.

## Sections held back pending facts

- **Plan vs traditional insurance** — commented out in `index.html`. The brief
  says to skip it entirely unless the LP explicitly provides every cell. It
  will only ship if the source supports it.
- **Reviews / testimonials** — scaffolded but will be deleted outright if the
  source LP carries none.
- **FAQ** — same.

## Third-party data deliberately NOT used

Public directory listings (Yelp, the practice's own non-campaign pages as
surfaced by search) show an address, phone number, hours and an owner name for
this practice. None of it was written into the page: it is not the campaign LP,
the brief names the campaign LP as the source of truth, and directory data is
frequently stale. It is recorded here only so it can be checked against the
real LP, and it is flagged as a possible discrepancy to confirm rather than a
fact to publish.
