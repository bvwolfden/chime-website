# Clann Website (prvail.ai)

Static marketing site for **Clann** — the family location + parental-controls app.
Hosted on **GitHub Pages** at **https://prvail.ai**.

## Files

- **index.html** — Landing page (Clann brand: sage/green, warm cream, Fraunces + Inter)
- **privacy.html** — Privacy Policy (location + parental-controls + backend; required for App Store)
- **support.html** — Support / FAQ
- **terms.html** — Terms of Service
- **videos.html** — Setup videos page (the four narrated walkthroughs from `marketing/videos`)
- **videos/** — the rendered MP4s + poster JPEGs the page and the iOS inbox play
  (`Video1.mp4` … `Video4.mp4`; the app resolves `https://prvail.ai/videos/<Comp>.mp4`)
- **CNAME** — custom domain (`prvail.ai`)
- **assets/** — brand images used by the pages:
  - `logo-lockup.png` — "clann" wordmark + mark (header/footer)
  - `mark.png` — mark only (favicon)
  - `favicon-180.png` — apple-touch-icon
  - `hero-illustration.png` — family-at-the-lake hero backdrop
  - `screenshots/` — **drop real app screenshots here** (see below)

## Where it actually deploys (IMPORTANT)

`prvail.ai` is **not** served from this monorepo. GitHub Pages serves it from a
**separate repo**:

- **Repo:** `github.com/bvwolfden/chime-website`
- **Source:** branch `main`, path `/` (root)
- **Domain:** `prvail.ai` (CNAME already configured + HTTPS enforced)

> **Drift warning (2026-09-05):** the live repo had edits that never came back
> here (privacy policy date bump, `terms.html`, copy tweaks). They were synced
> into this folder on 2026-09-05. Before an `rsync --delete`, diff this folder
> against a fresh clone of `chime-website` so a stale copy never overwrites a
> newer live page.

This `docs/website/` folder is the **source of truth**. To publish, copy its
contents to the **root** of `chime-website` and push `main`:

```bash
# clone the site repo somewhere outside this monorepo
git clone https://github.com/bvwolfden/chime-website.git /tmp/chime-website
cd /tmp/chime-website

# replace the old site with the new Clann site (keep CNAME)
rsync -a --delete \
  --exclude '.git' \
  /Users/brian/Projects/chime/docs/website/ ./

git add -A
git commit -m "Rebrand site to Clann"
git push origin main
```

Pages rebuilds automatically; live within ~1 minute.

> The old repo also contained `wishjar-privacy.html` / `wishjar-support.html` and
> old Chime PNGs — the `rsync --delete` above removes them. Drop the `--delete`
> flag if you want to keep any of those.

## Screenshots (real app captures — refreshed 2026-09-24 for Clann 2.0.3)

Everything under `assets/screenshots/` is a real capture from the app, not a mock:

- `panels/01-…10-*.jpg` — the **same ten App Store panels** attached to version 2.0.3
  (family map, Usage today / detail / apps + bonus / week, live telemetry, trip replay,
  flight tracking, Precision Find, navigate), downscaled to 645×1398 JPEG. Source of
  truth is `marketing/appstore-previews/` — regenerate a panel there (`gen-panels.mjs`,
  or headless Chrome over `render/<Name>.html` for the older ones), then
  `sips -s format jpeg -s formatOptions 80 -z 1398 645 <panel>-1290x2796.png --out panels/<nn>-<name>.jpg`.
- `hero-usage.jpg` / `detail-usage.jpg` — the Usage tab and a kid's full-day page, status bar
  cropped off (`marketing/appstore/crop.swift <src> <dst> 0 100 764 1590`), shown inside the
  page's CSS phone frames.
- `card-*.jpg` — tight crops of real UI (family roster, bonus-time card, week heatmap, live
  telemetry, trip replay stats) used as the media cards beside each feature section.

When the App Store screenshot set changes, refresh `panels/` first — the gallery caption text
in `index.html` mirrors each panel's headline, and the "What's new · Clann x.y.z" card near the
top of the page should be bumped with the release.

## Before going live — checklist

- The App Store URL is the live listing: `https://apps.apple.com/us/app/clann-by-prvail/id6755217813`
  (Apple resolves by id; the slug is cosmetic).
- Render a quick check before publishing: headless Chrome at 1280 wide, and a 390px-wide
  `<iframe>` wrapper for mobile (Chrome enforces a ~500px minimum window, so a bare
  `--window-size=390` screenshot is NOT a phone-width render).
