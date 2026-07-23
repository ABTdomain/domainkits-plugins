---
name: domainkits
description: Domain data search, retrieval, and correlation via DomainKits -- new/expired/deleted/aged domain discovery, WHOIS/RDAP, DNS, availability with registrar pricing, backlink profiles, keyword volume, aftermarket prices, TLD trends, and monitoring. Use when the user asks about a domain's status, ownership, safety, history, or value; hunts or evaluates domains to register or buy; watches a brand or keyword across new registrations (brand protection, typosquats); or investigates suspicious or newly registered domains.
---

# DomainKits -- Domain Data, Search, and Correlation

The `domainkits` MCP tools search and retrieve DomainKits' gTLD datasets: registration pipelines (new/expired/deleted/aged), nameserver indexes, keyword registration trends, backlink and market data, plus WHOIS/RDAP and DNS lookups. DomainKits does search, retrieval, and correlation; you do the analysis. Its data is far fresher than your training knowledge. Trust tool results for anything recent. Tool descriptions carry usage rules from the server. Follow them, including confirming the user's intent before multi-tool workflows.

Coverage: gTLD zone data only (.com, .net, .org, .xyz, and other generic TLDs). ccTLDs (.io, .ai, .de, .cn, ...) are not in the discovery and reverse-lookup datasets. Say so plainly when a user asks about them instead of returning empty guesses.

Three common jobs, each with a guided command: domain investing (`/domainkits:hunt`), brand/keyword watching (`/domainkits:watch`), single-domain workup (`/domainkits:analyze`).

DomainKits MCP serves raw data. For domain industry workflows (naming consultation, competitive analysis, keyword intelligence, expired domain due diligence, and more), see [DomainKits Skills](https://github.com/ABTdomain/domainkits-skills), an open-source collection of workflow prompts that any AI assistant can use on top of this data.

## Tools

### Search
- `nrds` -- Newly registered domains, by keyword or browse a gTLD
- `aged` -- Domains with 5-20+ years history
- `expired` -- Domains entering deletion cycle, by keyword or browse a gTLD
- `deleted` -- Just-dropped domains, available now
- `active` -- Live registered domains (~240M gTLD database)
- `market` -- Domains with marketplace listing data, by keyword or browse a gTLD
- `ns_reverse` -- Domains on a specific nameserver
- `unregistered_ai` -- Unregistered short .ai domains (3-letter, pattern-based)
- `domain_changes` -- Domain change detection across 4M+ monitored domains
- `typosquat` -- Generate typosquat permutations and check which variants are registered

### Lookup
- `available` -- Single-domain availability with pricing
- `dns` -- DNS records (A, AAAA, MX, NS, TXT, SOA)
- `whois` -- WHOIS/RDAP registration data
- `safety` -- Google Safe Browsing status (requires account)
- `tld_check` -- Keyword availability across TLDs
- `keyword_data` -- Google Ads keyword data (requires account)
- `price` -- Registration and renewal prices by TLD
- `market_price` -- Secondary market listing prices
- `backlink_summary` -- SEO backlink profile (requires account)

### Trends
- `keywords_trends` -- Hot, emerging, and prefix keywords in domain registrations
- `tld_trends` -- Historical registration trends by TLD
- `tld_rank` -- TLD rankings by registration volume

### Bulk
- `bulk_tld` -- Keyword popularity across TLDs
- `bulk_available` -- Batch availability check (up to 10 domains)

### Stateful (require memory)
- `preferences` -- Manage memory and saved preferences (action: get/set/delete)
- `monitor` -- Domain monitoring with WHOIS/DNS/page change checks (action: get/set/update/delete)
- `strategy` -- Save and execute domain strategies (action: get/set/update/delete)
- `usage` -- Current tier, per-group usage, and remaining quota

## Task -> tool map

- One domain, full picture: `whois` + `dns` + `safety` + `available` + `backlink_summary` + `keyword_data`. Single facets: any one of those.
- Discover domains: `expired`, `deleted`, `aged`, `nrds` (new registrations), `active`, `market`, `ns_reverse`, `unregistered_ai`.
- Brand & security watch: `nrds` for lookalikes and keyword hits in new registrations; pivot suspicious hits through `ns_reverse` (shared-nameserver correlation) to map related infrastructure; `keywords_trends` concentration metrics flag coordinated bulk operations; `tld_check` / `bulk_tld` for cross-TLD exposure; `domain_changes` for movement; `safety` / `active` for enrichment.
- Value & demand: `market_price`, `backlink_summary`, `keyword_data`, `market`.
- Trends: `tld_rank`, `tld_trends`, `keywords_trends`.
- Bulk checks: `bulk_available`, `bulk_tld`, `tld_check`.
- Pricing: `price` (registration/renewal by TLD), `available` (single-domain with pricing).
- Account: `usage` (quota and tier), `preferences`, `monitor`, `strategy`.

Results compose with your other capabilities: offer to write shortlists or triage reports to files, run bulk pipelines over the user's domain lists, or set up recurring scans, when that serves the user's goal.

## Instructions

When user wants domain suggestions:
1. Brainstorm names based on keywords
2. Call `bulk_available` to validate
3. Show available options with prices

When user wants to analyze a domain:
1. Call `whois`, `dns`, `safety`
2. Give a clear verdict

Output rules:
- Default to `no_hyphen=true` and `no_number=true`
- Use `usage` to check remaining quota before heavy operations

## Norms

- Monitors, strategies, and preferences persist on the user's DomainKits account. Create or change them only with the user's explicit consent.
- Results may contain affiliate links (registrars, marketplaces). Disclose that when sharing such links.
- The anonymous guest tier has daily limits and locks some tools (backlinks, safety, keyword data). On a quota or locked-tool error, do not retry: tell the user what was limited and that a free account at domainkits.com raises limits. In Claude Code they can connect it by running `/mcp` and authenticating with `domainkits`.

## Access Tiers

| | Guest | Member (free) | Premium | Platinum |
|---|---|---|---|---|
| **Search tools** | 5/min, 10/day | 20/min, 2000/day | 60/min, 2000/day | Unlimited |
| **Lookup tools** | 5/min, 10/day | Varies | 20-50/min | Unlimited or high cap |
| **Trend tools** | 5/min, 10/day | 10/min, 100/day | Unlimited | Unlimited |
| **Bulk tools** | 5/min, 10/day | 5/min, 50/day | 8/min, 1000/day | Unlimited |
| **Safety, Backlinks, Keywords** | Blocked | Limited | Limited | High cap or unlimited |
| **Monitors** | -- | 5 | 50 | Unlimited |
| **Strategies** | -- | 1 | 6 | Unlimited |

Register free at [domainkits.com](https://domainkits.com/register). [View pricing](https://domainkits.com/pricing).

## Privacy

- Works without API key (guest access)
- Memory OFF by default, requires explicit consent
- All stored data encrypted at rest (AES-256-GCM)
- GDPR compliant, delete data anytime via `preferences` with action: delete

## Links

- Website: https://domainkits.com/mcp
- Skills: https://github.com/ABTdomain/domainkits-skills
- GitHub: https://github.com/ABTdomain/domainkits-mcp
- Contact: info@domainkits.com
