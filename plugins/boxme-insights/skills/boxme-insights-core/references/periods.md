# Period presets

Insights only accepts fixed presets. Free date ranges and single dates are refused, on the portal and in the MCP. Each `period` chart lists the presets it accepts in `period_presets`; monthly charts (fees, return handling, compensation) accept only month-or-longer presets.

Weeks start on Monday. Days follow Vietnam time (Asia/Ho_Chi_Minh) for every country for now.

| Preset | Meaning | Includes today / the running unit? |
|---|---|---|
| `today` | Today | yes |
| `yesterday` | Yesterday | no |
| `current_week` | Monday this week → today | yes |
| `last_week` | Previous Monday → Sunday | no (completed week) |
| `last_7_days` | Last 7 days | yes |
| `last_30_days` | Last 30 days | yes |
| `current_month` | 1st of this month → today | yes |
| `last_month` | Previous calendar month | no (completed month) |
| `current_quarter` | Start of this quarter → today | yes |
| `last_quarter` | Previous calendar quarter | no |
| `last_3_months` | 2 previous months + the current month | yes (the current month is partial) |
| `last_6_months` | 5 previous months + the current month | yes |
| `last_12_months` | 11 previous months + the current month | yes |
| `current_year` | 1 January → today | yes |

If no preset is passed, the dashboard default applies and `period_applied.source` is `dashboard_default`. Tell the seller which window that was.

## Mapping the seller's words

| Vietnamese | English | Thai | Preset |
|---|---|---|---|
| hôm nay | today | วันนี้ | `today` |
| hôm qua | yesterday | เมื่อวาน | `yesterday` |
| tuần này | this week | สัปดาห์นี้ | `current_week` |
| tuần trước, tuần rồi | last week | สัปดาห์ที่แล้ว | `last_week` |
| 7 ngày qua | last 7 days | 7 วันที่ผ่านมา | `last_7_days` |
| 30 ngày qua, 1 tháng gần đây | last 30 days | 30 วันที่ผ่านมา | `last_30_days` |
| tháng này | this month | เดือนนี้ | `current_month` |
| tháng trước, tháng rồi | last month | เดือนที่แล้ว | `last_month` |
| quý này | this quarter | ไตรมาสนี้ | `current_quarter` |
| quý trước | last quarter | ไตรมาสที่แล้ว | `last_quarter` |
| 3 tháng gần đây | last 3 months | 3 เดือนที่ผ่านมา | `last_3_months` |
| 6 tháng gần đây | last 6 months | 6 เดือนที่ผ่านมา | `last_6_months` |
| 12 tháng, 1 năm gần đây | last 12 months | 12 เดือนที่ผ่านมา | `last_12_months` |
| năm nay | this year | ปีนี้ | `current_year` |

## Named months, dates and custom ranges

A named month equal to the previous month ("tháng 10" when today is in November) → `last_month`. The current month → `current_month`.

Any other named month, date or range ("tháng 8", "từ 5/10 đến 20/10", "Black Friday") cannot be selected directly. Do not silently substitute another window. Instead:

1. Say that Insights only supports fixed periods.
2. If a trend chart with weekly/monthly rows covers it (e.g. `last_3_months` includes August when today is in October or November), offer to read that month's row from the trend.
3. Otherwise offer the nearest preset and state exactly which dates it covers.

## Month-on-month comparisons

- "Tháng này so với tháng trước": `current_month` is partial. Say how many days are in it, or compare the same weekly rows instead.
- Two completed months: run a monthly trend chart with `last_3_months` and compare its rows.
