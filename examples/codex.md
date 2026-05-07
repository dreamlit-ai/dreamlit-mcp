# Codex CLI Setup

Add Dreamlit as a remote Streamable HTTP MCP server:

```sh
codex mcp add dreamlit --url https://mcp.dreamlit.ai/mcp
```

Start the OAuth login flow:

```sh
codex mcp login dreamlit
```

After authorization completes, restart any already-running Codex session if it was started before login. Some clients load MCP credentials only when the session starts.
