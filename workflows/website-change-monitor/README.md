# Monitor website changes from a Google Sheets watchlist and email a daily summary

Know when competitor pricing pages, supplier terms, docs, or client sites change — without checking them by hand.

## Who's it for

Anyone who needs to watch web pages for changes: founders tracking competitors, agencies watching client sites, buyers watching supplier terms.

## How it works

1. Runs every morning on a schedule
2. Reads your watchlist from a Google Sheet (`URL, Label, LastHash` columns)
3. Fetches each page as clean markdown with the Acrewity community node (JavaScript-rendered pages work too)
4. Compares a content hash against the stored one to detect changes
5. Emails one digest listing every changed page via Gmail
6. Writes the new hashes back to the sheet, so tomorrow compares against today

The watchlist lives in the sheet, so you add or remove pages without touching the workflow. The first run stores hashes and reports pages as newly tracked; real change alerts start from the second run. Failed fetches are skipped safely without corrupting stored hashes.

## Requirements

- n8n with the verified community node `@acrewity/n8n-nodes-acrewity` installed
- Acrewity API key — free at [acrewity.com](https://acrewity.com) (100 free credits/month, 1 credit per page check)
- Google Sheets and Gmail credentials connected in n8n

## How to set up

1. Create a sheet with columns: `URL, Label, LastHash` (leave LastHash empty — the workflow fills it)
2. Import `workflow.json` (Workflows > Import from file)
3. Add credentials: Acrewity on "Fetch page as markdown", Google Sheets on both sheet nodes, Gmail on the digest node
4. Pick your spreadsheet in both Sheets nodes
5. Set your notification address in "Workflow configuration"
6. Activate

## How to customize

Change the schedule time in the trigger, or swap the Gmail digest for Slack or Telegram.
