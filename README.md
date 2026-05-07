# Dreamlit MCP

Dreamlit MCP lets AI clients create, inspect, test, publish, and unpublish Dreamlit notification workflows.

Dreamlit is a database-driven notification workflow platform for Supabase and Postgres apps. Use this MCP server when you want an AI client to help build notification workflows from outcome-oriented prompts, then review and publish them through Dreamlit.

## Server

- Production MCP URL: `https://mcp.dreamlit.ai/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth, with personal access token fallback for clients that do not support OAuth

This repository contains public setup docs and MCP registry metadata for Dreamlit's hosted remote MCP server. The production backend implementation is not open source.

## Quick Start

Use your MCP client's remote server flow and enter:

```text
https://mcp.dreamlit.ai/mcp
```

The client should open a Dreamlit authorization page. Choose the workspace you want the AI client to access and approve the requested scopes.

### Codex CLI

```sh
codex mcp add dreamlit --url https://mcp.dreamlit.ai/mcp
codex mcp login dreamlit
```

### MCP Inspector

```sh
npx @modelcontextprotocol/inspector
```

Then choose Streamable HTTP and use:

```text
https://mcp.dreamlit.ai/mcp
```

## Tools

Dreamlit exposes workflow-level tools, not low-level graph editing APIs.

| Tool | Scope | Purpose |
| --- | --- | --- |
| `get_status` | `workflows:read` | Get Dreamlit guidance, workspace context, project setup, schema hints, workflow state, and app URLs. |
| `list_projects` | `workflows:read` | Find accessible Dreamlit projects in the approved workspace. |
| `list_workflows` | `workflows:read` | Find workflows in a project by name, description, trigger type, and pagination. |
| `get_workflow_and_preview_url` | `workflows:read` | Inspect a workflow draft and get the Dreamlit preview or builder URL before editing or publishing. |
| `create_or_update_workflow` | `workflows:write` | Create a new workflow draft or update an existing draft from a natural-language prompt. |
| `send_workflow_test` | `workflows:write` | Confirm and send a draft email or Slack test without publishing the workflow. |
| `prepare_publish` | `workflows:publish` | Validate a workflow before publishing and return confirmation fields. |
| `confirm_publish` | `workflows:publish` | Publish or schedule a workflow after explicit user confirmation. |
| `unpublish_workflow` | `workflows:publish` | Disable live triggers or schedules for a workflow. |

## Recommended Flow

1. Call `get_status` first to understand the workspace, project setup, and prompting guidance.
2. Use `list_projects` and `list_workflows` if the user names a project or workflow without IDs.
3. Use `get_workflow_and_preview_url` before editing an existing workflow.
4. Use `create_or_update_workflow` to create or update a draft.
5. Open the returned preview or builder URL and send workflow tests for important email or Slack messages.
6. Publish only after explicit user confirmation, using `prepare_publish` followed by `confirm_publish`.

Drafts are not live after authoring. Publishing is always a separate explicit step.

## Prompting Tips

Ask for the outcome, not a workflow graph. Good prompts include:

- The event or schedule that should start the workflow.
- The audience or recipient.
- The message goal and tone.
- The data needed for personalization.
- Timing, timezone, and business rules.
- Whether recipients should be able to unsubscribe.

Examples:

```text
When a new organization row is inserted, send an internal Slack alert with the organization name, owner email, and plan.
```

```text
Every Monday at 9 AM America/New_York, send admins a weekly usage digest summarizing active users, failed payments, and new signups.
```

```text
Tomorrow at 10 AM, announce the launch to active users who opted into product updates. Include unsubscribe.
```

## Access Model

OAuth access is scoped to the workspace selected during authorization. Personal access tokens are project scoped and can be created from Dreamlit project settings.

Available scopes:

- `workflows:read`
- `workflows:write`
- `workflows:publish`

Use the least privilege that fits the client. Read-only clients should request only `workflows:read`.

## Data Handling

Dreamlit MCP can access workflow metadata and connected project context needed to perform the requested workflow actions. It does not require clients to send database credentials through MCP.

Do not paste secrets, raw credentials, or private tokens into prompts. Use Dreamlit's app settings for integrations and credentials.

## Support

For support, contact `support@dreamlit.ai`.
