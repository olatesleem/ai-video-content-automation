# Social-media publishing workflow

**Export:** `workflows/social-media-publishing/workflow.json`

## Purpose

Publish a prepared video post through Postiz and update the associated Google Sheets content-calendar row.

## Main stages

1. **Schedule:** `Schedule Trigger` starts the publishing workflow. The exported schedule contains multiple interval entries, including repeated 10-minute intervals; review this configuration before activation.
2. **Read content row:** `Google Sheets - Read Row` reads from the content calendar using the `TIKTOK STATUS` column as its configured lookup field. Confirm the filter value and returned-row behaviour in your own sheet.
3. **Find publishing destination:** `Postiz1` retrieves available Postiz integrations.
4. **Create post:** `Postiz2` uses the selected integration and video asset ID/path from the spreadsheet to submit a post. The exported node contains example copy and a fixed date; replace these with the intended row-driven values or desired schedule.
5. **Update status:** `Update row in sheet1` matches the row by `ID` and sets `TIKTOK STATUS` to `POSTED`.

## Configuration required

- Reconnect Google Sheets and Postiz credentials.
- Replace the `YOUR_GOOGLE_SHEET_ID` placeholder.
- Confirm the sheet tab and the exact field names, especially `TIKTOK STATUS`, `ID`, `postis video ID` and `postis video Path`.
- Ensure the row-selection logic returns only content ready to publish.
- Replace the sample caption/title and fixed post date before activating.
- Test the Postiz integration and confirm the resulting post status before relying on the spreadsheet update.

## Export status

The original export contains six nodes, including one disabled manual trigger. The public copy preserves the original node graph and disabled trigger, removes credential references and spreadsheet identifiers, and is set inactive.
