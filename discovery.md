# Cardamon Optimiser — Repository Discovery

## Website Structure
- **Type**: Static HTML website (3 pages: index, about, blog)
- **Framework**: Vanilla HTML/CSS/JavaScript with CDN-hosted libraries
- **Deployment**: Docker + Nginx (Alpine Linux)
- **Build System**: None (no build step required)

## Pages Measured by Cardamon
1. `/` → index.html (939 lines, 36KB)
2. `/about` → about.html (747 lines, 28KB)
3. `/blog` → blog.html (718 lines, 28KB)

## Critical Findings

### PILLAR 1: Frontend Device Energy — HIGH IMPACT
**Multiple `setInterval()` loops running continuously during 10-second measurement:**
- index.html: 4 active setInterval timers (including counter animation in tight loop)
- about.html: 2 active setInterval timers + 1 `setInterval(draw, 33)` rendering loop
- blog.html: 3 active setInterval timers
- These keep CPU actively busy for the entire 10-second Cardamon window
- **Estimated impact**: 40-60% of frontend CPU cost

**Animated background particles + grid animations:**
- CSS `animation: float-particle linear infinite` (particle system)
- CSS `animation: grid-move 20s linear infinite` (blog/about)
- These trigger continuous GPU/CPU work
- **Estimated impact**: 15-25% of CPU cost if GPU falls back to CPU

### PILLAR 2: Network Transfer Energy — HIGHEST IMPACT
**Duplicate font imports across all pages:**
- Inter font imported twice on every page (lines 7-8)
- Roboto, Playfair Display, Source Code Pro, etc. loaded on all pages
- **Estimated waste**: ~50KB per page load (font files)

**Heavy external library loading with low/zero utilization:**
- jQuery (36KB) — only used for Bootstrap modal/tooltip init
- Lodash (71KB) — only used once for `_.cloneDeep()`
- Moment.js (62KB) — loaded but never called
- D3.js (270KB) — loaded but never used
- Plotly.js (3.1MB) — loaded but never used
- Chart.js (64KB, blog only) — loaded but never used
- Marked.js (48KB, blog only) — loaded but never used
- Highlight.js (79KB, blog only) — loaded but never used
- **Estimated total waste**: ~3.8MB of unused JavaScript + CSS

**Unused CSS frameworks:**
- Bootstrap CSS (180KB) — only for basic grid, modal backdrop
- Bootstrap JS (80KB) — only for modal toggle
- Font Awesome (180KB) — only 10-15 icons used
- Material Design Icons (100KB) — 2-3 icons used max
- Animate.css (64KB) — only basic fade-in animations

**Image optimization opportunity:**
- Unsplash images loaded with `w=1200` and `fm=jpg` (lowest quality)
- No WebP/AVIF fallbacks
- **Estimated waste**: 20-30% larger than necessary

**Total Network Estimate:**
- index.html loads: ~3.5-4MB of unused dependencies
- blog.html loads: ~3.8-4.2MB of unused dependencies
- about.html loads: ~3.5MB of unused dependencies

### PILLAR 3: Frontend Screen Energy
**Continuous animations (prefers-reduced-motion not implemented):**
- `.particle { animation: float-particle linear infinite }`
- `.grid-bg { animation: grid-move 20s linear infinite }`
- These run for entire session duration and consume screen power

### PILLAR 5: Server Configuration
**nginx.conf observations:**
- No gzip/brotli compression enabled ❌
- No cache headers set ❌
- Static assets are cacheable but not configured ❌
- **Estimated impact**: Network transfer doubled on every request

## Priority Ranking (by Cardamon impact)

1. **Remove unused JavaScript libraries** (Plotly 3.1MB, D3 270KB, Chart.js 64KB, Marked 48KB, Highlight 79KB, Lodash 71KB, Moment 62KB) → ~3.8MB saved per page
2. **Enable gzip compression in nginx** → 60-70% reduction in transfer size
3. **Remove duplicate font imports** → ~50KB saved per page
4. **Eliminate setInterval loops** → 40-60% CPU reduction
5. **Support prefers-reduced-motion** → Accessibility + energy win
6. **Optimize image serving** (remove unused URLs, WebP/AVIF) → 20-30% image size reduction
7. **Configure static asset caching** → Energy on return visits
8. **Remove unused CSS frameworks** (unused Font Awesome, MDI icons, Animate.css) → ~350KB saved

## Estimated Total Savings
- **Network Transfer**: 4-5MB per first visit (83-88% reduction)
- **Frontend CPU**: 40-60% reduction (timers only)
- **Screen Energy**: 50-70% reduction (animation loops)
- **Cardamon Rating Impact**: Likely A+ (from current D/E range)
