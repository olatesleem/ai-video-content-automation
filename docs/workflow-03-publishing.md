# Workflow 03 — Create Video Post

**Export:** `workflows/social-media-publishing/workflow.json`

## Purpose

Reads a record from the Content calendar Google Sheet, retrieves Postiz integration information, creates a post through Postiz, and updates the spreadsheet.

## Important behavior in the supplied export

The Postiz node's title and caption are hardcoded values in the supplied JSON. They are not dynamically populated from the spreadsheet in this export. If dynamic post copy is required, update the Postiz node mappings and test them before enabling the workflow.

The workflow also uses sheet fields for video ID/path information. Confirm those columns and the exact asset format expected by Postiz.

## Configuration

1. Reconnect Google Sheets and Postiz credentials.
2. Replace `REPLACE_WITH_CONTENT_CALENDAR_SHEET_ID` with your spreadsheet ID.
3. Confirm the Content calendar tab and expected columns.
4. Re-select the correct Postiz integrations and social destinations.
5. Review the schedule trigger and its interval configuration in n8n.
6. Test with a private/test social destination before enabling production posting.

## Duplicate-posting caution

Workflow 02 also contains social-publishing nodes. Do not enable both publishing routes for the same content unless you have confirmed that their triggers, row filters, and idempotency controls prevent duplicate posts.
