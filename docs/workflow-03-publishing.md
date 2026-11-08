# Workflow 03 — Create Video Post

**Export:** `workflows/social-media-publishing/workflow.json`

## Purpose

Reads a record from the Content calendar Google Sheet, retrieves Postiz integration information, creates a post through Postiz, and updates the spreadsheet.

## Dynamic title and caption mappings

The Postiz node now reads both fields from the row returned by **Google Sheets - Read Row**:

- **Post title:** `Title`
- **Post caption/content:** `Content ` (the supplied sheet schema contains a trailing space in this column name)

The expressions are:
- `={{ $('Google Sheets - Read Row').item.json.Title }}`
- `={{ $('Google Sheets - Read Row').item.json['Content '] }}`

Make sure your Google Sheet header is exactly `Title` and `Content ` (including the trailing space on the latter), or update the expression to match your actual header. The caption field should contain the full post copy and hashtags you want sent to Postiz.

## Other media fields

The supplied workflow maps the Postiz video asset from the sheet fields `postis video ID` and `postis video Path`. Confirm those column names and the exact asset format expected by Postiz.

## Configuration

1. Reconnect Google Sheets and Postiz credentials.
2. Replace `REPLACE_WITH_CONTENT_CALENDAR_SHEET_ID` with your spreadsheet ID.
3. Confirm the Content calendar tab and expected columns, including the exact `Title` and `Content ` headers.
4. Re-select the correct Postiz integrations and social destinations.
5. Review the schedule trigger and its interval configuration in n8n.
6. Test with a private/test social destination before enabling production posting.

## Duplicate-posting caution

Workflow 02 also contains social-publishing nodes. Do not enable both publishing routes for the same content unless you have confirmed that their triggers, row filters, and idempotency controls prevent duplicate posts.
