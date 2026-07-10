# Send quote PDFs from form submissions and follow up automatically

Turn quote requests into sent quotes in seconds — and never forget the follow-up.

## Who's it for

Freelancers, agencies, and service businesses that receive quote requests and lose deals by replying late or forgetting to follow up.

## How it works

1. A prospect fills out the built-in n8n form (no external form tool needed)
2. The workflow builds a professional quote and renders it to PDF with the Acrewity community node
3. The quote is emailed to the prospect via Gmail within seconds of the request
4. After a configurable delay (default 3 days) a polite follow-up email referencing the quote number is sent automatically

## Requirements

- n8n with the verified community node `@acrewity/n8n-nodes-acrewity` installed
- Acrewity API key — free at [acrewity.com](https://acrewity.com) (100 free credits/month, 1 credit per PDF)
- Gmail credential connected in n8n

## How to set up

1. Import `workflow.json` (Workflows > Import from file)
2. Add your Acrewity API credential to the "Convert quote to PDF" node
3. Add your Gmail credential to both email nodes
4. Edit the "Workflow configuration" node: company name, sender name, quote validity, follow-up delay
5. Activate the workflow and share the form URL shown on the trigger node

## How to customize

- Edit the form fields in the trigger node
- Change the quote layout in "Build quote HTML"
- Adjust both email texts in the Gmail nodes
- Add an If node before the follow-up to skip prospects who already replied, or a CRM node to log every lead
