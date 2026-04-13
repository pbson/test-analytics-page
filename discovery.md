# Repository Discovery - Test Analytics Page

**Date:** 2026-04-13 (updated)

## Project Overview
- **Type**: Static HTML marketing website (MegaStack cloud platform)
- **Framework**: None - pure static HTML
- **Build System**: None - static files
- **Deployment**: Docker + Nginx with gzip compression
- **Pages**: 3 (index.html, about.html, blog.html)

## External Dependencies (as of 2026-04-13)

### Fonts
- **Google Fonts**: Inter (weights: 300, 400, 500, 600, 700, 800, 900) - loaded twice + @import
- **Unused**: Roboto, Playfair Display, Source Code Pro (font-family never used in CSS)
- **Loaded on**: All 3 pages

### CSS Libraries (all pages)
- Font Awesome 6.5.1 - USED on index.html only (6 icons), UNUSED on about/blog
- Animate.css 4.1.1 - UNUSED on all pages
- Bootstrap CSS 5.3.2 - UNUSED on all pages
- Material Design Icons 7.4.47 - UNUSED on all pages
- highlight.js github-dark CSS (blog.html) - UNUSED

### JS Libraries (all pages)
- jQuery 3.7.1 - UNUSED on all pages
- Lodash.js 4.17.21 - Used for console.log convenience (_.cloneDeep, _.sortBy, _.map)
- Moment.js 2.30.1 - Used for console.log timestamps
- D3.js 7.9.0 - UNUSED on all pages
- Plotly.js 2.29.1 - UNUSED on all pages (~3MB each!)
- Bootstrap bundle JS 5.3.2 - UNUSED on all pages
- GSAP 3.12.4 - UNUSED on all pages
- GSAP ScrollTrigger (index) - UNUSED
- Three.js r128 (about) - UNUSED (~600KB)
- marked.js 12.0.0 (blog) - UNUSED
- highlight.js 11.9.0 (blog) - UNUSED
- Chart.js 4.4.1 (blog) - UNUSED

## CPU/Timer Issues (Frontend Pillar 1)

### index.html
- 60 CSS-animated particles (float-particle infinite)
- mousemove handler: calculates distance on every pixel
- setInterval 100ms: reads getBoundingClientRect on all .feature-card elements
- setInterval 5000ms: fetch worldtimeapi.org
- setInterval 2000ms: getComputedStyle on ALL DOM elements (very expensive!)

### about.html
- Matrix rain canvas at 30fps (setInterval 33ms) - highest CPU impact!
- setInterval 10000ms: fetch GitHub API for stars count
- setInterval 3000ms: detect device capabilities
- scroll listener: queries getBoundingClientRect on all team/value/mission cards

### blog.html
- setInterval 30000ms: fetch RSS feeds from 3 URLs
- setInterval 1000ms: focus log recording (every second!)
- setInterval 5000ms: update heading attributes (read time, word count, etc.)
- buildSearchIndex: builds full-text index on page load (one-time)
- Preloads / and /about via fetch on page load

## Server Configuration
- Nginx with gzip compression for text/css, text/javascript, application/json
- Static files - minimal server processing

## Actual Font Weights Used in CSS
- 600, 700, 800, 900 (explicit)
- 400 (implicit body text default)
- NOT USED: 300, 500
