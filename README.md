# WealthLens PWA — Deployment Guide
**Author: John Bass (AI Assisted)**

---

## What This Is

This folder contains WealthLens packaged as a **Progressive Web App (PWA)**. When hosted on a web server, it:
- Installs on your iPhone/Android home screen like a native app
- Runs full-screen with no browser bar
- Works offline after first load
- Uses the same codebase — zero rewrites needed

---

## Quick Start — GitHub Pages (Free, 5 minutes)

### 1. Create a GitHub Account
Go to [github.com](https://github.com) and sign up (free).

### 2. Create a New Repository
- Click **"New repository"**
- Name it `wealthlens` (or anything you want)
- Set to **Public** (required for free GitHub Pages)
- Click **Create repository**

### 3. Upload Files
- Click **"uploading an existing file"**
- Drag ALL files from this folder:
  - `index.html`
  - `manifest.json`
  - `sw.js`
  - `icons/` folder (with all icon files)
- Click **Commit changes**

### 4. Enable GitHub Pages
- Go to **Settings** → **Pages**
- Under "Source", select **main** branch
- Click **Save**
- Wait 1-2 minutes

### 5. Your App is Live
- URL will be: `https://yourusername.github.io/wealthlens/`
- Open this URL on your phone in **Safari**
- Tap **Share** → **"Add to Home Screen"**
- You now have a WealthLens app icon — full screen, offline capable

---

## Alternative Hosting Options

| Service | Cost | Setup Time | URL |
|---------|------|-----------|-----|
| **GitHub Pages** | Free | 5 min | yourusername.github.io/wealthlens |
| **Netlify** | Free | 2 min | Drag folder to netlify.com/drop |
| **Vercel** | Free | 3 min | Import from GitHub |
| **Tiiny.host** | Free (7 days) | 30 sec | yourname.tiiny.site |
| **Cloudflare Pages** | Free | 5 min | yourproject.pages.dev |

**Netlify is the fastest:** Go to [app.netlify.com/drop](https://app.netlify.com/drop), drag the entire `pwa` folder onto the page, and you get a URL instantly.

---

## File Structure

```
pwa/
├── index.html              ← The full WealthLens app
├── manifest.json           ← PWA metadata (name, icons, colors)
├── sw.js                   ← Service worker (offline caching)
├── icons/
│   ├── icon-192.png        ← Android/PWA icon
│   ├── icon-512.png        ← Android/PWA splash
│   ├── icon-192.svg        ← Vector icon
│   ├── icon-512.svg        ← Vector icon
│   └── apple-touch-icon.png ← iOS home screen icon
└── README.md               ← This file
```

---

## Path to the Apple App Store

### Phase 1 — PWA (Current)
✅ Works on iOS home screen
✅ Full-screen, offline, app-like
✅ No Apple Developer account needed
❌ Not in App Store
❌ No push notifications on iOS

### Phase 2 — Capacitor Wrapper
When ready for the App Store, wrap the PWA in **Capacitor** (by Ionic):

```bash
npm install @capacitor/core @capacitor/cli
npx cap init WealthLens com.johnbass.wealthlens
npx cap add ios
# Copy index.html + assets into the www/ folder
npx cap sync
npx cap open ios    # Opens Xcode
```

**Requirements:**
- Mac with Xcode installed
- Apple Developer Account ($99/year)
- The Capacitor wrapper adds a native iOS shell around your existing HTML/JS

**What Capacitor gives you:**
- App Store distribution
- Push notifications
- Native file system access
- Face ID / Touch ID integration
- Haptic feedback
- Native share sheet

### Phase 3 — Native Features
As the app grows, Capacitor plugins add native capabilities:
- `@capacitor/local-notifications` — budget alerts
- `@capacitor/share` — native share sheet for export
- `@capacitor/biometrics` — Face ID login
- `@capacitor/filesystem` — direct file access
- `@capacitor/haptics` — tactile feedback on interactions

### Entities to Remove Before App Store
Before publishing, remove or replace:
- All third-party account names from seed data
- Chart.js CDN link (bundle locally instead)
- Google Fonts CDN link (bundle the font file)
- Any references to specific financial institutions

---

## Updating the App

1. Make changes to `WealthLens.html` (the main development file)
2. Copy the updated file into this folder as `index.html`
3. Push to GitHub / re-upload to your hosting provider
4. The service worker auto-updates on next visit

**Version bumping:** Change `CACHE_NAME` in `sw.js` from `'wealthlens-v1'` to `'wealthlens-v2'` etc. to force cache refresh on all devices.
