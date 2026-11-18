# StockLens MCP Server

Explainable stock scores, company analysis, discovery screening and portfolio insights for ChatGPT and Claude.

StockLens hosts this MCP server remotely. There is nothing to install or run: point your client at the endpoint.

| | |
| --- | --- |
| Endpoint | `https://mcp.stocklens.com/mcp` |
| Transport | Streamable HTTP |
| Sign-in | OAuth 2.1 with PKCE, only for account tools |
| MCP Registry | `com.stocklens/stocklens` |

## Connect

### Claude

**claude.ai and Claude Desktop.** StockLens is listed in [Claude's connector directory](https://claude.ai/directory/connectors/stocklens). Open **Customize → Connectors**, select **Discover**, search for StockLens and connect. Team and Enterprise owners add it for the organization first. To add it as a custom connector instead, use this URL:

```text
https://mcp.stocklens.com/mcp
```

**Claude Code.**

```bash
claude mcp add --transport http stocklens https://mcp.stocklens.com/mcp
```

Run `/mcp` in Claude Code to sign in when you first use an account tool.

### ChatGPT

Install StockLens from the [ChatGPT plugin directory](https://chatgpt.com/plugins/plugin_asdk_app_6a383168e69881918059edd89ef27451). ChatGPT has no config file for it. Ask for a score straight away, and sign in when you first use a portfolio or analysis tool.

### Cursor

Add the server to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

```json
{
  "mcpServers": {
    "stocklens": {
      "url": "https://mcp.stocklens.com/mcp"
    }
  }
}
```

### Other MCP clients

Any client that speaks streamable HTTP can connect to `https://mcp.stocklens.com/mcp`. Clients register themselves through OAuth dynamic client registration, so no client ID is needed.

## Tools

### No account needed

These cover the largest companies in each market.

| Tool | What it does |
| --- | --- |
| `ping` | Checks that the connection is healthy. Reads no account or market data. |
| `get_market_summary` | One company's latest nightly reading: score and rating, domain breakdown, the drivers that shaped it, and its standing within its own market. |
| `get_shortlist_summary` | The companies you name, read in one call. Companies from different markets sit side by side, never on one scale. |

### Sign-in required (OAuth 2.1 with PKCE)

| Tool | What it does |
| --- | --- |
| `initiate_analysis` | Starts a full StockLens analysis of a company. A new run may use one analysis credit. |
| `fetch_analysis_result` | Checks an analysis by id: its progress while it runs, then the saved report. |
| `inspect_reading` | Explains a saved reading from the evidence it already holds: why a score reason, finding or assessment says what it does. Starts no analysis. |
| `discover_stocks` | Screens one market by exchange, sector, industry, market-cap band and volume, sorted by StockLens scores, market cap, volume or ticker. |
| `get_portfolio_insights` | Reads a portfolio: each company's score, rating and standing in its market, the largest sector share and the biggest movers over 7 nights. |
| `add_to_watchlist` | Adds one company to a portfolio to follow it. Records no holding and places no trade. |
| `add_to_watchlist_batch` | Adds up to 100 companies in two steps: a preview that adds nothing, then only the rows you approve. |
| `remove_from_watchlist` | Removes one company from a portfolio. Entries that carry transactions are kept. |

Signed-in tools follow the account's StockLens plan (Free, Pro or Max). Plans and limits: [stocklens.com/features/ai-integrations](https://stocklens.com/features/ai-integrations)

Informational and educational only, not investment advice.
