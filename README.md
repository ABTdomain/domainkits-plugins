# DomainKits — Domain Intelligence for Claude

DomainKits turns gTLD domain data into answers. It does the search, retrieval, and correlation across registration pipelines (new / expired / deleted / aged), nameserver indexes, keyword registration trends, WHOIS/DNS, backlink and market datasets. Claude does the analysis.

Three jobs: **finding domain opportunities**, **protecting your brand**, and **watching new registrations for threats**.

**Coverage: gTLDs** (.com, .net, .org, .xyz, .app, and the other generic TLDs). ccTLDs (.io, .ai, .de, ...) are not covered by the discovery and reverse-lookup datasets.

## Who it's for

### Domain investors -- trends, discovery, valuation

- "What keywords are spiking in new registrations this week, and which spikes are real demand vs. bulk speculation?"
- "Find expired .com domains about fitness with a clean backlink profile" → `/domainkits:hunt`
- "Is brightpay.com worth the $3k ask? Full due diligence" → `/domainkits:analyze brightpay.com`
- "Which naming prefixes are trending, and where is the .com still open?"

### Brand protection -- who is registering around your name

- "Any new registrations containing 'acme' in the last 10 days?" → `/domainkits:watch acme`
- "The same prefix just appeared across 30+ TLDs, is someone building around our name?"
- "Where is 'acme' registered across gTLDs, and which are still open to defend?"
- "Watch acme-related domains for WHOIS/DNS changes" (account feature)

### Security teams -- NRDs as the signal, nameserver correlation as the pivot

- "New domains resembling 'ourbank' registered this week?" → `/domainkits:watch ourbank`
- "This lookalike is an active phishing site, what else is hosted on its nameservers?" (`ns_reverse` maps the campaign)
- "Any emerging keyword spikes with single-registrar, single-nameserver concentration?" (coordinated-operation signal)
- "Full WHOIS/DNS workup on this suspicious domain" → `/domainkits:analyze`

In Claude Code, results compose with everything else Claude can do: write triage reports and shortlists to files, run bulk pipelines over your domain lists, schedule recurring sweeps, cross-check with web research.

## Commands

| Command | For | What it does |
|---|---|---|
| `/domainkits:hunt [thesis]` | Investors | Opportunity discovery: expired, deleted, aged, trending, or unregistered names matching your thesis |
| `/domainkits:watch <brand/keyword>` | Brand & security | Sweep new registrations and TLDs for a term; triage into benign / brand conflict / suspicious; pivot suspects through their nameservers |
| `/domainkits:analyze <domain>` | Everyone | Full workup on one domain: registration, DNS, safety, backlinks, value, market signals |

No command needed for ad-hoc questions. The bundled skill auto-activates whenever domains come up.

## Capabilities

- **Discover**: newly registered domains (last 60 days), expired, deleted, aged, and active domains; reverse-nameserver mapping (all gTLD domains behind one NS); unregistered short .ai domains
- **Evaluate**: backlink profiles, keyword volume/CPC, aftermarket prices, Google Safe Browsing status
- **Act**: availability checks with registrar pricing, bulk checks, TLD-wide keyword availability
- **Trends**: keyword registration trends with quality metrics (.com share, for-sale ratio, registrar/NS concentration), TLD ranking and historical trends
- **Automate**: monitors (WHOIS/DNS/page changes) and recurring strategies on your DomainKits account

## Bundled workflow skills

The plugin ships eight open-source workflow skills that auto-activate on matching tasks:

| Skill | What it does |
|---|---|
| brand-protection | Scan typosquats and lookalike registrations around a brand, evaluate each domain individually on registration facts, offer monitoring |
| domain-analyze | Evidence-based picture of one domain: registration, DNS, safety, backlinks, cross-TLD footprint, market context |
| domain-cma-valuation | Comparative Market Analysis against verified for-sale substitutes in the same keyword market |
| domain-generator | Creative brandable names from a keyword, concept, or taken domain, verified available at check time |
| domain-name-advisor | Naming consultation across registration, drop-catch, backorder, and aftermarket paths |
| keyword-intel | Evidence map for one keyword: search, advertiser, registration, supply, and transaction layers kept separate |
| keyword-trend-hunter | Discover registration keyword spikes and validate them against new-registration cohort signals |
| domain-market-beat | Time-bounded market briefing: sales, registration trends, and domain movements with source tiers |

Source repo (standalone install for other agents): [DomainKits Skills](https://github.com/ABTdomain/domainkits-skills).

## Architecture

```
domainkits plugin
├── .mcp.json                    → remote MCP server (https://api.domainkits.com/v1/mcp)
├── skills/domainkits/SKILL.md   → core skill: tool listing, task→tool map, usage norms, access tiers
├── skills/<workflow>/SKILL.md   → 8 bundled workflow skills (brand-protection, domain-analyze, ...)
└── commands/                    → /domainkits:hunt · /domainkits:watch · /domainkits:analyze
```

No local code execution: the plugin is a remote endpoint, nine skill files, and three command prompts.

## Install

**Claude Code** (CLI, desktop, or VS Code):

```
/plugin marketplace add ABTdomain/domainkits-plugins
/plugin install domainkits@domainkits
```

**claude.ai / Cowork** (as a connector instead of a plugin):

1. Settings → Connectors → Add custom connector
2. Name: `DomainKits`, URL: `https://api.domainkits.com/v1/mcp`
3. Start a new conversation

## Tiers and limits

Works out of the box, no API key, no sign-up. The anonymous guest tier has daily per-tool limits, and some data sources (backlinks, keyword volume, safety checks) require an account.

A free account at [domainkits.com](https://domainkits.com) raises limits; paid tiers unlock the full dataset. Full per-tool limits by tier: [domainkits.com/mcp#limits](https://domainkits.com/mcp#limits). MCP limits are metered separately from the web interface. To connect your account in Claude Code, run `/mcp` and authenticate with `domainkits` (OAuth). On claude.ai the connector prompts for sign-in the same way. Ask Claude for your "DomainKits usage" anytime to see your quota.

## Data and privacy

Queries (domain names, keywords, search filters) are sent to `api.domainkits.com` to fetch results. The plugin reads no local files and ships no executable code.

Search and lookup tools are stateless: nothing you ask is retained. Three tools store data across sessions, and only after you enable memory:

| Tool | What it stores |
|---|---|
| `monitor` | The domains you watch and the results of each check |
| `preferences` | Your saved preferences and the memory switch |
| `strategy` | Strategy text you wrote, run timestamps and the most recent result |

Memory is off by default. Stored data is encrypted at rest (AES-256-GCM) in isolated per-user directories, is tied to your DomainKits account rather than to one client, and can be deleted in full at any time by asking Claude to delete your DomainKits data (GDPR Article 17).

Responses contain no registrant personal data: WHOIS results carry registrar, dates, status codes and nameservers only.

## License

Code: MIT (see [LICENSE](LICENSE)). Domain data is provided by [DomainKits.com](https://domainkits.com) under its own terms; attribution required when republishing data.
