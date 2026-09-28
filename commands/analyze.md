---
description: Full due diligence on one domain: registration, DNS, backlinks, value, market signals
argument-hint: <domain>
---

Run a full due-diligence pass on the domain: $ARGUMENTS

1. If no domain was provided, ask which domain to analyze and stop until given. The user invoked this command explicitly, that is consent for the data pipeline below; only ask a clarifying question first if the goal is genuinely ambiguous (buying vs. selling vs. monitoring changes the emphasis, not the pipeline).
2. Run the core pipeline in parallel where possible: `whois` (registration data), `dns` (records), `available` (status and pricing).
3. Deepen along the user's goal and tier: `backlink_summary` (link profile), `keyword_data` (search demand), `market_price` (aftermarket listing), `market` (marketplace signals).
4. If a tool returns a quota or tier-lock error, skip it, note what was unavailable and why, and continue with the rest. Never retry.
5. Deliver a clear assessment the user can act on: current status, price context, key risks, and the evidence behind each claim. Clearly separate retrieved data from your own inference. If the user asks for a buy / pass recommendation, give one explicitly labeled as opinion, not fact.
6. Offer natural follow-ups: `/domainkits:hunt` for alternatives, `/domainkits:watch` on the underlying brand or keyword, or (only with explicit consent) a `monitor` on this domain.
