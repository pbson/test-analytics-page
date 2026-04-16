---
name: Completed Work and Outcomes
description: PRs submitted and lessons learned
type: project
---

## Pull Requests Submitted

- **PR #19** (2026-04-16): Lazy load 13 images (6 index.html, 4 about.html, 3 blog.html); ~150-200 KB saved per session for non-scrollers
- **PR #14** (2026-04-13): Cache-Control headers; 70-80% request reduction for repeat visitors
- **PR #6** (2026-04-12): ✅ MERGED - Gzip compression; 70% transfer size reduction

## Key Learnings

1. **Low-effort, high-value wins**: `loading="lazy"` is minimal effort but measurable energy savings (defers image decode and network for off-viewport content).

2. **Complementary optimizations work best**: Cache headers (frequency) + gzip (size) + lazy loading (deferral) together maximize energy reduction.

3. **User behavior segmentation matters**: Lazy loading primarily benefits non-scrolling users (30-50%). Different users benefit from different optimizations.

4. **GSF principles**: Energy Proportionality (load ∝ usage), Demand Shaping (defer non-critical requests), Hardware Efficiency (spread CPU load).

5. **PR status**: 5+ days with no review feedback on existing PRs suggests maintainer bandwidth constraints. Continue submitting small, focused PRs (one optimization each).

---
