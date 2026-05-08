# Deploy Guide · Tassie Roof Painting

Step-by-step from local folder → live site at tassieroofpainting.com.au.

This is the **Claude Code → GitHub → Netlify** workflow. Once it's set up, every change you make in Claude Code can be pushed to GitHub with one command, and Netlify auto-deploys to the live site within ~30 seconds.

---

## 0. Prerequisites (one-time, takes ~10 minutes)

You'll need:

- **A GitHub account.** Free at [github.com](https://github.com).
- **A Netlify account.** Free at [netlify.com](https://netlify.com). Sign up with **"Sign up with GitHub"** so the two are connected from day one.
- **Git installed.** On Mac it's already there. To check: open Terminal and run `git --version`.
- **Claude Code installed.** Run `npm install -g @anthropic-ai/claude-code` then `claude` in your project folder.

---

## 1. Connect this folder to Claude Code

1. Make sure the `tassie-roof-painting/` folder is sitting on your Desktop (or anywhere sensible — `~/Sites/tassie-roof-painting` is the convention).
2. In Terminal:

   ```bash
   cd ~/Desktop/tassie-roof-painting
   claude
   ```

   That opens Claude Code in the folder. From here, ask Claude for any tweak — copy changes, image swaps, palette tuning, new suburb pages — and it'll edit the files directly.

3. Quick sanity check — ask Claude something like **"What's in this project?"** to confirm it's reading the codebase. Then move on.

---

## 2. Push the project to GitHub

The first time only. After this, every change is just `git add` + `git commit` + `git push`.

### 2a. Create the repo on GitHub

1. Go to [github.com/new](https://github.com/new)
2. **Repository name:** `tassie-roof-painting`
3. **Visibility:** Private is fine.
4. **Do NOT tick** "Add a README", ".gitignore", or "license" — we already have what we need.
5. Click **Create repository**.

### 2b. Initialise and push from your local folder

In Terminal, from inside the project folder:

```bash
git init
git add .
git commit -m "Initial site build · Tassie Roof Painting"

git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/tassie-roof-painting.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your actual GitHub username. The first push may ask you to authenticate — easiest way is to install [GitHub CLI](https://cli.github.com/) (`brew install gh` on Mac) then run `gh auth login` once.

After the push completes, refresh your GitHub repo page — all the files should be there.

---

## 3. Connect Netlify to the GitHub repo

1. Go to [app.netlify.com](https://app.netlify.com) and log in.
2. Click **Add new site → Import an existing project**.
3. Pick **GitHub** as the provider. Authorise Netlify if prompted.
4. Select the `tassie-roof-painting` repo.
5. **Branch to deploy:** `main`
6. **Build command:** *(leave blank)*
7. **Publish directory:** *(leave blank, or just `.`)*
8. Click **Deploy**.

About 30 seconds later Netlify gives you a live URL like `https://random-words-12345.netlify.app`. The site is live.

### 3a. Rename the Netlify subdomain (optional but tidier)

In Netlify: **Site configuration → Change site name** → make it `tassie-roof-painting`. The URL becomes `https://tassie-roof-painting.netlify.app`. Useful for testing before the real domain points here.

---

## 4. Point tassieroofpainting.com.au at Netlify

1. In Netlify: **Domain management → Add a custom domain** → enter `tassieroofpainting.com.au`.
2. Netlify will show you the DNS records to set. Two paths:

   **Easier — let Netlify host the DNS:** point your domain's nameservers at Netlify's. Netlify gives you four nameserver addresses; you set those at your registrar (e.g. Crazy Domains, GoDaddy, Namecheap, wherever the domain is registered). Takes ~24 hrs to propagate fully. After that, every DNS change is in Netlify.

   **Manual — keep DNS at your registrar:** add the records Netlify shows you (typically an `A` record pointing to a Netlify IP, plus a `CNAME` for `www`). Faster initial setup, but every future tweak means logging back into the registrar.

3. Once DNS resolves, Netlify auto-issues a free SSL certificate via Let's Encrypt. The site loads at `https://tassieroofpainting.com.au` without any extra setup.

---

## 5. The everyday workflow (after setup)

This is what you do every time you (or Claude Code) make a change:

```bash
# From inside the project folder:
git add .
git commit -m "Short description of what changed"
git push
```

Within ~30 seconds Netlify redeploys, and the live site reflects the change.

If you want Claude Code to push for you, just say **"commit and push these changes with the message 'updated reviews'"** and it'll run those three commands.

---

## 6. Hooking up Netlify Forms (quote form + popup)

The site has Netlify Forms wired in. You don't need to do anything for it to start working — Netlify auto-detects the hidden `<form name="quote">` and `<form name="lead-popup">` blocks at the top of `index.html` on first deploy.

To see submissions:

1. In Netlify: **Forms** in the left nav.
2. You'll see two forms: `quote` and `lead-popup`.
3. Submissions appear here. Enable **Email notifications** (Forms → Notifications → Add notification → Email) so Bryce gets an email every time someone submits.

**Set up the email notification (do this for both forms):**

- Notification type: **Email notification**
- Form: `quote` (then repeat for `lead-popup`)
- Email to notify: `bstewart2009@live.com.au`
- Save. Test by submitting the form on the live site.

---

## 7. Pre-launch checklist

Before pointing the domain over, walk through this list:

- [ ] **Logo finalised.** Already in `images/logo.png`. If a higher-res version arrives, drop it in.
- [ ] **Favicon set generated.** A placeholder is in `images/favicon.png`. Use [favicon.io](https://favicon.io) — drop the logo in, download the `.zip`, drop the files into `images/`.
- [ ] **Facebook URL confirmed.** Currently `https://www.facebook.com/profile.php?id=100077404508461`. Confirm this is correct — search the codebase for `100077404508461`.
- [ ] **Hero video supplied** (if Bryce has one). Drop into `images/roof-aerial.mp4`. Already wired into the source — will start playing automatically once the file exists.
- [ ] **Image compression.** Photos are already in good shape (~250KB avg). Run them through [Squoosh](https://squoosh.app) if you want to push lower.
- [ ] **Test the form.** Submit a real quote on the live site, confirm the email lands in `bstewart2009@live.com.au`.
- [ ] **Test on mobile.** Open the live URL on Bryce's phone, scroll the whole site, tap the call button, tap "Get a Quote", make sure the popup works.
- [ ] **301 redirects from the old site.** The old Tassie site has these URLs indexed by Google. Set up `_redirects` in the project root:

   ```
   /index.php                                  /            301
   /about-us-php                               /#about      301
   /roof-painting-php                          /#services   301
   /roof-coating-php                           /#services   301
   /pressure-cleaning-php                      /#services   301
   /rust-treatment-php                         /#services   301
   /dulux-acratex-roof-solution-php            /#services   301
   /cpage-php                                  /#quote      301
   /blog-top-10-steps-to-keep-your-roof-in-top-condition-php  /  301
   ```

   Commit, push, done.

- [ ] **Tagline confirmed.** Currently using a neutral placeholder ("Tassie roofs. Properly coated."). When Bryce supplies his preferred line, search the codebase for that string and replace.

---

## 8. Common Claude Code commands you'll use a lot

```bash
# Edit a specific file with Claude
claude "update the hero copy to lead with 'Tasmania's roof painting specialists'"

# Add a new suburb landing page
claude "create a new service-area page for Launceston, mirroring the Devonport one"

# Swap the palette
claude "change --accent to a slightly cooler ochre, around #C99033"

# Compress all images
claude "run an image compression pass on /images using cwebp; target 250KB each"

# Update reviews
claude "add a new 5-star review from a customer named 'Pat' to the reviews carousel"
```

Claude Code edits the files directly. Then `git add . && git commit -m "..." && git push` and you're live.

---

## 9. If something breaks

- **Site shows a 404 after deploy.** Check the Netlify build log (Site overview → Deploys → click the latest one). Usually a typo in a filename. Fix locally, commit, push.
- **Form submissions aren't arriving.** Check Netlify Forms is enabled (Site configuration → Forms → toggle on). Then check the email notification is set up (step 6).
- **CSS or JS not loading.** Likely a relative-path issue. The site uses `css/main.css` and `js/main.js` — those paths are relative.
- **DNS not resolving.** Allow 24 hours for full propagation. Use [whatsmydns.net](https://whatsmydns.net) to check from multiple regions.
- **Images broken.** Filenames are case-sensitive on the live server. If `Hero.jpg` works locally but not deployed, it's because the file is actually `hero.jpg` (or vice versa). Rename to match.

---

## 10. Files in this project that are safe to share publicly

If the GitHub repo goes public, this is what visitors see:

✅ All HTML, CSS, JS — fine to be public
✅ Images in `/images` — already public on the live site
✅ README.md, DEPLOY.md, LAST_BUILD_SUMMARY.md — fine

❌ Do NOT commit:
- API keys, passwords, tokens
- Real customer data in plain text
- The actual ABN if Bryce considers it sensitive (currently displayed publicly in the footer — that's standard practice for AU businesses, but flag if it's an issue)

The current build has zero secrets. Safe to push as-is.

---

That's the whole pipeline. Once steps 0–4 are done once, every future change is `git push` and you're live in 30 seconds.
