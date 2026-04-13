# Cardamon Optimisation Progress

**Last Updated:** 2026-04-13

## Completed Tasks

### ✅ Task 1: Repository Discovery
- Full codebase scan completed (updated 2026-04-13)
- See `discovery.md` for full analysis

## Created PRs

### 🔧 Task 2: Network Transfer - Remove Unused Dependencies
- **PR #12**: "Remove unused external dependencies to reduce network transfer"
- **Branch**: cardamon/remove-unused-dependencies-8ad77017f52973df
- **Status**: Open, awaiting merge

**What was removed:**
- 3 unused font families: Roboto, Playfair Display, Source Code Pro
- Duplicate Inter font import + redundant @import
- Inter weight optimised from 7 weights to 5 (400,600,700,800,900)
- CSS: Animate.css, Bootstrap CSS, Material Design Icons (all pages)
- CSS: Font Awesome (about.html, blog.html only - kept on index.html)
- CSS: highlight.js github-dark (blog.html)
- JS: jQuery, D3.js, Plotly.js, Bootstrap bundle JS, GSAP (all pages)
- JS: GSAP ScrollTrigger (index.html)
- JS: Three.js (about.html)
- JS: marked.js, highlight.js, Chart.js (blog.html)
- **Estimated savings: ~3.5MB+ across all 3 pages combined**

### 🔧 Task 3: Frontend CPU - Remove Unnecessary Timers
- **PR Created**: "Remove unnecessary CPU-intensive timers"
- **Branch**: cardamon/remove-unnecessary-timers
- **Status**: Open, awaiting merge
- **Run**: 24371979945

**What was removed (index.html):**
- setInterval(100ms): getBoundingClientRect on all .feature-card elements
- setInterval(5000ms): fetch worldtimeapi.org external API
- setInterval(2000ms): getComputedStyle on ALL DOM elements

**What was removed (about.html):**
- setInterval(33ms) matrix rain → replaced with rAF capped at 30fps + visibility API + prefers-reduced-motion
- setInterval(10000ms): fetch GitHub API stars
- setInterval(3000ms): detect device capabilities loop

**What was removed (blog.html):**
- setInterval(1000ms): focus log recording
- setInterval(30000ms): fetch 3 RSS feeds
- setInterval(5000ms): update heading data-attributes

## Remaining Tasks

### 🟡 Task 5: Caching Headers
- PR #14 (from other agent) already open with Cache-Control headers in nginx.conf
- No need to duplicate this work

### Low priority remaining items
- Click event logger in index.html (addEventListener, only fires on user action)
- Preload fetches in about.html and blog.html (one-time, not loops)
