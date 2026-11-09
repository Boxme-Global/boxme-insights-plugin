---
name: boxme-insights-lastmile
description: Answer a Boxme seller's delivery questions from Boxme Insights — shipments handed to carriers, delivery success, not-yet-delivered, average delivery days, on-time delivery, carrier comparison, COD collected by carriers, delivery exceptions and failed-delivery reasons, and shipments in delivery right now — using the Last-mile Insights, Delivery & Carrier Performance and Exception & Risk dashboards and the BM-DELIVERY-OPS live reports via the Insights MCP. Use whenever a seller asks things like "tỷ lệ giao thành công", "hãng nào giao nhanh", "đơn giao trễ", "giao thất bại vì sao", "COD hãng đã thu", "delivery success rate", "which carrier is best", "การจัดส่ง", even without naming Insights. Always apply boxme-insights-core together with this skill.
---

# Boxme Insights — Last-mile

Apply every rule in `boxme-insights-core` first. Chart meanings are in `../boxme-insights-core/references/catalog.md` (in the core skill) (section Last-mile). This skill tells you which source to use, which date each chart counts by, and how to read the delivery metrics without mixing them up.

## Two kinds of source

| Seller asks | Use |
|---|---|
| Shipments in delivery **right now**: how many, how many late, at which carrier | `run_report` **BM-DELIVERY-OPS-OVERVIEW** (window by date, default 14 days, max 90; params `courier`, `ff_center_code`, `order_type`, `service`, `status`) |
| Which shipments exactly | `run_report` BM-DELIVERY-OPS-ORDERS (paged) |
| Results over a period: success, speed, on-time, carriers | Dashboards below |

BM-DELIVERY-OPS-OVERVIEW returns `kpis` (`total_open`, `late`, `late_pct`, `with_failed_attempt`, `avg_fulfillment_hours`, `avg_shipping_hours`), an `aging` breakdown (`not_due`, `due_within_12h`, `overdue_0_24h`, `overdue_24_48h`, `overdue_48h_plus`, `no_sla`) and breakdowns by courier, warehouse, order type, service, status and region. Its `data_as_of` is `unknown`; use `data.last_refresh` for the time (UTC → local) and call the figures "số trực tiếp". Ignore `by_seller`: it only repeats the seller's own total.

## Each dashboard counts by a different date

This decides which period a shipment falls into. Say it when it matters.

| Dashboard / chart | Date basis |
|---|---|
| Last-mile Insights, Delivery & Carrier Performance (all charts except one) | **Order creation date** |
| Last-mile Insights › Return Status Breakdown | Return record date — do not net it against the KPIs |
| Exception & Risk (all charts) | **Expected delivery date**; exception type is evaluated at read time |

All three dashboards exclude return orders, test warehouses and orders cancelled before warehouse intake.

## Where the answers are

| Seller asks about | Dashboard › chart | Notes |
|---|---|---|
| How many shipments | Last-mile Insights › Shipments; Delivery & Carrier › Carrier KPIs (`Total Orders`) | |
| Delivery success | Last-mile Insights › Delivery Success Rate | Delivered ÷ created |
| Not delivered yet | Last-mile Insights › Not Yet Delivered Rate (column `Failed Rate`) | **Includes in-transit orders** — not a failure rate |
| Delivery speed | Last-mile Insights › Avg Delivery (days); Delivery & Carrier › AVG Delivery Time Trend (days), AVG Delivery Time by Courier (days) | Days from carrier pickup to delivery |
| On time | Last-mile Insights › On-time Delivery (SLA); Delivery & Carrier › Carrier KPIs, On-time Delivery Rate Trend (%), On-time Rate by Courier (%), On-time Delivery Rate by Warehouse (%) | Delivered within 2 days of pickup ÷ delivered |
| Late deliveries | Delivery & Carrier › Carrier KPIs (`Late Delivered Orders`) | |
| Carrier comparison | Last-mile Insights › **Carrier Performance** (volume, delivered, success %, failed %, avg days); Volume Share by Courier | Prefer this table: it carries volume |
| Daily / weekly trend | Last-mile Insights › Daily Delivery Trend, Daily COD Amount; Delivery & Carrier › Delivery Volume Trend | Settled days / complete ISO weeks only (`2026-W43`) |
| COD collected | Last-mile Insights › COD Collected, Daily COD Amount | Cash collected by carriers on delivered orders |
| Returns by status | Last-mile Insights › Return Status Breakdown | Different date basis |
| Exceptions, failed reasons | Exception & Risk › Exception Type Distribution, Failed Delivery Reason, Exception Detail | Expected-delivery date basis |

Filters: `Country`, `Warehouse`, `Courier`, `Period`. Default period is `last_30_days`.

## Reading the metrics correctly

- **Success rate reads low for recent periods.** Orders still in transit stay in the denominator. For `current_week`, `today` or `last_7_days`, say the rate will rise as shipments complete; for a stable figure use `last_week` or `last_month`.
- **Not Yet Delivered ≠ failed.** Never call `Failed Rate` a failure rate. For real failures use Exception & Risk › Failed Delivery Reason.
- **On-time uses a flat 2-day rule** from pickup, not each carrier's promised time, and its denominator is delivered orders only. Do not compare it with Delivery Success Rate (all created orders) or with Outbound FHR (warehouse step).
- **COD Collected ≠ Sales COD Amount.** COD Collected is cash carriers collected on delivered shipments in Boxme's last-mile system; Sales COD Amount is the value of orders that chose COD. Marketplace-collected COD usually does not appear here (unconfirmed — say "thường là do").
- **Settled days only.** Daily and weekly trend charts hide the most recent days/weeks because the pipeline lags; KPI cards include them. Explain small gaps between a KPI and the sum of the trend.
- **Small carriers.** Always show shipment volume next to a carrier's rate; a carrier with a handful of shipments at 100% is not "the best".

## Recipes

**"Tỷ lệ giao thành công tuần trước?"** → Delivery Success Rate, `last_week`. Add Avg Delivery (days) and On-time Delivery (SLA) for context, each labelled.

**"Hãng nào giao tốt nhất?"** → Carrier Performance with the asked period. Rank by success rate among carriers with meaningful volume, show avg delivery days, and note any carrier with very low volume.

**"Bây giờ có bao nhiêu đơn đang giao trễ?"** → BM-DELIVERY-OPS-OVERVIEW. Report `total_open`, then the overdue buckets and which couriers hold them. Offer the order list (BM-DELIVERY-OPS-ORDERS) if the seller wants to follow up.

**"Vì sao giao thất bại?"** → Failed Delivery Reason and Exception Type Distribution, same period; mention the expected-delivery date basis. For specific orders, Exception Detail.

**"COD hãng đã thu tuần này?"** → COD Collected, `current_week`; if the seller means the value of COD orders, point to Sales COD Amount instead.

**"Kho nào giao đúng hạn kém?"** → On-time Delivery Rate by Warehouse (%); remember the clock starts at carrier pickup, so warehouse handling time is not in it — for that use Outbound FHR (operation skill).
