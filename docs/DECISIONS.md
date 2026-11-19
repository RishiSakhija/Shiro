# Decision Log

> Format: Date | Decision | Who Decided | Context

## 2026-11-19 — Project Name: Shiro

- **Decision**: Name the project "Shiro" (白 — Japanese for "white", fits violet/off-white theme)
- **Who**: Product Lead
- **Context**: Short, memorable, works in English and Hindi contexts. No trademark conflicts found in quick search.

## 2026-11-19 — Demo Category: Toys

- **Decision**: First seller vertical = toys (educational, wooden, soft toys)
- **Who**: Product Lead
- **Context**: Demo seller is a home-based toy seller (~150 orders/month, Instagram primary). Toys have variants (color, size), seasonal demand, gift-wrapping needs — good for testing inventory and order agents.

## 2026-11-19 — Seller Profile

- **Decision**: Target small Indian online sellers (home-based, Instagram/WhatsApp, 50–500 orders/month)
- **Who**: Product Lead
- **Context**: Underserved by existing tools. Pain points: COD fraud, RTO, manual ops, multilingual support (Hindi/Gujarati). Willing to pay ₹500–2000/month for time savings.

## 2026-11-19 — Theme: Violet & Off-White

- **Decision**: Primary brand colors = Violet (#6D28D9) + Off-White (#FAFAF9)
- **Who**: Tech Lead + Product Lead
- **Context**: Violet = trust, premium; Off-white = clean, readable. Works for both storefront (customer trust) and admin (long sessions). Tailwind config will define `shiro-violet` and `shiro-offwhite` palette.

## 2026-11-19 — MVP Feature Lists

- **Decision**: Split features into MVP (must have for launch) vs Later (post-launch)
- **Who**: Tech Lead + Product Lead
- **Context**: See [FEATURES.md](FEATURES.md). MVP focuses on: orders, products, stock, approvals, COD fraud flow. Later: loyalty, subscriptions, multi-seller marketplace, advanced analytics.

## 2026-11-19 — Tech Stack Commitments

- **Decision**: Next.js (web), Supabase (DB+Auth), Python/LangGraph (agents), Telegram (approvals), Vercel+Render (hosting)
- **Who**: Tech Lead
- **Context**: All have generous free tiers. Supabase RLS solves multi-tenant auth. LangGraph is purpose-built for agent workflows. Telegram is universal in India for business comms.

## 2026-11-19 — Human Approval Required for All Agent Actions

- **Decision**: No agent executes without explicit owner approval (except read-only Audit Agent)
- **Who**: Tech Lead + Product Lead
- **Context**: Core differentiator. Small sellers fear losing control. Audit trail protects both seller and platform.

## 2026-11-19 — COD Fraud & RTO as Primary Agent Use Case

- **Decision**: Order Agent's first job = flag suspicious COD orders, request verification
- **Who**: Product Lead
- **Context**: COD is ~60% of orders for small Indian sellers. Fake orders = wasted shipping + RTO charges. High impact, clear ROI.

## 2026-11-19 — Multilingual Replies (Hindi/Gujarati) in Review Agent

- **Decision**: Review & Support Agent must draft replies in Hindi and Gujarati (Latin script + Devanagari)
- **Who**: Product Lead
- **Context**: Seller's customers prefer local language. Agent uses templates + LLM translation, owner approves before send.

## 2026-11-19 — Repository Structure (Monorepo-Style)

- **Decision**: Separate folders for web (Next.js), agents (Python), database (SQL), docs
- **Who**: Tech Lead
- **Context**: Clear ownership, independent deployments, easy to split repos later if needed. No Turborepo/Nx yet — add when complexity demands.