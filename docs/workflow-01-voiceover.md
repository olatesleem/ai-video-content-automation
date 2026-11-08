# Workflow 01 — Generate Video Voiceover

**Export:** `workflows/Generate Video Voiceover.json`

## Purpose

Creates a structured health-education video concept and voiceover from content supplied through Google Sheets, then saves generated metadata to a sheet.

## Generated content

The supplied workflow's prompt/output structure covers elements such as:
- Hook and problem
- Health tip and why it works
- Benefit
- Visual story and environment
- Style, palette, camera, lighting, and mood
- Voiceover, sound, and caption

The workflow uses an AI agent and structured-output parsing before writing the generated information to Google Sheets.

## Configuration

After importing:
1. Reconnect the Google Sheets credential.
2. Replace `REPLACE_WITH_VOICEOVER_SHEET_ID` with the ID of your own spreadsheet.
3. Confirm the target tab, columns, and row-selection logic.
4. Reconnect the AI provider credential and verify the selected model.
5. Test with one non-production content row.

The export has been left inactive. Review the nodes and mappings before activation.
