# AI Video Content Automation

An n8n-based content production system that turns spreadsheet-driven health-education ideas into voiceover-led short-form videos and supports social publishing.

This repository contains three separate workflow exports:

| Workflow | Purpose |
|---|---|
| 01 — Generate Video Voiceover | Develops a health-content concept and voiceover, then stores the generated metadata in Google Sheets. |
| 02 — Generate Video from the Voiceover | Reads a voiceover record, prepares scene and visual-search data, calls the Short Video Maker service to render a video, and includes social-publishing nodes. |
| 03 — Create Video Post | Reads video/post data from the Content calendar sheet, uses Postiz integrations to create a social post, and updates the sheet. |

## Repository structure

```text
workflows/
  Generate Video Voiceover.json
  Generate video from the voiceover.json
  social-media-publishing/
    workflow.json
docs/
  architecture.md
  workflow-01-voiceover.md
  workflow-02-video-generation.md
  workflow-03-publishing.md
  setup.md
  security.md
```

## Architecture at a glance

1. A content idea is processed by Workflow 01 to produce a structured concept and voiceover.
2. Workflow 02 consumes voiceover data, prepares visual scenes/search terms, and sends a rendering payload to the separately deployed Short Video Maker service.
3. Workflow 02 also contains social-publishing functionality. Workflow 03 is an additional Postiz-based publishing workflow that reads from the Content calendar sheet. These are distinct publishing paths; this repository does not assume they are automatically chained together.

## Requirements

- A running n8n instance compatible with the exported node versions.
- Google Sheets credentials and the relevant spreadsheet structures.
- The AI provider credentials used by the workflows.
- A reachable Short Video Maker service for video rendering.
- Postiz account/integrations for Workflow 03.
- API credentials required by any enabled external services.

The exports are sanitized for public sharing. They do not include your live credentials or private spreadsheet IDs. Configure placeholders and reconnect credentials after importing.

## Import and configure

1. Download or clone this repository.
2. In n8n, import each JSON file separately.
3. Reconnect credentials for Google Sheets, AI providers, HTTP services, and Postiz where applicable.
4. Replace the Google Sheets document placeholders with your own spreadsheet IDs and confirm sheet/tab names and column mappings.
5. Configure the Short Video Maker endpoint so it is reachable from the n8n runtime.
6. Review every publishing node, account integration, destination, and schedule before enabling a workflow.
7. Test with a non-public test record before activating production runs.

See [setup guide](docs/setup.md), [architecture](docs/architecture.md), and [security notes](docs/security.md).

## External rendering dependency and attribution

The Short Video Maker deployment is based on the upstream project [gyoridavid/ai_agents_az](https://github.com/gyoridavid/ai_agents_az). That upstream implementation is not authored by this repository owner. This project documents its use as an external rendering dependency and the integration from n8n.

## Project status and validation

The workflow JSON files were parsed and sanitized before being committed. Credential objects and private spreadsheet identifiers were removed/replaced, and the exports were left inactive. This is a static export validation only: no live n8n execution, API connectivity, rendering, or social publishing test is claimed.

## Important limitations

- Workflow 03 currently contains hardcoded post title and caption values in its Postiz node. Those fields are not dynamically mapped from the spreadsheet in the supplied export.
- Workflow 02 has its own publishing nodes, so review both publishing paths to avoid unintended duplicate posts.
- Google Sheets placeholders must be configured consistently across the workflows.
- Imported workflows may require node-version compatibility adjustments in your n8n instance.
