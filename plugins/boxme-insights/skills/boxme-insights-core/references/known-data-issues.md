# Known data and server issues (as of 08/11/2026)

Temporary. Items are removed as they are fixed.

| Issue | How to answer around it |
|---|---|
| `period_applied.end` can be in the future (end of the running month/quarter). | Write "đến hôm nay (dd/mm)". |
| Numbers may come as strings with 9 decimals. | Parse and format (core skill §3). |
| Rows are not sorted; "Top 10 …" charts return up to 200 rows. | Sort by time or by the measure yourself; keep N for "Top N". |
| No caveats or currency field in the response. | Use the caveats in `catalog.md`; apply the glossary; currency follows the country. |
| `run_report` returns `data_as_of: "unknown"` and the window as epoch seconds. | Use `data.last_update` (backlog) or `data.last_refresh` (delivery ops); convert epoch to dates before quoting. |
| Some sellers do not have Products P&L, Platform Cost Analysis, Buyer Behavior, Geographic Sales or Demand Forecast published. | If `list_dashboards` does not show it, say it is not available on their account yet; do not substitute another dashboard's numbers. |
| No Thai labels on the server yet. | Answer in Thai, keep server metric names in English with a Thai gloss. |
| Fulfillment Cost: Storage fee for **09/2026 shows 0** (Fee by Service, Fee Trend, Avg Net Fee trend) although storage volume exists that month. Under investigation. | Do not report September storage fee or its per-m³ fee; say it is being checked. Other services and months are fine. |
| Storage average and fee per m³ are empty for the running month. | Expected until billed days are available; give the last closed month. |
| Daily data lag: stock data reaches Insights about 2 days late (refresh order upstream). | Quote `data_as_of`; for "hôm nay/hôm qua" stock questions, say the latest day available. |
| Some dashboards refresh late (Inventory Overview/Risk Alerts were ~26 h old on 07/11). | Always quote `data_as_of`; if it is more than 24 h old, say so. |

## Empty charts that are expected

- Return Loss & Cost › `RL - Return Loss Compensation by Month`: empty when the seller had no compensation for damaged or lost returns in the window (the query keeps 3 months).
- Fulfillment Cost › `Discount Detail by Seller & Fee Type`: empty when the seller has no fee discounts.
