# Modularity & Scope Analysis v0.1
Date: 2026-07-05
Status: Accepted 2026-07-05 — D5/D6 registered in DECISIONS.md
Question: Are the 1-50 employee and services-first limits necessary, or can modular design address a larger crowd immediately?
Sources: web research 2026-07-05 (SaaStr, Rippling, SaaS Mag, BVP, ERP Research, brandhistories)

## 1. Evidence from advanced SaaS products

| Company | Pattern | Lesson for us |
|---------|---------|---------------|
| Rippling | "Compound startup": 10+ product lines >$1M ARR on one shared Employee Graph; 115-125% NRR; multi-product cos grow ~21% faster (2026 benchmarks) | Shared-spine + parallel modules is validated — but every module shares **one buyer, one data graph, one GTM motion**. Compound architecture ≠ broad targeting |
| HubSpot | SMB marketing wedge (2006) -> multi-hub -> upmarket only from ~2019; ARPU $6.5k->$11.2k via mix shift | Even the best SMB platform waited ~a decade to widen. Wedge first, expand on a working motion |
| Shopify | SMB e-commerce wedge -> platform -> Plus upmarket after core dominance | Same sequence |
| Odoo | Maximal modularity, horizontal ambition: 16k+ modules, decision paralysis, 12-24 wk partner-led implementations, $25k-150k | **Modularity without opinionation transfers integration cost to the customer.** This is the pain we exploit (P3, F5) — going broad-modular recreates it |
| Vertical AI (2025-26) | Vertical SaaS growing ~2x horizontal; 35-60% higher retention; horizontal SaaS valuations down ~35% YoY; vertical AI competes for labor budgets (60-70% of spend) | AI-native wedges win by going deep on a workflow, not wide on a category |

## 2. Analysis

### Q1: Is the 1-50 employee limit necessary?
It was never a product cap — D1 already says "architecture scales beyond." The limit is a GTM focus. Keep it as such, but stop presenting it as a boundary:
- Multi-tenant architecture, RBAC, event log already scale past 50 seats; nothing in v1 scope hard-codes company size.
- What a >50 GTM would force *now*: SSO, compliance certifications, procurement cycles, multi-entity — pure roadmap drag against the 2-week time-to-value promise (P3).
- Verdict: **beachhead, not limit.** Product story says "grows with you"; sales targets 5-30.

### Q2: Is services-first necessary?
Split the question into architecture vs GTM:

**Architecture — no, and we should design as if it isn't.** The spine is already vertical-agnostic: Info Layer entity types (Company, Offering, Policy, Process, Capability, Glossary), CRM pipeline, agent runtime, MCP surface apply to any SMB. Verticality only enters at:
1. Engagement semantics (time & materials -> invoice basis is services-shaped)
2. Onboarding interview content
3. Templates, defaults, agent playbooks

**GTM — yes, keep it.** Selling "for everyone" triggers the category-confusion risk already flagged (market-analysis §4). Odoo shows modularity alone doesn't deliver time-to-value. Vertical depth is what makes the AI agent actually good (F7: "can we take this job?" requires domain semantics).

### Q3: Can modular design address a larger crowd immediately?
Partially, and cheaply: if the spine stays vertical-agnostic and vertical logic lives in **packs** (templates + entity subtypes + interview scripts + agent playbooks), then non-services companies can self-serve the Info Layer + CRM + assistant from day one — we simply don't optimize or market for them yet. The larger crowd is captured **by architecture, not by GTM spend.**

## 3. Product story reframe (the deliverable)

> **Horizontal spine, vertical packs.**
> The Info Layer + BYO-AI via MCP is a universal company asset — works for any business, any AI, any size. Capability modules ship as opinionated vertical packs; the Services Pack (CRM -> Engagement -> invoice basis) is first. New verticals = new packs on the same spine, not new products.

This gives marketing the broad ambition ("AI-native business OS that grows with you, works with any AI") while sales stays pointed at services 5-30. It also makes the e-commerce/manufacturing roadmap (D2) legible as pack releases rather than re-platforms.

## 4. Design implications (feed into v1 build plan)
- Engagement becomes a **generic container of sold work** (parties, commercial model, deliverables, billing basis); services semantics (T&M, hours) live in the Services Pack as subtypes/templates — not in the core schema.
- Onboarding interview (I4) is **template-driven per vertical**; v1 ships the services template only.
- No company-size assumptions anywhere in schema, pricing logic, or RBAC.
- Pack = versioned bundle: entity subtypes + policies + process templates + interview script + agent playbooks. Define the pack format in the build plan.

## 5. Decisions
| # | Decision | Rationale | Date |
|---|----------|-----------|------|
| D5 | Core spine is vertical- and size-agnostic; all vertical semantics live in packs (templates, subtypes, playbooks) | Captures larger market via architecture; keeps Odoo-style config burden out of the core | 2026-07-05 |
| D6 | D1/M1 reframed as GTM beachhead, not product caps; product story = "horizontal spine, vertical packs", messaging leads "grows with you" | Every successful analog (HubSpot, Shopify, Rippling) sequenced wedge -> expand; vertical AI outperforms horizontal 2025-26 | 2026-07-05 |

## 6. Iteration log
- v0.1 (2026-07-05): Initial analysis from web research + existing docs D1-M3; accepted same day, D5/D6 registered
