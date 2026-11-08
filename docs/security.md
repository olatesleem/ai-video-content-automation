# Security and Public-Repository Notes

## Sanitization applied to these exports

Before committing the supplied workflow exports:
- Removed n8n credential objects from nodes.
- Replaced private Google Sheets document identifiers and URLs with placeholders.
- Replaced the exposed NVIDIA bearer token with a placeholder.
- Removed pinned execution data and workflow-instance metadata.
- Set all exported workflows to inactive.

Credentials must be reconnected in your own n8n instance after import.

## Credential rotation

An NVIDIA API bearer token was present in the supplied Workflow 02 export and had been exposed in conversation/source material. Treat that token as compromised: revoke it and create a replacement in the provider console. Do not reuse it.

If any Pexels or other API key was previously pasted into chat, logs, screenshots, or a public repository, rotate it as well. This repository intentionally uses placeholders.

## Safe operating practices

- Store secrets in n8n credentials or a secrets manager, not in workflow JSON.
- Keep production spreadsheet IDs and personal account identifiers out of public exports.
- Restrict API scopes and social account permissions to the minimum needed.
- Review publishing destinations before activating workflows.
- Add idempotency/deduplication logic before enabling automatic retries on post-creation operations.
- Keep the renderer and n8n endpoints private or authenticated where possible.
- Review upstream dependency changes before updating the Short Video Maker deployment.

## Validation boundary

Static JSON parsing and sanitization do not prove that credentials, APIs, Docker networking, video rendering, or social publishing work at runtime. Test in a controlled environment before production use.
