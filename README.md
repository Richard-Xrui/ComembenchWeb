# CoMemBench Website

Public-facing static website for **CoMemBench: Benchmarking Collaborative Memory Boundaries across Multi-Agent Workflow Topologies**.

## Publishing

The site is published from `dist/` by the GitHub Actions workflow in `.github/workflows/deploy-pages.yml`.

- Do not commit datasets, evaluation outputs, credentials, or access-request records to this repository.
- Dataset access belongs in a gated repository; this site only links to the approved release.
- After the final domain is purchased, add it in **Settings → Pages → Custom domain** first, then create the DNS records GitHub supplies. Do not create a wildcard DNS record.

## Evidence boundary

The homepage shows only the certified v18 release coverage: 800 task families across four domains, with 200 certified families in each domain. It does not publish a leaderboard until approved, reproducible result records exist.
