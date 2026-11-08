# Social Media Publishing Automation

This project has two publishing routes:

1. Publishing nodes embedded in Workflow 02.
2. Workflow 03, which reads a row from the Content calendar Google Sheet and publishes through Postiz.

## Workflow 03 — Postiz

The Postiz title and caption/content are dynamically mapped from the row returned by `Google Sheets - Read Row`:

- Post title: `Title`
- Post caption/content: `Content ` (note the trailing space in the supplied column name)

The workflow also reads the video asset identifier and path from `postis video ID` and `postis video Path`.

Check the sheet headers carefully. If the actual caption column is named `Content` without a trailing space, edit the n8n expression to match the actual header. The row's Content field should contain the caption and hashtags intended for publication.

## Before enabling

- Reconnect Google Sheets and Postiz credentials.
- Verify the correct Postiz integration and social destination.
- Confirm video ID/path values are valid and accessible to Postiz.
- Review the schedule trigger and row filtering.
- Test against a private/test destination.
- Ensure Workflow 02 and Workflow 03 cannot publish the same content twice.

The repository exports are inactive. Static JSON validation does not verify live Postiz behavior.
