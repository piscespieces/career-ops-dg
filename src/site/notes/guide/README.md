---
{"dg-publish":true,"permalink":"/guide/readme/","tags":["gardenEntry"],"dg-note-properties":{}}
---

# Career-Ops Documentation

This folder contains the user-facing documentation for Career-Ops. It follows the [Divio Documentation System](https://docs.divio.com/documentation-system/), which organizes docs into four distinct types so you can always find the right kind of help.

---

## Tutorials — learn by doing

Start here if you are new to Career-Ops. Tutorials are step-by-step guides that get you from zero to a working result.

| Guide                                  | What you will do                                                                  |
| -------------------------------------- | --------------------------------------------------------------------------------- |
| [Quick Start](QUICKSTART.md) | Install the system, set up your profile and CV, and run your first job evaluation |

---

## How-to guides — solve a specific problem

Use these once you have completed the Quick Start. Each guide assumes you already have a working setup and focuses on one task.

| Guide | What it solves |
|---|---|
| [Customize the system to your career](customize-the-system.md) | Adjust archetypes, scoring weights, narrative, and deal-breakers |
| [Scan job portals](scan-job-portals.md) | Set up `portals.yml` and run automated portal scans |
| [Batch-evaluate multiple offers](batch-evaluate-offers.md) | Process a backlog of job URLs in parallel |
| [Generate a standalone PDF](generate-a-pdf.md) | Create a tailored PDF resume for a specific job |
| [Prepare for an interview](prepare-for-an-interview.md) | Build STAR+R stories and a company-specific prep report |

---

## Reference — look things up

Dry, precise descriptions of the system's components. Use these when you need to know exactly what a field, command, or status does.

| Reference | What it describes |
|---|---|
| [Profile fields](profile-fields.md) | Every field in `config/profile.yml` |
| [Commands](commands.md) | Every `/career-ops` subcommand |
| [Scoring system](scoring-system.md) | What each block measures and how the 0–5 score is calculated |
| [Canonical statuses](canonical-statuses.md) | Valid values for application status and when to use each |

---

## Explanation — understand why

Background reading for when you want to understand the reasoning behind how Career-Ops works, not just the mechanics.

| Explanation | What it covers |
|---|---|
| [How the auto-pipeline works end to end](how-the-pipeline-works.md) | The full sequence from URL paste to report, PDF, and tracker entry |
| [Why this scoring system](why-this-scoring-system.md) | The philosophy behind quality over quantity and human-in-the-loop design |
| [How to think about archetypes](how-to-think-about-archetypes.md) | What archetypes are, how they affect scoring, and how to define yours |
