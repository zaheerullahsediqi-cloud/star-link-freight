# Star Link Freight — Fleet Finance

A single-file web app that replaces the "Corrected Star_Link_Freight_Fleet_Finance_2026.xlsx"
spreadsheet: per-truck load logs, expenses, shareholder draws, and a dashboard with revenue
and profit rollups. Works on desktop and phone browsers, syncs live between devices.

## Stack

- Plain HTML/CSS/JS — no framework, no build step (`index.html` is the entire app).
- Firebase Firestore (loaded via CDN, compat SDK) as the data backend, so the same data shows up on every device.
- SheetJS (via CDN) for one-click Excel import/export.

## Local development

There's nothing to build. Open `index.html` directly in a browser, or serve the folder with any static file server, e.g. `npx serve .`

## Deploying (GitHub + Vercel)

git init && git add . && git commit -m "Initial commit" && git branch -M main && git remote add origin https://github.com/zaheerullahsediqi-cloud/star-link-freight.git && git push -u origin main

Then in the Vercel dashboard: Add New → Project → Import the GitHub repo. No build command or output directory needed.

## First-run setup

See SETUP-GUIDE.md for connecting the app to a Firebase project, importing the existing spreadsheet, and setting a PIN.
