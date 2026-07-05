# Info Layer Spec v0.1
Date: 2026-07-05
Status: Draft
Closes: O1 (schema), A-O2 (context packs)

## 1. Purpose
Single source of truth about the company. Dual-rendered: human UI + agent context packs. Every module and every agent grounds through it.

## 2. Entity types
| Type | Contains | Example |
|------|----------|---------|
| Company | Identity, legal, locations, fiscal, tone-of-voice | "Acme Consulting Oy, FI, 12 people" |
| Offering | Services/products, pricing model, delivery model | "CRM implementation, T&M 120e/h" |
| Policy | Rules agents/humans must follow | "Discounts >10% need owner approval" |
| Process | How work is done, step definitions | "Lead -> qualify -> proposal -> close" |
| Capability | Skills, people, capacity (stub v1) | "2 senior devs, React, 60h/wk free" |
| Glossary | Company-specific terms | "'Sprint pack' = 2-wk fixed bundle" |

## 3. Record envelope (every record)
```json
{
  "id": "uuid",
  "type": "Policy",
  "version": 4,
  "status": "active | draft | archived",
  "owner": "user_id",
  "source": "human | agent | import",
  "confidence": 0.0,
  "effective_from": "date",
  "body": {},
  "embedding": "auto-generated on write"
}
```
- Append-only versioning; current = latest active
- Single mutation API: humans and agents propose; policies define what auto-applies vs needs approval

## 4. Context packs (agent grounding)
- Scoped assembly per task: pack(task_type, entities[]) -> structured markdown+JSON
- Tiered by model context budget: S (2k tok) / M (8k) / L (32k), probed per model via adapter
- Deterministic sections first (company, relevant policies), vector retrieval fills remainder
- Pack includes permission summary so the model knows its own limits

## 5. Update loops
- Agents flag stale/contradictory records (confidence decay on age)
- Onboarding agent interviews owner to seed the layer — first-run experience

## 6. Decisions
| # | Decision | Rationale | Date |
|---|----------|-----------|------|
| I1 | Six entity types v1 | Minimal complete set for CRM+Engagement | 2026-07-05 |
| I2 | Append-only versioned records, single mutation API | Auditability; humans and agents equal citizens | 2026-07-05 |
| I3 | Tiered context packs (S/M/L) | BYO-AI models vary; adapter probes and selects | 2026-07-05 |
| I4 | Onboarding = AI interview that seeds the layer | Solves cold-start; SMB owners won't fill forms | 2026-07-05 |

## 7. Iteration log
- v0.1 (2026-07-05): Initial spec
