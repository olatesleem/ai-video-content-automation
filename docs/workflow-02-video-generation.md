# Workflow 02 — Generate Video from the Voiceover

**Export:** `workflows/Generate video from the voiceover.json`

## Purpose

Consumes voiceover information, prepares scene-level visual inputs, calls the Short Video Maker service to render a video, and updates workflow/sheet records. The supplied export also contains social-publishing nodes.

## Main stages represented

- Read the source voiceover row from Google Sheets.
- Prepare four scenes and generate Pexels search terms.
- Build the payload expected by the Short Video Maker service.
- Call the external rendering service.
- Process the result and update spreadsheet/status fields.
- Execute the publishing functionality included in this workflow, where configured.

## External rendering dependency

The renderer is based on [gyoridavid/ai_agents_az](https://github.com/gyoridavid/ai_agents_az). The upstream repository and its author retain attribution for that implementation. This project documents the deployment/integration, not authorship of the upstream code.

The service must be reachable from the n8n runtime. A host-local URL such as `localhost` inside a container may refer to the n8n container itself, not the renderer; configure the correct Docker service/network hostname or reachable host address.

## Configuration

1. Reconnect Google Sheets and AI provider credentials.
2. Replace `REPLACE_WITH_VOICEOVER_SHEET_ID` and `REPLACE_WITH_CONTENT_CALENDAR_SHEET_ID` with your own sheet IDs where referenced.
3. Reconnect Pexels or other HTTP/API credentials using n8n credentials or secure environment variables.
4. Configure the Short Video Maker endpoint and required request fields.
5. Confirm output paths/URLs and that n8n can access the rendered asset.
6. Review every publishing node and destination before activation.

## Safety

The workflow export is inactive. Test rendering with a private/test destination first. Since this workflow has publishing functionality and Workflow 03 is a separate publisher, coordinate activation to avoid duplicate posts.
