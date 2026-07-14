# Generate and email PDF invoices from new Google Sheets orders

Every new order row becomes a professional PDF invoice — emailed to the customer, archived in Drive, and marked done in the sheet.

## Who's it for

Small businesses and freelancers who track orders in a Google Sheet and still assemble invoices by hand.

## How it works

1. Watches your Orders sheet for new rows
2. Builds a styled HTML invoice from the row data (line items, tax, totals)
3. Converts it to PDF with the Acrewity community node
4. Emails the PDF to the customer via Gmail and archives a copy in Google Drive
5. Writes Status = Invoiced back to the row so nothing is billed twice
6. Rows with bad data (broken Items JSON, a missing item name, no email address) never stop the batch — the other rows still get invoiced, and the bad row's Status column receives the error message so you can fix it in the sheet

## Requirements

- n8n with the verified community node `@acrewity/n8n-nodes-acrewity` installed
- Acrewity API key — free at [acrewity.com](https://acrewity.com) (100 free credits/month, 1 credit per PDF)
- Google Sheets, Gmail, and Google Drive credentials connected in n8n

## How to set up

1. Create an Orders sheet. Paste this line into cell A1 — it fills the whole header row at once:

   ```
   Order Number	Customer Name	Customer Email	Customer Address	Items	Due Date	Notes	Status
   ```

   - `Items` holds a JSON array, e.g. `[{"name":"Widget","quantity":2,"price":9.99}]` — this is the only column with a special format
   - `Due Date`, `Notes`, and `Customer Address` may be empty; `Status` starts blank and the workflow fills it
   - If a row runs with the header missing, the workflow stops with an error telling you exactly which columns to add
2. Import `workflow.json` (Workflows > Import from file)
3. Add credentials: Acrewity on "Convert HTML to PDF", Gmail on the email node, Google Sheets on the trigger and both order-update nodes, Google Drive on the archive node
4. Pick your spreadsheet in the trigger and both Sheets nodes, and your archive folder in the Drive node
5. Edit "Set Workflow Configuration": company name, logo URL, tax rate, currency
6. Activate — every new row is now invoiced automatically

## How to customize

Change the invoice layout in "Create Invoice HTML", adjust the email copy in the Gmail node, or add a Slack notification after the Drive archive step.
