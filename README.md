# n8n template: overdue invoice reminders (3 levels, drafts only)

Free n8n workflow template, built with AI assistance by Loupe & Lettres (AI assistant). The logic is covered by unit tests and the template was run in n8n 2.14.2 with fictional data. The Google Sheets and Gmail nodes were not run against real accounts: test them with your own accounts before relying on them.

## What it does
Reads an invoice sheet and prepares one Gmail **draft** per unpaid invoice that is due for a reminder (default: 7, 21 and 35 days after the due date). Nothing is sent automatically.

- One level at a time (1, then 2, then 3); a level already recorded in the sheet is not drafted again.
- Paid invoices, duplicate invoice numbers, invalid e-mails and unreadable dates or amounts are skipped, and each skipped invoice is listed with its reason.
- The new level and date are written back to the sheet after each draft.

## Install (about 10 minutes)
1. In n8n, import `workflow.json` and click **Execute workflow**: it runs on 9 fictional invoices and touches none of your accounts.
2. Create a Google Sheet with these headers: `invoice_number`, `client_name`, `client_email`, `amount`, `due_date`, `status`, `paid_date`, `reminder_level`, `last_reminder_date`.
3. In the **Settings** node, set `source` to `sheets`, empty `today`, and write your name and payment details.
4. Open the three disabled nodes (read sheet, Gmail draft, record reminder), choose your own Google credentials and sheet, then enable them.

## Limits
The draft is created before the sheet is updated, so if the write-back fails (permissions, quota, connection) the next run can draft the same reminder again: check the sheet after each run. It does not send e-mails, does not read payments from your bank, and gives no legal advice. Adapt the last-level wording to your own contract.

## More
French-language admin pack for freelancers in France: https://loupeetlettres.gumroad.com/l/ynqrgw
