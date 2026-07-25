# VALYRIFY Vision Demo — Site

Static site, no build step required. Two pages so far:

- `index.html` — the landing page / vision overview (Prototype 1)
- `app.html` — the interactive product demo: Dashboard, Properties, ROI Calculator, Admin (Prototype 2)

They're linked together: "Enter the Demo" and each module row on the landing
page jump straight into the matching tab in `app.html` (e.g. `app.html#roi`).
The app's logo and "← Overview" link go back to `index.html`.

All data is sample data held in memory in the browser — it resets on page
refresh. There is no backend, database, or real AI call behind any of it,
by design (per the Vision Demo proposal).

## Deploy on Vercel

**Option A — Vercel dashboard (no CLI, easiest):**
1. Go to vercel.com → Add New → Project
2. Choose "Deploy without Git" / drag-and-drop, and drop this whole folder in
   (or zip and upload it)
3. Framework preset: "Other" — no build command, no output directory needed
4. Deploy. You'll get a live `.vercel.app` URL immediately.

**Option B — GitHub + Vercel (recommended if you'll keep iterating):**
1. Push this folder to a new GitHub repo
2. In Vercel: Add New → Project → Import the repo
3. Framework preset: "Other" (static site) — leave build settings blank
4. Deploy. Every future `git push` auto-deploys a new preview/production URL.

**Option C — Vercel CLI:**
```
npm i -g vercel
cd valyrify-site
vercel
```
Follow the prompts (link or create a project), then `vercel --prod` to push
to production.

## Adding the next prototype

Each new module can be its own HTML file at the root (self-contained, like
`app.html` — inline CSS/JS, Google Fonts + Chart.js via CDN, no build step).

To wire a new prototype in:
1. Add the file, e.g. `roadmap-full.html`
2. Add/point a nav link or module row in `index.html` (or a tab in `app.html`)
   to it, same pattern as the existing `app.html#dashboard` links
3. Redeploy (push to GitHub, or re-drag the folder / re-run `vercel --prod`)

`vercel.json` has `cleanUrls: true`, so once deployed, `app.html` is also
reachable at `/app` (no extension needed) — keep that in mind when linking.
