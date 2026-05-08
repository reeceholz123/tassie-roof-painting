# Premium Roofing Site · Starter Kit

A self-contained kit for building the next site in the Stewart-family roof-restoration family of websites. Designed to be unzipped, dropped into a fresh Claude project, and turned into a finished site by Claude Code in a single working session.

This is the kit version of the workflow that built **Heatshield Roof Restorations** (QLD) and **Coast and Country Roof Coatings** (NSW). The reference implementation included here is Coast and Country — the most recent and most refined of the family.

---

## What's in this kit

```
starter-kit/
├── README.md                       ← this file
├── PROJECT_BRIEF.md                ← brief for the next build (currently scoped to Tasmania)
├── SITE_BUILD_SPEC.md              ← the universal technical spec (read this end-to-end)
└── reference-codebase/             ← the canonical reference site
    ├── index.html                    · long landing page (the only conversion page)
    ├── service-area.html             · suburb-specific SEO page template
    ├── thanks.html                   · post-form-submit page
    ├── css/
    │   └── main.css                  · single design-system stylesheet
    ├── js/
    │   └── main.js                   · single IIFE with 21 interactive behaviours
    ├── README.md                     · the C&C site README (kept as a format-template for the new site's README)
    └── DEPLOY.md                     · the C&C deploy guide (kept as a format-template for the new site's deploy doc)
```

What's deliberately NOT in the kit:

- No `images/` folder. Images are 100% per-business and the placeholders in the codebase are styled to be intentionally visible until real photos are supplied.
- No `_redirects` file. Every site has different legacy URLs to handle.
- No favicons. Regenerated per build via [favicon.io](https://favicon.io).
- No `.git`, no `node_modules`, no build artefacts. There's no build step.

---

## How to use this kit (for the human running the project)

1. **Create a new Claude project** at [claude.ai](https://claude.ai). Name it after the new business.
2. **Upload the contents of this folder** as project knowledge:
   - `PROJECT_BRIEF.md`
   - `SITE_BUILD_SPEC.md`
   - All five reference-codebase files (`index.html`, `service-area.html`, `thanks.html`, `css/main.css`, `js/main.js`)
3. **Open a new chat in that project** and paste the starter prompt below.
4. **Answer the open questions** in `PROJECT_BRIEF.md` §6 before any code is written.
5. **Once the open questions are settled**, follow the build sequence in §9 of the brief. Most of this can be delegated to Claude Code in the project folder.

### Starter prompt to kick off the new chat

> *"Read `PROJECT_BRIEF.md` and `SITE_BUILD_SPEC.md` first, in that order. Then walk me through the open questions in §6 of the brief — one at a time, no preamble. Once we've answered them, follow the build sequence in §9, using the reference codebase as the structural exemplar. Stay strictly within the design language documented in the spec, and audit at the end against the C&C strings listed in §9 step 15."*

---

## How to use this kit (for the Claude that picks it up)

You are not building a site from scratch. You are forking a refined working build into a new brand.

The reference codebase you'll find in `reference-codebase/` is **Coast and Country Roof Coatings** — Bryce Stewart's NSW arm. It contains:

- A 20-section landing page with an asymmetric hero, magazine-style services grid, editorial about section, 4-step process timeline, gallery carousel, Colorbond colour guide, animated guarantee gauge, reviews carousel, areas accordion, FAQ, dual-form (in-page + modal) Netlify quote system, lead-capture popup, sticky mobile CTA bar.
- A single `css/main.css` design system using `--brand`, `--brand-deep`, `--accent` plus an ink/paper/line neutral set.
- A single `js/main.js` IIFE with 21 interactive behaviours — all brand-agnostic except for 3 console / comment strings on lines 2, 8, and 557 of `main.js`.

**The structural spine, the JS behaviours, the form pattern, and the responsive strategy do NOT change between sites.** Only the brand wrapper (palette, fonts, copy, suburbs, photos, schema) changes.

Read `SITE_BUILD_SPEC.md` end-to-end before touching code. It is the source of truth — when something on the new site contradicts the spec, fix the site, not the spec.

---

## What "premium" means in this kit

Three things, in order of priority:

1. **Real-world honesty.** No stock photography, no fake review counts, no fake urgency timers, no inflated guarantees. Every claim has to be defensible in person by the tradie. Diagonal-stripe placeholders are intentionally visible until real photos arrive — they signal "missing" rather than hiding gaps.

2. **Mobile-first, but desktop-considered.** The 720px-breakpoint mobile hero is the most distinctive design moment in the build (3:4 aspect ratio, image visible, text top, CTAs bottom — *not* a shrunk desktop hero). It's the easiest thing to lose in a brand-swap, and the most important thing to preserve.

3. **Tradie-confident voice.** Big condensed display type, uppercase eyebrows, generous negative space, single strong accent against an ink + warm-paper neutral pair. Punchy, declarative, second-person. "We climb up. You get a fixed price. We prep properly. You pay when the job's done."

If a design decision in the new build feels "more polished" but loses any of those three, it's not more polished — it's worse. Mirror the reference.

---

## When this kit ages

Any time a new site is built, the **most-refined** of the existing sites should become the new reference codebase. The progression so far:

- v1 reference: Rob's Roof Painting (the original parent template)
- v2 reference: Heatshield Roof Restorations (refined the structure)
- **v3 reference (current): Coast and Country Roof Coatings** ← this kit
- v4 reference: ???

When site #4 is finished, copy its `index.html`, `service-area.html`, `thanks.html`, `css/main.css`, `js/main.js` over the contents of `reference-codebase/`, update the cross-mentions in `PROJECT_BRIEF.md` §1, bump the version note above, and the kit is ready for site #5.

---

*One folder, one chat, one working session. That's the design.*
