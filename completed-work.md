---
name: Completed Work and Outcomes
description: PRs submitted, measurement results, and lessons learned
type: project
---

## Pull Requests Submitted

### PR: Enable gzip compression in nginx
**Status**: ⏳ Draft (awaiting review)  
**Energy Impact**: ~70% reduction in network transfer size (92KB → 28KB)  
**Proxy Metric**: Network transfer size (maps to client radio energy, CDN energy, server I/O energy)  

**Measurements**:
- Baseline uncompressed: 92 KB (index 36KB + about 28KB + blog 28KB)
- With gzip level 6: 28 KB total
- Reduction: 64 KB per load cycle
- For 1000 daily users: ~64 MB/day saved from network

**Lessons Learned**:
- Static sites with heavy HTML/CSS are ideal candidates for gzip
- The 70% compression ratio is typical for HTML with lots of whitespace and repetition
- CPU cost of compression is negligible (<1-2ms) compared to bandwidth savings

## In Progress

**Opportunity**: Identify unused JavaScript libraries (jQuery, lodash, d3, plotly, etc.)  
**Status**: Blocked pending PR review  
**Estimated Impact**: HIGH (reduce page load by removing 500KB+ of unused code)  

**Opportunity**: Add HTTP Cache-Control headers to static assets  
**Status**: Pending (next in queue after gzip PR reviewed)  
**Estimated Impact**: HIGH (eliminate redundant requests)  

---

## Measurement Techniques Validated

1. **gzip compression**: Use `gzip -k filename && du -h` to estimate transfer size reduction
2. **Static analysis**: grep and line counting for quick opportunity identification
3. **CDN approximation**: Compare local file sizes as proxy for network energy (valid for static sites)
