---
{"dg-publish":true,"permalink":"/how-to-guides/batch-evaluate-offers/","title":"Batch-evaluate Multiple Offers","dg-note-properties":{"title":"Batch-evaluate Multiple Offers"}}
---

# How to Batch-Evaluate Multiple Offers

Use this guide when you have 10 or more job offers to review and want to process them all in one session instead of one by one.

Each offer gets its own Claude worker. That worker reads your CV, scores the match, writes a full report, and saves a tailored PDF — all without you lifting a finger.

## Before you start

Make sure you have:

- The `career-ops` folder open in Claude Code
- A list of job posting URLs ready to paste
- Enough time — each offer takes about 5–10 minutes, so 20 offers at 2 workers at a time takes roughly 1–2 hours

---

## Step 1: Add your offers to the input file

The batch system reads job URLs from a file called **`batch/batch-input.tsv`**. Think of it as a to-do list for the evaluator.

1. Open **`batch/batch-input.tsv`** in any text editor.
2. Add one row per offer. Each row has four columns separated by a tab:

   | Column | What to enter |
   |--------|---------------|
   | `id` | A unique number for this offer (1, 2, 3, …) |
   | `url` | The full job posting URL |
   | `source` | Where you found it (e.g., `LinkedIn`, `Greenhouse`) |
   | `notes` | An optional note — leave blank if you have none |

3. Save the file.

**Example:**

```
id	url	source	notes
1	https://jobs.example.com/senior-engineer	LinkedIn	
2	https://greenhouse.io/jobs/fullstack-dev	Greenhouse	priority
3	https://builtinaustin.com/job/rails-dev	BuiltIn	
```

> **Tip:** Each ID must be a unique number. Do not skip numbers or repeat them.

---

## Step 2: Preview your batch (recommended)

Before processing anything, run a quick check to see how many offers are waiting. Nothing gets evaluated yet — this is just a preview.

```bash
./batch/batch-runner.sh --dry-run
```

You'll see a list of pending offers and their IDs. If something looks wrong, fix the input file now before spending time on a bad list.

---

## Step 3: Run the batch

When you're ready, start the batch. You can run one offer at a time or several at once.

**One at a time (slowest, uses the least memory):**

```bash
./batch/batch-runner.sh
```

**Two at a time (a good default):**

```bash
./batch/batch-runner.sh --parallel 2
```

**Three at a time (faster, but heavier on your machine):**

```bash
./batch/batch-runner.sh --parallel 3
```

**Skip offers that score below a threshold (e.g., below 4.0 out of 5):**

```bash
./batch/batch-runner.sh --parallel 2 --min-score 4.0
```

Watch the terminal as the batch runs. Each line tells you which offer is being processed and whether it finished or failed.

---

## Step 4: Read results as they come in

You don't need to wait for the batch to finish. Results appear as each offer completes.

**Full evaluation reports** → `reports/`

Each report is a file named like `042-company-name-2026-04-14.md`. Open it to see:

- A summary of the role
- How well your CV matches the job
- Salary research
- A suggested interview prep plan

**One-line tracker entries** → `batch/tracker-additions/`

Each offer also drops a short summary file here. These get added to your main tracker in Step 6.

---

## Step 5: Retry any failed offers

Sometimes a worker fails — for example, if a job posting URL stopped loading. Failed offers show up in the terminal with a short error message.

**Retry only the failed offers:**

```bash
./batch/batch-runner.sh --retry-failed
```

**Retry with up to 3 attempts instead of the default 2:**

```bash
./batch/batch-runner.sh --retry-failed --max-retries 3
```

The batch skips any offer that already finished successfully — so re-running this is always safe.

---

## Step 6: Merge results into your tracker

After the batch finishes, run this command to add all new evaluations to `data/applications.md`:

```bash
node merge-tracker.mjs
```

This script:

1. Reads the summary files from `batch/tracker-additions/`
2. Checks for duplicates so you never get two rows for the same offer
3. Adds new entries to your applications tracker
4. Archives the processed files into `batch/tracker-additions/merged/`

**To preview the changes without writing anything:**

```bash
node merge-tracker.mjs --dry-run
```

---

## What to do next

Open **`data/applications.md`** to see all your evaluations in one table. From there you can:

- Sort by score to find your best matches
- Open individual reports in `reports/` for a full deep-dive
- Start the application process for your top picks using `/career-ops apply`

---

## Quick reference

| Task | Command |
|------|---------|
| Preview pending offers | `./batch/batch-runner.sh --dry-run` |
| Run batch (1 at a time) | `./batch/batch-runner.sh` |
| Run batch (2 at a time) | `./batch/batch-runner.sh --parallel 2` |
| Skip low-score offers | Add `--min-score 4.0` to any run command |
| Retry failed offers | `./batch/batch-runner.sh --retry-failed` |
| Merge into tracker | `node merge-tracker.mjs` |
| Preview merge changes | `node merge-tracker.mjs --dry-run` |
