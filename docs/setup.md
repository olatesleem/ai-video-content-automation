# Setup Guide

This guide covers the configuration required after importing the sanitized workflow exports. It does not claim that the user's live infrastructure has been independently tested.

## 1. Import the workflows

Import each JSON export separately into n8n:
- `workflows/Generate Video Voiceover.json`
- `workflows/Generate video from the voiceover.json`
- `workflows/social-media-publishing/workflow.json`

The exports are inactive. Keep them inactive while reconnecting credentials and checking mappings.

## 2. Reconnect credentials

Create/select credentials in n8n for each service used by the nodes:
- Google Sheets
- AI model/provider APIs
- Pexels or other HTTP services used for visual search
- Postiz
- Any additional APIs referenced by enabled nodes

Do not paste API keys directly into node parameters or commit them to this repository.

## 3. Configure Google Sheets

Replace placeholders in the imported nodes:
- `REPLACE_WITH_VOICEOVER_SHEET_ID`
- `REPLACE_WITH_CONTENT_CALENDAR_SHEET_ID`

Confirm spreadsheet tab names, column names, row IDs, and read/update operations. The exports refer to separate voiceover and Content calendar sheets.

## 4. Configure the Short Video Maker service

Workflow 02 calls a separately deployed Short Video Maker service. The user's deployment notes identify the upstream project as [gyoridavid/ai_agents_az](https://github.com/gyoridavid/ai_agents_az), using the `episode_7` project area and a Docker service exposed on port `3123`.

The following are the user's supplied configuration notes, not independently verified deployment instructions:
- Docker image: `gyoridavid/short-video-maker:latest-tiny`
- Container name: `short-video-maker`
- Port mapping: `3123:3123`
- Data directory mounted at `/app/data`
- Environment configuration noted: `LOG_LEVEL=debug`, `DATA_DIR_PATH=/app/data`, `DOCKER=true`, `WHISPER_MODEL=tiny.en`, `KOKORO_MODEL_PRECISION=q4`, `CONCURRENCY=1`, and `VIDEO_CACHE_SIZE_IN_BYTES=2097152000`
- Pexels API key supplied through a secure environment variable
- Docker network noted as `n8n_default`

The exact command sequence and Whisper installation details can vary with the upstream project version. Follow the upstream repository's current instructions and verify the service health endpoint/logs before connecting n8n. Do not assume a host path, container network, or service URL without checking your deployment.

## 5. Review publishing

Workflow 02 includes publishing nodes, and Workflow 03 publishes through Postiz. Review the destinations, media fields, captions, scheduling, and retry behavior. Workflow 03 currently has hardcoded title/caption values in the supplied export.

## 6. Test and activate

1. Run one test record through each workflow separately.
2. Verify sheet updates and rendered video output.
3. Verify that retries do not create duplicate posts.
4. Publish to a private/test destination.
5. Enable production triggers only after all checks pass.
