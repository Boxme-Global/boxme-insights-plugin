# Boxme Insights for Claude

Plugin for Boxme sellers. It connects Claude to **Boxme Insights** and teaches it how to read your dashboards: sales, warehouse operations, last-mile delivery and fulfillment fees. Every number Claude gives comes from your own Insights data; Claude does not estimate or use outside figures.

## What is inside

| Part | What it does |
|---|---|
| Connector `boxme-insights` | Remote MCP server at `https://insights.boxme.asia/api/method/insights_seller.mcp.handle`. Sign in with your Boxme seller account. Read-only. |
| `boxme-insights-core` | Rules for every answer: period presets, source line, currency, formatting. Holds the dashboard and chart catalog. |
| `boxme-insights-sales` | Sales Overview, Product Performance, Platform Subsidy. |
| `boxme-insights-operation` | Outbound, Inbound, Return, Return Loss & Cost, live backlog reports. |
| `boxme-insights-lastmile` | Last-mile, Delivery & Carrier Performance, Exception & Risk, live delivery reports. |
| `boxme-insights-cost` | Fulfillment Cost Insights. |

## Install

**claude.ai (web, desktop):** Customize › Plugins › Add, paste `https://github.com/Boxme-Global/boxme-insights-plugin`, install **Boxme Insights**, then connect the connector from the plugin's Connectors tab.

**Claude Code:** `/plugin install boxme-insights --marketplace Boxme-Global/boxme-insights-plugin` (the connector itself is supported on claude.ai and Cowork).

Sign in to https://insights.boxme.asia in the same browser before you connect.

## Example questions

- "Doanh thu tháng trước bao nhiêu, kênh nào bán tốt nhất?"
- "How many orders are overdue at the warehouse right now?"
- "Tỷ lệ giao thành công theo từng hãng tháng này?"
- "Phí fulfillment tháng trước tăng hay giảm so với tháng trước nữa?"

## Support

Contact your Boxme account manager.
