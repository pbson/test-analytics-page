# Cardamon Optimisation Progress

**Last Updated:** 2026-04-13

## Completed Tasks

### ✅ Task 1: Repository Discovery
- Full codebase scan completed (updated 2026-04-13)
- Found massive number of unused libraries not identified in first scan
- See `discovery.md` for full analysis

## In Progress / Created PRs

### 🔧 Task 2: Network Transfer - Remove Unused Dependencies
- **PR Created**: "Remove unused external dependencies to reduce network transfer"
- **Branch**: cardamon/remove-unused-dependencies
- **Status**: Awaiting merge

**What was removed:**
- 3 unused font families: Roboto, Playfair Display, Source Code Pro
- Duplicate Inter font import
- Redundant @import inside <style>
- Inter weight optimised from 7 weights (300-900) to 5 (400,600,700,800,900)
- CSS: Animate.css, Bootstrap CSS, Material Design Icons (all pages)
- CSS: Font Awesome (about.html, blog.html only - kept on index.html)
- CSS: highlight.js github-dark (blog.html)
- JS: jQuery, D3.js, Plotly.js, Bootstrap bundle JS, GSAP (all pages)
- JS: GSAP ScrollTrigger (index.html)
- JS: Three.js (about.html)
- JS: marked.js, highlight.js, Chart.js (blog.html)

**Estimated savings (gzip estimates):**
- Plotly.js: ~600KB × 3 pages = ~1.8MB
- D3.js: ~100KB × 3 = ~300KB
- Material Design Icons CSS: ~180KB × 3 = ~540KB
- Three.js: ~165KB × 1 (about)
- Font Awesome: ~60KB × 2 (about, blog)
- Bootstrap CSS: ~25KB × 3 = ~75KB
- Bootstrap JS: ~25KB × 3 = ~75KB
- GSAP: ~30KB × 3 = ~90KB
- marked + hljs + Chart.js: ~80KB × 1 (blog)
- Fonts (unused families + duplicate): ~20KB × 3 = ~60KB
- **Total: ~3.5MB+ across all 3 pages combined**

## Remaining High-Impact Tasks

### 🔴 Task 3: Frontend CPU Reduction (HIGH PRIORITY after PR merge)
- **about.html**: Matrix rain canvas running at 30fps (setInterval 33ms) - biggest issue
- **index.html**: setInterval 100ms calling getBoundingClientRect on all cards
- **index.html**: setInterval 2000ms calling getComputedStyle on ALL DOM elements
- **blog.html**: setInterval 1000ms focus log
- None of these intervals serve any user-facing purpose
- Estimated: significant CPU reduction during 10s Cardamon measurement window

### 🟡 Task 5: Caching Headers
- Nginx config has gzip but no explicit cache headers visible
- Could add Cache-Control for static assets

## Notes
- Sites loaded in dark theme (low brightness = natural lower screen energy)
- All images use loading="lazy" (good)
- prefers-reduced-motion already implemented on all pages
