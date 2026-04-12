---
name: Energy Efficiency Opportunities Backlog
description: Prioritized list of identified efficiency improvements, grouped by focus area
type: project
---

## HIGH Priority Opportunities

### 1. Network & I/O: Add HTTP Caching Headers to Static Assets
**Focus Area**: Network & I/O Efficiency  
**Estimated Impact**: HIGH  
**Effort**: LOW  
**Measurement Strategy**: Monitor cache hits in nginx logs; verify Cache-Control headers with curl  

**Issue**: Nginx config has no caching headers (Cache-Control, ETag, Expires). Every request fetches full HTML files.  
**Solution**: Add Cache-Control headers with appropriate TTLs (e.g., 1 year for index, shorter for pages). Add ETags for validation.  
**Rationale**: Browser caching reduces repeated downloads → lower network energy consumption across the stack (client, CDN, server)  
**GSF Principle**: Energy Proportionality (only serve what's needed; cached responses use zero server energy)  

---

### 2. Network & I/O: Enable gzip Compression in nginx
**Focus Area**: Network & I/O Efficiency  
**Estimated Impact**: HIGH (30-50% reduction in transfer size)  
**Effort**: VERY LOW  
**Measurement Strategy**: Compare response size with/without gzip (curl -H "Accept-Encoding: gzip")  

**Issue**: HTML files (36KB, 28KB, 28KB) are uncompressed; gzip could reduce to ~8-10KB.  
**Solution**: Enable gzip in nginx.conf with appropriate compression levels.  
**Rationale**: Smaller payloads = less bandwidth = less energy across network stack  
**GSF Principle**: Hardware Efficiency (reduce bandwidth usage, lower CPU for compression vs. transfer savings)  

---

### 3. Network & I/O: Eliminate Duplicate External Resource Requests
**Focus Area**: Network & I/O Efficiency  
**Estimated Impact**: HIGH  
**Effort**: LOW  
**Measurement Strategy**: Count HTTP requests before/after; check browser network tab  

**Issue**: 
- Inter font loaded twice (lines 7-8 in index.html)
- Inter also imported via @import in CSS (line 25)
- This creates redundant requests and blocks rendering  

**Solution**: 
- Remove duplicate font request (line 8)
- Replace @import with link preload for faster loading (one request per font)  

**Rationale**: Fewer HTTP requests = fewer round-trips = lower energy  
**GSF Principle**: Demand Shaping (eliminate unnecessary requests)  

---

## MEDIUM Priority Opportunities

### 4. Frontend/UI: Disable Animations by Default; Respect prefers-reduced-motion
**Focus Area**: Frontend / UI Energy  
**Estimated Impact**: MEDIUM  
**Effort**: MEDIUM  
**Measurement Strategy**: Measure GPU/CPU usage with DevTools Performance tab (animation playback time)  

**Issue**: 
- 11 @keyframes animations run continuously (float-particle, gradient-shift, orb-pulse, orb-move, etc.)
- No respect for `prefers-reduced-motion` media query
- Animations running 24/7 consume GPU cycles and power  

**Solution**: 
- Add `@media (prefers-reduced-motion: reduce)` block disabling animations
- Disable heavy animations by default; enable only on interaction  

**Rationale**: Continuous animations on static page = wasted GPU energy. Users with reduced-motion preference could save significant battery.  
**GSF Principle**: Hardware Efficiency (reduce GPU/CPU utilization for non-functional animations)  

---

### 5. Code-Level: Remove Unused Heavy Libraries
**Focus Area**: Code-Level Efficiency  
**Estimated Impact**: MEDIUM  
**Effort**: MEDIUM (requires verification that libraries aren't used)  
**Measurement Strategy**: Check page source; grep for library method calls; browser DevTools to confirm lib not called  

**Issue**: 
Loading from CDN:
- jQuery (36KB) - not used on static site?
- lodash (70KB) - not used on static site?
- moment.js (65KB) - for date parsing?
- d3 (280KB) - for data visualization?
- plotly (3.2MB) - for interactive plots?
- gsap (150KB) - for animations (see opportunity #4)

**Solution**: 
- Audit which libraries are actually used in JavaScript
- Remove unused libraries; replace heavy ones with lighter alternatives  

**Rationale**: Fewer downloaded bytes = faster load time = less energy across network and client CPU  
**GSF Principle**: Energy Proportionality (don't load features not used)  

---

### 6. Data: Optimize External Images from Unsplash
**Focus Area**: Data Efficiency  
**Estimated Impact**: MEDIUM  
**Effort**: MEDIUM  
**Measurement Strategy**: Compare image file sizes; check transfer time with curl -w  

**Issue**: 
- External Unsplash images loaded (w=1200, q=100)
- JPEGs from external source not cached locally
- No responsive image variants (same image for all viewport sizes)  

**Solution**: 
- Host images locally with appropriate size variants
- Serve WebP with JPEG fallback (WebP ~25% smaller)
- Add responsive srcset for different viewports  

**Rationale**: Local caching + optimized formats = fewer bytes downloaded + less processing on client  
**GSF Principle**: Hardware Efficiency (reduce bandwidth and decode energy)  

---

## LOW Priority Opportunities

### 7. Frontend/UI: Lazy Load Off-Screen Images
**Focus Area**: Frontend / UI Energy  
**Estimated Impact**: LOW (if images below fold)  
**Effort**: LOW  

**Issue**: All images loaded eagerly; if images are off-screen on smaller devices, they waste bandwidth.  
**Solution**: Add loading="lazy" attribute to <img> tags.  

---

### 8. Data: Verify Google Fonts Load Only Used Weight Variants
**Focus Area**: Data Efficiency  
**Estimated Impact**: LOW-MEDIUM  
**Effort**: LOW  

**Issue**: Google Fonts requests specify many weight variants (300-900). May not all be used.  
**Solution**: Audit CSS to verify all requested weights are used; remove unused weights from request.  

---

## Backlog Cursor
Last checked: 2026-04-12  
Next to investigate: Opportunities 4 and 2 (animations, gzip compression)
