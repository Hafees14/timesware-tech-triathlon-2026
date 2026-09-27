# Waypoint — Integration Notes

## 1) Premium interaction layer (all 16 pages)
`docs/css/wow-premium.css` + `docs/js/wow-premium.js` are linked on every page,
each with a small page-appropriate init block. No existing colors, fonts,
layout, or component markup were changed.

## 2) Home page — centered scroll hero (index.html only)
Added directly inside `index.html`'s own `<style>`/`<script>` blocks — no shared
CSS/JS files were touched for this:
- A new `.wp-hero` section (180vh) sits above the existing hub card. Its inner
  stage is `position: sticky`, so as the user scrolls through it the Waypoint
  "W" mark scales/rotates/translates in, holds center with the wordmark
  crossfading in (translate + scale, not a plain fade), then scales out to
  release into the unchanged hub/role-grid below.
- Progress is computed directly from `scrollY` every frame and smoothed with a
  light lerp (0.18) for inertia — fast scrolls catch up quickly, slow scrolls
  stay glued, and the whole sequence resolves in well under one extra screen
  of scrolling.
- A small cursor-proximity offset (peaks mid-sequence, off at the ends) nudges
  the object a few pixels — magnetic, not a hover-card effect.
- `prefers-reduced-motion` gets a static CSS fallback (everything visible,
  no transforms).
- Existing background pseudo-elements and the network canvas were switched
  from `position:absolute` to `position:fixed` (same visuals, now anchored to
  the viewport instead of stretching across the taller, scrollable page).

## 3) Home navigation on every page
- Dispatcher pages (Overview, Planning, Live Operations, Deferrals, Capacity —
  all rendered by the shared `docs/js/app.js` shell): added a "Home" item at
  the top of the sidebar, and the sidebar's Waypoint mark/wordmark now links
  to `index.html`.
- Driver pages (phone frames): added a small Home icon next to the existing
  avatar / back-link in the top bar.
- Loader pages (tablet frames): the "Waypoint · Loader" wordmark now links to
  `index.html`; added a small Home icon next to the avatar.
- Store pages (5): the "Waypoint · Store" wordmark now links to `index.html`;
  added a small Home icon next to the outlet chip.
- All links are relative (`index.html`, same folder) — no path changes needed
  for GitHub Pages.

## Push to GitHub

```bash
cd timesware-tech-triathlon-2026
git init
git add .
git commit -m "Add premium interaction layer, home hero, and site-wide Home navigation"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

`docs/.nojekyll` is already present for GitHub Pages served from `docs/`.
