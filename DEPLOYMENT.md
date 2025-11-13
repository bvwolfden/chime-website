# Deployment Instructions

## Step 1: Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: **chime-website** (or any name)
3. Description: "Chime app website"
4. **Make it PUBLIC** ✅ (required for free GitHub Pages)
5. **Don't** initialize with README (we already have one)
6. Click **Create repository**

## Step 2: Push to GitHub

Copy your repository URL from GitHub, then run:

```bash
cd /Users/brian_vukmir/dev/chime-website

# Add your GitHub remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/chime-website.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## Step 3: Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** → **/ (root)** folder
4. Click **Save**

Wait 1-2 minutes, then you'll see: "Your site is live at..."

## Step 4: Configure Custom Domain

Still in Settings → Pages:

1. Under **Custom domain**, type: `prvail.ai`
2. Click **Save**
3. Wait for DNS check
4. Check **Enforce HTTPS** (after DNS propagates)

## Step 5: Update GoDaddy DNS

Log in to GoDaddy and manage DNS for prvail.ai:

### Add 4 A Records:

```
Type: A, Name: @, Value: 185.199.108.153, TTL: 600
Type: A, Name: @, Value: 185.199.109.153, TTL: 600
Type: A, Name: @, Value: 185.199.110.153, TTL: 600
Type: A, Name: @, Value: 185.199.111.153, TTL: 600
```

### Add CNAME for www:

```
Type: CNAME, Name: www, Value: YOUR_USERNAME.github.io, TTL: 600
```

### Remove any existing A or CNAME records for @

(Keep MX records for email if you have them)

## Step 6: Wait & Test

- DNS propagation: 10-60 minutes
- Test: https://prvail.ai
- Test: https://prvail.ai/privacy
- Test: https://prvail.ai/support

## Done! ✅

Your website will be live at https://prvail.ai

## Updating Your Website

To make changes:

```bash
cd /Users/brian_vukmir/dev/chime-website

# Edit HTML files
# Then:

git add .
git commit -m "Update content"
git push

# Live in 1-2 minutes!
```

## Troubleshooting

- **DNS not working?** Wait longer (up to 48 hours max)
- **Check DNS:** https://www.whatsmydns.net/#A/prvail.ai
- **HTTPS error?** Disable and re-enable "Enforce HTTPS" in GitHub Pages settings

## App Store Connect URLs

Use these URLs in your App Store listing:

- **Privacy Policy:** `https://prvail.ai/privacy`
- **Marketing URL:** `https://prvail.ai`
- **Support URL:** `https://prvail.ai/support`

