# Architecture

This repository contains two separate n8n workflows that cover different parts of a short-form content operation.

## 1. Video generation and voiceover preparation

The active branch in the supplied export is:

```text
Schedule Trigger
  -> Get row(s) in sheet
  -> AI Agent3 (health concept)
  -> Save Idea & Metadata to Google Sheets1
  -> Set Master Prompt1
  -> AI Agent4 (four scenes + narration)
      +-> URL Final Video2 (write prompts/script to Sheets)
      +-> Update row in sheet (update source status/title)
      +-> Format Prompt1 (currently no downstream connection)
```

The first agent uses the queued topic to create a structured health-education concept. The second agent turns the concept into four connected scene prompts, approximately 15 seconds each, and a voiceover script. The master prompt sets a Wan 2.2 label and 9:16 aspect ratio.

## 2. Social-media publishing

```text
Schedule Trigger
  -> Google Sheets - Read Row
  -> Postiz1 (retrieve integrations)
  -> Postiz2 (submit post)
  -> Update row in sheet1 (mark POSTED)
```

This workflow uses a spreadsheet row as the source for the video asset reference and post content, then updates the TikTok status after the Postiz node.

## Boundary between the workflows

The exports are separate. They both use Google Sheets, but the supplied graph does not prove a fully configured hand-off from generated media to the publishing workflow. The operator must ensure that the generated video asset ID/path and the publishing row are populated consistently.

## Rendering branch status

The video workflow contains a separate intended branch involving a video-generation HTTP request, wait/poll, download, Google Drive upload, and final URL update. In the supplied export:
- the generation, wait, download, upload and final-URL nodes are disabled;
- the `Format Prompt1` output is not connected to `Generate Video with VEO`;
- the `Split Out` node has no incoming connection;
- the model naming is inconsistent: the master prompt says Wan 2.2, while the format-code node labels its payload `veo3_fast`.

Treat rendering as unfinished until these points are reconciled and tested.
