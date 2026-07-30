# VALYRIFY — Property Intelligence Platform

Static site, no build step required. Two pages:

- `index.html` — the platform itself: Dashboard, Properties, ROI Calculator, and
  Admin are tabs directly in the top nav. This is the whole product experience
  in one page, GBP/UK data throughout.
- `roadmap.html` — dedicated Future Roadmap page, every upcoming feature
  grouped by quarter.

`app.html` still exists as a redirect stub (in case any old links or bookmarks
point to it) — it forwards straight to `index.html`, preserving any `#hash` or
`?query` on the URL.

All data is sample UK property data held in memory in the browser — it resets
on page refresh. There is no backend, database, or real AI call behind any of
it, by design (per the Vision Demo proposal).

The "Login / Signup" button in the nav opens the sign-in modal (choose Viewer
or Admin to preview role-based access). Linking to `index.html?login=1` opens
that modal automatically on load.

The ROI Calculator includes a live "How this is calculated" breakdown — every
formula (mortgage payment, cash flow, cash-on-cash ROI, cap rate, payback
period, 5-year value) is shown with the actual numbers plugged in, and updates
as you change any input.

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

## Structure notes

- Tabs are just `<section class="view">` blocks toggled by JS (`switchView()`
  in `index.html`) — no routing library, no build step.
- `#dashboard`, `#properties`, `#roi`, `#admin` in the URL hash open the
  matching tab on load (used by `roadmap.html`'s nav links back into the app).
- `vercel.json` has `cleanUrls: true`, so `index.html` is also reachable at
  the bare domain root, and `roadmap.html` at `/roadmap`.
