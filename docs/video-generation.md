# Video generation and voiceover workflow

**Export:** `workflows/video-generation-voiceover/workflow.json`

## Purpose

Prepare short-form health-education video concepts and narration from a topic in a Google Sheets content queue. The second AI agent expands the concept into four connected visual prompts and a complete voiceover.

## Main stages

1. **Queue intake:** the schedule trigger starts the workflow and `Get row(s) in sheet` reads a content item.
2. **Concept generation:** `AI Agent3` receives the topic from the `Content ` field. Its prompt requests a hook, problem, actionable health tip, explanation, benefit, visual story, environment, style, palette, camera, lighting, mood, sound, title, caption and voiceover.
3. **Structured output and storage:** the structured output parser validates the concept response; `Save Idea & Metadata to Google Sheets1` appends the concept and metadata.
4. **Scene prompt preparation:** `Set Master Prompt1` defines the master prompt template, the model label `Wan 2.2`, and `9:16` aspect ratio.
5. **Voiceover and scene generation:** `AI Agent4` creates four connected scene prompts of approximately 15 seconds each, a combined final prompt, and narration fields. The configured output includes scene-level voiceover and a complete voiceover.
6. **Spreadsheet updates:** `URL Final Video2` writes scene prompts, combined prompt and voiceover fields to the sheet. `Update row in sheet` updates the source row's title and status.

## Model and integration notes

The two active language-model nodes are named `OpenAI Chat Model` and `OpenAI Chat Model1`, but the model identifier in their parameters is `nvidia/llama-3.3-nemotron-super-49b-v1.5`. Credentials are deliberately removed from the public export and must be reconnected on import.

The master prompt sets `Wan 2.2`. Separately, `Format Prompt1` labels its output model `veo3_fast`. That code node is not connected downstream in the supplied graph. Do not assume the two model labels refer to a working, interchangeable rendering configuration.

## Rendering branch: incomplete in this export

The workflow contains nodes named `Generate Video with VEO`, `Wait for VEO3 Rendering1`, `Download Video from VEO`, `Upload file`, and `URL Final Video1`. These are disabled. In addition, the prompt-formatting node does not connect to the generation request, and `Split Out` has no incoming connection.

Consequently, this export supports the concept, scene-prompt and voiceover-preparation stages, but does not demonstrate a completed end-to-end rendered-video pipeline. Reconnect and test the renderer, polling, download, upload and final-URL update before describing it as fully automated video generation.

## Before running

- Reconnect Google Sheets and language-model credentials.
- Replace spreadsheet and workflow ID placeholders.
- Verify the sheet tab and exact column names, including the source field `Content `.
- Check that the queue filter selects the intended row and that status updates cannot mark an incomplete item as done.
- Reconcile Wan 2.2 and `veo3_fast` model configuration.
- Verify the video provider's endpoint, authentication, request schema, job polling response and download URL.
- Validate health-related claims before publication. The prompt asks for generally accepted advice, but the export does not include a dedicated medical-source retrieval or fact-checking stage.

## Export status

The original export contained 27 nodes, 11 disabled. The public portfolio copy preserves those nodes and their disabled state, removes credential references and account-specific identifiers, and sets the workflow inactive for safe import.
