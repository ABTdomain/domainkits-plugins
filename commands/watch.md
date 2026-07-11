---
description: Watch a brand or keyword across new domain registrations — spot conflicts, typosquats, and threats early
argument-hint: <brand or keyword>
---

Watch domain registrations around a brand or keyword: $ARGUMENTS

1. If no term was given, ask what to watch and which angle matters most — brand protection (conflicts, defensive registrations) or security (typosquats, phishing infrastructure) — and stop until given. If provided, infer the angle from context and confirm in one line.
2. Sweep current exposure (gTLD zones): `nrds` for recent registrations containing or resembling the term — watch `prefix_tld_count` (the same prefix appearing across many TLDs means someone is actively building around the name); `brand_match` for conflict scoring; `tld_check` / `bulk_tld` for where the exact name is registered vs. still open.
3. For suspicious hits, pivot to infrastructure — this is the core security move: `whois` + `dns` to get registrant and nameservers, then `ns_reverse` to enumerate sibling gTLD domains on the same nameservers (one bad domain often exposes the whole campaign). Registrar or nameserver concentration across hits (`keywords_trends` quality metrics show this at keyword level) signals a coordinated operation. Feed notable siblings back through the same triage. Enrich with `safety` (reputation — a lagging signal, confirmation not discovery) and `active` (what is actually hosted).
4. On quota or tier-lock errors: skip, note what was unavailable, continue — never retry.
5. Report in three buckets, each with its live evidence: ① likely benign, ② brand conflicts worth action (including which open TLDs are worth defensive registration), ③ suspicious lookalikes worth escalation.
6. Offer follow-ups: write the triage report to a file, repeat this sweep on a schedule, `/domainkits:analyze` on specific hits, or — only with explicit consent — server-side `monitor`s on named domains or a recurring `strategy` for the term.
