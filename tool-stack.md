---
title: Developer Resources & Tool Stack
excerpt: An overview of the recommended tech stack, external APIs, and data sources used across AAO Data Lab projects.
---

# Developer Resources & Tool Stack

## Recommended Stack

| Layer | Technology |
|---|---|
| Frontend | React + Vite, Tailwind CSS |
| Backend | Node.js / FastAPI (Python) |
| Database | PostgreSQL / Supabase |
| Mapping | Mapbox GL JS / Leaflet |
| CI/CD | GitHub Actions |
| Hosting | Vercel / Railway / GitHub Pages |

The live AAO Data Lab homepage is at [lab.allaboardohio.org](https://lab.allaboardohio.org).

## External Data Sources

- **ODOT Open Data** — Ohio Department of Transportation datasets (traffic counts, infrastructure)
- **US Bureau of Transportation Statistics** — National passenger rail ridership data
- **US Census TIGER/Line** — Geospatial boundaries for counties, cities, and statistical areas
- **OpenStreetMap** — Base map tiles and rail network geometry
- **GovTrack / LegiScan** — Legislative tracking for state and federal rail bills

## Environment Variables

All AAO Data Lab projects use a `.env.local` file (gitignored) for secrets. Never commit secrets to GitHub.

```
VITE_MAPBOX_TOKEN=your_mapbox_token
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

Request API keys from the `#dev-resources` channel in the [AAO Slack](https://join.slack.com/t/all-aboard-ohio/shared_invite/zt-3wgj180pu-eWAJoGn4_6~y9YHR9Lq3qA).
