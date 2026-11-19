# Feature Lists

> **Status**: Planned — not implemented. MVP = minimum for Phase 6 launch.

---

## Storefront (Customer-Facing)

### MVP (Must Have)

| Feature | Description |
|---------|-------------|
| Home page | Hero, featured products, category links, trust badges |
| Product listing | Grid, filter by category/price, sort, pagination |
| Product detail | Images (zoom), variant selector (color/size), quantity, add to cart |
| Cart | Persistent (localStorage + server sync), update qty, remove |
| Checkout | Address form (Indian pincode autocomplete), COD/UPI/prepaid, order summary |
| Order confirmation | Order number, expected delivery, WhatsApp share button |
| Order tracking | Public page: order number + phone → timeline |
| Mobile-first | Touch-friendly, fast on 3G, Instagram in-app browser tested |
| Theme: Violet/Off-white | Consistent design tokens, dark mode later |

### Later (Post-Launch)

| Feature | Description |
|---------|-------------|
| Wishlist / Save for later | Heart icon, persistent |
| Guest checkout + account creation after | Reduce friction |
| Coupon/discount codes | Percentage, fixed, free shipping |
| Gift wrapping + message | Upsell at checkout |
| Product reviews + ratings | Verified buyers only |
| Recently viewed | Local storage based |
| PWA / Install prompt | Add to home screen |
| Multi-language UI | Hindi, Gujarati (Latin + script) |
| WhatsApp "Order on WhatsApp" fallback | For non-tech customers |
| SEO: structured data, sitemap, meta | Product, breadcrumb, organization |

---

## Admin Panel (Owner-Facing)

### MVP (Must Have)

| Feature | Description |
|---------|-------------|
| Owner login | Supabase Auth (magic link/OTP), session management |
| Dashboard | Today's orders, revenue, pending approvals, low stock count |
| Orders list | Filter by status/date/payment, search by order#/customer |
| Order detail | Full timeline, customer info, items, payments, shipments, actions |
| Order actions | Confirm, Print invoice, Ship (add tracking), Cancel, Refund |
| Products CRUD | Create/edit/archive, images, variants (SKU, price, stock) |
| Stock view | Table: variant, available, reserved, reorder point, status |
| Low stock alerts | Banner + dedicated page, "Create PO" button |
| Customers list | Search, tags, order history, lifetime value |
| Approvals queue | All pending approvals, filter by agent/type |
| Approval detail | Proposal, reasoning, Approve/Reject/Modify, comments |
| Settings | Store name, logo, theme colors, shipping rates, COD enabled, payment methods |
| Audit log viewer | Read-only, filter by entity/date/agent |

### Later (Post-Launch)

| Feature | Description |
|---------|-------------|
| Bulk actions | Bulk ship, bulk status update, bulk tag customers |
| Returns/RMA flow | Customer initiates, owner approves, pickup scheduled |
| Invoice GST compliance | HSN codes, GSTIN, auto-generate PDF |
| Sales reports | Daily/weekly/monthly, top products, cohort retention |
| Customer segments | RFM, tags, export for WhatsApp broadcast |
| Supplier management | PO tracking, received qty, payables |
| Multi-user roles | Packer, accountant (read-only), manager |
| Webhooks | Shiprocket, Razorpay, WhatsApp Business API |
| Dark mode | For late-night packing sessions |
| Keyboard shortcuts | Power user speed |
| Export/Import CSV | Products, customers, stock |

---

## Agent Features (Post Phase 6)

| Agent | MVP Capability | Later |
|-------|----------------|-------|
| Order Agent | Flag suspicious COD, propose verify/cancel | Auto-verify via WhatsApp call, RTO prediction |
| Audit Agent | Log all proposals/decisions, flag drift | Compliance reports, anomaly detection |
| Inventory Agent | Low stock alert, propose PO | Demand forecasting, auto-reorder rules |
| Review & Support Agent | Draft replies (Hindi/Gujarati/English), FAQ match | Auto-resolve tier-1, sentiment analysis |
| Orchestrator | Route tasks, enforce approvals | Parallel workflows, SLA tracking |

---

## Status Summary

| Area | MVP Items | Later Items | Total |
|------|-----------|-------------|-------|
| Storefront | 9 | 11 | 20 |
| Admin Panel | 13 | 12 | 25 |
| Agents | 5 (1 each) | 5+ | 10+ |