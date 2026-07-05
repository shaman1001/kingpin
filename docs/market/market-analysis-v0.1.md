# Market Analysis v0.1
Date: 2026-07-05
Status: Draft
Sources: web research 2026-07-05 (Mordor Intelligence, industry comparisons, PYMNTS, US Chamber)

## 1. Market needs and pains

### Macro
- SMB software market ~$77B (2026) -> ~$108B by 2031, ~6.9% CAGR
- Average SMB runs 8+ SaaS tools; ~23% of software budget spent on connecting tools, not licenses
- 66% of small firms cite integration headaches as a top pain
- ~73% of small businesses still handle 3+ core operations manually (scheduling, invoicing, customer comms)
- SMBs adopt AI faster than enterprises — necessity-driven; 91% of AI-using SMBs report revenue lift

### Pain inventory (ranked for services SMB 1-50)
| # | Pain | Evidence | Our answer |
|---|------|----------|-----------|
| P1 | Tool fragmentation / integration tax | 8+ tools, 23% budget on glue, data trust erosion | One entity graph, modules on shared spine |
| P2 | Owner does admin at night: quotes, invoices, chasing payments | Consistent across sources | Agents draft quote->engagement->invoice basis; owner approves |
| P3 | ERP too heavy, too costly, adoption fails | 5-yr TCO $50-240K; only 26% of employees use ERP post go-live; 70%+ projects miss goals | 2-week time-to-value, AI-interview onboarding, no implementation partner |
| P4 | AI is bolt-on: copilots without unified data | Cross-domain AI questions impossible on siloed data | AI-native data model; agents answer "can we take this job and stay profitable?" |
| P5 | Company knowledge lives in owner's head | No product addresses this for SMB | Info Layer as first-class product |
| P6 | Unbilled work / revenue leakage | 10-20% hidden revenue loss reported in field services | Engagement entity ties delivery->invoice basis automatically |
| P7 | Vendor AI lock-in fears / data privacy | Rising with AI adoption | BYO-AI (managed / own key / self-hosted) — near-unique |

### ICP v1
Services companies 5-30 people (consultancies, agencies, IT services, professional services): sell time+expertise, run HubSpot-free-tier + spreadsheets + accounting tool, owner is bottleneck.

## 2. Where we outperform current solutions

### Competitive frame
| Competitor | Their position | Their weakness we exploit |
|------------|----------------|---------------------------|
| Odoo | Modular, cheap, broad | Legacy schema, needs implementation partner/dev resources, AI bolt-on |
| HubSpot | Best SMB CRM, AI features | CRM-only spine; no engagement->delivery->invoice chain; expensive tiers |
| NetSuite/Dynamics | Deep ERP | Cost/complexity absurd for 1-50; 3-6+ month implementations |
| Vertical tools (Jobber etc.) | Great niche UX | Fracture at scale, accounting integrity breaks, no AI depth |
| Agent startups / DIY (n8n, Copilot Studio) | Cheap automation | No system of record; agents on fragmented data — 75% of in-house agent builds fail |

### Outperformance theses (functionality)
| # | Capability | Why incumbents can't easily copy |
|---|-----------|----------------------------------|
| F1 | Cross-module agent actions in one command (proposal -> capacity check -> engagement -> invoice basis) | Requires unified entity graph + policy layer; legacy schema retrofit = multi-year rebuild |
| F2 | Info Layer: versioned, authoritative company knowledge for humans and any AI | No incumbent treats company knowledge as primary asset |
| F3 | BYO-AI: managed / own frontier key / self-hosted | Incumbents monetize their own AI; conflict of interest |
| F4 | MCP-native: customer's own external agents operate the system with permissions | Incumbents expose partial APIs, not agent-grade tool surfaces |
| F5 | Onboarding = AI interview, minutes not months | Incumbents' partner-led implementation is their revenue model; won't cannibalize |
| F6 | Zero unbilled work: everything delivered under an Engagement flows to invoice basis | Requires CRM+delivery+billing on one graph |
| F7 | Capability-aware answers: "can we take this job?" uses real capacity/skills data | Unique module combo; nobody models capabilities for SMB |

### Where we do NOT compete (v1)
- Accounting/compliance depth -> integrate (QuickBooks/local equivalents)
- Marketing automation depth -> integrate or defer
- Enterprise multi-entity -> later

## 3. Positioning statement (draft)
"The AI-native business OS that knows your company, runs your sales-to-invoice flow, and works with any AI — yours or ours. Built for services SMBs first; grows with you."

Per D6: ICP (M1) is the beachhead sales target, not the product boundary. Story = horizontal spine, vertical packs; verticals arrive as pack releases (D2 order).

## 4. Risks
| Risk | Mitigation |
|------|-----------|
| Incumbents ship "good enough" AI on installed base | Speed + info layer moat + BYO-AI positioning |
| SMB churn/price sensitivity | Fast time-to-value, land on CRM+info layer, expand modules |
| Trust: agents touching money/customers | Approval gates default-on, full audit log (A5) |
| Category confusion ("another CRM?") | Lead marketing with agent outcomes (F1), not category |

## 5. Decisions
| # | Decision | Rationale | Date |
|---|----------|-----------|------|
| M1 | ICP v1: services companies 5-30 ppl | Sharpest pain fit P1-P6, D2 vertical order | 2026-07-05 |
| M2 | Positioning leads with AI outcomes + BYO-AI, not "ERP/CRM" category | Category terms carry TCO/complexity baggage | 2026-07-05 |
| M3 | Integrate accounting, never build it | Compliance swamp, confirms O3 | 2026-07-05 |

## 6. Iteration log
- v0.1 (2026-07-05): Initial analysis from market research
- v0.1 amended (2026-07-05): Positioning updated per D5/D6 (beachhead framing, "grows with you")
