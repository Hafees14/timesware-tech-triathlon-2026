# Premium Interaction Layer — Integration Notes

This repo is your original Waypoint site with one addition: a premium interaction
layer (cursor tracking, scroll reveals, card elevation, sticky topbar, click
expansion) wired into **all 16 pages** under `docs/`.

Nothing about the existing design was changed:
- Colors, typography, layout, and component markup are untouched.
- `docs/css/tokens.css`, `layout.css`, `components.css`, `wow.css` — unchanged.
- `docs/js/app.js`, `data.js`, `wow.js` — unchanged.

What was added:
- `docs/css/wow-premium.css` and `docs/js/wow-premium.js` — the interaction engine.
- One `<link>` to `wow-premium.css` before `</head>` on every page.
- One `<script>` to `wow-premium.js` before `</body>` on every page, followed by a
  small inline init block tailored to that page's role (hub / dispatcher /
  operational), so no manual setup or console command is needed after deploy.

## Push to GitHub

```bash
cd timesware-tech-triathlon-2026
git init
git add .
git commit -m "Add premium interaction layer to all pages"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

If this is a GitHub Pages site served from `docs/`, no further config is needed —
`docs/.nojekyll` is already present.
