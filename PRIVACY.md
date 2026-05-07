# Privacy And Data Handling

Dreamlit MCP is a hosted remote MCP server for managing Dreamlit workflows.

## What The MCP Server Can Access

Access depends on the scopes granted by the user:

- `workflows:read`: read workflow metadata, project context, setup status, and preview URLs.
- `workflows:write`: create or update workflow drafts and send confirmed draft workflow tests.
- `workflows:publish`: publish, schedule, or unpublish workflows after explicit confirmation.

OAuth grants are scoped to the selected Dreamlit workspace. Personal access tokens are scoped to a Dreamlit project.

## What Not To Send

Do not send secrets through MCP prompts or tool inputs. This includes:

- Database passwords.
- API keys.
- OAuth secrets.
- Personal access tokens.
- Private customer credentials.

Configure integrations and credentials inside the Dreamlit app instead.

## Workflow Tests

Workflow tests send draft email or Slack messages for review. They do not publish, schedule, or edit the workflow draft.

## Revocation

Personal access tokens can be revoked in Dreamlit project settings. If you need help disconnecting an OAuth MCP client, contact `support@dreamlit.ai`.
