# Agent Team

> **Status**: Planned — not implemented. Agents will be built one by one after Phase 1 (website + admin).

## Agent Definitions

| Agent | Job | Inputs | Outputs | Needs Human Approval For |
|-------|-----|--------|---------|--------------------------|
| **Orchestrator** | Routes tasks, coordinates agents, ensures audit trail | New events (order, message, stock change), agent proposals | Task assignments, workflow state | — (coordinates only) |
| **Order Agent** | Processes new orders, flags fraud, manages status | New order, payment info, customer history, address | Fraud flags, status updates, shipment proposals | COD verification, address correction, cancellation, refund |
| **Inventory Agent** | Tracks stock, predicts restock, manages variants | Stock levels, sales velocity, supplier lead times | Low-stock alerts, restock proposals, variant sync | Purchase orders, price changes, discontinuing SKUs |
| **Review & Support Agent** | Drafts replies, manages reviews, handles FAQs | Customer messages, order context, template library | Draft replies, review responses, FAQ matches | Sending replies, public review responses, policy exceptions |
| **Audit Agent** | Watches all agents, verifies actions match proposals, flags drift | All DB writes, agent proposals, approval records | Audit log entries, discrepancy alerts, compliance reports | — (read-only watcher) |

## Human Approval Flow (All Agents Except Audit)

```
Event → Agent analyzes → Proposal written to approvals table
                        → Admin Panel + Telegram notify owner
                        → Owner: Approve / Reject / Modify
                        → Orchestrator executes (if approved)
                        → Audit Agent records outcome
```

## Approval Categories by Agent

### Order Agent
- ✅ Verify COD order (call/WhatsApp customer)
- ✅ Cancel suspicious order
- ✅ Correct shipping address
- ✅ Initiate refund/return
- ✅ Mark as shipped (with tracking)

### Inventory Agent
- ✅ Create purchase order
- ✅ Update variant price
- ✅ Discontinue product
- ✅ Adjust stock manually

### Review & Support Agent
- ✅ Send drafted reply to customer
- ✅ Post public review response
- ✅ Make policy exception (e.g., late return)
- ✅ Escalate to human support

### Orchestrator
- No direct approvals — routes to other agents

### Audit Agent
- No approvals — read-only monitor, alerts on drift

## Agent Independence Rule

Each agent:
- Reads only what it needs (least privilege)
- Writes proposals to `approvals` table
- Never executes directly — always via approval
- Logs reasoning in proposal for audit trail