# ravidvr.github.io

[![Deals freshness](https://github.com/ravidvr/ravidvr.github.io/actions/workflows/deals-freshness.yml/badge.svg)](https://github.com/ravidvr/ravidvr.github.io/actions/workflows/deals-freshness.yml)

Personal site of Ravi Dronamraju — links to my Berlin open-data projects and LinkedIn.

Live: https://ravidvr.github.io/

Single self-contained `index.html`. No build step, no dependencies, no tracking.

## Repo layout

- `index.html` — the personal site (EN/DE toggle, project cards)
- `deals/` — public copy of the Berlin Deals map (synced Tue+Fri by a cron on a home Mac; the GitHub Actions badge above watches its freshness)
- `coops/` — public copy of the German Worker Co-ops map
- `robots.txt` / `sitemap.xml` — crawler discovery
