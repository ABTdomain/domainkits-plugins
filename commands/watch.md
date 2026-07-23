---
description: Watch a brand or keyword across new domain registrations -- spot conflicts, typosquats, and threats early
argument-hint: <brand or keyword>
---

Watch domain registrations around a brand or keyword: $ARGUMENTS

1. If no term was given, ask what to watch and which angle matters most (brand protection or security) and stop until given. If provided, infer the angle from context and confirm in one line.
2. Sweep current exposure (gTLD zones): `nrds` for recent registrations containing or resembling the term; `tld_check` / `bulk_tld` for where the exact name is registered vs. still open.
3. For suspicious hits, pivot to infrastructure: `whois` + `dns` to get registrant and nameservers, then `ns_reverse` to enumerate sibling gTLD domains on the same nameservers (one bad domain often exposes the whole campaign). Feed notable siblings back through the same triage. Enrich with `safety` (reputation) and `active` (what is hosted).
4. On quota or tier-lock errors: skip, note what was unavailable, continue. Never retry.
5. Report in three buckets, each with its evidence: (1) likely benign, (2) brand conflicts worth action (including which open TLDs are worth defensive registration), (3) suspicious lookalikes worth escalation.
6. Offer follow-ups: write the triage report to a file, repeat this sweep on a schedule, `/domainkits:analyze` on specific hits, or (only with explicit consent) server-side `monitor`s on named domains or a recurring `strategy` for the term.
