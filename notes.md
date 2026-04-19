# Cardamon Optimiser - Discovery Notes

## Site Overview
- **Framework**: Static HTML (no build system)
- **Pages**: index.html (/), about.html (/about), blog.html (/blog)
- **Server**: nginx in Docker (nginx.conf present)
- **Deployment**: Docker container serving static files

## Findings by Pillar

### Pillar 2 — Network Transfer (HIGHEST PRIORITY)

#### Completely Unused Libraries (zero API calls):
| Library | Pages | Est. Size |
|---------|-------|-----------|
| plotly.js 2.29.1 | all 3 | ~3.5MB |
| d3.js 7.9.0 | all 3 | ~560KB |
| three.js r128 | about only | ~600KB |
| Chart.js 4.4.1 | blog only | ~250KB |
| highlight.js 11.9.0 (CSS+JS) | blog only | ~1.2MB |
| marked 12.0.0 | blog only | ~100KB |
| jQuery 3.7.1 | all 3 | ~87KB |
| animate.css 4.1.1 | all 3 | ~77KB |
| MaterialDesign-Webfont 7.4.47 | all 3 | ~270KB CSS + fonts |
| gsap 3.12.4 + ScrollTrigger | all 3 (index: both) | ~95KB |

#### Unused Fonts (never referenced in CSS font-family):
- Roboto (all 3 pages)
- Playfair Display (all 3 pages)
- Source Code Pro (all 3 pages)
- Inter loaded 3x per page (2x link + 1x @import) — should be 1x

#### Libraries with minor usage (keep for now):
- Bootstrap CSS + JS — some class usage
- lodash — _.cloneDeep used wastefully in console.log
- moment.js — used for date formatting in console.log

### Pillar 1 — Frontend CPU (HIGH PRIORITY)

#### Harmful setIntervals (persistent, never clear):
- index.html: 100ms — card positions getBoundingClientRect (never used)
- index.html: 5000ms — fetch worldtimeapi.org
- index.html: 2000ms — getComputedStyle on ALL DOM elements
- about.html: 33ms — matrix rain canvas draw loop
- about.html: 10000ms — fetch GitHub stars API
- about.html: 3000ms — device capabilities polling
- blog.html: 30000ms — fetch 3 RSS feeds
- blog.html: 1000ms — focus log array
- blog.html: 5000ms — reading time headings setAttribute

#### CSS Animations (infinite, no reduced-motion):
- .particle — float-particle infinite (60 particles on index, 40 shapes on blog)
- .gradient-bg — gradient-shift 8s infinite
- .glow-orb — orb-pulse + orb-move infinite (3 orbs)
- about.html — layer-drift-1/2/3, text-glow, card-float, avatar-rotate, dot-pulse, icon-bounce
- blog.html — grid-move, shape-float, border-rotate, progress-shimmer

### Pillar 5 — Server Config
- nginx.conf: No gzip compression configured
- nginx.conf: No cache headers for static assets

## PRs Created
(none yet)

## Run History
- 2026-04-19: First run - Discovery complete
