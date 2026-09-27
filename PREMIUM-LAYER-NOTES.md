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

## 4) Client-polish pass (this session)
- **Fixed a CSS bug** in `docs/css/wow-premium.css`: two `transition` rules
  (`.kpi-card, .card` and `.role-card`) had a stray extra `)` after
  `var(--ease-smooth)`, which made the whole `box-shadow` transition
  declaration invalid and silently dropped by the browser. Removed the
  extra paren in both places — hover shadow transitions on cards now
  actually animate instead of snapping.
- **Home hero now tells the delivery story explicitly**, not just via
  object scale/opacity. Added, inside `index.html`'s existing hero
  `<style>`/`<script>` (no shared files touched, same pattern as the
  original hero):
  - A thin SVG route line with a start node, an end node, and a
    traveling dot. The dot's position is driven by the *same* scroll
    progress value as everything else — no independent animation, so
    "vehicle position = route progress" holds literally.
  - A small uppercase state label (`Planned → In transit → Approaching →
    Delivered`) that swaps as the user scrolls/scrubs, mirroring the
    IN TRANSIT → ARRIVED → DELIVERED transformation the brief asks for,
    using Waypoint's existing brand-gold color and type scale only.
  - End node gets a `.on` state (brand-gold ring) once the dot arrives,
    giving a visible "delivery confirmed" beat without a giant animation.
  - Everything fades in/out on the same easing curve as the existing
    object/copy, and is fully hidden under `prefers-reduced-motion`
    (existing fallback rule extended to cover the new elements).
- **Live Operations: vehicle marker on the existing progress bar.**
  Rows with status "In Transit" now show a small glowing dot riding at
  the bar's current `%` — the literal Uber principle (map → route →
  vehicle → destination → status) applied to the one page that's
  already a live-ops table, using the existing `.progress` component
  unchanged (marker is a small additive absolutely-positioned span, no
  markup restructuring, respects `prefers-reduced-motion`).

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
