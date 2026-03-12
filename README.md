# Google Ads MCP Server

An [MCP (Model Context Protocol)](https://modelcontextprotocol.io/) server that connects Claude to the Google Ads API. Query campaign performance, explore account structure, research keywords, and more — all through natural language in Claude Code or Claude Desktop.

## Prerequisites

- **Python 3.10+** installed
- **pipx** installed ([installation guide](https://pipx.pypa.io/stable/installation/))
- A **Google Ads API credentials file** (see step 2)

## Quick Start

### 1. Clone this repository

```bash
git clone https://github.com/googleads/google-ads-mcp.git
cd google-ads-mcp
```

### 2. Get API credentials

Reach out to **Justin Arak** or **Sal Rapisarldi** to get the API credentials file (`api-credentials.json`) and developer token. Save the credentials file somewhere safe (e.g., `~/google-ads-mcp/api-credentials.json`).

### 3. Install with pipx

```bash
pipx install -e .
```

### 4. Register with Claude Code

Add the MCP server to Claude Code with the required environment variables:

```bash
claude mcp add google-ads-mcp \
  -e GOOGLE_APPLICATION_CREDENTIALS="/path/to/your/api-credentials.json" \
  -e GOOGLE_ADS_DEVELOPER_TOKEN="your-developer-token" \
  -e GOOGLE_ADS_LOGIN_CUSTOMER_ID="your-manager-account-id" \
  -- google-ads-mcp
```

> **Note:** `GOOGLE_ADS_LOGIN_CUSTOMER_ID` is optional but recommended if you access client accounts through a Manager account. Use the 10-digit account ID without hyphens.

### 5. Verify it works

Start Claude Code and try:

```
What Google Ads accounts do I have access to?
```

## Available Tools

| Tool | Description |
|------|-------------|
| `search` | Query Google Ads data using GAQL (Google Ads Query Language). Supports all resources including campaigns, ad groups, keywords, ads, and metrics. |
| `list_accessible_customers` | List all Google Ads customer accounts accessible with the current credentials. |
| `generate_keyword_ideas` | Get keyword suggestions with search volume, competition data, and bid estimates using the Keyword Planner API. |

## Example Queries

Once connected, you can ask Claude things like:

- "What Google Ads accounts do I have access to?"
- "Show me all active campaigns and their budgets"
- "What are my top 10 keywords by spend this month?"
- "How did my campaigns perform last week vs. the week before?"
- "Generate keyword ideas related to 'running shoes' in the US"
- "Show me search terms that triggered my ads in the last 30 days"
- "What's my impression share for my top campaigns?"

## Troubleshooting

### "GOOGLE_ADS_DEVELOPER_TOKEN environment variable not set"
Make sure you passed the `-e GOOGLE_ADS_DEVELOPER_TOKEN="..."` flag when registering the MCP server with `claude mcp add`.

### "Could not automatically determine credentials"
Ensure `GOOGLE_APPLICATION_CREDENTIALS` points to a valid service account JSON key file and the path is correct.

### "The caller does not have permission"
- Verify the service account has been granted access in Google Ads (Admin > Access and security)
- Check that the Google Ads API is enabled in the Google Cloud project
- If using a Manager account, ensure `GOOGLE_ADS_LOGIN_CUSTOMER_ID` is set correctly

### "Developer token is not approved"
- New developer tokens start with **Test account** access only
- Apply for **Basic** or **Standard** access in the API Center if you need to access production accounts

### Server not showing up in Claude Code
Run `claude mcp list` to check registered servers. If missing, re-run the `claude mcp add` command from step 4.

## License

Apache License 2.0 — see [LICENSE](LICENSE) for details.
