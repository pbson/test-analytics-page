---
name: Repository Structure
description: Project overview, build system, and test capabilities
type: reference
---

## Project Overview

**pbson/test-analytics-page** is a static HTML website served via nginx in Docker.

### File Structure
- `index.html` (36 KB, 939 lines) - main landing page
- `about.html` (28 KB, 747 lines) - about page
- `blog.html` (28 KB, 718 lines) - blog page
- `Dockerfile` - nginx:alpine base, copies HTML files
- `nginx.conf` - serves static HTML with basic routing

### Build System
**No traditional build system** - this is a static site with no build step:
- ❌ No package.json or npm
- ❌ No Makefile or build scripts
- ❌ No test suite
- ❌ No linting/formatting tools configured
- ❌ Docker build tested but fails in CI environment (permission denied)

### CI/CD
Only workflow configured is `daily-efficiency-improver.md` (this agent).

## Discovered Build Commands

| Command | Status | Notes |
| ------- | ------ | ----- |
| `docker build -t test-analytics:latest .` | ❌ FAILS | Permission denied in sandboxed environment |
| Manual HTML validation | ⚠️ Possible | No tools configured, would need external tool |
| nginx config validation | ⚠️ Possible | Could use `nginx -t` if nginx available |

## Key Limitations
- Static site with no build/test/benchmark infrastructure
- No JavaScript tooling or bundle analysis
- No performance profiling tools configured
- Measurement strategy will rely on static analysis + manual inspection
