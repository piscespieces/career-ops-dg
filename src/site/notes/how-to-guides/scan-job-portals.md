---
{"dg-publish":true,"permalink":"/how-to-guides/scan-job-portals/","title":"Scan Job Portals","dg-note-properties":{"title":"Scan Job Portals"}}
---

# How to Scan Job Portals

This guide walks through setting up `portals.yml` and running the portal scanner to find new job openings automatically.

**Before you start:** Make sure you have completed the [Getting Started](../getting-started.md) guide. You need `cv.md` and `modes/_profile.md` in place before scanning is useful.

---

## Set up portals.yml

`portals.yml` is the file that controls what the scanner looks for and where it looks. You create it once from the included template, then edit it to match your target roles.

Run this command from the project folder:

```bash
cp templates/portals.example.yml portals.yml
```

Open `portals.yml` in any text editor. The file has three sections. The steps below walk through each one.

---

### Configure your title filter

The title filter is how the scanner decides if a job is worth showing you. It checks the job title against two lists of keywords.

Find the `title_filter` section near the top of the file:

```yaml
title_filter:
  positive:
    - "AI"
    - "ML"
    - "Product Manager"
  negative:
    - "Junior"
    - "Intern"
  seniority_boost:
    - "Senior"
    - "Staff"
    - "Lead"
```

**Replace the `positive` list** with keywords that match your target roles. A job must match at least one keyword from this list to pass through. The check is not case-sensitive, so `"AI"` also catches `"ai engineer"`.

**Replace the `negative` list** with keywords that rule a job out. If any of these appear in the title, the job is skipped — even if it matched a positive keyword.

**Leave `seniority_boost` as is** unless you want to add or remove seniority levels. These keywords do not filter anything out — they just move matching jobs higher in the results.

**Example:** If you are looking for Rails engineering roles, your filter might look like this:

```yaml
title_filter:
  positive:
    - "Rails"
    - "Ruby"
    - "Full Stack"
    - "Backend"
  negative:
    - "Junior"
    - "Intern"
    - "PHP"
    - "Java"
  seniority_boost:
    - "Senior"
    - "Staff"
    - "Lead"
```

> **Tip:** Start with a small `positive` list of three to five keywords. You can always add more later. A long list makes it harder to see why a job passed or failed.

---

### Add companies to track

The `tracked_companies` section is a list of specific companies you want the scanner to check every time. The scanner goes directly to each company's job page and reads the open roles.

Find the `tracked_companies` section near the bottom of the file. Each entry looks like this:

```yaml
tracked_companies:
  - name: Anthropic
    careers_url: https://job-boards.greenhouse.io/anthropic
    api: https://boards-api.greenhouse.io/v1/boards/anthropic/jobs
    enabled: true

  - name: OpenAI
    careers_url: https://openai.com/careers
    enabled: true
```

**To add a company**, copy an existing entry and change the values:

| Field         | What to put                                                                                        |
| ------------- | -------------------------------------------------------------------------------------------------- |
| `name`        | The company name as you want it to appear in results                                               |
| `careers_url` | The direct URL to the company's job listings page                                                  |
| `api`         | Optional. The Greenhouse API URL if the company uses Greenhouse. Leave it out if you are not sure. |
| `enabled`     | Set to `true` to include the company or `false` to skip it without deleting the entry.             |

**To find a company's `careers_url`**, go to the company's website, click Careers or Jobs, and copy the URL of the page that lists open roles. That is the URL to use.

**To disable a company without deleting it**, set `enabled: false`:

```yaml
  - name: Stripe
    careers_url: https://stripe.com/jobs/search
    enabled: false
```

> **Note:** Every company in `tracked_companies` must have a `careers_url`. Without it, the scanner has no page to visit and will skip that entry.

---

### Review the search queries

The `search_queries` section runs broader web searches to find roles at companies not in your tracked list. The template includes many pre-built queries.

You do not need to change this section to get started. The pre-built queries cover major job boards including Greenhouse, Ashby, Lever, and Wellfound.

When you are ready to customize, each query looks like this:

```yaml
search_queries:
  - name: Greenhouse — Rails Engineer
    query: 'site:job-boards.greenhouse.io "Rails Engineer" OR "Ruby on Rails" remote'
    enabled: true
```

To turn off a query you do not need, set `enabled: false`. To add a new one, copy an existing entry, give it a new `name`, and update the `query` text.

---

<!-- ============================================================
     SECTION PLACEHOLDER: Run a scan
     
     Cover:
     - Two ways to run: `npm run scan` (zero tokens, API only) vs
       `/career-ops scan` inside Claude Code (Playwright + AI)
     - When to use each
     - The --dry-run and --company flags for npm run scan
     ============================================================ -->

---

<!-- ============================================================
     SECTION PLACEHOLDER: Read the scan output
     
     Cover:
     - What the summary table means (found / filtered / duped / new)
     - Where new jobs go (data/pipeline.md)
     - What scan-history.tsv is and why it matters
     ============================================================ -->

---

<!-- ============================================================
     SECTION PLACEHOLDER: Evaluate new offers from a scan
     
     Cover:
     - After a scan, how to process pipeline.md
     - Running /career-ops pipeline to evaluate pending URLs
     ============================================================ -->

---

<!-- ============================================================
     SECTION PLACEHOLDER: Schedule automatic scans
     
     Cover:
     - Using /schedule or /loop to run scans on a recurring interval
     - Suggested cadence (every 2-3 days)
     ============================================================ -->
