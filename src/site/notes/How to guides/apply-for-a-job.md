---
{"dg-publish":true,"permalink":"/how-to-guides/apply-for-a-job/","title":"Apply for a Job","dg-note-properties":{"title":"Apply for a Job"}}
---

This guide walks through using `/career-ops apply` to fill out a job application form with answers tailored to your profile, proof points, and the specific role you are applying to.

**Before you start:** Make sure you have completed the [Scan Job Portals](scan-job-portals.md) guide. The `apply` command depends on an existing evaluation report. If no report exists for the role, run the pipeline first.

---

## Run the apply command

Open Claude Code in the CareerOps root folder and type one of the following:

```
/career-ops apply company_name
```

For example:

```
/career-ops apply Anthropic
```

CareerOps finds the matching report in `reports/`, uses Playwright to open a browser window, and reads the form. It then generates an answer for every field — ready to copy and paste. You do not need to open the browser yourself.

> **Note:** If Playwright is not available, CareerOps falls back to WebFetch to read the form. See [Set up Playwright](set-up-playwright.md) if you want to enable the full browser-based experience.

**If you run the command `/career-ops apply` without arguments**, the system prompts you to provide context manually:

| Option                    | How                                                                                      |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| Share a screenshot        | Take a screenshot of the form and share it in the chat. CareerOps reads images directly. |
| Paste the questions       | Copy the form questions as text and paste them into the chat.                            |
| Name the company and role | Type the company name and job title. CareerOps searches `reports/` for the match.        |
| Share the application URL | Paste the URL and CareerOps navigates to the form.                                       |

---

## Fill in the form

The system returns a numbered list of answers — one per form field — that mirrors the order of the form. Go through the list top to bottom and paste each answer into the corresponding field.

The output has two parts:

**Answers** — every field on the form, in order:

```
1. Name
   Andres Urdaneta

2. Email
   andres@example.com

...

12. Cover Letter (optional)
    I've spent 5+ years shipping production Rails applications...
```

Simple fields like name, email, and yes/no questions come first. Free-text fields like the cover letter come at the end.

**Key notes** — a short block after the answers with anything worth flagging before you submit:

```
Key notes:
- No salary field — you'll negotiate at offer. Anchor to $160K–$175K at offer stage.
- Add github.com/yourhandle to your resume PDF before uploading.
- Cover letter is optional but the draft above is tight — worth including.
```

Each answer is built from a specific part of your evaluation report:

| Field type                    | Source                                                |
| ----------------------------- | ----------------------------------------------------- |
| Cover letter, "why this role" | Proof points from Block B + STAR stories from Block F |
| Short free-text questions     | Most relevant proof point or story for that question  |
| Dropdowns, yes/no             | Direct answers pulled from your profile               |

**Upload fields:** Use the file in `output/` generated when the report was created. If no PDF exists yet, run `/career-ops pdf` first, then return to the form. See [Generate a PDF](generate-a-pdf.md).

---

## Submit the application

Review every answer, then submit the form yourself. CareerOps does not click Submit.

After submitting, confirm in the chat:

> "Submitted."

CareerOps will:

1. Update `data/applications.md` — changing the status from `Evaluated` to `Applied`
2. Save the final answers to Section G of the report for future reference

---

## What to do next

| Score             | Next step                                                                                                                                                                                        |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **4.0 or higher** | Run `/career-ops contacto`. CareerOps finds a hiring manager or team member on LinkedIn and drafts an outreach message. Sending it before your application is reviewed improves your visibility. |
| **Any score**     | Run `/career-ops tracker` to see the current status of everything in your pipeline.                                                                                                              |
