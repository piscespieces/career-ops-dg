---
{"dg-publish":true,"permalink":"/guide/how-to-guides/batch-evaluate-offers/","dg-note-properties":{}}
---

# How to Batch-Evaluate Multiple Offers

> **Coming soon.** This guide is planned. In the meantime, run `/career-ops batch` inside Claude Code or see `batch/batch-runner.sh` for the orchestrator script.

This guide explains how to evaluate 10 or more job offers in parallel using background workers, so you can process a backlog in one session.

**What this covers:**

- Adding URLs to `data/pipeline.md` for queued processing
- Running `/career-ops batch` to start parallel workers
- How `batch/batch-runner.sh` orchestrates `claude -p` sub-agents
- Reading results as they arrive in `reports/` and `batch/tracker-additions/`
- Running `node merge-tracker.mjs` after a batch to update the tracker
