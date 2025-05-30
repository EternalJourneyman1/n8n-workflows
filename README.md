# n8n Template: Google Sheet Filter & Gmail Sender

## Description
This n8n workflow template triggers on new rows in a Google Sheet, filters those rows based on custom criteria defined in a Code node, and then sends a customizable email via Gmail for each filtered row.

## Features
- Triggers on new Google Sheet rows.
- Customizable JavaScript filter for rows.
- Sends emails via Gmail.
- Includes a generic HTML email body template.

## Prerequisites
- n8n instance (tested on version X.Y.Z)
- Google Sheets API enabled for your Google Cloud Project.
- Gmail API enabled for your Google Cloud Project.
- Valid OAuth2 credentials for Google Sheets and Gmail within n8n.

## Setup Instructions

1.  **Import Workflow:** Download the `workflow.json` file from this folder and import it into your n8n instance.
2.  **Configure Node 1: Google Sheets Trigger ('Trigger: New Google Sheet Row')**
    * **Credential:** Select or create your Google Sheets OAuth2 credential.
    * **Document:** Choose your target Google Spreadsheet.
    * **Sheet:** Select the specific sheet name to monitor.
    * *(Optional)* Adjust 'Poll Times' and 'Trigger On' settings.
3.  **Configure Node 2: Code Node ('Custom Code: Filter...')**
    * This node filters rows. By default, it might be set up to filter rows where a specific column (e.g., 'Student ID') is empty.
    * **To Customize:** Edit the JavaScript. The key filter logic is typically a line like `!item.json['Your Column To Check']`.
        * Replace `'Your Column To Check'` with the actual column name from your sheet.
        * Adjust the condition as needed.
    * **Alternative:** For simpler filtering, you can replace this Code node with a standard n8n 'IF' or 'Filter' node.
4.  **Configure Node 3: Gmail Node ('Send Email to Recipient (from Row)')**
    * **Credential:** Select or create your Gmail OAuth2 credential.
    * **To:** Ensure the 'To' field correctly maps to your email column (e.g., `{{ $json['Email Column Name'] }}`).
    * **Subject:** Customize the email subject line. You can use expressions like `{{ $json['Column Name'] }}`.
    * **Message (HTML):** Edit the HTML body. Use expressions like `{{ $json['Column Name'] }}` to insert data. Refer to the comments in the HTML for where to place your specific column names.

## Customizing the Email Body
The HTML email body is designed to be generic. You will need to:
- Update placeholder labels (e.g., `[Identifier Field Label]:`).
- Change data expressions `{{ $json['[Your Column Name Here]'] }}` to use your actual column names from the Google Sheet.
- Modify the "Action Required / Next Steps" list to fit your process.

---

*(Optional: Add sections for Troubleshooting, Example Data, etc.)*
