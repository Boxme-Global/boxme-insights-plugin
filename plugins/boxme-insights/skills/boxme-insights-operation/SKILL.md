---
name: boxme-insights-operation
description: Answer a Boxme seller's warehouse-operation questions from Boxme Insights — outbound handling speed and Fast Handover Rate (FHR), late/overdue orders, inbound receiving and SLA pass rate, putaway time, returns and return-inspection SLA, return handling fees, damaged returned stock, compensation, and live backlog of open orders — using the Outbound SLA, Inbound, Return, Return Loss & Cost dashboards and the BM-/OM- live reports via the Insights MCP. Use whenever a seller asks things like "đơn trễ SLA", "bao nhiêu đơn đang tồn", "tỷ lệ đóng gói đúng hạn", "hàng nhập kho đạt SLA không", "đơn hoàn chờ kiểm", "phí xử lý hoàn", "orders overdue", "backlog", "inbound SLA", even without naming Insights. Always apply boxme-insights-core together with this skill.
---

# Boxme Insights — Operation

Apply every rule in `boxme-insights-core` first. This skill tells you where operational answers live and which of two kinds of source to use:

- **Dashboards** (Boxme warehouse data): what happened over a period.
- **Live reports** (`run_report`): what is open or at risk right now.

## Choose the source

| Seller asks | Use |
|---|---|
| "Bao nhiêu đơn đang tồn / chưa xử lý / đang trễ?" (now) | `run_report` **BM-BACKLOG-SUMMARY** |
| Which open orders exactly | `run_report` BM-BACKLOG-ORDERS (paged) |
| Orders not yet pushed from the store to the warehouse | `run_report` OM-BACKLOG-SUMMARY (different count from BM-BACKLOG) |
| Orders cancelled at the store after a shipment existed, or status mismatches | `run_report` OM-HANDOVER-RISK-SUMMARY (window ≤ 14 days) |
| Returns at risk of not coming back into the warehouse | `run_report` OM-RETURN-RISK-SUMMARY |
| Performance over a period (rates, times, trends) | Dashboards below |

Live-report notes:
- Call `describe_report` before the first use to see accepted params and windows. Get filter values from BM-BACKLOG-FILTERS / OM-BACKLOG-FILTERS.
- For BM-BACKLOG-SUMMARY the window filters the store creation date only; the open total does not depend on it. Never present it as "orders created in the last N days".
- These reports return `data_as_of: "unknown"`; use `data.last_update` instead (UTC → seller's local time) and call the figures "số trực tiếp". Convert epoch windows to dates before quoting.
- BM-BACKLOG-SUMMARY `data` holds `total`, `by_sla` (overdue buckets, e.g. `yesterday_from_0h_to_2359`), status breakdowns (`by_courier`, `by_channel_bar`, `timeseries`) and `sla_reference`. Ignore `by_seller`: it only repeats the seller's own total.

## Dashboards

| Seller asks about | Dashboard › chart | Window |
|---|---|---|
| Outbound headline: orders, FHR, average fulfilled time, overdue | Outbound SLA Insight › **OB - KPIs** | period |
| FHR over time / by warehouse | OB - FHR Achievement (%), OB - FHR Warehouse (%) | period |
| On-time vs overdue orders | OB - Orders Ontime vs Overdue FHR, OB - Order overdue by Warehouse, OB - Orders Overdue by Courier | period |
| Handling speed | OB - Avg Fulfilled Time trend, OB - Avg Fulfilled Time by warehouse, OB - Delay Distribution | period |
| Handover to carriers | OB - Handover Time by Courier (hours) | period |
| List of late orders | OB - Overdue Order detail (last 30 days) | period |
| Inbound headline | Inbound Insights › **IB - KPIs** | period |
| Inbound SLA | IB - SLA Pass Rate Trend (%), IB - SLA Pass Rate by Warehouse (%), IB - SLA Passed vs Failed Qty by Warehouse | period |
| Received quantity, putaway time | IB - Received Qty Trend, IB - Avg Putaway Time Trend / by Warehouse (h), IB - Inbound Detail by Warehouse | period |
| Returns headline | Return Insights › **RT - Return KPIs** | period |
| Return volume and rate | RT - Return Order Trend, RT - Return Rate Trend, RT - Return Orders by Warehouse, RT - Return Type | period |
| Returns waiting for inspection | RT - Return Processing Aging | period |
| Inspection SLA | RT - Ontime Rate Trend, RT - Ontime vs Overdue SLA by Warehouse, RT - SLA Rate by Warehouse | period |
| Return handling fees | Return Loss & Cost › RL - Return Handling KPIs, RL - Return Handling Fee Trend, RL - Return Handling Fee by Sales Channel | period, month-or-longer presets only |
| Damaged returned stock | RL - Damaged Stock Value by Condition (current), RL - Damaged Stock Value by Warehouse (current), RL - Top 10 Categories by Damaged Stock Value (current), RL - Damaged Stock Detail by SKU (current) | **fixed**: current snapshot |
| Compensation for damaged or lost returns | RL - Return Loss Compensation by Month | period: `current_month`, `last_month`, `current_quarter`, `last_3_months` only |

Prefixes in chart names: OB = outbound, IB = inbound, RT = returns, RL = return loss & cost.

## Recipes

**"Tỷ lệ đóng gói / bàn giao đúng hạn tuần này?"** → OB - KPIs, `current_week`. Explain FHR = Fast Handover Rate: share of packed orders ready for handover within the outbound SLA.

**"Có bao nhiêu đơn đang quá hạn?"** → BM-BACKLOG-SUMMARY; give `total` open, the overdue count from `by_sla`, and the status split (awaiting process, processing, ready to ship, waiting to handover). If the seller then asks "which ones", page BM-BACKLOG-ORDERS.

**"Kho nào xử lý chậm?"** → OB - Avg Fulfilled Time by warehouse and OB - FHR Warehouse (%), same period. Give volume next to each rate so a small warehouse is not over-read.

**"Hàng nhập tháng trước có đạt SLA không?"** → IB - KPIs, `last_month`; add IB - SLA Pass Rate by Warehouse if more than one warehouse.

**"Đơn hoàn đang chờ kiểm bao lâu?"** → RT - Return Processing Aging; name the oldest bucket and its count.

**"Tháng này được bồi thường bao nhiêu?"** → RL - Return Loss Compensation by Month, `current_month`. Empty = no compensation in the window, which is common.

## Cautions

- FHR, inbound SLA pass rate, return on-time rate and last-mile on-time are different metrics (core glossary). Never merge them into one "on-time" figure.
- Outbound `Total Orders` counts warehouse-processed orders, not sales-channel orders.
- Damaged stock is a snapshot: do not add it across months.
- Do not judge "good/bad" against outside benchmarks; compare with the seller's own earlier periods or warehouses.
