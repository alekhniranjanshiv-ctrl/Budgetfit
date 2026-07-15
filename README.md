# BudgetFit

**Budget-fit home theater quotation and room-plan engine**, built for Alekh Niranjan (AV systems integration, Nagpur). Single self-contained HTML file — no build step, no backend, no server. Enter a client's budget, get a fully speced, priced, GST-compliant quotation and a professional 2D room plan in seconds.

Everything runs entirely in the browser. Your price list, quotes, and settings are stored locally on your device — nothing is uploaded anywhere.

---

## Quick start

**Option A — just open it.** Double-click `BudgetFit.html`. Works fully offline after the first load (fonts/PDF/Excel libraries are cached by the browser).

**Option B — host it on GitHub Pages** (recommended if you want a stable URL you can open from any device, or install as an app):

1. Create a new GitHub repository and upload `BudgetFit.html`, `index.html`, and `icon.svg` to the root.
2. Go to **Settings → Pages**, set Source to the `main` branch, root folder.
3. GitHub gives you a URL like `https://yourusername.github.io/your-repo/` — `index.html` auto-loads there and instantly forwards to `BudgetFit.html`, so the clean root URL still works.
4. Open it in Chrome → address bar → **Install BudgetFit**. It installs as a standalone app with its own window and icon, separate from a browser tab, and launches straight into `BudgetFit.html` (skipping the redirect).

No build tools, no `npm install`, nothing to compile. It's one app file.

---

## What it does

**Quotation engine** — type a budget and channel configuration (5.1 through 9.1.4), and a hill-climbing allocator picks one product per category to land as close to that number as possible, respecting your category weights, brand preferences, and technical constraints (an AVR is never picked with fewer channels than the system needs, for example).

**Room Plan** — a professional, architect-style 2D drawing generated directly from the live quote: wall-snapped speaker positions, dimension lines in feet-inches, a title block, north arrow, cable runs, and a full placement schedule with the practical on-site measurements (speaker-to-speaker separation, distance from walls). Acoustic-transparent screens automatically reposition front L/C/R behind the screen; in-ceiling speakers draw on the ceiling, not the wall.

**Quotation PDF** — a polished, GST-itemized PDF with company branding. Optionally adds two more pages: the room plan drawing, and a dedicated speaker-position reference sheet in plain English, ready to hand to an installation crew.

**Price list** — add products manually or bulk-import via Excel. Supports real technical attributes per category: AVR channel count, screen size/frame type/acoustic transparency, projector resolution/light source, speaker mounting (standmount/in-wall/in-ceiling), and a free-form technical specifications field that prints on the quotation.

**Selection preferences** — filter what the engine is allowed to pick: preferred brand (per category or "match all speakers to one brand"), projector resolution/light source, screen size/frame/material, and a one-tap "Architectural" speaker style for in-wall/in-ceiling builds.

**Business logic** — GST handling (always treated as inclusive), an Installation % that can work backward from an all-inclusive client number, a minimum design/installation charge floor, discount that applies to equipment only (never your labour), and 1–4 subwoofer support with sensible corner/wall placement.

**Dashboard** — confirmed quotes, monthly totals, pipeline value, JSON export/import and Excel export/import for full data portability.

---

## Data & privacy

Everything — your price list, confirmed quotes, company settings, preferences — lives in the browser's `localStorage`, scoped to whatever URL you're opening the file from. That means:

- If you open it as a local file, data stays on that device, in that browser.
- If you host it on GitHub Pages, data is tied to that URL, shared across any device where you open that URL in the same browser.
- Clearing browser data / site data for that origin will erase it. **Export your price list (Excel) and confirmed quotes (JSON) periodically as backups** — buttons for both are on the Dashboard and Price List tabs.
- Nothing is sent to any server. The only network calls are to load Google Fonts and the jsPDF/SheetJS libraries from a CDN on first load, and those are unrelated to your data.

---

## File structure

```
BudgetFit.html   — the entire app (HTML, CSS, JS, all in one file) — this is the file you edit/update
index.html       — a tiny redirect to BudgetFit.html, so GitHub Pages' root URL still works
icon.svg         — app icon (used for the browser tab, PWA install, and home-screen icon)
README.md        — this file
```

`BudgetFit.html` is clearly named on purpose — so it's never confused with the generic `index.html` you'll have in other projects. When you get an updated version of the app, just replace `BudgetFit.html` and leave `index.html`/`icon.svg` alone.

`icon.svg` isn't strictly required for the app to run — the icon is also embedded inside `BudgetFit.html` itself — but it's included as a standalone file in case you want to reuse it elsewhere (a favicon on another page, printed materials, etc.).

---

## Price list Excel format

Import/export uses these columns (only `category`, `brand`, `model`, `price` are required — everything else is optional):

| Column | Notes |
|---|---|
| `category` | must match an existing category id (e.g. `avr`, `fronts`, `screen`, `projector`) |
| `brand`, `model`, `price`, `qty` | qty = units per system, e.g. 2 if a front speaker is priced per piece, 1 if priced per pair |
| `channels` | AVR only — amplified channel count |
| `screentype`, `acoustictransparent`, `screensize` | Screen only |
| `resolution`, `lightsource` | Projector only (`HD`/`4K`, `Lamp`/`Laser`) |
| `mounttype` | Fronts/Center/Surrounds only (`standmount`/`inwall`/`inceiling`) |
| `specs` | Free-form technical specs, pipe-separated, e.g. `Power: 130W \| THX Certified: Yes` |

Re-importing a brand+model that already exists updates its price/qty in place rather than duplicating it.

---

## Browser support

Built and tested for current Chrome/Edge (desktop and mobile). Uses standard HTML5/CSS/ES6 — no framework, no transpiler — so it should work in any modern evergreen browser, though PDF/Excel export depend on the CDN-hosted jsPDF and SheetJS libraries loading successfully, which needs an internet connection at least once.

---

## Support

This is a bespoke internal tool. There's no issue tracker or public support channel — if something breaks or you want a feature, that request goes back through whoever built it with you.
