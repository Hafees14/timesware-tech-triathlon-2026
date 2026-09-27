# Timesware — Tech-Triathlon 2026

Team Timesware's submission for Tech-Triathlon 2026: a delivery planning system for **Waypoint Group**, a fictional retailer running three brands (Fresh, Style, Tech) across 120 outlets and 60 vehicles from two depots.

The competition runs in three phases, all scored independently.

## Designathon
UX design for the four roles who touch the delivery workflow: dispatcher, loader, driver, store manager.

- [Design document](designathon/Timesware_Designathon.md) — personas, screen flows with rationale, degradation scenario, booklet compliance check
- [Live prototype](https://hafees14.github.io/timesware-tech-triathlon-2026/)

## Hackathon
Working implementation of the design above. Not started yet.

## Datathon
Three ML/analytics tasks: service-time and lateness prediction, demand forecasting, and peak-day fleet allocation (feasibility-checked with `check_allocation.py`). Not started yet.

## Team
Timesware

## UI/UX transformation pass (design-system layer)

Applied a first transformation pass toward the "operational editorial" visual identity brief:

- **Color system**: introduced a cold-chain ice/cyan accent (`--c-accent`) as the primary operational color for buttons, focus states, sidebar active states, and progress bars — replacing the previous default-everywhere amber. Amber (`--c-brand`) is now reserved for warning/exception tones only, per the brief.
- **Typography**: added Fragment Mono alongside Space Grotesk + Inter for metrics/telemetry/timestamps (`--f-mono`).
- **Route + movement signature**: added a reusable `route-svg` / `route-strip` component (the `●━━━━━━●` motif) with a self-drawing SVG stroke animation (`prefers-reduced-motion`-aware), used on the landing hub hero.
- **Live system feel**: added a `WOW.syncTicker()` helper ("SYNCED Ns AGO" → "SYNCED JUST NOW") wired into Live Operations.
- Existing KPI count-up, reveal, tilt, and magnetic-button interactions (already present in `wow.js`) now inherit the new palette automatically since all components consume shared CSS custom properties.

**Not yet done in this pass** (flagged honestly, not hidden): per-page layout rework beyond the dashboard/live-ops/hub (asymmetric layouts, oversized editorial metrics), the SVG route-draw + moving-vehicle interaction on the Live Operations map itself, the commit-plan transition sequence, and the command palette (Ctrl/Cmd+K). The design-system layer (tokens + components) was prioritized first since every page inherits it; remaining work is page-by-page application of that system.
