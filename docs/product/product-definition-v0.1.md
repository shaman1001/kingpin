# Product Definition v0.1
Date: 2026-07-05
Status: Draft — foundation for iteration

## 1. Product
AI-native modular business OS for SMBs. Combines ERP, CRM, and capability management on a shared, AI-and-human-readable company information layer. Agents act across modules; the info layer is the context spine and source of truth.

## 2. Market gap
Existing SMB tools (Odoo, HubSpot, Pipedrive, NetSuite) bolt AI onto legacy schemas. No product has an AI-native data model where agents are first-class actors and company knowledge is structured, versioned, and authoritative.

## 3. Decisions log
| # | Decision | Rationale | Date |
|---|----------|-----------|------|
| D1 | Target: SMB 1-50 employees, architecture must scale beyond | Fast time-to-value, avoid enterprise complexity; no rewrite later | 2026-07-05 |
| D2 | Vertical order: Services -> e-commerce -> manufacturing | Services SMBs have lowest data-model complexity, highest pain in project/invoice/CRM flow, fastest AI-delivery leverage | 2026-07-05 |
| D3 | Build order: Company Info Layer + CRM first | Info layer proves the thesis; CRM is fastest path to daily-use value | 2026-07-05 |
| D4 | Projects/Engagements are a core entity from day one | What is sold must live somewhere: feeds invoice generation now, AI-assisted delivery later | 2026-07-05 |

## 4. Core entity graph (draft)
Company Info Layer (spine)
- Company profile: identity, offerings, pricing models, policies, tone
- Capabilities: skills, people, capacity (stub in v1, full module later)

CRM module
- Account -> Contact -> Opportunity -> **Engagement (project/sold work)**
- Engagement -> Deliverables -> Time/Items -> Invoice basis

Key principle: Engagement is the bridge entity. CRM closes into it, invoicing reads from it, AI delivery assistance later operates on it.

## 5. AI-native principles
1. Agent-first: agents read/write the same entities humans do, governed by the info layer
2. Info layer is primary asset, modules are consumers
3. Structured + versioned + authoritative (not a wiki, not just embeddings)
4. Starts trivially simple, grows with the company

## 6. Scope v1 (proposed)
IN: Info layer, CRM pipeline, Engagement entity, invoice-basis data (not invoice sending), 1 core agent (context-aware assistant across CRM+info)
OUT (later): capability mgmt module, e-commerce/manufacturing verticals, accounting integration, AI-assisted delivery

## 7. Open items
- O1: Info layer schema — CLOSED by info-layer-spec-v0.1
- O2: Agent permission model — CLOSED by A5
- O3: Invoice generation: export/integrate to existing tools — CONFIRMED by M3
- O4: Tech architecture doc — CLOSED by architecture-v0.1

## 8. Iteration log
- v0.1 (2026-07-05): Initial definition from decisions D1-D4
