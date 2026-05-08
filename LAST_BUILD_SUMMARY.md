# Last Build Summary · Tassie Roof Painting

Site #4 in the Stewart-family roof-restoration site family.
Forked from Coast and Country Roof Coatings (NSW), adapted for Tasmania.

Built May 2026 in a single working session.

---

## 1. Decisions made in this build

| Topic | Decision | Notes |
|---|---|---|
| Business name | **Tassie Roof Painting** | matches existing trading name registered with ABR (Jan 2022) |
| Owner shown on site | Not named publicly except in real reviews | "Stewart family partnership" framing in About copy |
| Address shown | None | service-area only in JSON-LD; no street pin until later |
| Phone | 0487 509 027 | shared with C&C |
| Email | bstewart2009@live.com.au | shared with C&C |
| ABN | 27 641 453 645 | A Stewart & B.T Stewart Family Partnership, active since 1 Jan 2007 |
| Hours | Mon–Fri, 9am–7pm | weekend not displayed |
| Guarantee | 10 years written | matches C&C and Heatshield |
| Years messaging | "25 years on Australian roofs" | softer than C&C's "30 years," rounded down |
| Domain (target) | tassieroofpainting.com.au | unconfirmed at build time |

## 2. Service mix (6 cards)

1. **Roof Painting** — Popular sticker + "From $18/m²" pill badge (the differentiator from C&C)
2. **Roof Coating**
3. **Pressure Cleaning & Moss Treatment**
4. **Rust Treatment**
5. **Dulux AcraTex Solution** — Premium navy sticker
6. **Farm Sheds & Rural Roofs**

The price-from-$18 callout is pulled from the truck signage in the supplied photos. It's the single strongest positioning lever this brand has — kept it loud.

## 3. Areas (24 towns, 3 regions)

- **North-West Coast**: Devonport, Burnie, Ulverstone, Wynyard, Smithton, Penguin, Latrobe, Sheffield
- **North & Tamar Valley**: Launceston, Deloraine, Westbury, Longford, Perth, George Town, Beaconsfield, Scottsdale
- **East Coast**: Bicheno, St Helens, Scamander, Triabunna, Swansea, St Marys, Coles Bay, Orford

## 4. Brand system

### Colour palette (logo-driven)
- `--brand: #092768` — navy extracted from the supplied logo (deeper and more saturated than C&C's `#0E2A4F`)
- `--brand-deep: #051A48` — darker shadow variant
- `--accent: #D49B3A` — warm ochre, distinct from C&C's `#2787DB` bright blue. Used on POPULAR stickers and CTA hover. Differentiator from C&C without breaking the family aesthetic.

### Fonts
- Display: **Antonio** (replaces C&C's Big Shoulders Display) — narrower, more condensed feel suited to Tassie's tradie tone
- UI: **Saira Condensed** (replaces Archivo Narrow)
- Body: **DM Sans** (replaces Source Sans 3)

The font swap is the single biggest visual differentiator from C&C while staying inside the same condensed-display + condensed-UI + clean-body family.

## 5. Reviews (6 real customers)

All sourced from the existing Tassie Roof Painting Facebook page, the old website, and Google reviews. Order optimised for emotional arc (Yoga's full enthusiastic story → Nicholas's price-point line → Jodie's family bond → Vivien's faded-to-great → Helen's communication → Amber's quick endorsement).

| # | Reviewer | Source | Notes |
|---|---|---|---|
| 1 | Yoga | Google + Facebook | full quote, names Bryce |
| 2 | Nicholas | Google | "great price point" |
| 3 | Jodie | old site | "Bryce and his family" — naturally validates the family-partnership framing |
| 4 | Vivien | old site | "faded → great" arc |
| 5 | Helen | old site | "communication and result" |
| 6 | Amber | Facebook | short and warm |

Last names omitted for privacy.

## 6. Photos delivered (39 files in `/images`)

All photos are real Tassie work. No diagonal-stripe placeholders needed for any slot — the photo set covers the entire site.

**Hero pair**: `hero_image_desktop.jpg` (grand country home with charcoal roof) + `hero_image_mobile.jpg` (Emma's white weatherboard, 3:4 friendly crop)

**Featured Job (slot 8)**: coastal east-coast beach house, blue before/after — the after-shot includes the Tassie Roof Painting truck in frame, which doubles as a subtle trust signal.

**More Work carousel (slot 11, 4 pairs)**: green→charcoal, red→grey, charcoal+red trim refresh, weathered cottage→clean grey.

**Process trio (slot 10)**: weathered green roof → solar covered during prep → fresh charcoal coating.

**Gallery (slot 12, 25 tiles)**: full mix of jobs across NW Coast + East Coast. Truck shot included as the first gallery tile to anchor brand identity.

**Logo**: extracted as PNG from the `.webp` original, kept at full resolution (2911×634) for crisp retina rendering.

**Favicon**: auto-generated 192×192 crop of the logo. Bryce should regenerate the full favicon set via [favicon.io](https://favicon.io) before launch.

## 7. Things known to be missing / placeholders

- **Tagline** is currently "Tassie roofs. Properly coated." — neutral placeholder. Replace when Bryce supplies his preferred line.
- **Aerial drone video** — `images/roof-aerial.mp4` is referenced but not present. Site degrades gracefully (JS hides the block if file is missing). Drop the video in if/when Bryce supplies one.
- **Facebook URL** — set to `https://www.facebook.com/profile.php?id=100077404508461`. Confirm with Bryce before launch.
- **Trust badge "FAMILY PARTNERSHIP · Stewart · Since 2007"** — text only. If Bryce wants real Dulux AcraTex / Colorbond logo PNGs, drop them in `images/` and swap the text spans for `<img>` tags in slot 9b.

## 8. What's structurally identical to C&C

- 22-section spine (announce ticker → header → sticky creds → mobile drawer → hero → services ticker → services grid → featured job → about → trust badges → why → process → more work → gallery → problems → colour guide → guarantee gauge → reviews → areas → FAQ → quote form → footer → sticky mobile CTA → lead popup → quote modal)
- Single-file `js/main.js` IIFE with all 21 interactive behaviours
- Single `css/main.css` design system
- Netlify form pattern (hidden pre-registration + 3 visible forms all named `quote` and `lead-popup`)
- Mobile hero spec at 720px breakpoint (3:4 image, text top, CTAs bottom — the most distinctive design moment in the family, fully preserved)

## 9. What's distinctly Tassie

- Logo navy (`#092768`) replaces C&C's softer navy
- Ochre accent replaces bright-blue accent
- Antonio + Saira Condensed + DM Sans replaces the C&C font set
- "From $18/m²" price badge on the Roof Painting card (new component class added to CSS)
- Climate language throughout: "damp Bass Strait southerlies," "salt air," "south-facing tiles," "Tassie weather"
- Stewart family partnership framing instead of "Bryce, with thirty years"
- 24 Tassie towns instead of 24 NSW suburbs
- Real Tassie-only customer reviews (Yoga, Nicholas, Jodie, Vivien, Helen, Amber — no C&C reuse)

## 10. Deploy notes for next session

- **Form notification email** — Netlify Forms → set up email notification to `bstewart2009@live.com.au` for both `quote` and `lead-popup` forms.
- **301 redirects** — old Tassie site has WordPress URLs (`/about-us-php`, `/roof-painting-php`, `/roof-coating-php`, `/dulux-acratex-roof-solution-php`, `/pressure-cleaning-php`, `/rust-treatment-php`, `/cpage-php`, `/blog-…`). Add a `_redirects` file at the project root mapping these to the corresponding hash anchors on the new site (see `DEPLOY.md` for the format).
- **Image compression** — current photos average ~250KB which is good. Logo is 388KB (PNG); convert to WebP later if needed.
- **OG image** — currently set to `grand_house_grey.jpg`. Confirm this renders correctly when shared on Facebook before launch.

## 11. When this kit graduates to v4

Per the kit README: when site #5 is being briefed, the most-refined existing site becomes the new reference codebase. Tassie's price-badge component, the Tas-climate language, and the Antonio/Saira/DM Sans set are the candidate carry-overs. Everything else mirrors C&C and should be evaluated against whichever build feels strongest at that point.
