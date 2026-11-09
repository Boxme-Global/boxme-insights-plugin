# Metrics that share a name

Each insight measures a different step of the order journey. When the seller's wording could mean more than one, ask which step, or show each one labelled with its step. Never compare them with each other.

## "Đúng hạn" / on-time

Sales Insights has no on-time metric (removed 08/11/2026). An on-time question always refers to one of the warehouse or carrier steps below.

| Insight › chart › field | What it measures | Notes |
|---|---|---|
| Outbound SLA Insight › OB - KPIs › `FHR rate (packed <= SLA)` (Fast Handover Rate) | Share of warehouse orders packed and ready for handover within the outbound SLA | Denominator = orders already packed. Call it "tỷ lệ bàn giao nhanh đúng SLA xuất kho". |
| Inbound Insights › IB - KPIs › `SLA Pass Rate` | Share of inbound quantity received within the inbound SLA | Measured on quantity, not on shipments. |
| Return Insights › RT - Return KPIs › `SLA Completion Rate`; RT - Ontime Rate Trend | Share of returns inspected within the return-inspection SLA | |
| Last-mile Insights › On-time Delivery (SLA) › `SLA On-time Rate` | Share of shipments delivered successfully within 2 days of carrier pickup | Flat 2-day rule, not each carrier's promised time. |

## "Tổng đơn" / total orders

| Insight › field | What it counts |
|---|---|
| Sales Overview › `Total Orders` | Orders placed on the seller's sales channels (Omisell), including cancelled ones |
| Outbound SLA Insight › `Total Orders` | Orders the Boxme warehouse processed for outbound |
| Last-mile Insights › `Shipments` | Shipments handed over to carriers |

These differ by design: cancelled orders, orders shipped from other warehouses, and orders not yet handed over.

## COD

| Insight › field | What it measures |
|---|---|
| Sales Overview › `COD Amount`, `COD Share %` | Value of sales orders where the buyer chose cash on delivery, whoever collects it |
| Last-mile Insights › `COD Collected` | Cash collected by carriers on shipments in Boxme's last-mile system |

Marketplace orders whose COD is collected by the platform (e.g. Shopee, TikTok Shop) usually do not appear in `COD Collected`. That explanation is not yet confirmed by BI — present it as "thường là do", not as fact.

## Other definitions to quote

- **Gross Sales / Net Sales** (Sales Overview): both are returned by the server; the exact deductions between them are not yet documented. Quote the names as returned and do not explain the difference until the metadata confirms it.
- **Return Rate % (of completed)**: returned orders ÷ completed orders.
- **GM%** (Product Performance): covers only SKUs that have a cost price; always mention the `COGS Coverage %` tile next to it.
- **Subsidy % of NMV** (Platform Subsidy): platform-funded vouchers, discounts and coins ÷ NMV. Shipping rebates are shown only once settled (lag of about 10 days); the latest days are incomplete.
- **Fees** (Fulfillment Cost Insights): after discount, before VAT, by month.
- **Damaged stock value** (Return Loss & Cost): current snapshot, not a period total.
