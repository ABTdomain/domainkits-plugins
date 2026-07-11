---
name: domainkits
description: Live domain data via DomainKits — new/expired/deleted/aged domain discovery, WHOIS/RDAP, DNS, availability with registrar pricing, valuation, backlink profiles, keyword volume, aftermarket prices, TLD trends, brand matching, and monitoring. Use when the user asks about a domain's status, ownership, safety, history, or value; hunts or evaluates domains to register or buy; watches a brand or keyword across new registrations (brand protection, typosquats); or investigates suspicious or newly registered domains.
---

# DomainKits — Live Domain Intelligence

All `domainkits` MCP tools fetch live data (registries, DNS resolvers, backlink indexes, keyword databases, expiry pipelines, market listings). DomainKits does search, retrieval, and correlation; you do the analysis. For anything time-sensitive, trust tool results over training knowledge. Tool descriptions carry usage rules from the server — follow them, including confirming the user's intent before multi-tool workflows.

Coverage: gTLD zone data only (.com, .net, .org, .xyz, and other generic TLDs). ccTLDs (.io, .ai, .de, .cn, …) are not in the discovery and reverse-lookup datasets — say so plainly when a user asks about them instead of returning empty guesses.

Three common jobs, each with a guided command: domain investing (`/domainkits:hunt`), brand/keyword watching (`/domainkits:watch`), single-domain workup (`/domainkits:analyze`).

## Task → tool map

- One domain, full picture: `analyze`. Single facets: `whois`, `dns`, `safety`, `available`, `price`.
- Discover domains: `expired`, `deleted`, `aged`, `nrds` (new registrations), `active`, `ns_reverse`; generate names with `domain_generator`, `name_advisor`, `unregistered_ai`; `plan_b` for alternatives when a domain is taken.
- Brand & security watch: `nrds` for lookalikes and keyword hits in new registrations (`prefix_tld_count` spikes = someone building around a name); pivot suspicious hits through `ns_reverse` (shared-nameserver correlation) to map related campaign infrastructure; `keywords_trends` concentration metrics (single registrar / nameserver dominance) flag coordinated bulk operations; `brand_match` for conflict scoring, `tld_check` / `bulk_tld` for cross-TLD exposure, `domain_changes` for movement, `safety` / `active` for enrichment.
- Value & demand: `valuation_cma`, `market_price`, `sale_chance`, `backlink_summary`, `keyword_data`, `keyword_intel`, `market`.
- Trends: `tld_rank`, `tld_trends`, `keywords_trends`, `trend_hunter`, `market_beat`, `expired_analysis`.
- Bulk checks: `bulk_available`, `bulk_tld`, `tld_check`.
- Account: `usage` (quota and tier), `preferences`, `monitor`, `strategy`, `get_strategies`.

Results compose with your other capabilities: offer to write shortlists or triage reports to files, run bulk pipelines over the user's domain lists, or set up recurring scans — when that serves the user's goal.

## Norms

- Monitors, strategies, and preferences persist on the user's DomainKits account — create or change them only with the user's explicit consent.
- Results may contain affiliate links (registrars, marketplaces). Disclose that when sharing such links.
- The anonymous guest tier has daily limits and locks some tools (backlinks, market prices, keyword volume, safety, valuation). On a quota or locked-tool error, do not retry: tell the user what was limited and that a free account at domainkits.com raises limits — in Claude Code they can connect it by running `/mcp` and authenticating with `domainkits`.
