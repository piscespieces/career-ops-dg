---
{"dg-publish":true,"permalink":"/getting-started/","title":"Getting Started","dg-note-properties":{"title":"Getting Started"}}
---

This guide walks you through setting up Career-Ops and running **your first job evaluation**. By the end, you will paste a job posting and get back a full report, a score, and a tailored PDF resume — all in one step.

---

## What you need before you start

Make sure you have the following installed on your computer:

- **[Claude Code](https://claude.ai/code)** — the AI coding assistant that powers this system. Install it and log in before continuing.
- **[Node.js](https://nodejs.org) version 18 or later** — a JavaScript runtime used for generating PDFs and running helper scripts.
- **[Git](https://git-scm.com/)** — for cloning the project. Most computers already have it. To check, open a terminal and run `git --version`.

You do not need to know how to code. You only need to be comfortable running commands in a terminal.

> **New to the terminal?** If you have never used a command line before, that is completely fine — but this guide is not the place to learn it. To get up to speed quickly, read the [Command Line for Beginners](https://www.freecodecamp.org/news/command-line-for-beginners/) handbook by freeCodeCamp. It covers everything you need to follow along here. Once you are comfortable opening a terminal and running a command, come back and continue from Step 1.

---

## Step 1: Download the project

Open a terminal and run the following command to clone the project to your computer:

```bash
git clone https://github.com/santifer/career-ops.git
```

Then move into the project folder:

```bash
cd career-ops
```

Install the required packages:

```bash
npm install
```

Install the browser that Career-Ops uses to generate PDF resumes:

```bash
npx playwright install chromium
```

When the commands finish, you are ready to configure the system.

---

## Step 2: Verify your setup

Before you configure anything, run the setup checker to make sure everything installed correctly:

```bash
npm run doctor
```

The output tells you what is working and what is missing. Fix any issues it flags before moving on.

---

## Step 3: Create your profile

Your profile is a simple text file that tells the system who you are. Career-Ops uses it to score jobs against your background and preferences.

Copy the example profile to create your own:

```bash
cp config/profile.example.yml config/profile.yml
```

Now open `config/profile.yml` in any text editor and fill in your details. The most important fields are:

| Field | What to put |
|---|---|
| `full_name` | Your full name |
| `email` | Your email address |
| `location` | Your city and country |
| `target_roles.primary` | The job titles you are looking for |
| `compensation.target_range` | Your salary target (for example, `"$120K-160K"`) |
| `narrative.headline` | One sentence that describes your professional identity |

You do not need to fill in every field right now. The required ones above are enough to get started.

---

## Step 4: Add your CV

Career-Ops reads your CV every time it evaluates a job. It uses your actual experience to check how well you match each role.

Create a file called `cv.md` in the project's root folder. Paste your CV into it using plain text. Use this structure as a guide:

```markdown
# Your Name

## Summary

Two or three sentences about who you are and what you do.

## Work Experience

### Company Name — Job Title
2022–Present

- What you did and the impact it had.
- Another accomplishment with a number if you have one.

## Skills

Python, SQL, project management, etc.

## Education

University Name — Degree, Year
```

If you are not sure what to write, look at `examples/cv-example.md` in this project for a full example you can model yours after.

> **Tip:** The more detail you put in your CV, the better the evaluations get. Include numbers, team sizes, tools, and specific outcomes where you can.

---

## Step 5: Set up job portals (optional)

If you want to scan job boards later, copy the portal config file:

```bash
cp templates/portals.example.yml portals.yml
```

You can skip this for now. It is not needed to run your first evaluation.

---

## Step 6: Open Claude Code

Start Claude Code inside the project folder:

```bash
claude
```

When it opens, it reads `CLAUDE.md` and loads the Career-Ops system automatically. You do not need to type any setup commands.

> **Note:** The first time Claude Code opens in this folder, it may ask if you trust the project files. Say yes to continue.

---

## Step 7: Evaluate your first job description

You are ready to run your first evaluation. There are two ways to do this:

**Option A — Paste a job URL:**

Copy the link to any job posting and paste it directly into the Claude Code chat. For example:

```
https://jobs.example.com/senior-engineer-ai
```

**Option B — Paste the job description text:**

If you do not have a URL, copy the full job description text and paste it into the chat.

Career-Ops detects that you shared a job posting and runs the full pipeline automatically. This is called the **auto-pipeline**.

---

## What happens next

After you paste the job, Career-Ops does the following steps on its own:

1. **Reads the job description** to understand the role, requirements, and compensation.
2. **Reads your CV** from `cv.md` to find matches and gaps.
3. **Scores the job** from 0 to 5 across multiple dimensions, like role fit, compensation, and remote policy.
4. **Writes a report** to the `reports/` folder with a detailed breakdown.
5. **Generates a tailored PDF resume** to the `output/` folder, customized for this specific job.
6. **Adds a row** to your application tracker in `data/applications.md`.

The whole process takes about one to two minutes. When it finishes, Claude Code shows you the score and a summary of the report.

---

## Reading your results

Open the report file in `reports/`. The filename follows the pattern `{number}-{company}-{date}.md`. Inside, you will find:

- **Score** — a number from 0.0 to 5.0. Anything below 4.0 means the job is probably not a strong fit.
- **Block A** — a plain-English summary of the role.
- **Block B** — a table showing how your CV matches each job requirement, plus any gaps.
- **Block C** — a strategy recommendation for how to position yourself for this role.
- **Block D** — compensation research comparing the offer to market rates.
- **Block E** — personalization notes for your application.
- **Block F** — interview preparation with STAR stories tailored to this job.

Your tailored PDF resume is in the `output/` folder. Review it before sending it anywhere. Career-Ops never submits anything without your approval.

---

## What to do next

Now that your first evaluation is done, here are a few things you can explore:

- **Improve your profile.** Open Claude Code and say: *"Here is more context about me: [paste details]."* The system updates your profile and future evaluations get more accurate.
- **Evaluate more jobs.** Paste more URLs. Each one adds to your tracker.
- **Scan job boards.** Type `/career-ops scan` in the Claude Code chat to search dozens of company career pages at once.
- **Compare offers.** If you have several reports, type `/career-ops ofertas` to get a ranked comparison.

---

## If something goes wrong

**The report did not generate.** Make sure `cv.md` exists in the root folder and has content in it. Without a CV, the system cannot score match quality.

**The PDF did not generate.** Run `npx playwright install chromium` again. If that does not fix it, check that Node.js is version 18 or higher by running `node --version`.

**The score seems off.** The first few evaluations are rough. The system does not know you well yet. After each evaluation, tell Claude Code what it got wrong. For example: *"That score is too high — I have no experience with Kubernetes."* It will learn and adjust.

**Something else is broken.** Run `npm run doctor` for a full health check, or ask Claude Code directly: *"What is wrong with my setup?"*

---

## Found a bug or have a question?

If something is not working the way this guide says it should, please report it. Bug reports help everyone who comes after you.

- **Report a bug:** Open an issue on the [GitHub repository](https://github.com/santifer/career-ops/issues). Describe what you expected to happen, what actually happened, and paste any error message you saw.
- **Ask a question:** Join the [Discord community](https://discord.gg/8pRpHETxa4). It is the fastest way to get help from other users and the author.
- **Contribute a fix:** If you know how to fix the issue yourself, read [CONTRIBUTING.md](https://github.com/santifer/career-ops/blob/main/CONTRIBUTING.md) before opening a pull request. The short version: open an issue first to discuss the change, then submit your PR.

---

## Next steps

You have completed the Getting Started guide. Here is what to read next depending on what you want to do:

| I want to…                                       | Go to                                                                         |
| ------------------------------------------------ | ----------------------------------------------------------------------------- |
| Make the evaluations feel more accurate          | [[how-to-guides/customize-the-system\|How to customize the system to your career]]          |
| Understand what the score and each block mean    | [[reference/scoring-system\|Scoring system reference]]                                  |
| Search dozens of company job pages automatically | [[how-to-guides/scan-job-portals\|How to scan job portals]]                                 |
| Evaluate 10+ jobs in parallel                    | [[how-to-guides/batch-evaluate-offers\|How to batch-evaluate offers]]                       |
| See all available commands                       | [[reference/commands\|Commands reference]]                                              |
| Full setup options                               | [Setup Guide](https://github.com/santifer/career-ops/blob/main/docs/SETUP.md) |

For a deeper look at all the commands right now, see the [Setup Guide](https://github.com/santifer/career-ops/blob/main/docs/SETUP.md). To customize the scoring system, archetypes, and negotiation scripts, just ask Claude Code — it can edit its own configuration files on your behalf.
