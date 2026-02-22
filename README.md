# VJ·POS — Viet Jewelers Point of Sale

Mobile-first POS web app for a jewelry business in Vietnam. Built as a single HTML file deployed via GitHub Pages.

**Live URL:** https://maipham1712-collab.github.io/VJ-Pos/

## Tech Stack

- **Frontend:** Single `index.html` — React 18 (CDN), vanilla CSS, no build step
- **Backend API:** Google Apps Script web app (REST endpoints)
- **Database:** Google Sheets (Products, Orders, Payments, Commission, etc.)
- **Hosting:** GitHub Pages (this repo)
- **Automation:** n8n self-hosted + Telegram bots

## How It Works

- `index.html` is the entire app — HTML + CSS + JS in one file
- React components are written with `createElement()` calls (no JSX, no build)
- On load, it fetches products/orders/staff from the Google Apps Script API
- Staff log in with a 4-digit PIN → validated against the Staff sheet
- Products tab → browse/search → tap to add to cart → Order tab → checkout
- Orders saved to Google Sheets via POST to the Apps Script endpoint

## API Endpoint

```
GET:  https://script.google.com/.../exec?action=products|staff|orders|login&pin=XXXX
POST: https://script.google.com/.../exec  (body: JSON with action field)
```

Actions: `submit_order`, `add_payment`, `void_order`, `bulk_import`

## Key Features

- PIN-based staff auth with role-based access (admin vs staff)
- Product catalog with images, categories, brand filters
- Cart with per-item and bill-level discounts (fixed or %)
- Card fee toggle (3%), shipping fee, order notes
- Draft orders — work on multiple orders simultaneously
- Order history with payment tracking (paid/partial/unpaid)
- Admin: bulk stock import, void orders
- Commission calculation per vendor type

## File Structure

```
index.html    ← Entire app (HTML + CSS + React JS)
README.md     ← This file
TODO.md       ← Current bugs and planned features
```

## Development

1. Edit `index.html` directly on GitHub or locally
2. Commit to `main` branch
3. GitHub Pages auto-deploys (may take 1-2 min)
4. Hard refresh on device to see changes (`?v=timestamp` if cached)

## Known Issue — Search Bar Not Sticky

See `TODO.md` for details. The search bar on the Products tab scrolls away with the product grid instead of staying pinned below the header. Multiple approaches tried (position:sticky, flex layout, position:fixed) — needs debugging on actual iPhone.
