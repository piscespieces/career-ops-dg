---
{"dg-publish":true,"permalink":"/guide/reference/canonical-statuses/","dg-note-properties":{}}
---

# Canonical Statuses Reference

> **Coming soon.** This reference is planned. In the meantime, see `templates/states.yml` for the authoritative list of statuses.

A reference for every valid application status in `data/applications.md`. Use this page when you want to know which status to set and when.

**What this covers:**

- `Evaluated` — report completed, decision pending
- `Applied` — application sent
- `Responded` — company has responded
- `Interview` — in active interview process
- `Offer` — offer received
- `Rejected` — rejected by the company
- `Discarded` — withdrawn by you, or offer is no longer active
- `SKIP` — does not fit, do not apply
- Formatting rules: no bold, no dates, no extra text in the status field
- How `node normalize-statuses.mjs` fixes non-canonical entries automatically
