---
name: domainkits
description: Domain data search, retrieval, and correlation via DomainKits -- new/expired/deleted/aged domain discovery, WHOIS/RDAP, DNS, availability with registrar pricing, backlink profiles, keyword volume, aftermarket prices, TLD trends, and monitoring. Use when the user asks about a domain's status, ownership, history, or value; hunts or evaluates domains to register or buy; watches a brand or keyword across new registrations (brand protection, typosquats); or investigates suspicious or newly registered domains.
---

# DomainKits -- Domain Data, Search, and Correlation

The `domainkits` MCP tools search and retrieve DomainKits' gTLD datasets: registration pipelines (new/expired/deleted/aged), nameserver indexes, keyword registration trends, backlink and market data, plus WHOIS/RDAP and DNS lookups. DomainKits does search, retrieval, and correlation; you do the analysis. Its data is far fresher than your training knowledge. Trust tool results for anything recent. Tool descriptions carry usage rules from the server. Follow them, including confirming the user's intent before multi-tool workflows.

Coverage: gTLD zone data only (.com, .net, .org, .xyz, and other generic TLDs). ccTLDs (.io, .ai, .de, .cn, ...) are not in the discovery and reverse-lookup datasets. Say so plainly when a user asks about them instead of returning empty guesses.

Three common jobs, each with a guided command: domain investing (`/domainkits:hunt`), brand/keyword watching (`/domainkits:watch`), single-domain workup (`/domainkits:analyze`).

DomainKits MCP serves raw data. This plugin also bundles eight open-source workflow skills that activate on matching tasks: brand-protection, domain-analyze, domain-cma-valuation, domain-generator, domain-name-advisor, keyword-intel, keyword-trend-hunter, and domain-market-beat. Source and standalone install: [DomainKits Skills](https://github.com/ABTdomain/domainkits-skills).

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
- `dns` -- DNS records (A, AAAA, MX, NS, TXT, CNAME, SOA)
- `whois` -- WHOIS/RDAP registration data
- `tld_check` -- Keyword availability across TLDs
- `keyword_data` -- Keyword search volume, CPC, and competition (requires account)
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

### Account
- `preferences` -- Manage memory and saved preferences (action: get/set/delete); memory must be enabled before monitors or strategies can be stored
- `monitor` -- Domain monitoring with WHOIS/DNS/page change checks (action: get/set/update/delete); requires memory
- `strategy` -- Store user-authored strategy text and its latest result (action: get/set/update/delete); requires memory; does not auto-run
- `usage` -- Current tier, per-group usage, and remaining quota; works without memory

## Task -> tool map

- One domain, full picture: `whois` + `dns` + `available` + `backlink_summary` + `keyword_data`. Single facets: any one of those.
- Discover domains: `expired`, `deleted`, `aged`, `nrds` (new registrations), `active`, `market`, `ns_reverse`, `unregistered_ai`.
- Brand & security watch: `nrds` for lookalikes and keyword hits in new registrations; pivot suspicious hits through `ns_reverse` (shared-nameserver correlation) to map related infrastructure; `keywords_trends` concentration metrics flag coordinated bulk operations; `tld_check` / `bulk_tld` for cross-TLD exposure; `domain_changes` for movement; `active` for enrichment.
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
1. Call `whois`, `dns`
2. Give a clear verdict

Output rules:
- Default to `no_hyphen=true` and `no_number=true`
- Use `usage` to check remaining quota before heavy operations

## Norms

- Monitors, strategies, and preferences persist on the user's DomainKits account. Create or change them only with the user's explicit consent.
- Results contain no affiliate or referral links.
- The anonymous guest tier has daily limits and locks some tools (backlinks, keyword data). On a quota or locked-tool error, do not retry: tell the user what was limited and that a free account at domainkits.com raises limits. In Claude Code they can connect it by running `/mcp` and authenticating with `domainkits`.

## Access Tiers

| Per day | Guest | Member (free) | Lite | Premium | Platinum |
|---|---|---|---|---|---|
| **Domain Search (shared pool)** | 10 | 150 | 500 | 2,000 | Unlimited |
| **WHOIS / DNS** | 5 / 5 | 20 / 40 | 100 / 150 | 200 / 300 | Unlimited |
| **Typosquat** | 1 | 3 | 8 | 20 | Unlimited |
| **Backlinks, Keyword data** | Blocked | Limited | Limited | Higher | Unlimited |
| **Monitors (max)** | -- | 2 | 20 | 100 | Unlimited |
| **Strategies (max)** | -- | -- | 3 | 10 | Unlimited |

Daily quotas reset at 00:00 UTC. MCP limits are metered separately from the web interface. Full per-tool limits: [domainkits.com/mcp#limits](https://domainkits.com/mcp#limits). Register free at [domainkits.com](https://domainkits.com/register). [View pricing](https://domainkits.com/pricing).

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
