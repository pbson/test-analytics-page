# Cardamon Optimisation Progress

**Last Updated:** 2026-04-13

## Completed Tasks

### ✅ Task 1: Repository Discovery
- Scanned full codebase (3 static HTML pages, Docker/Nginx deployment)
- Identified all external dependencies (Google Fonts, Unsplash images)
- Categorised Cardamon impact by pillar
- See `discovery.md` for full analysis

### ✅ Task 2: Network Transfer - Font Optimization (Partial)
- **PR #1 Created**: Remove unused Google Fonts weights 300 & 500
- **Status**: Awaiting merge
- **Estimated impact**: 20–30 KB per page, ~1.2–1.8 mWh per 1,000 visits
- **Model pillar**: Network Transfer (both device radio + infrastructure)

## Remaining High-Impact Tasks

### 🟡 Task 2: Network Transfer - Image Optimization
- **Status**: Low priority
- **Finding**: 16 images already in WebP format with lazy loading
- **Opportunity**: Verify image dimensions match display sizes (minor savings only)
- **Skip for now**: Already well-optimised

### 🟡 Task 2: Network Transfer - CSS Deduplication
- **Status**: Medium priority
- **Finding**: Navigation, footer, and typography CSS duplicated across 3 pages
- **Estimated savings**: ~2–3 KB total per page (not per visit, due to CSS size)
- **Blocker**: Would require either:
  1. Extract to separate stylesheet (breaks inline-CSS-only pattern)
  2. Build step to inject shared CSS (no build system currently)
- **Recommendation**: Defer unless CSS grows significantly

### 🟢 Task 3: Frontend CPU Reduction
- **Status**: Not applicable
- **Finding**: No repeating timers, polling, or problematic event handlers
- **Site design**: Minimal JavaScript (only form validation on blog)

### 🟢 Task 4: Screen Energy & Accessibility
- **Status**: Already implemented
- **Finding**: `prefers-reduced-motion` support on all 3 pages
- **No action needed**: Site respects reduced-motion preference

### 🟢 Task 5: Compression & Caching
- **Status**: Well configured
- **Finding**: Nginx gzip compression enabled
- **Cache headers**: Not visible in nginx.conf (using Nginx defaults)
- **Recommendation**: No changes needed unless cache behaviour changes

## Next Run Priorities

1. **Merge PR #1** if ready (fonts)
2. Consider **CSS deduplication** if worth effort (low savings)
3. Monitor for new dependencies or features that might affect Cardamon score

## Notes

- Site uses `display=swap` for fonts (good - no invisible text flash)
- All images use `loading="lazy"` (good - below-fold deferred)
- Form validation is lightweight (regex only, no heavy processing)
- Dark theme with low brightness = natural lower screen energy
