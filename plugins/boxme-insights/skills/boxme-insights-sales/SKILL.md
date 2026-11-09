---
name: boxme-insights-sales
description: Answer a Boxme seller's sales questions from Boxme Insights — revenue, orders, AOV, cancel/return/completion rates, COD share, sales channels (Shopee, TikTok Shop, Lazada, Haravan, retail), stores, SKU performance, rising/declining SKUs and platform subsidies — using the Sales Overview, Product Performance and Platform Subsidy dashboards via the Insights MCP. Use whenever a seller asks things like "doanh thu tháng trước", "kênh nào bán tốt nhất", "SKU bán chạy", "store nào nhiều đơn", "tỷ lệ huỷ", "trợ giá sàn", "sales last week", "top products", "ยอดขาย", even without naming Insights. Always apply boxme-insights-core together with this skill.
---

# Boxme Insights — Sales

Apply every rule in `boxme-insights-core` first (period presets, source line, one currency, no outside numbers). This skill only tells you **where** each sales answer lives and **how** to read it.

Source of all three dashboards: Omisell orders on the seller's sales channels. Amounts are in the country's currency and never converted — the dashboards warn: select one Country before comparing absolute figures.

## Where the answers are

Dashboard names are stable; look up their ids with `list_dashboards`, chart ids with `get_dashboard`.

| Seller asks about | Dashboard › chart | Window |
|---|---|---|
| Revenue, orders, AOV, completion/cancel/return rate, COD share — one headline | Sales Overview › **Sales - KPIs** | period |
| Revenue or orders over time | Sales Overview › Revenue Trend, Orders Trend (weekly rows) | period |
| Which channel sells most / channel mix | Sales Overview › Revenue by Sales Channel, Revenue Trend by Sales Channel | period |
| AOV by channel | Sales Overview › AOV by Sales Channel | period |
| Cancellations / order status by channel | Sales Overview › Order Status by Sales Channel | period |
| Best stores | Sales Overview › Top Stores by Revenue, Top Stores by Orders | period |
| COD value by channel | Sales Overview › COD Amount by Sales Channel | period |
| Orders still open (not completed/cancelled) | Sales Overview › Open Orders by Status (by order date), Open Orders by Status and Order Week | period |
| Returned sales value | Sales Overview › Return Sales - KPIs, Return Sales by Week | period |
| SKU headline (net sales, qty, GM%, COGS coverage) | Product Performance › **Product - KPIs** | period |
| Best-selling SKUs | Product Performance › Top 10 SKU by Net Sales, Top 10 SKU by Qty Sold | period |
| Weekly SKU trend | Product Performance › Net Sales by Week - Top 5 SKU, Qty Sold by Week | period |
| SKUs growing / falling | Product Performance › Rising SKU - L4W vs P4W / Declining SKU - L4W vs P4W (fixed window, ignores Period) | **fixed**: last 4 weeks vs previous 4 weeks |
| One SKU in detail | Product Performance › SKU Detail (filter `SKU`) | period |
| Platform-funded vouchers, discounts, coins | Platform Subsidy › Platform Subsidy - KPIs, Subsidy % of NMV by Week, Subsidy % of NMV by Sales Channel, Subsidy by Week and Type | period |
| Subsidy by store or SKU | Platform Subsidy › Top 20 Store by Platform Subsidy, Top 10 SKU by Platform Subsidy, Top 10 SKU by Subsidy % of NMV, SKU Subsidy Detail | period |
| Shipping rebate from the platform | Platform Subsidy › Shipping Rebate by Week (settled) | period; latest ~10 days incomplete |

Filters available on these dashboards: `Country`, `Sales Channel`, `Store`, `Warehouse` (Sales Overview), `SKU` (Product Performance, Platform Subsidy). Use only values from `allowed_values`.

**Not in these dashboards**: advertising spend, traffic/conversion, buyer demographics, profit after all costs. Products P&L, Platform Cost Analysis, Buyer Behavior and Geographic Sales exist for some accounts only — use them if `list_dashboards` shows them, otherwise say they are not available yet.

## Recipes

**"Doanh thu tháng trước bao nhiêu?"** → Sales - KPIs, `period=last_month`. Lead with Net Sales; add Total Orders and AOV. Gross Sales only if asked.

**"Tháng này so với tháng trước?"** → Sales - KPIs twice (`current_month`, `last_month`). `current_month` is partial: give days elapsed, or compare average per day, or use the weekly rows of Revenue Trend with `last_3_months`.

**"Kênh nào bán tốt nhất?"** → Revenue by Sales Channel. Give each channel's share of the total (sum the rows; they add up to Sales - KPIs Net Sales for the same window). Add AOV by channel if the seller asks "why".

**"SKU nào bán chạy?"** → Top 10 SKU by Qty Sold or by Net Sales (ask which if unclear; default to Net Sales). The chart may return up to 200 rows: sort by the measure and keep the top 10.

**"SKU nào đang tăng / giảm?"** → "Rising SKU - L4W vs P4W" / "Declining SKU - L4W vs P4W" charts. Say they always compare the last 4 weeks with the 4 weeks before, regardless of the period asked.

**"Tỷ lệ huỷ / hoàn có cao không?"** → Sales - KPIs for the asked period and for an earlier preset; describe the change. Do not judge against outside benchmarks.

**"Trợ giá sàn chiếm bao nhiêu?"** → Platform Subsidy - KPIs and Subsidy % of NMV by Sales Channel. Mention that shipping rebates appear only once settled.

## Metric notes

- Sales Insights has no on-time metric. For "đơn có giao đúng hạn không", hand over to the operation skill (Outbound FHR) or Last-mile on-time, labelled by step.
- `COD Amount` here is the value of COD orders, not cash collected by carriers.
- `Total Orders` includes cancelled orders; `Completed Orders` does not.
- GM% covers only SKUs with a cost price: always quote `COGS Coverage %` next to it.
- Weekly rows are labelled by the Monday of the week; the first week of a window may start before the window (e.g. week of 28/09 inside `last_month` = October covers only 01–04/10).
