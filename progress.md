# Cardamon Optimisation Progress

**Last Updated:** 2026-04-14

## Completed Tasks

### ✅ Task 1: Repository Discovery
- Full codebase scan completed (updated 2026-04-13)
- See `discovery.md` for full analysis

## Created PRs

### 🔧 Task 2: Network Transfer - Remove Unused Dependencies
- **PR #12**: "Remove unused external dependencies to reduce network transfer"
- **Branch**: cardamon/remove-unused-dependencies-8ad77017f52973df
- **Status**: Open, awaiting merge
- **Savings**: ~3.5MB across all 3 pages combined

### 🔧 Task 3: Frontend CPU - Remove Unnecessary Timers
- **PR #16**: "Remove unnecessary CPU-intensive timers (Frontend CPU pillar)"
- **Branch**: cardamon/remove-unnecessary-timers-b956f771ade94fbf
- **Status**: Open, awaiting merge
- **Run**: 24371979945

### 🔧 Task 4: Screen Energy - prefers-reduced-motion CSS
- **PR**: Created in run 24384123711 (branch: cardamon/prefers-reduced-motion-wf24384123711)
- **Status**: Open, awaiting merge
- Added `@media (prefers-reduced-motion: reduce)` to index.html, about.html, blog.html
- Stops 19 infinite CSS animations across all 3 pages

### 🔧 Task 5: Server Config - Gzip Compression
- **PR**: Created in run 24384123711 (branch: cardamon/add-gzip-compression-wf24384123711)
- **Status**: Open, awaiting merge
- Added gzip to nginx.conf: on, comp_level 6, min_length 1024, vary on
- Estimated ~60-80% reduction in HTML transfer sizes (~66 KB per 3-page session)

### Other PRs (from other agents)
- **PR #14**: Cache-Control headers (from Daily Efficiency Improver) - Open

## Remaining Tasks

### None identified
All major Cardamon pillars have been addressed:
- Network Transfer: PR #12 (dependencies) + gzip PR
- Frontend CPU: PR #16 (timers)
- Screen Energy: prefers-reduced-motion PR
- Server Config: gzip PR + PR #14 (cache headers)

### Low priority remaining items (not worth separate PRs)
- mousemove handler in index.html (only fires on user action, not continuous)
- Click event logger in index.html (only fires on click, not continuous)
- Preload fetches in about.html and blog.html (one-time on load, not loops)
- Scroll event handlers (read-only, no layout writes)
