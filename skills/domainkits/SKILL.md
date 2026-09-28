---
name: domainkits
description: How to use the DomainKits tools for domain data (newly registered, expired, and deleted domains; WHOIS, DNS, reverse nameserver, registrar, EPP status, and IP lookups; availability, prices, and registration trends). Use when calling these tools, to pick the right tool for each lifecycle stage, pass parameter values the tools accept, and read results and limit messages.
---

# DomainKits tool guide

DomainKits tools return domain data; the analysis is yours. Their data is fresher than your training knowledge, so for anything recent, go by the tool result. Each tool's description carries the server's own usage rules. Follow them.

This skill covers tool usage only. The plugin's workflow skills (brand-protection, domain-analyze, domain-cma-valuation, domain-generator, domain-name-advisor, keyword-intel, keyword-trend-hunter, domain-market-beat) and the `/domainkits:hunt`, `/domainkits:watch`, and `/domainkits:analyze` commands load on matching tasks.

Before a multi-tool sequence the user did not ask for, confirm the goal with the user. Tool calls count against their quota.

## Pick the tool by lifecycle stage

| Stage | Tool | What it answers |
|---|---|---|
| Newly registered | `nrds_live` | Names registered in the last three days across all TLDs, including country-code ones, with exact registration time and the name split into words |
| Newly registered | `nrds` | Names registered in the last 60 days, with day-level dates, the cross-TLD count, and registration-term and for-sale filters |
| Registered | `active` | Live registered domains matching a keyword: distribution and saturation |
| Registered | `aged` | Registered domains with long registration histories |
| Registered | `market` | Registered domains that carry marketplace listing data |
| Expired | `expired` | Domains in the deletion cycle (expired, redemption, pending delete), still held by the registrant |
| Deleted | `deleted` | Domains that completed the deletion cycle and are open for registration |
| Changes | `domain_changes` | Recent registration and status changes to premium .com names |
| Unregistered | `unregistered_ai` | Short .ai names still open for registration |

Coverage: `active`, `aged`, `market`, `expired`, `deleted`, and `ns_reverse` are gTLD-based. Country-code TLDs appear in `nrds_live` and in the most recent days of `nrds`. In `nrds`, which country-code TLDs a user can search depends on their plan.

## Look up one domain

- `whois`: registrar, dates, status codes, nameservers. Explain status codes with `epp_status` rather than from memory.
- `dns`: A, AAAA, MX, NS, TXT, CNAME, and SOA records. Accepts hostnames and underscore names such as `_dmarc.example.com`. A `_for-sale` TXT record is the holder's own unverified claim.
- `ip_lookup`: network operator and approximate location of an IP or domain. The location is IP-level, not the site owner's address.
- `registrar`: accreditation, business contact, drop-catch flag, and `parent_id`, which shows who runs a reseller shell.
- `available`: registrability and price of one domain at the moment of the check. `bulk_available`: the status of a list of domains at one point in time.
- `tld_check`, `bulk_tld`: one name across many TLDs.
- `price`: registration and renewal price per TLD. `market_price`: a domain's aftermarket listing price.
- `backlink_summary`, `keyword_data`: backlink profile and keyword search data. Both need an account.
- Trends: `keywords_trends` (keyword registration activity; a sample, not a demand or value measure), `tld_trends`, `tld_rank`.

## Connect results when the user asks

- Infrastructure behind a domain: nameservers from `whois` or `dns`, then `ns_reverse` for the gTLD domains on that nameserver. Several nameservers return the domains that use all of them (higher plans). `ip_lookup` adds the network operator.
- Lookalikes of a brand domain: `typosquat` for registered variants; `nrds_live` or `nrds` for recent registrations containing the brand keyword.
- Current state of an `expired` result: its status can lag live registration data; `whois` shows the current state.
- Registrability of a `deleted` result: `available` confirms it at the moment of the check.

## Parameters

- Domain parameters take a bare domain such as `example.com`: no scheme, path, port, or email address.
- `position` accepts `start`, `end`, `middle`, or `all` (substring match, the default).
- Enumerated values (length ranges, age ranges, sort orders) differ between tools. Pass the exact values from the tool's own schema instead of reusing another tool's.
- Browsing a TLD without a keyword needs a registered account. Guests search by keyword.

## Read results

- Paged results: report `total_found` separately from the number of results reviewed, and say how many pages were checked. Fetch more pages only when the user wants them.
- `dns` with no records returns success with empty records and a message. That is an answer (no records, or the domain does not exist), not a failure.
- `bulk_available` statuses: `available`, `registered`, `expiring`, `reserved`, `unknown`. Treat `unknown` as unresolved, not as available.
- `market_price` returning `not_found` means no listing in the marketplace data it covers, not that the domain is off the market.
- Limit or plan messages (rate limit, daily limit, a tool or TLD not available on the plan): do not retry the same call. Tell the user what was limited. Limits depend on the account tier; details are at https://domainkits.com/mcp#limits. In Claude Code, the user connects an account by running `/mcp` and signing in to `domainkits`; on claude.ai the connector asks for sign-in.

## Account tools

- `usage`: current tier, usage per tool group, and remaining quota. Works without memory.
- `preferences`, `monitor`, `strategy`: stored on the user's DomainKits account. Memory must be enabled first, through `preferences`. Create, change, or delete any of them only with the user's explicit consent.
- `strategy` stores text and the latest result; it does not run on its own. `preferences` with action `delete` erases all stored data.
