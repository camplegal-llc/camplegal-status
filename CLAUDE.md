# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an **Upptime-powered uptime monitoring and status page system** for CampLegal services. It's a configuration-driven, GitHub-native project with no traditional source code.

- **Live Status Page:** https://status.camplegal.com
- **Framework:** Upptime v1.41.0
- **Hosting:** GitHub Pages

## Architecture

```
.upptimerc.yml (single source of truth)
        │
        ▼
GitHub Actions Workflows (8 auto-generated)
        │
        ├──► api/         → JSON metrics (response times, uptime)
        ├──► history/     → YAML historical data
        └──► GitHub Pages → Static status website
```

**Monitored Services:**
- Lawyer Portal (https://lawyer.camplegal.com/)
- Customer Portal (https://client.camplegal.com/login)
- Corp Portal (https://corp.camplegal.com/login)
- API (https://api.camplegal.com/api/v1/mobile/ping)

## Critical Configuration Rule

**NEVER edit workflow files in `.github/workflows/` directly.** They are auto-generated and will be overwritten.

All configuration changes must be made to **`.upptimerc.yml`** only. This file controls:
- Sites to monitor and their expected status codes
- Workflow schedules (uptime checks run every 5 minutes)
- Status page branding and CNAME
- Incident management settings

## Workflow Schedule

| Workflow | Schedule |
|----------|----------|
| Uptime checks | Every 5 minutes |
| Response time | Daily 11 PM |
| Graphs generation | Daily midnight |
| Summary update | Daily midnight |
| Static site build | Daily 1 AM |

## Data Storage

- `api/{service}/` - JSON metrics files (response-time.json, uptime.json, time periods)
- `history/{service}.yml` - YAML historical status records
- `history/summary.json` - Aggregated status data
- GitHub Issues - Auto-created incident reports when services go down

## Commit Convention

All automated commits include `[skip ci] [upptime]` tags with emoji prefixes:
- 🟩 Service up notifications
- 🟥 Service down notifications
- `:card_file_box:` Status summary updates
- `:pencil:` README updates
- `:bento:` Graph updates
