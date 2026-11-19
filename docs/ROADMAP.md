# Roadmap

> All items unchecked unless marked ✅ Done. Phases 0–6 build the website + admin. Agents come after.

## Phase 0: Repository Setup ✅

- [x] Initialize Git repo
- [x] Create folder structure (docs, apps/web, services/agents, database, scripts, .github)
- [x] Add placeholder READMEs
- [x] Add .gitignore, .env.example, CONTRIBUTING, SECURITY, CODE_OF_CONDUCT
- [x] Add GitHub issue/PR templates
- [x] Write core documentation (this file, OVERVIEW, ARCHITECTURE, AGENTS, DATA_MODEL, DECISIONS, FEATURES)

## Phase 1: Foundation (Website + Admin)

- [ ] Next.js 14 + TypeScript + Tailwind setup
- [ ] Supabase project + Auth (email/phone OTP)
- [ ] Database schema migration (all tables from DATA_MODEL)
- [ ] RLS policies for all tables
- [ ] Shared UI component library (violet/off-white theme)
- [ ] CI pipeline (lint, typecheck, test)
- [ ] Vercel preview deployments

## Phase 2: Storefront (Customer-Facing)

- [ ] Home page with featured products
- [ ] Product listing + filtering
- [ ] Product detail page (variant selector, images, add to cart)
- [ ] Cart + Checkout (COD, UPI, prepaid)
- [ ] Order confirmation page
- [ ] Order tracking (public, by order number + phone)
- [ ] Responsive, mobile-first (Instagram traffic)
- [ ] SEO basics (meta, sitemap, structured data)

## Phase 3: Admin Panel (Owner-Facing)

- [ ] Owner login (Supabase Auth, magic link/OTP)
- [ ] Dashboard: orders today, revenue, low stock, pending approvals
- [ ] Orders list + detail (status timeline, customer info, actions)
- [ ] Order actions: confirm, ship, cancel, refund, print invoice
- [ ] Products CRUD (name, description, price, images, variants)
- [ ] Stock management (view, adjust, reorder alerts)
- [ ] Customers list + detail (order history, tags)
- [ ] Settings: store name, theme colors, shipping rates, payment methods

## Phase 4: Approvals UI (Human-in-the-Loop)

- [ ] Approvals queue in admin panel
- [ ] Approval detail: proposal, reasoning, approve/reject/modify
- [ ] Telegram bot: send approval requests with buttons
- [ ] Deep links from Telegram to admin approval page
- [ ] Real-time updates (Supabase Realtime)
- [ ] Audit log viewer (read-only)

## Phase 5: Polish & Harden

- [ ] Error boundaries, loading states, empty states
- [ ] Accessibility (WCAG AA)
- [ ] Performance: ISR for storefront, caching
- [ ] Tests: unit (utils), integration (API), e2e (critical flows)
- [ ] Monitoring: Sentry, Vercel Analytics
- [ ] Backup/restore verified
- [ ] Documentation for deployment

## Phase 6: Launch Prep

- [ ] Demo seller onboarded (toy seller, 150 orders/month)
- [ ] Load test (simulate 10x traffic)
- [ ] Security review (RLS, secrets, dependencies)
- [ ] Runbook: deploy, rollback, incident response
- [ ] Public repo decision (license, CONTRIBUTING)
- [ ] Launch 🚀

---

## After Phase 6: Agents (One by One)

| Agent | Depends On | Status |
|-------|------------|--------|
| Order Agent | Phase 4 approvals, orders table | Planned |
| Audit Agent | All agents (watches them) | Planned |
| Inventory Agent | Stock table, orders | Planned |
| Review & Support Agent | Customers, orders, templates | Planned |
| Orchestrator | All above agents exist | Planned |

Each agent: build → test in staging → human-in-loop verification → production.

---

## Mermaid Gantt (High-Level)

```mermaid
gantt
    title Shiro Roadmap
    dateFormat  YYYY-MM-DD
    axisFormat  %b %Y

    section Repo Setup
    Phase 0           :done, p0, 2026-11-19, 1d

    section Website + Admin
    Phase 1: Foundation     :active, p1, after p0, 14d
    Phase 2: Storefront     :p2, after p1, 21d
    Phase 3: Admin Panel    :p3, after p2, 21d
    Phase 4: Approvals UI   :p4, after p3, 14d
    Phase 5: Polish         :p5, after p4, 14d
    Phase 6: Launch Prep    :p6, after p5, 14d

    section Agents (Sequential)
    Order Agent     :crit, a1, after p6, 14d
    Audit Agent     :a2, after a1, 10d
    Inventory Agent :a3, after a2, 14d
    Review Agent    :a4, after a3, 14d
    Orchestrator    :a5, after a4, 10d
```

---

## Progress Checklist (Copy to Track)

```
Phase 0: Repository Setup          [##########] 100% ✅
Phase 1: Foundation                [          ]   0%
Phase 2: Storefront                [          ]   0%
Phase 3: Admin Panel               [          ]   0%
Phase 4: Approvals UI              [          ]   0%
Phase 5: Polish & Harden           [          ]   0%
Phase 6: Launch Prep               [          ]   0%
────────────────────────────────────────────────
Order Agent                        [          ]   0%
Audit Agent                        [          ]   0%
Inventory Agent                    [          ]   0%
Review & Support Agent             [          ]   0%
Orchestrator                       [          ]   0%
```