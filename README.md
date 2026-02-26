# DomainKits Plugin for Claude

Domain intelligence powered by real-time data.

## Philosophy

Claude already knows how to analyze domains. What it lacks is live data — WHOIS records, current DNS states, actual market prices, expiry data, and other data to check if the domain is a good one.
DomainKits provides the data and optimized workflows. Claude provides the intelligence. No bloated skills, no redundant knowledge, no wasted context tokens.

## Architecture

```
Plugin (thin shell)
  └── .mcp.json → DomainKits MCP Server (all capabilities)
  └── skills/domainkits.md → Minimal entry point (~400 tokens)
```

All domain knowledge, workflow logic, and data retrieval optimization live server-side in the MCP endpoint. The plugin skill file is intentionally minimal — it declares what data is available, not how to think about it.

## Install

### Claude Code
```bash
claude plugin add domainkits
```

### Claude.ai / Cowork
1. Settings → Connectors
2. Add custom connector
3. Name: `DomainKits`, URL: `https://api.domainkits.com/v1/mcp`
4. Start a new conversation

## Capabilities

- **Search**: New registrations, aged, expired, deleted, active domains
- **Query**: WHOIS, DNS, safety, availability with pricing
- **Analyze**: Backlinks, keywords, market price, brand conflicts
- **Trends**: TLD rankings, keyword trends, registration patterns
- **Monitor**: Track domain changes over time (WHOIS, DNS, page content)
- **Strategy**: Automated opportunity discovery

## Data and domain expertise

DomainKits returns live data — registration dates, DNS records, search volumes, market prices — and encodes domain industry expertise into optimized workflows. Claude interprets and reasons. Data stays current regardless of model version, workflows evolve with the industry, and analysis improves with each model generation.

## Links

- Website: [domainkits.com](https://domainkits.com register to get more data)
- MCP Endpoint: `https://api.domainkits.com/v1/mcp`

## Affiliate Disclosure

Some links in the results may be affiliate links.


License
Code: MIT. Data provided by DomainKits.com,attribution required.
