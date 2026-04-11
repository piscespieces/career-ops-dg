---
{"dg-publish":true,"permalink":"/explanation/how-the-pipeline-works/","dg-note-properties":{}}
---

# How the Auto-Pipeline Works End to End

> **Coming soon.** This explanation is planned. In the meantime, see `docs/ARCHITECTURE.md` for a technical overview.

This page explains what happens inside Career-Ops from the moment you paste a job URL to the moment a report, PDF, and tracker entry appear. Read this when you want to understand *why* the system behaves the way it does, not just how to use it.

**What this covers:**

- How Career-Ops detects that a pasted message is a job description (not a regular question)
- The role of `CLAUDE.md` as the agent's instruction set
- How archetype detection works and why it matters for scoring
- The sequence of reads: JD → `cv.md` → `modes/_profile.md` → `modes/oferta.md`
- How Playwright is used to verify that a job posting is still active
- How reports, PDFs, and TSV tracker additions are written and where they go
- How `node merge-tracker.mjs` safely adds rows to `data/applications.md`
- The difference between interactive mode (Claude Code) and batch mode (`claude -p`)
