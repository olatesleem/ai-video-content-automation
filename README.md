# AI Video Content Automation

An n8n-based workflow for coordinating faceless short-form video production, from a content queue to a rendered video and social publishing.

**Portfolio focus:** workflow orchestration, API integrations, media automation, and repeatable content operations.

## Project overview

This project demonstrates how separate services can be connected into a single content-production pipeline. A spreadsheet acts as the content queue, n8n coordinates the steps, stock footage and text-to-speech provide media assets, a video-rendering service assembles the output, and a publishing service handles the social distribution step.

## Workflow at a glance

```text
Google Sheets
     |
     v
    n8n
     |
     +----> Pexels (stock footage)
     |
     +----> Kokoro TTS (voice generation)
     |
     v
Short Video Maker (video rendering)
     |
     v
Postiz (publishing workflow / TikTok target)
```

The exact node sequence, filters, request payloads, and error-handling behaviour should be confirmed against the sanitised workflow export before being treated as implementation facts.

## Technology stack

| Component | Role |
|---|---|
| n8n | Workflow orchestration and integration logic |
| Google Sheets | Content queue / source data |
| Pexels | Stock-video asset source |
| Kokoro TTS | Voice generation; configured voice noted in the project is `af_bella` |
| Short Video Maker | Video assembly/rendering service |
| Postiz | Social publishing integration; TikTok is the intended target |

Captions are currently switched off in the described setup. No caption-generation or transcription stage is claimed here.

## Skills demonstrated

- Designing multi-step automation workflows
- Connecting services through APIs and webhooks
- Passing structured data between workflow stages
- Coordinating media retrieval, voice generation, rendering, and publishing
- Separating orchestration from specialist media services
- Documenting configuration, dependencies, and operational risks

## Repository contents

- [Architecture](docs/architecture.md) — system components and data flow
- [Setup guide](docs/setup.md) — deployment prerequisites and configuration approach
- [Security notes](docs/security.md) — credential handling and safe sharing

## Current project status

This repository is the documentation and portfolio home for the workflow. The public workflow export and node-by-node implementation notes will be added after the exported JSON has been reviewed and sanitised.

**Validation status:** not independently tested from this repository. Do not interpret the architecture diagram as proof that every integration is currently running.

## Security

Never commit API keys, access tokens, passwords, private webhook URLs, session cookies, or personal account identifiers. Use n8n credentials or environment variables for secrets. See [Security notes](docs/security.md).

## About

Built as a practical portfolio project by **Yesy121**, showcasing applied AI automation and workflow development.
