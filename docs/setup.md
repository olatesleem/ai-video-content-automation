# Setup guide

This guide describes the expected service categories. Exact versions, node settings, environment variables, and endpoint paths should be taken from the reviewed workflow export and the deployment being used.

## Prerequisites

- An n8n instance
- A Google account and a Google Sheets content queue
- Pexels API access
- Kokoro TTS service access
- A running Short Video Maker service
- A Postiz instance with the intended social account connected
- API credentials and webhook configuration for the integrations actually used

## Configuration checklist

1. Import the sanitised workflow JSON into n8n.
2. Recreate required credentials inside n8n. Do not paste secrets into workflow notes or this repository.
3. Confirm the Google Sheets document and expected columns.
4. Confirm the Pexels API credential and permitted request limits.
5. Confirm the Kokoro TTS endpoint and voice configuration.
6. Confirm the Short Video Maker endpoint and required input format.
7. Confirm Postiz connectivity and the target publishing account.
8. Run a test using non-sensitive sample content before enabling scheduled or unattended execution.

## Before running unattended

- Add error handling and notifications for failed service calls.
- Confirm duplicate prevention and the workflow's retry behaviour.
- Check API quotas, service availability, and publishing permissions.
- Keep a record of generated output and publishing status.
- Review each external service's terms and content rights.

## Not yet specified

The public documentation does not yet include exact endpoint URLs, node-by-node settings, sheet column names, or a tested import procedure. Those details should be added only after reviewing the current workflow export.
