---
name: boxme-insights-cost
description: Answer a Boxme seller's questions about Boxme fulfillment fees from Boxme Insights — total fees by month, fees by service (inbound, storage, fulfillment, material, shipping, management and support), by warehouse, average fee per unit, fee trend, adjustments and discounts, and logistics cost as a share of NMV — using the Fulfillment Cost Insights dashboard via the Insights MCP. Use whenever a seller asks things like "phí tháng trước bao nhiêu", "vì sao phí tăng", "phí lưu kho", "phí trên mỗi đơn", "chi phí logistics chiếm bao nhiêu % doanh thu", "fulfillment fee", "storage cost", "ค่าบริการ", even without naming Insights. Always apply boxme-insights-core together with this skill.
---

# Boxme Insights — Cost

Apply every rule in `boxme-insights-core` first. Chart meanings are in `../boxme-insights-core/references/catalog.md` (in the core skill) (section Cost).

Source: one dashboard, **5. Fulfillment Cost Insights**, built from Boxme billing data.

## Rules specific to fees

- **Every fee is after discount and before VAT**, by month. It is not the invoice total: VAT, invoice timing and payment are not in Insights. For an invoice question or dispute, give the Insights figures and refer the seller to their Boxme account manager.
- **Month grain.** The dashboard accepts month-or-longer presets only (`current_month`, `last_month`, `current_quarter`, `last_quarter`, `last_3_months`, `last_6_months`, `last_12_months`, `current_year`). `current_month` is partial and keeps changing until billing closes; say so.
- **Fixed-window charts.** Fee Trend and Avg Net Fee (ex-VAT) / Volume trend show their own window (about the last 12 months) and ignore `period`. Use them for month-by-month history; sort the rows by month (they can come unsorted).
- **One currency.** Fees are in the country's currency; never add countries together.
- **Simple arithmetic is allowed, new metrics are not.** You may add services, take differences between months and compute shares from returned numbers — label them "tính từ số Insights". Do not invent formulas Insights does not define (e.g. profit, cost per SKU).

## Services and their volume units

| Service (as in Fee Trend) | Fee column (Fee by Service) | Volume column (Volume Overview) | Average fee = fee ÷ |
|---|---|---|---|
| 1. Inbound | Inbound Fee | Inbound (Pcs) | piece received |
| 2. Storage | Storage Fee | Storage (CBM) — **average m³ per day** (closed months only) | m³ per month (AVG Storage Fee = fee per m³ per month) |
| 3. Fulfillment | Fulfillment Fee | Fulfillment (Order) | order fulfilled |
| 4. Material | Material Fee | Material (Order) | order packed |
| 5. Shipping | Shipping Fee | Shipping (Order) | order billed a Boxme shipping fee — far fewer than fulfilled orders; never divide shipping fee by all orders |
| 6. Management and Support Fee | (Fee Trend only) | — | — |

## Storage volume: average m³ per day (fixed 08/11/2026)

The dashboard now returns storage already as a **daily average**. Do not divide it again.

- `Storage (CBM)` in Volume Overview = **average m³ stored per day** in that month (CBM-days ÷ days of the month).
- `AVG Storage Fee` in Fee by Service and the Storage line of Avg Net Fee / Volume trend = **fee per m³ per month**, before VAT (e.g. 372,000 ₫/m³/month).
- **Closed months only.** For the running month both values are empty (`null`) until the number of billed days is available. Say "tháng đang chạy chưa có số bình quân" and give the last closed month. The default period (`last_3_months`) includes the running month, so the latest row is usually empty.
- Never present storage as a monthly total of m³, and never add daily averages across months; compare them month by month.
- When explaining a storage-fee change: change in average m³/day × change in fee per m³/month (and days in the month only if the seller asks why a 31-day month costs more).

## Where the answers are

| Seller asks about | Chart | Window |
|---|---|---|
| Total fee and fee by service per month, with average fee per unit | **Fee by Service** | period |
| Volumes behind the fees | Volume Overview | period |
| Fee mix by service | Fee by Service Type | period |
| Fee by warehouse | Fee by Warehouse | period |
| Month-by-month history | Fee Trend; Avg Net Fee (ex-VAT) / Volume trend | fixed (~12 months) |
| Service fee → adjustment → fee before discount → discount → fee | Service Fee detail | period |
| Logistics cost vs sales | Cost Efficiency Overview (`NMV`, `Total Cost`, `Cost % NMV`, avg chargeable weight per order, avg items per order) | period |
| Discounts granted | Discount Detail by Seller & Fee Type | period; empty = no discounts |

Filters: `Country`, `Warehouse`, `Service Type`, `Order Type`, `Period`.

## Recipes

**"Phí tháng trước bao nhiêu?"** → Fee by Service, `last_month`. Give the total (sum of the five service fees) and the two or three largest services with their share. Add Management and Support Fee from Fee Trend if it is non-zero for that month.

**"Vì sao phí tháng này / tháng trước tăng?"** Compare two complete months (use Fee Trend rows, or Fee by Service with `last_3_months`). For each service that moved, split the change into:
1. volume change (Volume Overview), and
2. average fee per unit change (the AVG columns of Fee by Service, or Avg Net Fee / Volume trend).
Then check Service Fee detail for adjustments or a change in discount. State the two or three biggest drivers with amounts. If the latest month is still open, say the comparison is provisional.

**"Phí trên mỗi đơn là bao nhiêu?"** → AVG Fulfillment Fee and AVG Material Fee per order (Fee by Service). If the seller wants "all-in per order", say Insights does not define one; offer Cost % NMV or the sum of per-order fees, labelled as computed.

**"Chi phí logistics chiếm bao nhiêu % doanh thu?"** → Cost Efficiency Overview, `Cost % NMV`. Mention that NMV comes from the seller's sales-channel data (Omisell) and Total Cost from Boxme billing, so a month where orders and billing fall in different months can swing the ratio.

**"Tôi đang lưu kho bao nhiêu khối?"** → Volume Overview, `last_month`: `Storage (CBM)` is already the average m³ per day. For the stock currently on hand, the inventory dashboards are the source, not this one.

**"Phí lưu kho của tôi cao không?"** → Storage Fee, average m³/day and AVG Storage Fee (per m³ per month) over closed months; compare with the seller's own history. Do not judge against market prices; Insights has none.

## Cautions

- Service Fee detail returns the service column as `service_type_sorted` (e.g. "2. Storage") and `Discount` may come as a string — parse it.
- Fee by Warehouse covers Boxme warehouses only; a seller with stock elsewhere sees only the Boxme part.
- Do not mix these fees with Return Loss & Cost (return handling fees, operation skill) unless the seller asks for all Boxme charges; if you combine them, list each source.
