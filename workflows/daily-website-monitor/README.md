# Daily Website Monitor

Runs on a schedule, fetches a list of URLs, converts each to Markdown, detects content changes from the previous run, and sends an email alert when a page has changed. Useful for monitoring competitor pricing, documentation updates, or regulatory pages.

## What you need

- Acrewity API key (free at [acrewity.com](https://acrewity.com)) — used for page fetching and email alerts
- n8n with the `n8n-nodes-acrewity` community node installed

## How to import

1. In n8n go to **Settings > Community Nodes** and install `n8n-nodes-acrewity`
2. Import `workflow.json` via **Workflows > Import from file**
3. Add your Acrewity credential: **Credentials > New > Acrewity API**
4. Update the URLs list and alert email address in the workflow

## How it works

1. **Every Day at 8 AM** — Cron trigger fires daily
2. **URLs to Monitor** — A Set node containing the list of URLs to check
3. **Loop Over URLs** — Iterates through each URL
4. **Fetch Page** — Converts the current page content to Markdown via Acrewity
5. **Detect Changes** — Compares content to the stored previous version using Acrewity's `text_diff`
6. **Send Change Alert** — If changes are detected, sends an email notification via Acrewity

## Configuration

Edit the **URLs to Monitor** node to add your target URLs. Edit the **Send Change Alert** node to set your notification email address and SMTP settings.
