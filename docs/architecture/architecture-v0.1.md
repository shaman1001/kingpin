# Architecture v0.1 — Initial
Date: 2026-07-05
Status: Draft
Depends on: Product Definition v0.1

## 1. Architecture principles
1. AI-agnostic core: business logic never depends on a specific model vendor
2. Everything is an API: every module capability is callable by humans (UI), agents (tools), and integrations — same endpoints
3. Info layer = context spine: all AI calls are grounded through it
4. Multi-tenant from day one, single-tenant deployable later (scaling per D1)

## 2. High-level system layout

```
+---------------------------------------------+
|  Clients: Web app | Mobile | Chat/agent UI  |
+---------------------------------------------+
|  API Gateway (REST + streaming)             |
+--------------+------------------------------+
|  Modules     |  AI Orchestration Layer      |
|  - CRM       |  - Agent runtime             |
|  - Engagement|  - Model adapter (BYO-AI)    |
|  - (Capab.)  |  - Tool registry (MCP)       |
|  - (ERP)     |  - Guardrails/permissions    |
+--------------+------------------------------+
|  Company Info Layer (versioned, structured) |
+---------------------------------------------+
|  Data: Postgres | Vector index | Event log  |
+---------------------------------------------+
```

## 3. AI interfacing — the core design

### 3.1 MCP as the native AI interface
Every module exposes its capabilities as **MCP (Model Context Protocol) servers**:
- Our hosted AI, customer's frontier model (Claude/GPT/Gemini), or customer's self-hosted model all connect through the same MCP tool surface
- AI-ready for models we've never seen — MCP is the industry-standard plug
- Internal and external agents use identical tools -> no second integration layer

### 3.2 Model adapter (BYO-AI)
| Mode | Description | Notes |
|------|-------------|-------|
| Managed | We provide AI (bundled, per-seat/usage pricing) | Default; we pick best model per task |
| BYO-key | Customer's API key to a frontier vendor | Their cost, their data agreements |
| Self-hosted | Customer points us at an OpenAI-compatible or custom endpoint | For regulated/privacy-sensitive SMBs |

Adapter normalizes: chat/completions, tool calling, streaming, structured output. Capability probing at connect time -> feature-gates agents accordingly.

### 3.3 Grounding & context
- Every agent invocation prefixed with scoped context pack from Info Layer
- Context packs are structured (typed JSON/markdown hybrid), not raw RAG dumps; vector search only for long-tail retrieval
- All agent actions logged to event log -> auditability + training signal

### 3.4 Permissions/guardrails
- Agents have role-based permissions like users (read CRM / write draft / send requires approval)
- Approval gates configurable per company in Info Layer

## 4. Technology options (high level)

| Layer | Option A (chosen/recommended) | Option B | Rationale |
|-------|------------------------------|----------|-----------|
| Backend | TypeScript (Node/NestJS or Hono) | Python (FastAPI) | One language across stack, strong MCP SDK |
| Frontend | React (Next.js) | SvelteKit | Ecosystem, component maturity |
| Primary DB | PostgreSQL | — | Relational graph + JSONB + pgvector |
| Vector | pgvector | Dedicated (Qdrant) | Start in Postgres; split at scale |
| Events/audit | Postgres event table -> NATS/Kafka later | — | Don't over-engineer for 1-50 seats |
| Agent runtime | Own thin runtime on MCP + vendor SDKs | LangGraph/similar | Frameworks churn; MCP does heavy lifting |
| Infra | Containers on managed cloud (Fly/Render/AWS ECS) | K8s | K8s only when scale demands |
| Auth | Managed (Auth0/WorkOS/Clerk) | Own | SSO later for upper SMB |

## 5. Info Layer — structural sketch
- Typed schema: Company, Offering, Policy, Process, Capability, Glossary
- Every record: versioned, owner, effective-date, confidence/source
- Dual rendering: human view (docs-like UI) and agent view (context pack API)
- Single write path — humans and agents propose changes through same versioned mutation API

## 6. Decisions log
| # | Decision | Rationale | Date |
|---|----------|-----------|------|
| A1 | MCP as native AI interface for all modules | Vendor-agnostic, industry standard, one integration surface | 2026-07-05 |
| A2 | Model adapter with 3 modes: Managed / BYO-key / Self-hosted | Product requirement; keeps core AI-agnostic | 2026-07-05 |
| A3 | PostgreSQL + pgvector as sole datastore in v1 | Simplicity, relational integrity, vectors without extra infra | 2026-07-05 |
| A4 | Thin own agent runtime, no heavy agent framework | Frameworks churn; MCP + vendor SDKs sufficient | 2026-07-05 |
| A5 | Agents governed by same RBAC as users + approval gates | Resolves O2; auditability | 2026-07-05 |
| A6 | Backend: TypeScript | Claude builds full solution; one language, best MCP SDK | 2026-07-05 |
| A7 | Local LLMs permitted for coding tasks where token-economical | Cost control during build | 2026-07-05 |

## 7. Open items
- A-O3: Tenancy/data isolation model for self-hosted-AI customers
- A-O4: Offline/degraded mode when customer's own model is down

## 8. Iteration log
- v0.1 (2026-07-05): Initial architecture, AI interfacing design, tech options, amendments A6-A7
