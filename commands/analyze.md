---
description: Full due diligence on one domain — registration, DNS, safety, backlinks, value, market signals
argument-hint: <domain>
---

Run a full due-diligence pass on the domain: $ARGUMENTS

1. If no domain was provided, ask which domain to analyze and stop until given. The user invoked this command explicitly — that is consent for the data pipeline below; only ask a clarifying question first if the goal is genuinely ambiguous (buying vs. selling vs. monitoring changes the emphasis, not the pipeline).
2. Start with the `analyze` workflow tool from the domainkits MCP server — it bundles WHOIS, DNS, availability, and core market signals in one call.
3. Deepen along the user's goal and tier: `valuation_cma` (comparable-sales value), `backlink_summary` (link profile), `keyword_data` (search demand), `market_price` and `sale_chance` (liquidity), `safety` (reputation).
4. If a tool returns a quota or tier-lock error, skip it, note what was unavailable and why, and continue with the rest — never retry.
5. Deliver a verdict the user can act on: buy / hold / pass, the price context, key risks, and the evidence behind each claim — clearly separating retrieved data from your own inference. Disclose affiliate links if any appear in results.
6. Offer natural follow-ups: `/domainkits:hunt` for alternatives, `/domainkits:watch` on the underlying brand or keyword, or — only with explicit consent — a `monitor` on this domain.
