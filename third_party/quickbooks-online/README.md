# QuickBooks Online

Cursor plugin that connects agents to [QuickBooks Online](https://quickbooks.intuit.com) — Intuit's cloud accounting product — through Intuit's remote [Model Context Protocol](https://modelcontextprotocol.io/) server, which Cursor credentials for you.

Read a company file's accounting data: invoices, bills, expenses, payments, customers and vendors, the chart of accounts, journal entries, and the standard financial reports.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **QuickBooks Online**.
3. Click **Install**, then sign in to Intuit when Cursor prompts you.

Or run `/add-plugin quickbooks-online` in chat.

## MCP

```json
{
  "mcpServers": {
    "quickbooks-online": {
      "type": "http",
      "url": "https://mcp-e2e.quickbooks.intuit.com/mcp"
    }
  }
}
```

Intuit hosts the server. Auth is OAuth against Intuit, which Cursor runs when the plugin connects — there is no command to run, and no API key or client secret to paste.

## Before you connect

Nothing to prepare. Cursor owns the OAuth client, so you do not need an Intuit developer account or an app of your own.

You will be asked to sign in to Intuit and pick a company. Authorization is per company file — connect once per company you want agents to reach, and grant only the ones you intend to expose.

## What agents can do

| Category | Capabilities |
| --- | --- |
| Accounts | Chart of accounts and company information |
| Contacts | Customers, vendors, and employees |
| Sales | Invoices, credit memos, and payments received |
| Purchases | Bills, expenses, purchase orders, and payments made |
| Banking | Bank transactions and journal entries |
| Items | Products, services, and tracking categories |
| Reports | Profit and loss, balance sheet, and cash flow statement |

The server is the source of truth for tool names and schemas.

## Skills

Bundled skills from Intuit's [QuickBooks plugin](https://github.com/intuit/quickbooks-claude-plugin) guide agents through multi-step workflows on top of the server's tools. Write actions (sending reminders or invoices, creating employees, changing pay) always ask for confirmation first.

| Skill | What it does |
| --- | --- |
| `quickbooks-setup` | Connect QuickBooks in Cursor and troubleshoot the connection |
| `business-health-check` | CFO-style briefing from profit and loss, cash flow, balance sheet, receivables aging, and sales |
| `industry-benchmark` | Compare the connected company's figures against regional industry peers |
| `chase-overdue-invoices` | Find overdue invoices and send reminders with tone matched to aging |
| `email-to-estimate-invoice` | Turn a customer email thread into an estimate or invoice (needs an email MCP such as Gmail or Outlook) |
| `payroll-help` | Read-only payroll lookups: employees, last run, payslips, pay types, deductions, time off |
| `analyze-payroll-cost` | Explain payroll cost changes, top-paid employees, and cost drivers |
| `payroll-employee-onboarding` | Add a new hire to QuickBooks Payroll with duplicate checks and read-back verification |
| `set-base-pay` | View or change an employee's salary or hourly rate |
| `lending` | QuickBooks Capital products, payment estimates, and the user's existing loans |

Payroll and lending skills only work on companies with QuickBooks Payroll or QuickBooks Capital. Intuit's skills are licensed under Apache 2.0; see `skills/LICENSE`.

## Notes

- Access follows whatever the signed-in Intuit user can see. The connector cannot reach a company file that user has no access to.
- QuickBooks Online and QuickBooks Desktop are different products. This connector is for QuickBooks Online.
- Disconnecting is two independent steps: uninstalling the plugin stops Cursor from offering the server, and revoking the connection in Intuit's account settings ends Cursor's access to your data.

## Docs

- QuickBooks Online: https://quickbooks.intuit.com
- Intuit Developer: https://developer.intuit.com
- Model Context Protocol: https://modelcontextprotocol.io
- Server URL: https://mcp-e2e.quickbooks.intuit.com/mcp

Logo is QuickBooks' official mark, from `quickbooks.intuit.com`.

## License

MIT
