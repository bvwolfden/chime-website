# Clann Website (prvail.ai)

Static marketing site for **Clann** — the family location + parental-controls app.
Hosted on **GitHub Pages** at **https://prvail.ai**.

## Files

- **index.html** — Landing page (Clann brand: sage/green, warm cream, Fraunces + Inter)
- **privacy.html** — Privacy Policy (location + parental-controls + backend; required for App Store)
- **support.html** — Support / FAQ
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

## Screenshots (swap-in)

The landing page's "Take a closer look" section uses styled placeholder phone
frames. To use real screenshots:

1. Save portrait iPhone screenshots (~1170×2532) as
   `assets/screenshots/1.png`, `2.png`, `3.png`.
2. In `index.html`, find the `<div class="shots">` block, **uncomment** the
   `<img …>` line in each frame, and delete the `.placeholder` block.

The hero device is a stylized (CSS/SVG) mock — you can also swap that for a real
screenshot later.

## Before going live — TODO

- **App Store URL:** every download button links to a placeholder
  `https://apps.apple.com/us/app/clann`. Search `TODO` in `index.html` and
  replace with the real listing URL once the app is published.
- **Privacy Policy review:** `privacy.html` is written to accurately reflect what
  Clann collects (location, screen-time, device, diagnostics) and is issued under
  Brian Vukmir (sole proprietor, US). Have it reviewed before relying on it
  legally; update the entity/jurisdiction if that changes.

## URLs

- Homepage: https://prvail.ai
- Privacy: https://prvail.ai/privacy.html
- Support: https://prvail.ai/support.html

## Notes

- Pure static HTML/CSS, no build step. Fonts load from Google Fonts.
- Contact email: **support@prvail.ai** (ensure forwarding is set up).
