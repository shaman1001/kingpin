# Decision Register
Single index. Details live in the source docs.

| ID | Decision | Source doc | Date |
|----|----------|-----------|------|
| D1 | Target SMB 1-50, architecture scales beyond | product-definition | 2026-07-05 |
| D2 | Verticals: services -> e-commerce -> manufacturing | product-definition | 2026-07-05 |
| D3 | Build order: Info Layer + CRM first | product-definition | 2026-07-05 |
| D4 | Engagement (sold work) core entity day one; feeds invoicing, later AI delivery | product-definition | 2026-07-05 |
| A1 | MCP as native AI interface for all modules | architecture | 2026-07-05 |
| A2 | Model adapter: Managed / BYO-key / Self-hosted | architecture | 2026-07-05 |
| A3 | PostgreSQL + pgvector sole datastore v1 | architecture | 2026-07-05 |
| A4 | Thin own agent runtime, no heavy framework | architecture | 2026-07-05 |
| A5 | Agents under same RBAC as users + approval gates | architecture | 2026-07-05 |
| A6 | Backend: TypeScript | architecture | 2026-07-05 |
| A7 | Local LLMs for coding tasks where token-economical | architecture | 2026-07-05 |
| I1 | Info Layer: 6 entity types v1 | info-layer-spec | 2026-07-05 |
| I2 | Append-only versioned records, single mutation API | info-layer-spec | 2026-07-05 |
| I3 | Tiered context packs S/M/L | info-layer-spec | 2026-07-05 |
| I4 | Onboarding = AI interview seeding the layer | info-layer-spec | 2026-07-05 |
| M1 | ICP v1: services companies 5-30 people | market-analysis | 2026-07-05 |
| M2 | Positioning: AI outcomes + BYO-AI, not ERP/CRM category | market-analysis | 2026-07-05 |
| M3 | Integrate accounting, never build it | market-analysis | 2026-07-05 |
| D5 | Core spine vertical- and size-agnostic; all vertical semantics live in packs (subtypes, templates, interview scripts, agent playbooks) | modularity-scope-analysis | 2026-07-05 |
| D6 | D1/M1 are GTM beachheads, not product caps; product story = "horizontal spine, vertical packs", messaging leads "grows with you" | modularity-scope-analysis | 2026-07-05 |

Next ID prefixes: B = build plan, S = security, U = UX.
