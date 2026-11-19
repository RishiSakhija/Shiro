# AGENTS.md — Rules for AI Coding Tools

This file instructs AI coding assistants (Cursor, Copilot, Claude Code, etc.) on project conventions.

## Tech Stack

| Layer | Tool | Version (Planned) |
|-------|------|-------------------|
| Web Framework | Next.js | 14+ (App Router) |
| Language (Web) | TypeScript | 5+ (strict) |
| Styling | Tailwind CSS | 3+ |
| Database | Supabase (PostgreSQL) | Latest |
| Auth | Supabase Auth | Latest |
| Agents | Python + LangGraph | 3.11+, 0.1+ |
| Hosting | Vercel (web), Render (agents) | — |
| CI/CD | GitHub Actions | — |

## Folder Structure

```
Shiro/
├── apps/web/           # Next.js storefront + admin
├── services/agents/    # Python agent service
├── database/           # SQL migrations, seeds
├── scripts/            # Utility scripts
├── docs/               # All documentation
│   └── assets/         # Logos, banners, diagrams
├── .github/            # Issue templates, PR template, workflows
├── CONTRIBUTING.md
├── SECURITY.md
├── CODE_OF_CONDUCT.md
├── .gitignore
├── .env.example
└── README.md
```

## Naming Rules

| Thing | Convention | Example |
|-------|------------|---------|
| Files (TS/TSX) | kebab-case | `order-card.tsx`, `api-utils.ts` |
| Files (Python) | snake_case | `order_agent.py`, `proposal_builder.py` |
| React Components | PascalCase | `OrderCard.tsx` |
| Functions/Variables | camelCase | `getOrderById`, `isCodOrder` |
| Python Functions/Variables | snake_case | `get_order_by_id`, `is_cod_order` |
| Database Tables | snake_case, plural | `orders`, `order_items` |
| Database Columns | snake_case | `created_at`, `payment_status` |
| Env Variables | UPPER_SNAKE_CASE | `SUPABASE_URL`, `LLM_API_KEY` |
| Git Branches | type/short-desc | `feat/order-agent`, `docs/architecture` |

## Critical Rules

### 1. Never Put Secrets in Code
- No API keys, tokens, passwords in source
- Use `.env.local` (gitignored) for local dev
- Reference `.env.example` for required variables
- Supabase service role key **only** in agent service (server)

### 2. Add Tests for Logic
- Unit tests for: proposal builders, fraud scoring, stock calculations, status transitions
- Integration tests for: API routes, database mutations
- E2E tests for: checkout flow, approval flow
- Target: >80% coverage on business logic

### 3. Explain Before Large Edits
- Before refactoring >50 lines or changing architecture: write a short plan in the PR or comment
- Include: what, why, risks, rollback plan

### 4. Keep Changes Small
- One PR = one feature/fix
- If you touch >5 files, consider splitting
- Small PRs review faster, merge safer

### 5. Database Changes
- All schema changes via migration files in `database/migrations/`
- Never edit production DB directly
- Test migrations on staging first

### 6. Agent Code Rules
- Agents write **proposals only** to `approvals` table
- Never execute side effects directly (no `send_email()`, `update_stock()` in agent)
- All reasoning logged in proposal `payload_json`
- Audit Agent is read-only — never writes proposals

### 7. RLS First
- Every new table: define RLS policies in same migration
- Default: deny all, grant specific
- Test with different auth contexts (anon, customer, owner, service_role)

### 8. Indian Context
- Phone numbers: store as `+91XXXXXXXXXX` (E.164)
- Currency: store as integer paise (₹1 = 100)
- Pincodes: 6 digits, validate on input
- Languages: Hindi (Devanagari + Latin), Gujarati (Latin + script)

## Example: Creating a New Agent Proposal

```python
# services/agents/order_agent/proposals.py
from dataclasses import dataclass
from typing import Literal
import json

@dataclass
class VerifyCodProposal:
    order_id: str
    reason: str
    risk_score: float  # 0.0 - 1.0
    signals: list[str]  # e.g., ["new_customer", "high_value", "address_mismatch"]

    def to_payload(self) -> dict:
        return {
            "proposal_type": "verify_cod",
            "order_id": self.order_id,
            "reason": self.reason,
            "risk_score": self.risk_score,
            "signals": self.signals,
        }

    def to_approval_row(self, agent_name: str) -> dict:
        return {
            "agent_name": agent_name,
            "proposal_type": "verify_cod",
            "payload_json": self.to_payload(),
            "status": "pending",
            "expires_at": "now() + interval '24 hours'",
        }
```

## When Unsure

- Check existing code in `apps/web/` or `services/agents/`
- Read `docs/ARCHITECTURE.md` and `docs/AGENTS.md`
- Ask in PR comments — don't guess