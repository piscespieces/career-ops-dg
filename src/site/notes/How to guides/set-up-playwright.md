---
{"dg-publish":true,"permalink":"/how-to-guides/set-up-playwright/","title":"Set Up Playwright","dg-note-properties":{"title":"Set Up Playwright"}}
---

This guide walks through three setup steps that give CareerOps its browser automation capabilities:

1. Install the Playwright Node package
2. Download the Chromium browser Playwright controls
3. Configure the Playwright MCP so Claude can operate the browser during the apply step

**Before you start:** Complete the [Getting Started](../getting-started.md) guide. Node.js 18 or later must be installed and you must be inside the CareerOps root folder.

---

## Install the Playwright package

Run `npm install` from the CareerOps root folder:

```bash
npm install
```

This installs Playwright and all other project dependencies declared in `package.json`. Skip this step if you already ran it during initial setup.

---

## Download Chromium

Playwright needs its own copy of Chromium to automate. Download it by running:

```bash
npx playwright install chromium
```

This is a one-time step. You do not need to repeat it after `npm` updates.

---

## Configure the Playwright MCP

The Playwright MCP lets Claude control the browser directly during the `/career-ops apply` step — navigating to job application forms, reading field labels, and suggesting answers.

### Register the MCP server

Run this command from anywhere to register the Playwright MCP with Claude Code:

```bash
claude mcp add playwright npx @playwright/mcp@latest
```

This is the one-step registration method from the [Playwright MCP docs](https://playwright.dev/docs/getting-started-mcp). It writes the server entry to your Claude settings automatically.

### Manual configuration (alternative)

If you prefer to configure it by hand, add the following entry to `.claude/settings.local.json` in the CareerOps root, or your global Claude settings:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["y", "@playwright/mcp@latest"]
    }
  }
}
```

Restart Claude Code after saving the file. CareerOps will then have access to `browser_navigate` and `browser_snapshot` during apply sessions.

---

## Verify the setup

Run the doctor script to confirm all three components are in place:

```bash
npm run doctor
```

Look for confirmation that Playwright, Chromium, and the MCP server are all ready. If the check passes, setup is complete.

---

## Watch the browser fill out the form

By default, Playwright runs in headless mode — it reads and fills the form in the background without opening a visible window.

To watch the browser open and fill out the form live, add an instruction to the apply command:

```
/career-ops apply [company_name] open up with playwright the browser and fill out the entire form
```

For example:

```
/career-ops apply Anthropic open up with playwright the browser and fill out the entire form
```

Without that instruction, CareerOps still uses Playwright and the MCP — it just operates silently in the background.

---

## What each component enables

| Component          | Purpose                                                                                                           |
| ------------------ | ----------------------------------------------------------------------------------------------------------------- |
| Playwright package | Core library that drives browser automation                                                                       |
| Chromium           | Renders pages, generates print-quality PDFs via `/career-ops pdf`, and checks whether job postings are still live |
| Playwright MCP     | Allows CareerOps to navigate forms and suggest field answers during `/career-ops apply`                           |
