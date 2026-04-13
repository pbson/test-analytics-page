---
name: Energy Efficiency Opportunities Backlog
description: Prioritized list of identified efficiency improvements, grouped by focus area
type: project
---

## COMPLETED ✅

### #1: Add HTTP Caching Headers (2026-04-13) ✅
**Impact**: 70-80% request reduction. Measurement: For 100 daily users, 70% repeat visits = 70 requests saved/day = 3.2 MB network energy saved.

### #2: Enable gzip Compression (2026-04-12) ✅ MERGED
**Impact**: 70% transfer size reduction. Measurement: 92 KB → 28 KB (64 KB saved per load).

---

## HIGH Priority (Ready to Implement)

### #3: Eliminate Duplicate Font Requests
**Issue**: Inter font loaded twice (lines 7-8 in index.html) + imported via CSS @import (line 25)  
**Solution**: Remove duplicate request, use link preload  
**Impact**: HIGH — Fewer HTTP requests = lower energy  
**Effort**: LOW  

### #4: Respect prefers-reduced-motion, Disable Animations
**Issue**: 11 @keyframes animations run continuously (float-particle, gradient-shift, orb-pulse, etc.)  
**Solution**: Add `@media (prefers-reduced-motion: reduce)` block  
**Impact**: MEDIUM — GPU/CPU energy savings for users with reduced-motion preference  
**Effort**: MEDIUM  

### #5: Remove Unused Heavy Libraries
**Issue**: jQuery (36KB), lodash (70KB), d3 (280KB), plotly (3.2MB), gsap (150KB) loaded from CDN  
**Solution**: Audit which are actually used; remove unused ones  
**Impact**: MEDIUM — Fewer bytes downloaded = less network/client energy  
**Effort**: MEDIUM  

### #6: Optimize External Unsplash Images
**Issue**: External images (w=1200, q=100) not cached, no responsive variants  
**Solution**: Host locally, serve WebP + JPEG fallback, add responsive srcset  
**Impact**: MEDIUM — Local caching + format optimization = fewer bytes  
**Effort**: MEDIUM  

### #7: Lazy Load Off-Screen Images
**Issue**: All images loaded eagerly  
**Solution**: Add `loading="lazy"` to <img> tags  
**Impact**: LOW  
**Effort**: LOW  

### #8: Verify Google Fonts Weight Variants
**Issue**: Requests may include unused weight variants  
**Solution**: Audit CSS, remove unused weights from request  
**Impact**: LOW-MEDIUM  
**Effort**: LOW  

---

## Backlog Cursor
Last checked: 2026-04-13  
Last completed: #1 (cache headers)  
Next: #3 (duplicate fonts)

---
