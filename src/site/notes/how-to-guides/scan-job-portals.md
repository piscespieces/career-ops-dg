---
{"dg-publish":true,"permalink":"/how-to-guides/scan-job-portals/","title":"Scan Job Portals","dg-note-properties":{"title":"Scan Job Portals"}}
---

# How to Scan Job Portals

> **Coming soon.** This guide is planned. In the meantime, run `/career-ops scan` inside Claude Code to start scanning with the default configuration.

This guide walks through configuring and running the portal scanner to find new job openings automatically across dozens of company career pages.

**What this covers:**

- Setting up `portals.yml` from the example template
- Configuring `title_filter.positive` to match your target roles
- Adding custom companies to `tracked_companies`
- Running `/career-ops scan` and reading the output
- Understanding dedup logic and `data/scan-history.tsv`
- Scheduling automatic scans on a recurring interval
