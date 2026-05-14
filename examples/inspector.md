# MCP Inspector Setup

Start the inspector:

```sh
npx @modelcontextprotocol/inspector
```

Use these settings:

- Transport: Streamable HTTP
- URL: `https://mcp.dreamlit.ai/mcp`

The inspector should open a Dreamlit authorization page. Approve access, then use read-only tools such as `get_status`, `list_projects`, `list_brand_kits`, or `get_analytics` before testing write or publish flows.
