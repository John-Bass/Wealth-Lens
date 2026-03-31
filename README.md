# WealthLens

**A personal finance dashboard that runs entirely in your browser.**

No server. No database. No account required with any third party. Your financial data stays on your device, encrypted in localStorage.

[**Launch WealthLens**](https://john-bass.github.io/Wealth-Lens/)

---

## What It Does

WealthLens gives you a clear picture of your net worth, spending, and financial trajectory — all from a single HTML file.

**Dashboard** — Net worth chart with 9 time ranges, summary cards (assets, liabilities, NW, account count), budget bar with savings rate, balance projection table with sliders, and inline-editable account rows.

**Accounts** — Card-based management with editable balance, APY, and monthly contribution fields. Full balance history with date/value/comment columns. Drag-and-drop reorder.

**Tools** — Retirement calculator with annual raise support, debt payoff simulator, Roth vs Traditional comparison, Wealth Multiplier (Money Guy method), and a 9-step Financial Order of Operations checklist.

---

## Key Features

| Feature | Details |
|---------|---------|
| **Zero Dependencies** | Single HTML file. Chart.js + Google Fonts via CDN. No build tools. |
| **Multi-User** | Each user gets isolated data. Create accounts with security questions. |
| **6 Themes** | Kyoto Dawn/Dusk, Tokyo Dawn/Dusk, Osaka Dawn/Dusk |
| **Encrypted Storage** | XOR encryption with double-hashed password-derived keys. SHA-256 password hashing. |
| **QR Sync** | Field-level diff sync via QR code. Scan to transfer changes between devices. |
| **Offline Capable** | Works without internet after first load. All computation is client-side. |
| **Mobile Optimized** | Responsive layout, touch targets, iOS Safari compatible, Settings FAB. |
| **Animations** | Subtle entrance animations, hover effects, and micro-interactions throughout. |

---

## Security Model

All data is encrypted at rest in the browser's localStorage:

- **Passwords**: SHA-256 hashed, salted with username
- **Financial data**: XOR encrypted with a key derived from double-hashing the password
- **Key separation**: The stored password hash cannot be used to decrypt data (different derivation path)
- **Memory clearing**: All in-memory data (accounts, budget, profiles) wiped on logout
- **Remember Me**: Credentials encrypted with XOR, keyed to username
- **QR sync**: Data encoded in URL hash fragment (never sent to any server)

No data ever leaves your browser. The GitHub Pages server only serves the static HTML file.

---

## Themes

Themes are named after Japanese cities, with Dawn (light) and Dusk (dark) variants:

| Theme | Vibe |
|-------|------|
| **Kyoto Dawn** | Warm cream, emerald green — serene and organic (default) |
| **Kyoto Dusk** | Warm dark tones, emerald accents — evening calm |
| **Tokyo Dawn** | Off-white canvas, gold accents — refined and executive |
| **Tokyo Dusk** | Near-black, gold — Bloomberg terminal premium |
| **Osaka Dawn** | Lavender, indigo accent — modern and clean |
| **Osaka Dusk** | Deep purple, glassmorphism, backdrop blur — neon nights |

On mobile, themes are accessible via the Settings button (bottom-right FAB).

---

## Tech Stack

- **HTML/CSS/JS** — Single file, no frameworks
- **Chart.js 4.4.7** — Line charts via CDN
- **Web Crypto API** — SHA-256 password hashing (built-in, no library)
- **qrcodejs** — Client-side QR code generation via CDN
- **Google Fonts** — DM Sans + Manrope
- **GitHub Pages** — Static hosting

---

## Author

**John Bass** (AI Assisted)

---

## Changelog

### v0.8.2 — 2026-03-30
**Final Audit + Cleanup**
- Fix settings FAB display conflict (inline style vs media query)
- Remove dead quick-edit code (4 unused functions, 4 unused CSS classes)
- Remove unused `quickEditId` variable
- Full browser test suite: 10/10 passed

### v0.8.1 — 2026-03-30
**Mobile Settings FAB**
- Replace mobile Update FAB with larger Settings button (gear icon)
- Settings modal with 2x3 theme button grid + Sync access
- Hide theme dropdown from navbar on mobile (moved to Settings)
- Show "Net Worth" label above value on mobile navbar

### v0.8.0 — 2026-03-30
**Security Hardening**
- SHA-256 password hashing via Web Crypto API (salted with username)
- XOR encryption for all financial data in localStorage
- Double-hash key derivation (stored hash cannot decrypt data)
- Encrypt Remember Me credentials
- Encrypt sync base snapshots
- Clear all in-memory data on logout
- Auto-migrate plain-text passwords and unencrypted data on login
- Penetration tested: brute force, cross-user, tampering, key separation, memory leak

### v0.7.2 — 2026-03-30
**Theme Picker Centering**
- Center theme picker on mobile with margin auto

### v0.7.1 — 2026-03-30
**Always-Visible Update Button**
- Remove visibility toggling from Update button

### v0.7.0 — 2026-03-30
**Code Cleanup**
- Remove dead `--page-bg` CSS variable and `theme-bento` class
- Add missing `markModified()` to drag-reorder, FOO toggle, profile deletes
- Extract `sortHistAndUpdateBal()` helper (3x duplicate → 1 function)
- Standardize modal close patterns

### v0.6.1 — 2026-03-30
**History Delete + Theme Centering**
- Add delete button (X) to each history entry row
- Confirm dialog before deletion, balance auto-updates

### v0.6.0 — 2026-03-30
**Animations & Micro-Interactions**
- Login card fade-slide-up, modal scale-in, tab content fade
- Summary card staggered entrance, NW value pop on load
- Hover effects on budget items, projection rows, chart panels, account cards
- Range slider thumb scale + glow, projection table horizontal scroll on mobile

### v0.5.2 — 2026-03-30
**Mobile 375px Fix**
- Hide NW label and username badge on mobile for narrow screens
- Reduce tab font and padding, constrain theme dropdown width

### v0.5.1 — 2026-03-30
**QR Fix + Theme Naming**
- Switch from qrcode (404) to qrcodejs@1.0.0 CDN
- Rename themes: Kyoto/Tokyo/Osaka Dawn/Dusk

### v0.5.0 — 2026-03-30
**Theme Overhaul**
- Replace 6 old themes with 3 concepts x light/dark
- Replace color picker with theme dropdown selector
- Default: Kyoto Dawn. Mobile: Kyoto Dawn/Dusk only in dropdown
- Floating Update FAB on mobile, golden savings rate color

### v0.4.0 — 2026-03-30
**Navbar Refinement**
- NW and user/Sign Out on same row as logo (2-row mobile navbar)
- Bumped text sizes for NW value, labels, badges

### v0.3.1 — 2026-03-30
**Sync Info Tooltip**
- Info panel in sync modal explaining QR sync and privacy

### v0.3.0 — 2026-03-30
**Field-Level Diff Sync via QR Code**
- Snapshot-based diff tracking for sync
- QR code generation with compressed diff payload (<2KB)
- Fullscreen QR overlay for easy scanning
- Handles both diff and legacy full-sync formats

### v0.2.0 — 2026-03-30
**Mobile Navbar + Cache Busting**
- Reorder mobile navbar rows, position Update button
- Share Link for cross-device sync via compressed URL hash
- Cache-busting meta tags + APP_VERSION auto-reload
- Delete README.md that was blocking GitHub Pages

### v0.1.0 — 2026-03-30
**Initial Release**
- Dashboard with summary cards, chart, account listings, balance projection
- Accounts tab with card management, editable history, drag-and-drop
- Tools: retirement calculator, debt payoff, Roth vs Traditional, Wealth Multiplier, FOO checklist
- Multi-user auth with security questions, Remember Me
- JSON export/import, email sync
- 6 original themes, background color picker
- iOS compatibility, PWA support
