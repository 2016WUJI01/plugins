# Vanta

Cursor plugin that connects agents to [Vanta](https://www.vanta.com) through Vanta's official remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Ask about your compliance posture, such as which tests are failing, which controls map to a framework, or which vulnerabilities are past their SLA, and have the agent help remediate failing tests.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Vanta**.
3. Click **Install**, then complete the Vanta sign-in prompt and click **Allow**.

Or run `/add-plugin vanta` in chat.

## MCP

```json
{
  "mcpServers": {
    "vanta": {
      "type": "http",
      "url": "https://mcp.vanta.com/mcp",
      "placement": "server"
    }
  }
}
```

Auth is MCP OAuth (Bearer). Cursor discovers the authorization server when the plugin connects and prompts for Vanta login. Vanta supports Dynamic Client Registration with PKCE, so there is no API token, client ID, client secret, or custom header to configure.

## Before you connect

You need an active Vanta user on a US-hosted Vanta instance. Any role can connect, including Editor, Collaborator, and View-only Admin. Unauthenticated requests to the server are rejected until that login completes.

Vanta hosts a separate MCP server per region. This plugin targets the US endpoint. EU and Australia instances use `https://mcp.eu.vanta.com/mcp` and `https://mcp.aus.vanta.com/mcp`; add those as a custom MCP server instead.

## Notes

- Tool calls run as the Vanta user who authorizes the connection and cannot exceed that user's permissions. Admins get the full tool set; other roles get the same tools minus a few that Vanta restricts to Admins.
- The agent can change your compliance data, such as creating risks or uploading policies. Review changes in Vanta.
- What the agent reads from or changes in your account goes through Vanta's servers, under the [Vanta Privacy Policy](https://www.vanta.com/legal/privacy).
- OAuth metadata is discovered at connect time (protected resource `https://mcp.vanta.com/.well-known/oauth-protected-resource`, authorization server `https://api.vanta.com/mcp`, scope `mcp-api.all:write`).
- If a connection stops working, remove and re-add it to start a fresh OAuth flow.
- The hosted runtime is the source of truth for tool names and schemas; tools are listed after sign-in.

## Docs

- Vanta MCP server: https://developer.vanta.com/docs/vanta-mcp
- Connecting to Vanta MCP: https://help.vanta.com/en/articles/14094979-connecting-to-vanta-mcp
- Server URL: https://mcp.vanta.com/mcp

Logo is the "V" glyph from Vanta's official wordmark, from `https://cdn.prod.website-files.com/64009032676f24f376f002fc/6400ac82429afb0f7b31fa6c_vanta-logo.svg` (Vanta Inc.).

## License

MIT
