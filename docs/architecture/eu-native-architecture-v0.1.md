# EU-Native Architecture Proposal v0.1
Date: 2026-07-05
Status: Proposal — decisions marked PROPOSED pending confirmation
Depends on: architecture-v0.1, modularity-scope-analysis (D5/D6)
Question: Plan for full EU data residency / sovereignty, given US provider instability.
Sources: web research 2026-07-05 (eualternative.eu, InfoQ, Eliatra, Mistral, european-alternatives.eu, simplyblock, Callista benchmark via fromeuropewithlove)

## 1. Sovereignty model — three layers, not one switch
"EU data residency" is not one thing. The CLOUD Act follows **ownership, not geography**: a US-owned provider must comply with US data requests even for EU-region data. AWS launched its European Sovereign Cloud (Jan 2026, eusc-de-east-1, ~15% premium, ~90 of 240+ services, no GPU/most Bedrock) and critics — and Microsoft's own counsel under oath before the French Senate — confirm US-owned "sovereign" clouds cannot rule out US access.

| Layer | Guarantee | Example | CLOUD Act exposure |
|-------|-----------|---------|--------------------|
| L1 Residency | Data stored/processed in EU | AWS eu-central-1, Azure EU Data Boundary, AWS EUSC | **Yes** (US ownership) |
| L2 EU-owned | EU-owned operator, EU jurisdiction end-to-end | Hetzner, OVHcloud, Scaleway, UpCloud, Exoscale, IONOS | No |
| L3 Self-hosted | Customer's own infra, single-tenant deploy | On-prem / customer's EU cloud account | No |

Target: **L2 as our default**, L3 already implied by architecture principle 4 ("single-tenant deployable later") and A2 self-hosted AI mode.

## 2. Why this is cheap for us
Existing decisions already make the stack ~90% sovereignty-portable:
- **A3** Postgres + pgvector sole datastore — runs identically on any EU provider (managed Postgres at Scaleway/OVH/UpCloud; self-managed on Hetzner)
- **A1/A4** MCP + thin own runtime — no US-SaaS agent framework dependency
- **A2** model adapter with self-hosted mode — the AI sovereignty escape hatch is already designed
- Containers on managed cloud, no K8s dependency — portable by construction
The gaps are the **managed periphery**, not the core: hosting default (Fly/Render = US), auth default (Auth0/WorkOS/Clerk = US), managed-AI default (US frontier vendors), email, observability, payments.

## 3. Proposal: EU-native by default, not as a special edition
Rationale: our ICP includes EU services SMBs (company examples are Finnish Oy); EU-owned clouds deliver 2–8x compute per euro vs AWS with zero egress fees (Hetzner ~14x value-per-compute-unit, Callista 2/2026); and sovereignty is already our positioning wedge (P7 vendor-AI-lock-in fears, F3 BYO-AI). Being EU-native by default is cheaper AND a near-unique sales story: **"your data and your AI never leave EU jurisdiction — provably, by ownership, not by promise."**

### 3.1 Reference stack (EU-sovereign profile)
| Layer | Choice (v1 recommendation) | Notes |
|-------|---------------------------|-------|
| Compute/hosting | Hetzner (DE/FI regions) or UpCloud (FI) | Pick at build plan; both 100% EU-owned; Hetzner best price-perf, Finland DCs |
| Managed Postgres + pgvector | Scaleway / OVH / UpCloud managed DB, or self-managed on Hetzner | Requirement: pgvector support + EU-owned operator |
| Auth | OIDC standard; ZITADEL (CH, EU-cloud or self-host) — alt: Ory (DE), Keycloak (self-host) | Replaces Auth0/WorkOS/Clerk default in architecture-v0.1 §4. Social login (Google/Apple/Microsoft) fully supported as upstream federated IdPs — login method, not data hosting: accounts/sessions/tokens stay on the EU IdP; upstream only returns identity claims. Disable-able per tenant for strict-sovereignty customers |
| LLM — managed mode | Mistral La Plateforme (EU-owned, EU-hosted; Medium 3.5 flagship 4/2026) | Only vendor with frontier API + open weights + EU governance |
| LLM — BYO/self-hosted | Any endpoint via A2 adapter; open weights (Mistral Medium 3.5 runs on 4 GPUs) on EU GPU cloud (Scaleway, Mistral Compute) | Already designed |
| Embeddings | EU-hosted or self-hosted model | Info Layer auto-embeds on every write (I-spec §3) — this flow must stay in-profile |
| Email | EU provider (Scaleway TEM / Brevo / Mailjet) | |
| Observability | OpenTelemetry + self-hosted Grafana stack / EU-hosted Sentry alternative | No US SaaS telemetry in data path |
| Payments (later) | Mollie / Adyen (EU) over Stripe | Card data tokenized either way; decide at monetization |
| DNS/CDN | EU registrar; CDN only if needed (Bunny.net = SI) | |

### 3.2 The sovereignty boundary rule
Enumerate **every external data flow** and keep each one inside the profile: LLM inference, embeddings, auth tokens/PII, transactional email, logs/traces/errors, backups, DNS, payments, support tooling. Concretely: every third-party dependency sits behind an adapter (we already do this for models via A2) with at least one EU-sovereign implementation. New dependencies must declare their sovereignty layer in the PR that introduces them.

### 3.3 Deployment profiles
| Profile | Infra | AI default | Who it's for |
|---------|-------|-----------|--------------|
| EU-Sovereign (default) | EU-owned cloud (L2) | Mistral EU or BYO | All customers; the launch product |
| Hyperscaler (optional, later) | US hyperscaler EU region (L1) | Any | Only if a customer/integration demands it |
| Self-hosted (later, per principle 4) | Customer infra (L3) | Self-hosted models | Regulated/paranoid SMBs; premium tier |

Multi-tenant single-region EU at v1; per-profile expansion is deployment work, not re-architecture.

### 3.4 Trade-offs accepted
- Fewer managed services on EU-owned clouds -> we self-manage more (mitigated by A3 single-datastore simplicity)
- Mistral Medium 3.5 vs US frontier models: adequate for context-pack-grounded CRM tasks; customers wanting Claude/GPT use BYO-key mode knowingly (their key, their data agreement — sovereignty responsibility transfers explicitly)
- No CloudFront-class global CDN — irrelevant for EU SMB app traffic

## 4. Proposed decisions (PROPOSED — not yet in DECISIONS.md)
| # | Decision | Rationale |
|---|----------|-----------|
| A8 (proposed) | EU-native by default: primary deployment on EU-owned infrastructure (L2); no US-owned service in the customer-data path | CLOUD Act follows ownership; 2-8x cost advantage; differentiator |
| A9 (proposed) | Every external dependency behind an adapter with ≥1 EU-sovereign implementation; new dependencies declare sovereignty layer | Keeps L2 guarantee enforceable as the stack grows |
| S1 (proposed) | Sovereignty layers L1/L2/L3 defined; customer-facing guarantee = "customer data never leaves EU jurisdiction (ownership, not geography)" in default profile | First security-register decision; makes the promise auditable |
| M4 (proposed) | Sovereignty joins BYO-AI as a lead positioning wedge (extends P7/F3) | Near-unique vs US incumbents; incumbents structurally cannot follow |

## 5. Open items
- EU-O1: Pick concrete hosting + managed-Postgres provider at build plan (Hetzner vs UpCloud vs Scaleway; criterion: managed pgvector, FI/DE latency, backup story)
- EU-O2: EU-hosted error tracking choice (self-hosted Sentry vs Grafana-stack-only)
- EU-O3: Aggregate embedding/inference quality gap Mistral vs US frontier for our agent tasks — benchmark during v1 with real context packs
- EU-O4: Backup/DR across two EU-owned providers (avoid single-operator risk)

## 6. Iteration log
- v0.1 (2026-07-05): Initial proposal from web research; A8/A9/S1/M4 proposed
