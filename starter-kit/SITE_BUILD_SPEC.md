# Family Roofing Sites · Master Build Spec

A shared specification for building roof-restoration websites for the same Australian family of tradies (Rob — NSW · Bryce — QLD · plus two more on the way). Each site is **structurally identical**, but **brand-distinct**. Read this end-to-end before starting a new build.

> **Reference build:** The current Heatshield Roof Restorations site (Bryce, QLD) is the canonical reference. When in doubt, mirror that. The previous Rob's Roof Painting site is the original parent template.

---

## 1. Philosophy

The visual identity is:

- **Tradie-confident, not corporate.** Big condensed display type, uppercase eyebrows, generous use of negative space, one strong accent colour against a near-black + warm-paper neutral pair.
- **Mobile-first, but desktop-considered.** The mobile hero in particular is a deliberate art-direction (3:4 aspect ratio, image visible, text top + CTAs bottom — *not* a shrunk desktop hero).
- **Real-world, not stock.** Placeholders (diagonal stripes + bracketed labels) are explicitly visible so the owner sees exactly what photo is missing. Never insert stock photography.
- **Family-trade language.** "Third generation", "family trade", first-name basis ("Bryce will call you back"), regional pride (Toowoomba grown / Hunter local / etc.).
- **No fake urgency.** No fake countdown timers, no fake review counts, no inflated guarantees. Every claim has a basis the tradie can defend in person.

Every new site keeps this voice. Only the brand wrapper changes.

---

## 2. Tech stack

- **Plain HTML + CSS + JS.** No build step, no framework, no bundler.
- **Netlify** for hosting and forms. The hidden form on every page (`<form name="quote-form" netlify hidden>`) is required for Netlify build-time form discovery.
- **Google Fonts** loaded via `<link>` in `<head>` (Anton + Oswald + Montserrat for the existing two sites; new sites will pick a different stack — see §6).
- **No analytics yet** — owners can add GA4 themselves later.
- **Single CSS file** (`css/main.css`), single JS file (`js/main.js`). Don't split.

### File structure

```
/
├── index.html              · the long landing page (only page that matters for conversion)
├── service-area.html       · template for /toowoomba, /brisbane etc. (one per major suburb when SEO needs it)
├── thanks.html             · post-form-submit page
├── css/
│   └── main.css
├── js/
│   └── main.js
└── images/
    ├── favicon.png
    ├── hero.jpg            · (or hero-mobile.jpg + hero-desktop.jpg)
    ├── *_before.jpg, *_after.jpg
    ├── job<colour><type>.jpg   · gallery photos
    └── roof-aerial.mp4     · optional drone clip
```

---

## 3. Page section order (the spine — DO NOT REORDER)

This sequence is deliberate and conversion-tuned. Every site uses it.

1. **Top announce ticker** — auto-scrolling marquee of credentials/promises.
2. **Header** — sticky, dark, wordmark/logo + 5 nav links + phone + Get a Quote button. Burger on mobile.
3. **Mobile drawer** — slides in from right, full-height, dark, large uppercase nav.
4. **HERO** — full-bleed image, eyebrow + huge condensed headline + subline + 2 CTAs.
5. **Services ticker** — second marquee, this one alternating accent/paper colours, listing service names.
6. **Services** — 6 cards (one POPULAR sticker, one NEW with price badge).
7. **About** — two-column "Story + portrait" with stats strip below.
8. **Featured Job** — single before/after slider + optional aerial video.
9. **More Work** — 2 additional before/after sliders.
10. **Gallery** — auto-drift horizontal strip of ~10 thumbs with dot navigation.
11. **Colour Guide** — Colorbond palette (8 popular + expand-to-22 toggle).
12. **Guarantee** — animated SVG pie gauge counting 0 → N years.
13. **Reviews** — carousel, 6 cards, 5 stars each, arrows + dots.
14. **Areas We Serve** — 3 columns of suburb lists + bottom CTA pill.
15. **FAQ** — 5 questions, single-open accordion.
16. **Quote form** — 6 fields (name, phone, email, address, message, photo upload) on dark bg.
17. **Footer** — wordmark + phone + email + credentials + 3 social/credential icons + copyright.
18. **Sticky mobile CTA bar** — fixed bottom (`Call` + `Quote`), shows on phones only.
19. **Lead-capture popup** — 15-second trigger or exit-intent.
20. **Quote modal** — opened by every Get a Quote CTA on the page.

If a new site genuinely doesn't need a section (e.g. no commercial work → drop the commercial card from Services), remove it cleanly — don't replace it with filler. Otherwise, keep the order.

---

## 4. Layout primitives

These class names appear on every page. Don't rename them.

| Class | Job |
|---|---|
| `.wrap` | Centred container, `max-width: 1200px`, 24px side padding (16px on mobile) |
| `section` | Auto vertical padding via `--section-py` (40px desktop / 32px mobile) |
| `.section-dark` | `background: var(--ink)`, `color: var(--paper)` |
| `.section-paper` | `background: var(--paper)`, `color: var(--ink)` |
| `.section-head` | Centred section header block (eyebrow + h2 + optional p), max-width 820px |
| `.eyebrow` | Small uppercase Oswald label in accent colour, `letter-spacing: 0.2em` |
| `.btn` `.btn-primary` `.btn-outline-light` `.btn-outline-dark` | The four button variants. Min-height 52px, Oswald, uppercase, `letter-spacing: 0.1em` |
| `.reveal` | Fade+slide-up on scroll-into-view (handled by JS IntersectionObserver) |
| `.phone-pill` | Big red rounded phone CTA used in Areas + popups |

**Section rhythm.** Alternate `.section-paper` and `.section-dark` for visual cadence. Current pattern is approximately: paper → paper → dark → paper → dark → paper → paper → paper → paper → dark → paper → dark.

---

## 5. Breakpoints

Three breakpoints, used consistently:

```css
@media (max-width: 960px) { /* tablet collapse — 2-col grids → 1-col, hide desktop nav */ }
@media (max-width: 720px) { /* phone — mobile hero, sticky CTA appears, areas accordion */ }
@media (max-width: 480px) { /* small phone — tighter padding, smaller phone-pill */ }
```

The 720px breakpoint is the most important — it triggers the mobile-specific hero layout, sticky CTA bar, areas accordion, and the burger menu.

---

## 6. Typography (PER-SITE VARIABLE)

The reference site uses three Google Fonts:

| Font | Use | Weight | Notes |
|---|---|---|---|
| **Anton** | h1–h5, hero headline, brand wordmark main | 400 | Single weight, ultra-condensed display |
| **Oswald** | Eyebrows, buttons, nav, ticker, faq questions, brand wordmark sub | 400, 500, 600, 700 | Condensed UI workhorse |
| **Montserrat** | Body copy, paragraphs, form fields | 400, 500, 600, 700 | Readable sans for prose |

### For each new site, swap to a different but parallel stack.

The structure is **always: Display font (condensed/heavy) + UI font (condensed/medium) + Body font (humanist sans)**. Three fonts, one of each role. Suggested alt stacks (Claude Code: pick one per build, or ask the user):

- **Stack A** (more industrial): `Bebas Neue` + `Barlow Condensed` + `Inter`
- **Stack B** (warmer/heritage): `Big Shoulders Display` + `Archivo Narrow` + `Source Sans 3`
- **Stack C** (sharper/modern): `Antonio` + `Saira Condensed` + `DM Sans`

Whatever you pick, update:
- The `<link>` Google Fonts URL in **every** HTML file (`index.html`, `service-area.html`, `thanks.html`).
- The CSS rules — search `'Anton'` → display font, `'Oswald'` → UI font, `'Montserrat'` → body font.
- Letter-spacing and weight may need small adjustments (Bebas Neue is wider than Anton, for example).

Display font sizes (scale these only if the new font's optical size differs significantly):

```css
.hero-headline      { font-size: clamp(2.25rem, 10vw, 3rem); /* mobile */
                      → clamp(3rem,  6vw, 5.5rem); /* desktop */ }
.section-head h2    { font-size: clamp(2rem, 3.5vw + 1rem, 3.5rem); }
.eyebrow            { font-size: 0.75rem; letter-spacing: 0.2em; }
```

---

## 7. Colour system (PER-SITE VARIABLE)

The whole palette is six CSS custom properties at the top of `main.css`. The structure is **always: ink (near-black) + graphite + steel + concrete (warm grey) + paper (off-white) + line + brand accent + brand accent deep**.

### Reference (Heatshield) palette

```css
:root {
  --ink:      #0B0B0D;   /* near-black, dark sections */
  --graphite: #1C1C1E;   /* slightly lighter dark, used for striped placeholders */
  --steel:    #2A2A2E;   /* lightest dark, used for rules/borders on dark bg */
  --concrete: #8A8783;   /* warm grey, body copy on dark, captions */
  --paper:    #F5F2ED;   /* warm off-white, light section bg */
  --line:     #E3DFD8;   /* line/border colour on paper */
  --red:      #B91C1C;   /* brand accent — dominant */
  --red-deep: #8A1414;   /* brand accent hover */
  --orange:   #EF4E23;   /* secondary accent (alternating ticker, stat sep, review divider) */
}
```

### For each new site

Keep the **neutral structure identical** (ink, graphite, steel, concrete, paper, line). Only change the **two accent colours** and decide if a secondary accent is used:

- **Site 2 idea — a deep teal / petrol blue family**: `--brand: #0E6E76; --brand-deep: #0A565C;` with a warm gold secondary `#D4A437`.
- **Site 3 idea — a desaturated heritage olive**: `--brand: #4A5A2A; --brand-deep: #354220;` with a terracotta secondary `#C2542A`.

(These are starting points only. The owners may have a colour they want.)

**Naming convention:** rename `--red` / `--red-deep` to `--brand` / `--brand-deep` on the new sites — that way the variable name is brand-agnostic and Claude Code doesn't need to mentally translate. (The current Heatshield site uses `--red` for historical reasons; the new sites should use `--brand`.)

After swapping, do a global find for any hard-coded hex matching the old accent and replace.

---

## 8. The hero — the most important section

### Desktop (≥ 720px)

- Full-bleed background `<picture>` element, `object-fit: cover`.
- Dark gradient overlay (`linear-gradient(180deg, rgba(0,0,0,.55) 0%, rgba(0,0,0,.15) 50%, rgba(0,0,0,.7) 100%)`).
- Centred content: eyebrow → huge condensed headline (2 lines, `<br>`) → 1-line desktop subline → 2 CTAs in a row.
- Min-height ~80vh.

### Mobile (≤ 720px)

This is the key art-direction. **Do not collapse to a generic mobile hero.**

- Aspect ratio locked to **3:4** (`aspect-ratio: 3 / 4`), height auto.
- Image stays visible — `object-position: center 60%` so the roof sits in the lower half.
- Stronger gradient overlay (top 75% black + bottom 65% black, middle clear-ish) so the roof remains visible behind the central clear band.
- Content uses `flex-direction: column; justify-content: space-between` — eyebrow + headline + subline cluster at TOP, CTAs alone at BOTTOM. The middle is image.
- Mobile gets a different (shorter) subline via `.hero-sub-mobile` / `.hero-sub-desktop` toggle.
- CTAs are **full-width**, stacked, max-width 280px, 44px high (Apple HIG minimum).

```html
<p class="hero-sub hero-sub-mobile">Short punchy line. Credentials. No deposit.</p>
<p class="hero-sub hero-sub-desktop">Slightly longer one-line variant for desktop.</p>
```

```css
.hero-sub-mobile  { display: none; }
.hero-sub-desktop { display: block; }
@media (max-width: 720px) {
  .hero-sub-mobile  { display: block; }
  .hero-sub-desktop { display: none; }
}
```

### Hero copy formula

```
EYEBROW:    [LICENCE] · [REGION] · [GENERATION/CRED]
HEADLINE:   [VOICE LINE 1].
            [VOICE LINE 2 — REGION].
SUBLINE:    [BASE]-based [TRADE] team servicing all of [STATE].
CTAs:       [Get a Free Quote]   [Call us · 04xx xxx xxx]
```

Examples that work:
- "Tough on roofs. Built for Queensland." (Heatshield)
- "Hunter Valley locals. NSW workmanship." (Rob's)
- New sites should pick a similar two-line couplet — first line is character, second line is place.

---

## 9. Services section

6 cards in a 3 × 2 grid (collapses to 2 × 3 at 960px, 1-column at 480px).

- One card has a **POPULAR sticker** rotated `-8deg`, accent-bg, paper-text.
- One card has a **NEW badge** with a price (e.g. `$1.50 per screw`), paper-bg, brand-text, bordered.
- Each card has: icon (SVG line-art, currentColor) → title (Oswald 600 uppercase) → 2-line description → "Learn more →" link in accent.

The 6 services for any new site are likely:
1. Colorbond Respray — usually the POPULAR one
2. Tile Restoration / Terracotta Repaint
3. Roof Screw Replacement (with $ badge) — *if* they offer it
4. Heat Reflective Coatings
5. Ridge Capping / Rebedding & Repointing
6. Commercial Roofs — *if* applicable

Talk to the owner before assuming. Each tradie may have a slightly different mix.

---

## 10. About section formula

```
EYEBROW:   ABOUT
HEADLINE:  A family trade.
           [Place] [verb].         ← e.g. "Toowoomba grown" / "Hunter raised"
BODY:      [N] yrs [Owner] hands-on, third generation, [relationship to other family member],
           father [N]+ yrs.
STATS:     [N] YRS HANDS-ON · 3RD GENERATION · [TOP CRED]
PHOTO:     Owner on-site portrait, square crop, ink-toned border-top
```

Always cross-mention the brother/family — that's the whole point of the family-trade pitch. Bryce's site mentions Rob; Rob's site mentions Bryce; the next two sites should mention both.

---

## 11. Areas We Serve

3 columns, 8 suburbs each = ~24 suburbs total. On desktop, columns are static lists with `/` red bullets (`li::before { content: '/ '; color: var(--accent); }`).

**On mobile (< 720px) the columns become `<details>` accordions** — tap the column heading to expand.

Bottom CTA is a centred `.phone-pill` reading `Not On Your List? Call Us · 04xx xxx xxx`.

For each new site, plan the regional split:

- **Northern NSW site (idea)**: Hunter & Newcastle / Mid-North Coast / New England
- **Western Sydney / Blue Mtns site (idea)**: Hills District / Penrith & West / Blue Mountains
- **Far North QLD site (idea)**: Cairns & Tablelands / Townsville / Whitsundays

Use real suburb names. The owner will know the list.

---

## 12. Reviews

6 cards in a horizontal carousel:
- 5 SVG stars in accent colour
- Quote text (Montserrat 400, 1.05rem, line-height 1.5)
- Small accent divider line (60×1px)
- First name only (e.g. "Greg.")

Carousel has prev/next arrows (hidden on mobile, swipe is native), and 6 dots below. The active dot is `--accent` and 1.2× scale.

**Always** include an HTML comment above the section flagging the owner to swap with real Google reviews:

```html
<!-- NOTE TO [OWNER]: Placeholder reviews for launch. Replace with real Google reviews as you collect them. -->
```

Pick 6 different first names per site so they're distinguishable. Real reviews from family members or test reviews are better than completely fictional ones.

---

## 13. Components catalogue (CSS classes)

The full set Claude Code should know exists already and not reinvent:

```
Buttons:        .btn, .btn-primary, .btn-outline-light, .btn-outline-dark, .phone-pill
Layout:         .wrap, .section-dark, .section-paper, .section-head
Header/Nav:     .site-header, .nav, .nav-links, .nav-cta, .nav-phone, .nav-burger,
                .mobile-sheet, .mobile-sheet-head, .mobile-cta
Hero:           .hero, .hero-bg, .hero-bg-placeholder, .hero-content, .hero-top,
                .hero-bottom, .hero-eyebrow, .hero-headline, .hero-sub,
                .hero-sub-mobile, .hero-sub-desktop, .hero-ctas
Tickers:        .announce-bar, .announce-track, .ticker-track
Services:       .services-grid, .service-card, .service-card.featured,
                .service-sticker, .service-badge
About:          .about-grid, .about-photo, .about-stats, .about-stat, .about-stat-sep
B/A Slider:     .ba-pair, .ba-slider, .ba-handle, .ba-label
Gallery:        .gallery-strip, .gallery-track, .gallery-tile, .gallery-dots
Colour guide:   .colour-grid, .colour-swatch, .btn-outline-orange (legacy class name, fine to keep)
Guarantee:      .guarantee-gauge, .gauge-arc, .gauge-counter
Reviews:        .reviews-carousel, .reviews-track, .review-card, .review-stars,
                .review-text, .review-divider, .review-name, .reviews-arrow,
                .reviews-arrow-prev, .reviews-arrow-next, .reviews-dots, .review-dot
Areas:          .areas-cols, details.areas-col, .areas-col-title, .areas-cta
FAQ:            .faq-list, .faq-item, .faq-q, .faq-a, .plus
Form:           .quote-form, .form-row, .form-field, .form-dropzone, .form-submit
Footer:         .footer, .footer-brand, .footer-phone, .footer-email, .footer-creds,
                .footer-meta, .footer-social, .footer-line, .footer-copy
Sticky CTA:     .sticky-cta
Modal/Popup:    .modal, .modal-backdrop, .modal-card, .popup, .popup-card
Utility:        .reveal, .ph-label
```

**If you find yourself inventing a new class name, first check whether one of these covers it.**

---

## 14. JavaScript behaviours (already implemented)

`main.js` is a single IIFE that wires up:

1. Hero image resolution warning (console)
2. Quote-fields template injection (single-source-of-truth for both forms)
3. Mobile menu open/close
4. Header scroll-shadow (when `scrollY > 8`)
5. Ticker speed normalisation (matches pixels-per-second across both marquees)
6. Before/after slider drag handle (touch + mouse)
7. FAQ accordion (single-open: opening one closes others)
8. Areas accordion (open desktop, closed mobile, toggled on resize)
9. Scroll reveal + stagger (IntersectionObserver, respects prefers-reduced-motion)
10. Counter tween (for the guarantee gauge number)
11. Guarantee gauge SVG arc animation (0 → N years on viewport entry)
12. Gallery constant-drift + dot navigation (auto-scrolls, pauses on hover)
13. Reviews carousel arrows + dots + active tracking
14. Colour guide expand/collapse (8 popular ↔ 22 all)
15. Smooth scroll for in-page anchor links
16. File dropzone (click-to-browse + drag-drop + thumbnail previews) on the photo upload
17. Year auto-update in footer copyright
18. Video autoplay + fallback to first-frame poster
19. Image fallback (broken images replaced with styled placeholder)
20. Quote modal open/close
21. Lead popup smart triggers (15s + exit-intent + scroll-depth, fires once per session)

For new sites, this file should be **copied verbatim** and only the brand strings inside it changed (search for the brand name in console logs and update). All behaviours are brand-agnostic.

---

## 15. SEO & metadata pattern

Every page has, in order in `<head>`:

1. `<title>` — `[Brand] · [Top cred] · [Region] Wide`
2. `<meta name="description">` — 150-char pitch with brand, base, key creds, phone.
3. `<meta name="keywords">` — service + region pairs.
4. Favicon + Apple touch icon.
5. Open Graph block (site_name, locale, type, url, title, description, image, image:secure_url, image:type, image:width, image:height, image:alt).
6. Twitter Card block (card=summary_large_image, title, description, image, image:alt).
7. `<meta name="theme-color" content="#0B0B0D">` for Safari/Chrome browser chrome.
8. Google Fonts preconnect + stylesheet link.
9. Local CSS link.
10. **JSON-LD `RoofingContractor` schema block** — name, image, url, telephone, priceRange, address (PostalAddress), areaServed (State + containedInPlace Country), openingHoursSpecification.

Keep this exact order. The JSON-LD is the SEO spine — update name/url/telephone/address/areaServed for each new site.

---

## 16. Forms (Netlify)

Two identical forms: the in-page one (in `#quote` section) and the popup-modal one. Both share fields via a `<template id="quote-fields-template">` injected by JS — single source of truth, **don't duplicate fields by hand**.

Required setup:
- Hidden form pre-registered at top of `<body>` for Netlify build-time discovery
- Both visible forms have `data-netlify="true"` and `name="quote-form"` (the same name — Netlify dedupes)
- Honeypot field via `netlify-honeypot="bot-field"`
- Both submit to `/thanks.html`
- Six fields: name, phone, email, street address (with helper text), message, photo upload (drag-drop)

`thanks.html` is the same minimal "thank you, [Owner] will call you back within [hours]" page on every site — change only brand + owner name + phone.

---

## 17. Per-site variables checklist

When starting a new site, the very first thing Claude Code should do is fill out this table by asking the user (or referring to a brief). Keep it as the first commented block in `LAST_BUILD_SUMMARY.md` for that site.

```
BRAND
  business name:           ____________________
  owner first name:        ____________________
  tagline (≤ 8 words):     ____________________
  family link:             ____________________ (e.g. "younger brother of Rob, son of [father]")

CONTACT
  phone:                   04__ ___ ___
  email:                   ____________________
  base town:               ____________________
  state:                   ____________________
  ABN:                     ____________________
  licence # (state-specific): ____________________
  hours:                   ____________________

REGION
  state full:              ____________________  (Queensland / New South Wales / Victoria etc.)
  state abbrev:            ____________________  (QLD / NSW / VIC)
  3 region groupings:      1) ____________________  2) ____________________  3) ____________________
  ~8 suburbs each (24 total): see Areas section

BRANDING
  display font:            ____________________
  ui font:                 ____________________
  body font:               ____________________
  brand colour (hex):      #________________
  brand-deep colour (hex): #________________
  secondary accent (hex):  #________________ (or "none — use one accent only")

SERVICES (which 6, in order, which is POPULAR, which has $ badge)
  1. ___________________________________________________
  2. ___________________________________________________
  3. ___________________________________________________  (POPULAR)
  4. ___________________________________________________
  5. ___________________________________________________  (NEW · $X.XX badge)
  6. ___________________________________________________

CREDENTIALS LINE
  e.g. "QBCC Licensed · Fully Insured · Dulux Accredited Applicator"
  → ___________________________________________________

GUARANTEE
  years:                   __  (10 / 12 / 15)
  backer:                  ____________________  ("Dulux-backed" / "manufacturer-backed" / etc.)

DOMAIN
  primary URL:             https://________________________________

SOCIALS
  facebook URL:            ____________________
  instagram URL:           ____________________
  state-licence-search URL: ____________________
```

---

## 18. Build order (a new site, start to finish)

The fastest, lowest-risk way:

1. **Duplicate the reference site folder** verbatim (Heatshield is the cleanest reference).
2. **Fill out the per-site variables checklist (§17)** with the user — don't guess.
3. **Update `:root` palette** in `main.css` — rename `--red` to `--brand`, swap hex values. Find/replace any hard-coded old hex.
4. **Swap fonts** — update Google Fonts link in all 3 HTML files; find/replace `'Anton'`, `'Oswald'`, `'Montserrat'` in `main.css`.
5. **Update brand strings everywhere** — business name, owner name, phone, email, base town, state. There are roughly 18 brand mentions in `index.html`, 4 in `service-area.html`, 3 in `thanks.html`, ~6 in `main.js` (console messages).
6. **Replace JSON-LD schema** values.
7. **Rewrite hero** copy (eyebrow, headline, subline ×2, CTAs).
8. **Rewrite About** copy with the specific family link.
9. **Rewrite Services cards** to match the 6 chosen.
10. **Rewrite Areas** with the 24 suburbs in 3 groups.
11. **Rewrite Reviews** with 6 different first names + plausible quotes (flag for replacement).
12. **Rewrite FAQ** — 5 questions, keep #1 as price/quote-beat, customise the rest if the owner has specific FAQs.
13. **Update tickers** — both top announce ticker and services ticker reflect the new credentials and service mix.
14. **Update footer** — credentials, social URLs, state-licence-verification URL.
15. **Leave all images as styled placeholders** at first — the diagonal-stripe `[ HERO IMAGE — TO BE ADDED ]` block is correct behaviour. Only swap in real images when supplied.
16. **Run audit** — search the codebase for the previous brand name (e.g. "Heatshield"), the previous phone, the previous email, the previous town, the previous state, the previous licence number. Each should return 0 results.
17. **Generate a `LAST_BUILD_SUMMARY.md`** in the same format as the existing one — Bryce's existing summary is the template. This is the handover doc.

---

## 19. What never changes (the family DNA)

These are the through-lines across every site in the family. **Don't lose these in the differentiation push.**

- The 20-section spine, in that exact order.
- The 720px breakpoint mobile-hero approach (3:4 aspect ratio, image visible, text top + CTAs bottom).
- The dark/paper alternating section rhythm.
- The two-marquee tickers (announce + services).
- Three fonts: a condensed display + a condensed UI + a humanist body.
- The single-accent-colour approach against an ink + paper neutral pair.
- The Netlify hidden-form + template-injection pattern for forms.
- The IIFE single-file `main.js` with the 21 listed behaviours.
- The "tradie-confident, never corporate" voice.
- HTML placeholder comments flagging every TODO image and content swap.
- The family cross-mentions (Rob ↔ Bryce ↔ new owners).

---

## 20. What must change (per-site differentiation)

- Brand name + wordmark
- Owner first name
- Phone, email, address, ABN, licence number
- All three Google Fonts (display / UI / body trio)
- Brand accent colour (and brand-deep + optional secondary)
- Tagline / hero headline couplet
- About-section regional verb ("grown" / "raised" / "born and bred")
- Services mix (6, with appropriate POPULAR + $ badge cards)
- 24 suburbs across 3 region groupings
- Reviews: 6 different first names
- Credentials line
- Guarantee years + backer
- Domain
- Social URLs
- JSON-LD schema values
- OG image (final-state hero or a hero-job photo)

---

## 21. Open questions to ask the user before each new build

1. What's the **business name** and is there a logo, or do we use a wordmark?
2. Where's the owner **based**, and what's their **state**? What 3 regions/clusters do they cover?
3. Who's this owner's **link to the family** (sibling? in-law? son?) — exact wording for the about section.
4. What **services** do they offer? Confirm the 6, mark the POPULAR, mark any with a $ badge.
5. What are their **credentials** (licence body, insurance status, manufacturer accreditation)?
6. What's the **guarantee** (years + who backs it)?
7. Do they have a **brand colour** in mind, or should we pick one that distinguishes from Rob (red-orange) and Bryce (red)?
8. Any **font** preference, or should we pick a stack that distinguishes from the other two sites?
9. **Domain** secured?
10. **Photos** available now, or launch with placeholders?

---

*End of spec. Treat this file as the source of truth. If something on a new site contradicts this doc, the doc wins — fix the site to match.*
