---
name: quickbooks-setup
description: Connect and troubleshoot QuickBooks Online in Cursor. Use when the QuickBooks tools are unavailable, unauthenticated, or failing, when the user has just installed the QuickBooks Online plugin, or when the user asks how to connect QuickBooks, sign in to QuickBooks, switch company, or fix a QuickBooks connection error.
---

# QuickBooks Online Setup

The QuickBooks tools come from Intuit's hosted MCP server, which this plugin declares in
`mcp.json`. Cursor owns the OAuth client, so the user needs no Intuit developer account, API key,
or client secret.

## Check the connection first

Check whether QuickBooks tools (names starting with `qbo_` or containing `quickbooks`) are
available in this session. If a read-only tool such as `company_info` succeeds, setup is
complete — tell the user and stop.

## Step 1: Connect

1. If the plugin is not installed, have the user open **Cursor Settings → Plugins**, search for
   **QuickBooks Online**, and click **Install** (or run `/add-plugin quickbooks-online` in chat).
2. When the server shows as needing authentication, start sign-in (the `mcp_auth` tool on the
   QuickBooks server, or **Connect** next to it in **Cursor Settings → MCP**).
3. The user signs in with the Intuit account for the QuickBooks company, picks the company, and
   grants the requested permissions.

Authorization is per company file. Connect only the companies the user wants agents to reach.

Do not suggest adding the server by hand in a project or user `mcp.json`. A duplicate entry at the
same URL competes with the plugin's server and will not use Cursor's OAuth client.

## Step 2: Verify

Run one read-only request, for example "How is my business doing this month?", which runs the
`business-health-check` skill against the connected company. If tools still don't appear, have the
user start a new chat so the tool list reloads.

## Troubleshooting

- **Asks to authorize again or tools return 401**: reconnect the server from
  **Cursor Settings → MCP**. Plugins that moved to the native OAuth client (1.1.0) require one
  reauthorization.
- **Wrong company data**: disconnect and reconnect, choosing the correct company during Intuit
  sign-in.
- **A tool the skill names is missing**: the server is the source of truth for tool names and
  which products (Payroll, Capital lending) the company has. Explain the gap; don't invent data.
- **QuickBooks Desktop**: not supported. This server is for QuickBooks Online only.
- **Revoking access**: uninstalling the plugin stops Cursor from offering the server; revoking the
  connection in Intuit's account settings ends Cursor's access to the company data.
