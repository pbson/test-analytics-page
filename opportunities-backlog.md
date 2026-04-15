---
name: Energy Efficiency Opportunities Backlog
description: Prioritized list of identified efficiency improvements, grouped by focus area
type: project
---

## COMPLETED ✅

### #1: Add HTTP Caching Headers (2026-04-13) ✅
**Status**: PR #14 created and open, awaiting maintainer review  
**Impact**: 70-80% request reduction. Measurement: For 100 daily users, 70% repeat visits = 70 requests saved/day = 3.2 MB network energy saved.

### #2: Enable gzip Compression (2026-04-12) ✅ MERGED
**Status**: PR #6 merged to main (commit de043d7)  
**Impact**: 70% transfer size reduction. Measurement: 92 KB → 28 KB (64 KB saved per load).
**Note**: Cardamon created duplicate PR #18 for the same optimization on 2026-04-15

---

## IN PROGRESS (by Cardamon Agent)

### #3: Eliminate Duplicate Font Requests
**PR**: #12 - Remove unused external dependencies  
**Status**: Open, awaiting review  
**Issue**: Inter font loaded twice (lines 7-8 in index.html) + imported via CSS @import (line 25)  
**Solution**: Remove duplicate request, use link preload  
**Impact**: HIGH — Fewer HTTP requests = lower energy  
**Effort**: LOW  

### #4: Respect prefers-reduced-motion, Disable Animations
**PR**: #17 - Add prefers-reduced-motion CSS  
**Status**: Open, awaiting review  
**Issue**: 11 @keyframes animations run continuously (float-particle, gradient-shift, orb-pulse, etc.)  
**Solution**: Add `@media (prefers-reduced-motion: reduce)` block  
**Impact**: MEDIUM — GPU/CPU energy savings for users with reduced-motion preference  
**Effort**: MEDIUM  

### #5: Remove Unused Heavy Libraries
**PR**: #12 - Remove unused external dependencies  
**Status**: Open, awaiting review  
**Issue**: jQuery (36KB), lodash (70KB), d3 (280KB), plotly (3.2MB), gsap (150KB) loaded from CDN  
**Solution**: Audit which are actually used; remove unused ones  
**Impact**: MEDIUM — Fewer bytes downloaded = less network/client energy  
**Effort**: MEDIUM  

### #16: Remove Unnecessary CPU-Intensive Timers
**PR**: #16 - Remove unnecessary CPU-intensive timers  
**Status**: Open, awaiting review (Cardamon)  
**Issue**: 8 setInterval loops running continuously with no UI effect (getBoundingClientRect, getComputedStyle, external fetches)  
**Solution**: Remove unused timers; convert matrix rain to visibility-aware requestAnimationFrame  
**Impact**: HIGH — Reduced CPU utilization during measurement window  
**Effort**: MEDIUM  

### #18: Enable gzip Compression (Duplicate)
**PR**: #18 - Enable gzip compression in nginx  
**Status**: Open, awaiting review (Cardamon)  
**Note**: Duplicate of already-merged PR #6; addresses same optimization  
**Impact**: 70% transfer size reduction  
**Effort**: LOW  

---

## AVAILABLE FOR INDEPENDENT IMPLEMENTATION

### #6: Optimize External Unsplash Images
**Issue**: External images (w=1200, q=100) not cached, no responsive variants  
**Solution**: Host locally, serve WebP + JPEG fallback, add responsive srcset  
**Impact**: MEDIUM — Local caching + format optimization = fewer bytes  
**Effort**: MEDIUM  
**Status**: Not yet started  

### #7: Lazy Load Off-Screen Images
**Issue**: All images loaded eagerly  
**Solution**: Add `loading="lazy"` to <img> tags  
**Impact**: LOW  
**Effort**: LOW  
**Status**: Not yet started  

### #8: Verify Google Fonts Weight Variants
**Issue**: Requests may include unused weight variants  
**Solution**: Audit CSS, remove unused weights from request  
**Impact**: LOW-MEDIUM  
**Effort**: LOW  
**Status**: Not yet started  

---

## Backlog Cursor

**Last comprehensive scan**: 2026-04-13  
**Items completed**: #1, #2  
**Items in progress**: #3, #4, #5, #16, #18 (by Cardamon)  
**Next independent item to consider**: #6 (Optimize Unsplash images) or #7 (Lazy load)  

---

## Summary by Focus Area

### Network & I/O Efficiency
- ✅ #1: Cache-Control headers (PR #14 open)
- ✅ #2: Gzip compression (PR #6 merged, PR #18 duplicate)
- 🔄 #3: Duplicate font requests (PR #12 open)
- 🔄 #5: Remove unused libraries (PR #12 open)
- ⏳ #6: Optimize external images (not started)

### Frontend / UI Energy
- 🔄 #4: Prefers-reduced-motion (PR #17 open)
- 🔄 #16: Remove CPU timers (PR #16 open)
- ⏳ #7: Lazy load off-screen images (not started)
- ⏳ #8: Verify font weights (not started)

