# Kingpin — Executive Summary
Date: 2026-07-05
Sources: product-definition-v0.1, architecture-v0.1, info-layer-spec-v0.1, market-analysis-v0.1, DECISIONS.md, iteration 0

## What it is
Kingpin is an AI-native modular business OS: a **horizontal spine** (Company Info Layer + CRM + agent runtime — vertical- and size-agnostic) with **vertical packs** carrying domain semantics; the Services Pack ships first (D5/D6). The Info Layer is a structured, versioned, authoritative knowledge spine that both humans and AI agents read and write. Agents are first-class actors under the same RBAC as users, and customers can bring any AI (managed, own API key, or self-hosted) via MCP. GTM beachhead — not a product cap — is services SMBs of 5–30 people; messaging leads "grows with you."

## Why it wins (market gap)
Incumbents (Odoo, HubSpot, NetSuite, vertical tools) bolt AI onto legacy schemas. SMBs run 8+ fragmented tools, spend ~23% of software budget on glue, and owners do admin at night. No product treats company knowledge as a primary, AI-readable asset — and incumbents monetizing their own AI can't credibly offer BYO-AI. Positioning: lead with AI outcomes and BYO-AI, not the ERP/CRM category (M2).

## Core design
- **Info Layer** (spine): 6 entity types — Company, Offering, Policy, Process, Capability (stub), Glossary. Append-only versioned records, single mutation API for humans and agents, tiered context packs (S/M/L) for grounding any model. Onboarding = AI interview that seeds the layer.
- **Engagement** is the bridge entity: CRM closes into it, invoice basis reads from it, AI-assisted delivery later operates on it. Kills unbilled-work leakage. In core it is a generic container of sold work; services semantics (T&M, hours) live in the Services Pack (D5).
- **MCP-native**: every module exposes its capabilities as MCP servers — one tool surface for our agents, customer's frontier model, or self-hosted models.
- **Guardrails**: agents share user RBAC plus configurable approval gates; all actions logged to event log.

## Stack (decided)
TypeScript backend, React/Next.js frontend, PostgreSQL + pgvector as sole datastore v1, thin own agent runtime (no heavy framework), managed auth, containers on managed cloud. Accounting is integrated, never built (M3).

## Scope v1
IN: Info Layer, CRM pipeline, Engagement entity, invoice-basis data, one context-aware assistant agent.
OUT: capability module (full), other verticals, accounting integration, AI-assisted delivery, invoice sending.

## Status & next
Definition phase (iteration 0) complete: 4 docs, 20 binding decisions (D1–D6, A1–A7, I1–I4, M1–M3) incl. the horizontal-spine/vertical-packs reframe (iteration 0.1). Next: v1 build plan (B-decisions) incl. pack format definition, then repo scaffold.
