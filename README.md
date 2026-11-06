# AI Video Content Automation

An n8n portfolio project for AI-assisted short-form health video planning, voiceover scripting, scene-prompt generation, and social publishing.

**Portfolio focus:** AI agent orchestration, structured outputs, spreadsheet-driven workflows, API integrations, workflow state tracking, and social-media operations.

## Project overview

The repository contains two distinct workflows:

1. **Video generation and voiceover preparation** — reads a queued content topic, drafts a health-education concept, creates a voiceover, and prepares four connected vertical-scene prompts with a combined prompt.
2. **Social-media publishing** — reads a content-calendar row, retrieves Postiz integrations, submits a video post, and updates the TikTok status in the sheet.

These are separate workflow exports. The current exports do not establish a fully connected, automatic hand-off from the video-generation workflow to the publishing workflow; they share a spreadsheet-oriented operating model, but the integration between the two should be verified/configured in the user's n8n instance.

## Workflow architecture

```text
CONTENT QUEUE (Google Sheets)
          |
          v
   n8n video preparation
          |
          +--> AI concept + health tip
          |
          +--> Structured concept metadata
          |
          +--> Four scene prompts + voiceover
          |
          +--> Write prompts/script to Sheets

SEPARATE PUBLISHING WORKFLOW
          |
          +--> Read publishing row from Sheets
          +--> Retrieve Postiz integrations
          +--> Submit post with stored video asset reference
          +--> Mark TikTok status as POSTED
```

The scene-prompt workflow contains disabled and disconnected video-rendering nodes. The public export therefore documents the prompt/voiceover preparation stage and the intended rendering branch, but it should not be represented as a fully operational end-to-end renderer until that branch is reconnected and tested.

## Repository structure

- [Video generation and voiceover workflow](workflows/video-generation-voiceover/workflow.json)
- [Social publishing workflow](workflows/social-media-publishing/workflow.json)
- [Video generation notes](docs/video-generation.md)
- [Publishing notes](docs/publishing-automation.md)
- [Architecture](docs/architecture.md)
- [Setup guide](docs/setup.md)
- [Security notes](docs/security.md)

## Technology and integrations visible in the exports

- n8n for workflow orchestration
- Google Sheets for content queue, metadata, voiceover and status tracking
- AI Agent and structured-output parser nodes for concept and scene generation
- OpenAI-compatible chat model nodes configured with the model identifier `nvidia/llama-3.3-nemotron-super-49b-v1.5`
- Wan 2.2 named in the master prompt configuration
- Postiz for social publishing
- Google Drive, HTTP video-generation and WhatsApp nodes are present in the video workflow export but disabled

The workflow also contains a dormant `veo3_fast` model label in a code node. This conflicts with the Wan 2.2 configuration and needs to be reconciled before the rendering branch is activated.

## Import and configuration

1. Import the relevant JSON into your n8n instance.
2. Reconnect Google Sheets, model-provider, Postiz, Google Drive, HTTP-auth and WhatsApp credentials as required.
3. Replace the `YOUR_GOOGLE_SHEET_ID` and `YOUR_WORKFLOW_ID` placeholders with your own resource identifiers.
4. Confirm sheet tabs, column names, row filters, schedule rules, Postiz integration, posting date and media references.
5. Keep the workflow inactive while configuring and testing. The public exports are intentionally inactive.

See [Setup](docs/setup.md) and [Security](docs/security.md).

## Validation and limitations

- Both exported JSON files were parsed and checked for unique node names and references to missing connection targets.
- Credential objects and account-specific spreadsheet/workflow identifiers were removed or replaced with placeholders.
- Disabled nodes were preserved, not deleted, so the export retains the original design intent.
- The exports have not been executed against live services. JSON and connection-graph checks are not proof of runtime correctness.
- The video-generation branch is incomplete in the exported graph: the prompt-formatting output is not connected to the video-generation request, and the rendering/download/upload nodes are disabled.
- The publishing workflow contains a fixed sample post date and sample caption; review these before use.

## About

Built by **Ola Tesleem** as a practical portfolio project demonstrating applied AI automation and n8n workflow development.
