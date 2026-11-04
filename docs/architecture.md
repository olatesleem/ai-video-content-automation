# Architecture

## Purpose

Coordinate the production of faceless short-form videos through connected automation and media services.

## High-level flow

1. **Content queue — Google Sheets**  
   Holds the content records consumed by the workflow. The exact column names and status transitions must be documented from the workflow export.

2. **Orchestration — n8n**  
   Coordinates the process, transfers data between services, and manages the integration steps.

3. **Stock media — Pexels**  
   Supplies candidate stock footage for the video.

4. **Voice generation — Kokoro TTS**  
   Generates narration. The project configuration previously noted voice `af_bella`; confirm this against the current workflow before changing it.

5. **Rendering — Short Video Maker**  
   Receives the selected media and narration and produces the video output.

6. **Publishing — Postiz**  
   Handles the publishing stage, with TikTok as the intended destination.

## Important implementation notes

- Captions are currently disabled in the described configuration.
- This document intentionally does not specify node names, exact payload fields, retry rules, or status updates until they are checked against the exported n8n JSON.
- The diagram in the README is a conceptual view, not an execution trace.
- Add screenshots or a redacted execution example only after removing personal data and credentials.
