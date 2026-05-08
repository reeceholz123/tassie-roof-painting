# Tassie Roof Painting · Site

Production codebase for [tassieroofpainting.com.au](https://tassieroofpainting.com.au) — the Tasmanian arm of the Stewart family roof-restoration partnership.

Site #4 in the family. Forks from Coast and Country Roof Coatings (NSW).

---

## What's in this folder

```
tassie-roof-painting/
├── index.html              ← long landing page, the only conversion page
├── service-area.html       ← suburb-specific SEO page (Devonport sample)
├── thanks.html             ← post-form-submit page
├── css/
│   └── main.css            ← single design-system stylesheet
├── js/
│   └── main.js             ← single IIFE with 21 interactive behaviours
├── images/                 ← all photos, logo, favicon
├── README.md               ← this file
├── DEPLOY.md               ← step-by-step deploy guide
└── LAST_BUILD_SUMMARY.md   ← every decision made in the build session
```

## Stack

- Vanilla HTML / CSS / JS — no build step
- Netlify Forms (auto-detected from hidden pre-registration forms)
- Mobile-first responsive at 720px breakpoint

## Brand

- **Primary navy**: `#092768` (extracted directly from the supplied logo)
- **Deep navy**: `#051A48`
- **Accent ochre**: `#D49B3A`
- **Display font**: Antonio
- **UI font**: Saira Condensed
- **Body font**: DM Sans

## Working on this site locally

1. Open the folder in your code editor of choice.
2. Open `index.html` in a browser to preview. Refresh after changes.
3. For the Netlify Forms behaviour to work, you need to push the changes — forms only register on the live site, not locally.

## Common edits

- **Update reviews**: `index.html` — section 15 `<!-- 15. REVIEWS · paper -->`
- **Update areas**: `index.html` — section 16, three `<details class="areas-col">` blocks
- **Update FAQ**: `index.html` — section 17
- **Add a new suburb page**: copy `service-area.html`, rename it (e.g. `launceston.html`), find/replace `Devonport` → `Launceston`, update the hero, body copy, breadcrumb, and the two `suburb` hidden inputs.
- **Swap a hero image**: drop a new file in `/images`, edit the `<img class="hero-bg-desktop">` and `<img class="hero-bg-mobile">` paths in `index.html`.

## Deploying

See `DEPLOY.md` for the full Claude Code → GitHub → Netlify workflow.

The everyday update flow (after the initial setup):

```bash
git add .
git commit -m "Short description of what changed"
git push
```

Netlify auto-deploys within ~30 seconds.

## Pre-launch checklist

See `DEPLOY.md` section 7 for the full pre-launch list. Top items:

- [ ] Confirm Facebook URL (currently using profile id `100077404508461`)
- [ ] Drop in any final photos Bryce wants to add
- [ ] Test the quote form on the live site, confirm email lands at `bstewart2009@live.com.au`
- [ ] Test on Bryce's phone — full scroll, tap call, tap "Get a Quote", confirm popup works
- [ ] Add `_redirects` file for the old WordPress URLs from the previous Tassie site
- [ ] Regenerate the full favicon set via [favicon.io](https://favicon.io)

## Lineage

| Version | Site | Notes |
|---|---|---|
| v1 | Rob's Roof Painting | the original parent template |
| v2 | Heatshield Roof Restorations (QLD) | refined the structure |
| v3 | Coast and Country Roof Coatings (NSW) | most refined — direct parent of this build |
| **v4** | **Tassie Roof Painting (TAS)** | this site |

When site #5 starts, this codebase becomes the new reference. See the master kit's `README.md` for the procedure.
