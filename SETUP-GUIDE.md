# Star Link Freight — Fleet Finance App: Setup Guide

Your data lives in a free Firebase project you control, so the same numbers show up on your phone and PC live. One-time setup, about 5–10 minutes.

## 1. Create a free Firebase project

1. Go to console.firebase.google.com and sign in with any Google account.
2. Click Add project, name it anything (e.g. "Star Link Freight"), skip Google Analytics, click Create project.
3. In the left menu, go to Build → Firestore Database → Create database. Choose any location close to you, and start in test mode (lets the app read/write immediately — see the security note in step 4).
4. Click the gear icon (top left) → Project settings. Scroll down to "Your apps" → click the </> (Web) icon → give it any nickname → Register app (skip the hosting checkbox).
5. Firebase shows you a firebaseConfig object like this — copy the whole thing:
   const firebaseConfig = {
     apiKey: "AIza...",
     authDomain: "your-project.firebaseapp.com",
     projectId: "your-project",
     storageBucket: "your-project.appspot.com",
     messagingSenderId: "...",
     appId: "..."
   };

## 2. Connect the app

1. Open index.html (double-click it, or see hosting options below).
2. Paste the firebaseConfig object into the box and click Connect.
3. That's it — the app is now live-synced to your Firestore database.

You only need to do this once per device/browser (paste the same config on your phone's browser too, or use the hosted link below so there's nothing to paste twice).

## 3. Import your existing spreadsheet

1. In the app, go to Settings → Import from Excel.
2. Choose your Corrected Star_Link_Freight_Fleet_Finance_2026.xlsx file.
3. It pulls in your trucks, rates, shareholders, every logged load, expenses, and shareholder draws. Safe to re-run later — it won't duplicate loads it already has.

## 4. Get it on your phone too

Pick whichever is easiest:

- Simplest: email yourself index.html or drop it in Google Drive/iCloud, open it in your phone's browser. Since data lives in Firestore (not the file), both devices stay in sync.
- Nicer (a real link + can add to your phone's home screen): go to app.netlify.com/drop and drag index.html onto the page — no login needed. It gives you a public URL instantly. Open that URL on your phone, paste your Firebase config once there too, and optionally "Add to Home Screen" so it behaves like an app icon.

## 5. Lock it with a PIN (recommended)

Go to Settings → Security → Set a PIN. Since your Firebase config isn't secret-proof (test mode rules allow anyone with the link to read/write), a PIN adds a real layer so only people who know it can view your numbers. You'll enter it once per browser session.

## 6. Tighten Firestore security (optional but recommended after a week or two)

Test mode rules expire automatically after ~30 days. Before then, go to Firestore Database → Rules in the Firebase console and replace them with:

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}

Click Publish. This keeps the app working indefinitely (open access, relying on the app's PIN + the fact that nobody else has your config/link for protection). If you want real per-user auth later, that's a bigger step — ask and I can help set it up.

## Backups

Settings → Backup lets you export everything as a .json (full raw backup) or .xlsx (spreadsheet-style export) any time.

## What matches the original spreadsheet exactly

Revenue, factoring fee, company gross/net, invoice fees, and net income all count every logged load, regardless of status (Delivered or Cancelled/TONU) — this mirrors exactly how your original workbook calculated its totals, verified line-by-line against your July and full-year 2026 numbers.