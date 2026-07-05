# CLAUDE.md — project instructions for Claude Code

## What this is
Kingpin: AI-native modular business OS for services SMBs (1-50 people). Info Layer (company knowledge spine) + CRM + Engagement first; ERP/capability modules later. BYO-AI via MCP.

## Read first
1. docs/decisions/DECISIONS.md — 18 binding decisions (D1-M3)
2. docs/product/product-definition-v0.1.md
3. docs/architecture/architecture-v0.1.md
4. docs/architecture/info-layer-spec-v0.1.md

## Working rules
- Effective communication, no long stories
- Document every plan, decision, architecture change, iteration BEFORE/WITH the code
- New decisions: assign ID (B=build, S=security, U=UX), add to DECISIONS.md with rationale
- Each iteration gets a file in docs/iterations/
- Stack (decided): TypeScript backend, React/Next.js frontend, PostgreSQL+pgvector, MCP for all AI interfaces, thin own agent runtime
- Local LLMs allowed for coding subtasks where token-economical (A7)

## Current state
Definition phase complete (iteration 0). Next: v1 build plan, then scaffold.
