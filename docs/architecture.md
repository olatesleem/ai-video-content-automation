# System Architecture

## Workflow sequence and boundaries

```text
Content idea / source row
        |
        v
01 — Generate Video Voiceover
        |
        | structured concept, voiceover and metadata
        v
Google Sheets (voiceover data)
        |
        v
02 — Generate Video from the Voiceover
        |
        | read voiceover, prepare scenes and visual search data
        v
Short Video Maker service (external rendering dependency)
        |
        | rendered video / result metadata
        v
Google Sheets and workflow status updates
        |
        +----> Social publishing nodes contained in Workflow 02

Content calendar Google Sheet
        |
        v
03 — Create Video Post
        |
        v
Postiz integrations
        |
        v
Social post + spreadsheet status update
```

The diagram shows the roles represented in the supplied exports. It does not imply that Workflow 02 automatically triggers Workflow 03, or that every sheet update is a direct trigger for the next workflow. Confirm the actual trigger and row-selection conditions in n8n after import.

## Workflow responsibilities

- **Workflow 01:** generates a health-education content concept and voiceover, then stores metadata in Google Sheets.
- **Workflow 02:** reads voiceover information, prepares four-scene video inputs and Pexels search terms, builds a Short Video Maker payload, requests rendering, and contains additional publishing/status-update nodes.
- **Workflow 03:** reads a row from the Content calendar, resolves Postiz integrations, creates a post, and updates the spreadsheet.

## External service

Video rendering is delegated to a separately deployed service based on [gyoridavid/ai_agents_az](https://github.com/gyoridavid/ai_agents_az). The n8n workflow integrates with that service; it is not a reimplementation of the upstream renderer.

## Operational considerations

- Keep rendering and publishing responsibilities observable as separate stages.
- Use stable row identifiers and idempotency controls when retrying operations that create posts.
- Verify the rendered asset URL/path before handing it to a publishing node.
- Review schedule triggers and publishing destinations before activation.
- Both Workflow 02 and Workflow 03 include publishing functionality. Coordinate them to prevent duplicate publication.
