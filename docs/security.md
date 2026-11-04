# Security and safe sharing

This repository is public. Treat every committed file as visible to anyone.

## Never commit

- API keys, bearer tokens, OAuth refresh/access tokens, or passwords
- n8n credential exports or encryption keys
- Private webhook URLs or URLs containing secret query parameters
- Session cookies or authorization headers
- Personal email addresses, phone numbers, private social account identifiers, or customer data
- Real production content that is confidential or personally identifying

## Safe workflow export process

1. Export the workflow JSON from n8n.
2. Inspect every node, parameter, header, URL, expression, and sticky note.
3. Remove credentials and replace private values with placeholders such as `YOUR_API_KEY`.
4. Remove personal data and private account identifiers.
5. Check that no secret is embedded in a URL, expression, or example payload.
6. Import the redacted file into a test n8n environment, if possible, to ensure the redaction has not broken the structure.
7. Commit only the sanitised version.

## If a secret is exposed

Revoke or rotate it at the provider immediately. Removing it in a later commit does not make the exposed secret safe; it may remain in Git history.

## Credential management

Store credentials in n8n's credential manager or an appropriate secret manager. Use environment variables for deployment configuration where suitable. Keep production credentials separate from test credentials.
