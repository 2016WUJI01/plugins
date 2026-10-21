# Google Cloud BigQuery

Cursor plugin that connects agents to [Google Cloud BigQuery](https://docs.cloud.google.com/bigquery/docs/use-bigquery-mcp) through Google Cloud BigQuery's official remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Explore datasets and tables and run SQL queries.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **Google Cloud BigQuery**.
3. Click **Install**, then complete the Google Cloud BigQuery sign-in prompt.

Or run `/add-plugin google-cloud-bigquery` in chat.

## MCP

```json
{
  "mcpServers": {
    "google-cloud-bigquery": {
      "type": "http",
      "url": "https://bigquery.googleapis.com/mcp",
      "auth": {
        "CLIENT_ID": "${CLIENT_ID:-}",
        "CLIENT_SECRET": "${CLIENT_SECRET:-}"
      }
    }
  }
}
```

Auth is OAuth. Cursor prompts for Google Cloud BigQuery sign-in when the plugin connects. By default it signs in with Cursor's Google OAuth client, so there is nothing to configure. A team can use its own client instead; see below.

## Use your team's own OAuth client

A team admin can have every member sign in under one Google OAuth client the team owns, so consent and audit show the team's own app.

1. In the Google Cloud console, create an OAuth client for a **Web application** and add Cursor's OAuth callback URL as an authorized redirect URI. Add the `https://www.googleapis.com/auth/bigquery` scope to the project's OAuth consent screen.
2. In the Cursor dashboard, open the team's plugin settings for **Google Cloud BigQuery** and enter the **Client ID** and **Client secret**.

Members then sign in to BigQuery under that client. The secret is stored encrypted and stays on Cursor's backend; it is never sent to members' machines. Leave both fields empty to use Cursor's client. Changing the client signs members out, and they reconnect once.

## Before you connect

You need a Google Cloud project with the BigQuery API enabled, and your Google account needs the MCP Tool User role (`roles/mcp.toolUser`) plus BigQuery Job User and Data Viewer on that project.

## What agents can do

| Category | Capabilities |
| --- | --- |
| Explore | List datasets and tables and read their metadata and schemas |
| Query | Run read-only SQL, including BigQuery ML functions |
| Write | Run DML and DDL when the account allows it |
| Jobs | Poll results and cancel running query jobs |

The hosted runtime is the source of truth for tool names and schemas.

## Notes

- Queries are billed to the project id passed to the tool.
- Admins can block the write-capable `execute_sql` tool with an IAM deny policy while leaving read-only queries available.
- Grok also offers this connector with service-identity auth; this plugin configures only the user OAuth flow.

## Docs

- Use the BigQuery MCP server: https://docs.cloud.google.com/bigquery/docs/use-bigquery-mcp
- Tools reference: https://docs.cloud.google.com/bigquery/docs/reference/mcp
- Server URL: https://bigquery.googleapis.com/mcp

Logo is the official BigQuery product icon from Google Cloud's architecture icon set, on a padded white tile.

## License

MIT
