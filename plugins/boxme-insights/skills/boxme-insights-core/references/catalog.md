# Insights catalog — dashboard and chart definitions

Single source of descriptions for the Insights MCP (dashboards no longer carry description text). Thai (`th`) is not written yet.

Use it to pick the right chart and to explain what a number means. Ids are stable; titles are as the server returns them. `period` = follows the period preset; `fixed` = own window or current snapshot.

## Sales

### Sales Overview (`88r9eu0r37`)

- **Mục đích:** Đơn hàng, doanh thu và trạng thái đơn theo kênh bán.
- **Purpose:** Orders, revenue and order status by sales channel.
- **Kỳ mặc định:** last_3_months
- **Bộ lọc:** Period, Seller, Country, Sales Channel, Store, Warehouse
- **Lưu ý:**
  - Tiền tệ không quy đổi giữa các quốc gia; chọn một Country trước khi so số tuyệt đối.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Sales - KPIs | `57dst4hs24` | period | Chỉ số bán hàng và thanh toán: Net Sales, Gross Sales, số đơn, AOV, tỷ lệ hoàn tất/hoàn/hủy, COD | Key sales and payment metrics: Net Sales, Gross Sales, orders, AOV, completion/return/cancel rate, COD |
| Revenue Trend | `67e40l1g9b` | period | Xu hướng doanh thu Net Sales và Gross Sales | Net Sales vs Gross Sales revenue trend |
| Orders Trend | `f7ecodglbl` | period | Tổng đơn và đơn hoàn tất theo tuần. Chỉ hiển thị tuần đã kết thúc. | Total orders vs completed orders by week. Only completed weeks are shown. |
| Revenue by Sales Channel | `a7ft4f40gc` | period | Net Sales theo kênh bán | Net Sales compared across sales channels |
| Revenue Trend by Sales Channel | `a7g5qj1ard` | period | Xu hướng Net Sales theo kênh bán | Net Sales trend split by sales channel |
| Order Status by Sales Channel | `77f5cr63f5` | period | Cơ cấu trạng thái đơn theo kênh bán | Order status mix per sales channel |
| AOV by Sales Channel | `37h14u3ogq` | period | Giá trị đơn trung bình theo kênh bán | Average order value compared across sales channels |
| Top Stores by Revenue | `37gpusntgm` | period | Các store có Net Sales cao nhất | Stores with the highest Net Sales |
| Top Stores by Orders | `d7gg7u2plk` | period | Các store có nhiều đơn nhất | Stores with the most orders |
| COD Amount by Sales Channel | `07h8dtk204` | period | Giá trị COD theo kênh bán | COD amount compared across sales channels |
| Open Orders by Status (by order date) | `83c173smah` | period | Đơn chưa kết thúc (đang giao / đang hoàn / lỗi) đếm theo NGÀY ĐẶT trong kỳ lọc — không phải tồn đọng hiện tại. Thu hẹp Period sẽ bỏ sót đơn treo cũ. | Orders not yet closed (in transit / returning / problem) counted by ORDER DATE inside the selected period - this is not a live backlog snapshot. Narrowing Period hides older stuck orders. |
| Open Orders by Status and Order Week | `73ce4fi4dh` | period | Đơn chưa kết thúc theo tuần ĐẶT HÀNG và nhóm trạng thái. Đếm theo ngày đặt, không phải tồn đọng hiện tại. | Open orders by order week and status group. Counted by order date, not a live backlog snapshot. |
| Return Sales - KPIs | `fln1cljqjr` | period | Return Sales: doanh thu sản phẩm sau voucher trên đơn hoàn trả thành công | Return Sales: product revenue after voucher on successfully returned orders |
| Return Sales by Week | `6ln8nk2ca5` | period | Xu hướng Return Sales theo tuần | Return Sales trend by week |

### Product Performance (`58rfvrau3k`)

- **Mục đích:** Doanh thu, số lượng bán và biên lợi nhuận theo SKU.
- **Purpose:** Revenue, units sold and margin by SKU.
- **Kỳ mặc định:** last_3_months
- **Bộ lọc:** Period, Seller, Country, Sales Channel, Store, SKU
- **Lưu ý:**
  - GM% chỉ tính trên SKU đã khai giá vốn; luôn nêu kèm COGS Coverage %.
  - Nhiều SKU khai giá vốn theo thùng nhưng bán theo đơn vị lẻ, nên GM% có thể âm.
  - Kỳ lọc theo TUẦN: kỳ ngắn vẫn trả cả tuần.
  - Chart theo tuần chỉ gồm tuần đã kết thúc; thẻ KPI có cả tuần đang chạy.
  - Rising/Declining SKU dùng cửa sổ cố định 4 tuần gần nhất so với 4 tuần trước, không theo Period.
  - Tiền tệ không quy đổi giữa các quốc gia.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Product - KPIs | `b7hgl6vkir` | period | Chỉ số sản phẩm. ASP = Net Sales / số lượng của đơn hoàn tất. GM% CHỈ tính trên các SKU có giá vốn — xem COGS Coverage % trước khi tin con số này. | Product KPIs. ASP = Net Sales / qty of completed orders. GM% is computed ONLY on SKUs that have a cost price - check COGS Coverage % before trusting it. |
| Top 10 SKU by Net Sales | `87hpr65c5t` | period | 10 SKU có doanh thu thuần cao nhất | Top 10 SKUs by Net Sales |
| Top 10 SKU by Qty Sold | `37i1djbcgl` | period | 10 SKU bán chạy nhất theo số lượng | Top 10 SKUs by units sold |
| Net Sales by Week - Top 5 SKU | `b7igg0qh3q` | period | Doanh thu thuần theo tuần của 5 SKU bán chạy nhất (xếp hạng theo NMV 3 tháng trong seller × quốc gia; tuần hiện tại chưa kết thúc) | Weekly Net Sales of each seller's top 5 SKUs (ranked by 3-month Net Sales within seller × country; current week is partial) |
| Qty Sold by Week | `f7i9613vf1` | period | Số lượng bán ra theo tuần (tuần hiện tại chưa kết thúc) | Units sold per week (current week is partial) |
| Rising SKU - L4W vs P4W (fixed window, ignores Period) | `8k3o2bvs31` | fixed | SKU tăng doanh thu thuần mạnh nhất: 4 tuần trọn gần nhất so với 4 tuần trước đó. Cửa sổ cố định theo ngày hiện tại — KHÔNG đổi theo bộ lọc Period. | SKUs with the largest Net Sales increase: last 4 complete weeks vs the 4 weeks before. Fixed window anchored on today — NOT affected by the Period filter. |
| Declining SKU - L4W vs P4W (fixed window, ignores Period) | `6k447ulmfk` | fixed | SKU giảm doanh thu thuần mạnh nhất: 4 tuần trọn gần nhất so với 4 tuần trước đó. Cửa sổ cố định theo ngày hiện tại — KHÔNG đổi theo bộ lọc Period. | SKUs with the largest Net Sales decrease: last 4 complete weeks vs the 4 weeks before. Fixed window anchored on today — NOT affected by the Period filter. |
| SKU Detail | `d7io5rufg6` | period | Chi tiết theo SKU: sản lượng, Net Sales, ASP, COGS và GM%. GM% trống hoặc âm khi SKU thiếu giá vốn hoặc sai đơn vị giá vốn. | SKU detail: qty, net sales, ASP, COGS and GM%. GM% is blank or negative when the SKU has no cost price or the cost unit is wrong. |

### Platform Subsidy (`9j6goe5lsc`)

- **Mục đích:** Trợ giá do sàn tài trợ (voucher, giảm giá, xu sàn) đã nằm trong NMV, theo kênh.
- **Purpose:** Platform-funded vouchers, discounts and coins included in NMV, by channel.
- **Kỳ mặc định:** last_3_months
- **Bộ lọc:** Period, Country, Seller, Sales Channel, Store, SKU
- **Lưu ý:**
  - Platform Subsidy = voucher + giảm giá + xu sàn, đã nằm trong NMV.
  - Net Sales before Platform Subsidy = số tiền người mua thực trả.
  - Xu sàn chỉ có trên Shopee; kênh khác bằng 0 là đúng.
  - Shipping Rebate không phải trợ giá; được quyết toán trễ khoảng 10 ngày.
  - Hai chart tỷ lệ loại các dòng có trợ giá lớn hơn NMV (~0,3%).
  - CM% âm là trạng thái đã biết của tầng dữ liệu P&L hiện tại.
  - Tiền tệ không quy đổi giữa các quốc gia.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Platform Subsidy - KPIs | `4htc84o7ob` | period | Platform Subsidy = voucher sàn + giảm giá sàn + xu sàn. Cả ba đã nằm trong NMV. Hoàn phí vận chuyển (Shipping Rebate) KHÔNG thuộc subsidy, để riêng. | Platform Subsidy = platform voucher + platform discount + platform coin. All three are already inside NMV. Shipping Rebate is NOT part of subsidy and is shown separately. |
| Subsidy % of NMV by Week | `1htg0l2jjf` | period | Cường độ voucher theo tuần, kèm giảm giá sàn để đối chiếu và CM% hiện tại | Voucher intensity per week, with platform discount alongside and current CM% |
| Subsidy by Week and Type | `ehtmnp8u4m` | period | Đặt cạnh nhau, không chồng cột — hai cột lấy từ hai trường khác nhau và chỉ voucher được xác nhận là tiền sàn | Side by side, not stacked — the two come from different order fields and only the voucher is confirmed platform-funded |
| Top 20 Store by Platform Subsidy | `38nrlqpamv` | period | Cửa hàng nhận nhiều tiền sàn tài trợ nhất — cùng dòng tiền đó nhìn ở cấp shop | Stores receiving the most platform funding — the shop-level view of the same money |
| Subsidy % of NMV by Sales Channel | `ahu5h7v50o` | period | Sàn nào đang bỏ nhiều tiền voucher nhất cho doanh thu của bạn | Which marketplace funds your revenue most heavily through vouchers |
| Shipping Rebate by Week (settled) | `88lmirn6sd` | period | Hoàn phí vận chuyển là tiền logistics, không phải tài trợ hàng hoá — không cộng vào bất kỳ số subsidy nào. Đối soát trễ ~10 ngày nên các tuần mới nhất để trống | Shipping rebate is logistics money, not merchandise subsidy — kept out of every subsidy figure. Settles ~10 days late, so the newest weeks are blank |
| Top 10 SKU by Platform Subsidy | `8htrfngkov` | period | Những SKU nhận nhiều tiền voucher sàn nhất | SKUs receiving the largest platform voucher funding |
| Top 10 SKU by Subsidy % of NMV | `3hu0i8t3io` | period | Cường độ voucher cao nhất trong 50 SKU được tài trợ nhiều nhất — nhóm phụ thuộc tiền sàn nhất | Highest voucher intensity among the 50 most-funded SKUs — the ones most dependent on the platform paying |
| SKU Subsidy Detail | `5hual08q3i` | period | Voucher, giảm giá sàn và hoàn phí vận chuyển tách riêng theo SKU, kèm biên còn lại nếu ngừng voucher | Per-SKU voucher, platform discount and shipping rebate kept apart, with the margin left if the voucher stopped |

## Operation

### Outbound SLA Insight (`f3qcki9qqt`)

- **Mục đích:** Xuất kho: tốc độ xử lý, tỷ lệ bàn giao nhanh đúng SLA (FHR) và đơn trễ.
- **Purpose:** Outbound: handling speed, Fast Handover Rate (FHR) within SLA, and late orders.
- **Kỳ mặc định:** last_3_months
- **Bộ lọc:** Period, Seller, Warehouse, Country, Sales Channel, Courier, Order Type
- **Lưu ý:**
  - FHR = Fast Handover Rate: tỷ lệ đơn đã đóng gói sẵn sàng bàn giao trong SLA xuất kho.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| OB - KPIs | `f3qbojl4l9` | period | Chỉ số xuất kho chính. FHR = đơn đóng gói xong trước hạn SLA | Key outbound metrics. FHR (Fast Handover Rate) = order packed before sla_to_ship deadline |
| OB - FHR Achievement (%) | `f3qbf3lvt6` | period | Xu hướng tỷ lệ đạt FHR (%) | Fast Handover Rate (FHR) achievement trend (%) |
| OB - Orders Ontime vs Overdue FHR | `f3qbuf8at4` | period | Đơn đúng hạn và trễ hạn theo SLA bàn giao | On-time vs overdue orders against Fast Handover (FHR) SLA |
| OB - OB - Avg Fulfilled Time trend | `f3qbii6vsa` | period | Xu hướng thời gian xử lý đơn trung bình | Average fulfillment time trend |
| OB - FHR Warehouse (%) | `f3qb1du03b` | period | Tỷ lệ đạt FHR theo kho (%) | Fast Handover Rate (FHR) achievement compared across warehouses (%) |
| OB - Avg Fulfilled Time by warehouse | `f3qbc8ul64` | period | Thời gian xử lý đơn trung bình theo kho | Average fulfillment time compared across warehouses |
| OB - Order overdue by Warehouse | `f3qbv6g21q` | period | Đơn đúng hạn và trễ hạn theo kho (SLA = đóng gói xong trước hạn) | On-time vs overdue orders by warehouse (SLA = packed before sla_to_ship) |
| OB - Handover Time by Courier (hours) | `f3qbssh1m4` | period | Thời gian bàn giao trung bình cho từng hãng vận chuyển (giờ) | Average handover time to each courier (hours) |
| OB - Orders Overdue by Courier | `f3qbf0jmfl` | period | Đơn đúng hạn và trễ hạn theo hãng vận chuyển | On-time vs overdue orders by courier |
| OB - Delay Distribution | `f3qbns8785` | period | Phân bố đơn trễ theo thời gian trễ | Distribution of overdue orders by delay duration |
| OB - Overdue Order detail (last 30 days) | `f3qbffq0ge` | period | Chi tiết từng đơn trễ hạn trong 30 ngày gần nhất | Order-level detail of overdue orders in the last 30 days |

### Inbound Insights (`f3qcknplku`)

- **Mục đích:** Nhập kho: số lượng nhận, tỷ lệ đạt SLA nhập và thời gian putaway theo kho.
- **Purpose:** Inbound: received quantity, inbound SLA pass rate and putaway time by warehouse.
- **Kỳ mặc định:** last_3_months
- **Bộ lọc:** Country, Seller, Warehouse, Period
- **Lưu ý:**
  - Tỷ lệ đạt SLA nhập tính trên số lượng hàng, không tính trên số phiếu nhập.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| IB - Received Qty Trend | `f3qcirkmum` | period | Xu hướng số lượng hàng nhập kho theo ngày | Daily trend of inbound items received |
| IB - SLA Passed vs Failed Qty by Warehouse | `f3qc0a04nb` | period | Số lượng đạt và trễ SLA nhập kho theo kho | SLA passed vs failed inbound items per warehouse |
| IB - Received Qty by Customer | `f3qcc4gdhr` | period | Số lượng hàng nhận xếp hạng theo khách hàng | Received quantity ranked by customer |
| IB - Inbound Detail by Warehouse | `f3qcbrthl9` | period | Chi tiết nhập kho: số lượng nhận, đạt và trễ SLA | Inbound shipment details: received, passed and failed SLA quantities |
| IB - KPIs | `f3qc7h0c0n` | period | Chỉ số nhập kho chính: lô hàng, số lượng, tỷ lệ đạt SLA, thời gian putaway | Key inbound metrics: shipments, items, SLA pass rate, putaway time |
| IB - SLA Pass Rate Trend (%) | `eg37bmkhqi` | period | Tỷ lệ đạt SLA nhập kho theo ngày (%) | Daily inbound SLA pass rate (%) |
| IB - SLA Pass Rate by Warehouse (%) | `ffbdjjgbhk` | period | Tỷ lệ đạt SLA nhập kho theo kho (%) | Inbound SLA pass rate compared across warehouses (%) |
| IB - Avg Putaway Time Trend (h) | `3g39kj1lti` | period | Thời gian putaway nhập kho trung bình theo ngày (giờ) | Average inbound putaway time per day, in hours |
| IB - Avg Putaway Time by Warehouse (h) | `1g3ap9ejca` | period | So sánh thời gian putaway trung bình giữa các kho | Average putaway time compared across warehouses |

### Return Insights (`f3qc9p1mgh`)

- **Mục đích:** Hàng hoàn: sản lượng hoàn, SLA kiểm hoàn và hàng hoàn tồn đọng.
- **Purpose:** Returns: returned volume, inspection SLA and backlog.
- **Kỳ mặc định:** last_3_months
- **Bộ lọc:** Period, Country, Seller, Warehouse, Sales Channel, Courier, Return Status, Return Type

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| RT - Return KPIs | `b5vfkjfcfl` | period | Chỉ số hàng hoàn chính: sản lượng, tỷ lệ đúng hạn, thời gian kiểm | Key return metrics: volume, on-time rate, inspection time |
| RT - Return Order Trend | `f3qbm7bhoc` | period | Xu hướng đơn hoàn về kho theo ngày | Daily trend of return orders received |
| RT - Return Rate Trend | `f3qbqm6pft` | period | Tỷ lệ hoàn = đơn hoàn / đơn xuất (mẫu số đã loại đơn hoàn) | Return rate = return orders / outbound orders (returns excluded from denominator) |
| RT - Return Orders by Warehouse | `f3qb2vt2l2` | period | Số đơn hoàn theo kho | Return orders compared across warehouses |
| RT - Return Processing Aging | `25hgempql1` | period | Tuổi tồn của đơn hoàn chưa xử lý xong | Aging of returns still waiting to be processed |
| RT - Return Type | `d5hhimgmco` | period | Tỷ trọng hàng hoàn theo loại hoàn | Share of returns by return type |
| RT - Ontime Rate Trend | `25vgub8bhj` | period | Tỷ lệ xử lý hàng hoàn đúng hạn theo ngày (%) | Daily on-time rate for return processing (%) |
| RT - Ontime vs Overdue SLA by Warehouse | `15vhqceiu7` | period | Hàng hoàn xử lý đúng hạn và trễ hạn theo kho | On-time vs overdue return processing per warehouse |
| RT - SLA Rate by Warehouse | `45vk0asdcf` | period | Tỷ lệ đạt SLA kiểm hàng hoàn theo kho (%) | Return-inspection SLA pass rate compared across warehouses (%) |
| RT - Return Detail | `f3qc2lpfnk` | period | Chi tiết đơn hoàn và SLA kiểm hàng | Order-level detail of return orders and inspection SLA |

### Return Loss & Cost Insights (`9qvahnrf48`)

- **Mục đích:** Phí xử lý hoàn theo tháng và kênh bán, giá trị hàng hoàn hư hỏng hiện tại, và bồi thường hàng hoàn hư hỏng hoặc thất lạc.
- **Purpose:** Return handling fees by month and sales channel, current damaged-stock value, and compensation for damaged or lost returns.
- **Kỳ mặc định:** last_3_months
- **Bộ lọc:** Country, Period, Seller, Warehouse, Sales Channel, Condition
- **Lưu ý:**
  - Phí và bồi thường tính theo tháng; chart phí chỉ nhận mốc từ tháng trở lên.
  - Giá trị hàng hư hỏng là ảnh chụp hiện tại, không cộng dồn theo tháng.
  - Chart bồi thường chỉ giữ 3 tháng dữ liệu; rỗng nghĩa là không có bồi thường trong kỳ.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| RL - Return Handling KPIs | `6qgr19qard` | period | Số đơn hoàn/đổi được tính phí và phí xử lý hoàn | Return/exchange orders billed and return handling fee |
| RL - Return Handling Fee Trend | `2qiapghskf` | period | Phí xử lý hoàn theo tháng, tách đơn hoàn và đơn đổi | Monthly return handling fee, return vs exchange |
| RL - Return Handling Fee by Sales Channel | `8qilg13nuk` | period | Phí xử lý hoàn theo kênh bán | Return handling fee by sales channel |
| RL - Damaged Stock Value by Condition (current) | `3qjig4vcjt` | fixed | Giá trị tồn hư hỏng theo mức độ D1/D2/D3 | Damaged stock value split by condition level |
| RL - Damaged Stock Value by Warehouse (current) | `aqjttuesb1` | fixed | Giá trị tồn hư hỏng theo kho và mức độ | Damaged stock value by warehouse and condition |
| RL - Top 10 Categories by Damaged Stock Value (current) | `0qkumt0kqb` | fixed | Top ngành hàng theo giá trị tồn hư hỏng | Top categories by damaged stock value |
| RL - Return Loss Compensation by Month | `1qlcolquir` | period | Bồi thường hàng hoàn hư hỏng/thất lạc theo tháng | Monthly compensation for damaged/lost returns |
| RL - Damaged Stock Detail by SKU (current) | `1qlsebu15m` | fixed | Chi tiết SKU tồn hư hỏng, định giá theo đơn giá tồn kho | SKU-level damaged stock valued at inventory unit price |

## Inventory

### Inventory Overview (`6n0l7unjus`)

- **Mục đích:** Ảnh chụp tồn kho hiện tại theo kho, ngành hàng, nhóm tốc độ bán, tuổi tồn, trạng thái và tình trạng hàng.
- **Purpose:** Current stock snapshot by warehouse, category, velocity class, ageing, stock status and condition.
- **Kỳ mặc định:** không có (ảnh chụp/cửa sổ cố định)
- **Bộ lọc:** Country, Seller, Warehouse, Storage Type, Product Type, Category
- **Lưu ý:**
  - Ảnh chụp hiện tại, không theo Period.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Inventory KPIs | `5mk7gvfi4n` | fixed | Chỉ số tồn kho chính: số SKU, số lượng tồn, giá trị tồn | Key inventory metrics: SKUs, units on hand, stock value |
| Inventory Value by Warehouse | `9mk86t4lu2` | fixed | Giá trị tồn kho theo kho | Stock value compared across warehouses |
| Inventory Qty by Warehouse | `0mkasettd9` | fixed | Số lượng tồn kho theo kho | Units on hand compared across warehouses |
| Value by Category | `8mke0sjkhh` | fixed | Tỷ trọng giá trị tồn theo nhóm sản phẩm | Stock value share by product category |
| Velocity Class | `7mkmtpmnmp` | fixed | Tồn kho theo tốc độ luân chuyển (nhanh / chậm) | Stock split by velocity class (fast / slow moving) |
| Top SKU by Quantity | `7mkfgechj5` | fixed | Các SKU có số lượng tồn lớn nhất | SKUs with the largest units on hand |
| Top SKU by Value | `4mkhl7jajp` | fixed | Các SKU có giá trị tồn cao nhất | SKUs with the highest stock value |
| Inventory Value by Aging | `dmkjshi6qs` | fixed | Giá trị tồn kho theo tuổi tồn | Stock value grouped by inventory age |
| Stock Status Breakdown | `4mkk5g5u5m` | fixed | Tỷ trọng tồn kho theo trạng thái | Share of stock by status |
| Inventory by Condition | `0mko0d9dlk` | fixed | Số lượng tồn theo tình trạng hàng | Units on hand grouped by stock condition |

### Stock Risk & Replenishment (`c8djm4k8kq`)

- **Mục đích:** Rủi ro tồn kho hiện tại: nguy cơ hết hàng và ưu tiên đặt bổ sung, hàng chết và hàng tồn dư theo giá trị.
- **Purpose:** Current stock risk: stockout risk and reorder priority, dead stock and overstock by value.
- **Kỳ mặc định:** không có (ảnh chụp/cửa sổ cố định)
- **Bộ lọc:** Seller, Country, Warehouse, Risk Level, Category, Product Type
- **Lưu ý:**
  - Ảnh chụp hiện tại, không theo Period.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Stock Risk - KPIs | `586ddc80kh` | fixed | KPI rủi ro tồn kho: tổng SKU, giá trị tồn, SKU sắp hết hàng, lượng cần nhập thêm, giá trị hàng chết & tồn dư | Stock risk KPIs: total SKUs, stock value, stockout risk, reorder need, dead & excess stock |
| SKU Count by Risk Level | `786grdubad` | fixed | Phân bố SKU theo mức độ rủi ro tồn kho | Distribution of SKUs across risk levels |
| Stock Value by Risk Level | `f86jbt7dt3` | fixed | Giá trị tồn kho đang nằm ở từng mức rủi ro | Inventory value locked in each risk level |
| Stock Value by Warehouse & Risk | `386l0aod87` | fixed | Hàng rủi ro đang nằm ở kho nào | Where risky stock sits across warehouses |
| Reorder Priority - Stockout Risk SKUs | `186sv3gasp` | fixed | SKU sắp hết hàng kèm lượng đề xuất nhập thêm | SKUs at risk of stockout with suggested reorder quantity |
| Dead Stock - Top by Value | `386u6otmvd` | fixed | SKU hàng chết (không bán được) xếp theo giá trị vốn bị chôn | Dead stock SKUs (no sales) ranked by locked value |
| Overstock - Top Excess Value | `a871qss7dl` | fixed | SKU tồn dư quá mức xếp theo giá trị tồn vượt nhu cầu | Overstocked SKUs ranked by excess inventory value |

### Inventory Risk Alerts (`f5ok7o4sp4`)

- **Mục đích:** Cảnh báo tồn kho: hàng tồn lâu theo nhóm tuổi và hàng sắp hết hạn.
- **Purpose:** Inventory alerts: aged stock by bucket and expiring stock.
- **Kỳ mặc định:** không có (ảnh chụp/cửa sổ cố định)
- **Bộ lọc:** Country, Seller, Warehouse, Storage Type, Product Type, Category
- **Lưu ý:**
  - Ảnh chụp hiện tại, không theo Period.
  - Hàng không có hạn dùng không được coi là hết hạn.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Inventory Alert KPIs | `cnq1e7ki6j` | fixed | KPI cảnh báo: giá trị tồn lâu, hàng sắp hết hạn, hàng hỏng | Alert KPIs: aging stock value, expiring stock, damaged units |
| Aging Inventory by Bucket (Value) | `fnq4r5ghn1` | fixed | Giá trị tồn kho theo nhóm tuổi tồn | Stock value grouped by aging bucket |
| Aging Inventory - Top by Value | `enq7c4jbj1` | fixed | Các SKU tồn lâu có giá trị tồn kho cao nhất | Slow-moving SKUs with the highest stock value |
| Expiring Inventory by Time Bucket | `enqalsrvc9` | fixed | Tồn kho sắp hết hạn theo nhóm thời gian còn lại | Expiring stock grouped by time-to-expiry bucket |
| Expiring Inventory - Priority SKUs | `anqd060fhr` | fixed | Các SKU sắp hết hạn cần xử lý trước | SKUs closest to expiry that need action first |

### Inventory Movement & Turnover (`25oi922j2s`)

- **Mục đích:** Nhập, xuất, tồn và tỷ lệ hư hỏng/hoàn theo tháng, 3 tháng gần nhất.
- **Purpose:** Monthly inbound, outbound, stock and damaged/return rates, last 3 months.
- **Kỳ mặc định:** không có (ảnh chụp/cửa sổ cố định)
- **Bộ lọc:** Country, Seller, Warehouse, Period
- **Lưu ý:**
  - Cửa sổ cố định 3 tháng, không theo Period.
  - Closing Stock = tồn ngày cuối có dữ liệu của tháng (Business KPIs: tháng cuối trong khoảng). Stock Turnover = xuất kho ÷ tồn bình quân ngày. Damaged Rate = tồn hỏng cuối kỳ ÷ tồn cuối kỳ (sửa 08/11/2026).

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Business KPIs (Monthly) | `280hb3ps8f` | fixed | KPI tồn kho theo tháng: số lượng tồn, thể tích, phí lưu kho | Monthly inventory KPIs: stock units, storage volume, storage fee |
| Inbound vs Outbound Trend | `2b7r4mauds` | fixed | Số lượng nhập và xuất kho theo tháng | Monthly inbound vs outbound units |
| Closing Stock Trend | `6b86qbs070` | fixed | Xu hướng tồn kho cuối kỳ theo tháng | Month-end closing stock trend |
| Movement by Warehouse | `fb940u3rk9` | fixed | Số lượng nhập, xuất, hoàn theo kho | Inbound, outbound and return units per warehouse |
| Damaged & Return Rate Trend | `8b8nq9s290` | fixed | Tỷ lệ hàng hỏng và hàng hoàn trên luân chuyển tồn kho | Damaged and return rate as a share of stock movements |
| Monthly Movement by Warehouse | `db9fa90glm` | fixed | Chi tiết luân chuyển tồn kho theo tháng và kho | Monthly stock movement detail per warehouse |

## Last-mile

### Last-mile Insights (`6hnvjqb71j`)

- **Mục đích:** Kết quả giao hàng của hãng vận chuyển cho vận đơn Boxme bàn giao: giao thành công, chưa giao, số ngày giao trung bình, COD hãng đã thu, giao đúng hạn.
- **Purpose:** Carrier delivery results for shipments handed over by Boxme: delivery success, not-yet-delivered, average delivery days, COD collected by carriers, on-time delivery.
- **Kỳ mặc định:** last_30_days
- **Bộ lọc:** Country, Seller, Period, Warehouse, Courier
- **Lưu ý:**
  - Giao đúng hạn = giao thành công trong 2 ngày kể từ lúc hãng lấy hàng (mốc phẳng, chưa theo cam kết từng hãng).
  - COD Collected là tiền hãng vận chuyển trong hệ thống Boxme đã thu, khác COD Amount của Sales.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Shipments | `7hn0bkkntc` | period | Tổng số đơn TẠO trong kỳ đã chọn. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Total orders created in the selected period. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| Delivery Success Rate | `9hn2k4a3t4` | period | Tỷ lệ giao thành công = đơn status 800/801 ÷ tổng đơn tạo trong kỳ (%). Đơn chưa giao xong tại thời điểm refresh vẫn nằm ở mẫu số nên tỷ lệ của các ngày gần đây sẽ thấp giả tạo. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Delivered (status 800/801) ÷ orders created in the period (%). Orders still in transit at refresh time stay in the denominator, so recent days read artificially low. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| Not Yet Delivered Rate | `9hn4t6sihv` | period | Tỷ lệ 'thất bại' = đơn CHƯA ở status 800/801 ÷ tổng đơn tạo trong kỳ (%). ⚠ Nguồn tính mọi đơn chưa giao xong là 'failed', gồm cả đơn đang trên đường — không phải tỷ lệ giao hỏng thuần. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Orders NOT yet in status 800/801 ÷ orders created (%). ⚠ The source counts every not-yet-delivered order as failed, including in-transit ones — this is not a pure delivery-failure rate. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| Avg Delivery (days) | `5hn6nscip6` | period | Thời gian giao trung bình (ngày) = Σ(success_time − pickup_time) ÷ số đơn đã giao thành công. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Avg delivery days = Σ(success_time − pickup_time) ÷ delivered orders. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| COD Collected | `ahn8lo93cs` | period | COD đã thu trên đơn giao thành công. KHÔNG quy đổi tiền tệ — chỉ đọc khi chọn 1 quốc gia. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | COD collected on delivered orders. NOT currency-converted — read it with a single country selected. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| On-time Delivery (SLA) | `5hnc77hld8` | period | Tỷ lệ đúng hạn = đơn giao thành công có success_time ≤ pickup_time + 2 ngày ÷ đơn ĐÃ giao thành công (%). SLA phẳng 2 ngày, không dùng delivery_expected_time của hãng vận chuyển. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | On-time = delivered orders with success_time ≤ pickup_time + 2 days ÷ delivered orders (%). Flat 2-day SLA, not the carrier's delivery_expected_time. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| Daily Delivery Trend | `fhngufp6t5` | period | Sản lượng đơn tạo và đơn giao thành công theo ngày. Chỉ hiển thị các ngày đã chốt dữ liệu (is_complete_day) — các ngày gần nhất bị ẩn vì pipeline còn trễ. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Daily created vs delivered volume. Only settled days are shown (is_complete_day) — the most recent days are hidden because the pipeline lags. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| Daily COD Amount | `7hnpn1r837` | period | Số tiền COD thu theo ngày (không quy đổi tiền tệ). Chỉ các ngày đã chốt dữ liệu. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | COD amount per day (not currency-converted). Settled days only. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| Return Status Breakdown | `3hnl7n2p53` | period | Đơn hoàn theo trạng thái (nguồn bms_mat_return_daily, mốc = ngày bản ghi hoàn) — KHÁC mốc ngày tạo đơn của các KPI phía trên, không cộng trừ trực tiếp với chúng. | Return orders by status (source bms_mat_return_daily, dated by return record) — a DIFFERENT date basis from the KPIs above; do not net them against each other. |
| Carrier Performance | `8hntskv7do` | period | Bảng hãng vận chuyển: sản lượng, tỷ lệ thành công/thất bại, thời gian giao. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Carrier scorecard: volume, success/failed rate, delivery time. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| Volume Share by Courier | `8o8i213ar7` | period | Tỷ lệ sản lượng theo hãng vận chuyển. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Share of volume by carrier. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |

### Delivery & Carrier Performance (`3ap9jh26jj`)

- **Mục đích:** Hiệu suất giao hàng theo hãng: sản lượng, thời gian giao và tỷ lệ đúng hạn.
- **Purpose:** Delivery performance by carrier: volume, delivery time and on-time rate.
- **Kỳ mặc định:** last_30_days
- **Bộ lọc:** Country, Seller, Warehouse, Period, Courier
- **Lưu ý:**
  - Tỷ lệ đúng hạn dùng cùng quy tắc 2 ngày như Last-mile Insights.

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Carrier KPIs | `48gneog3nf` | period | Chỉ số hãng vận chuyển: sản lượng, tỷ lệ đúng hạn (trên đơn ĐÃ giao), thời gian giao, số đơn giao trễ. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Carrier KPIs: volume, on-time rate (of delivered orders), delivery time, late-delivered orders. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| Delivery Volume Trend | `a8e81po5go` | period | Sản lượng đơn theo tuần ISO. Chỉ các tuần đã trọn vẹn và đã chốt dữ liệu (is_complete_week). Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Weekly (ISO) order volume. Complete, settled weeks only (is_complete_week). Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| On-time Delivery Rate Trend (%) | `38fh8jdmcg` | period | Tỷ lệ giao đúng hạn theo tuần (% trên đơn đã giao, SLA phẳng 2 ngày). Chỉ tuần đã chốt dữ liệu. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Weekly on-time rate (% of delivered, flat 2-day SLA). Settled weeks only. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| Delivery Volume by Courier | `a8egbrsvhl` | period | Sản lượng đơn theo hãng vận chuyển (top 15). Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Order volume by carrier (top 15). Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| On-time Rate by Courier (%) | `48fublf72v` | period | Tỷ lệ đúng hạn theo hãng vận chuyển (% trên đơn đã giao, SLA phẳng 2 ngày). Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | On-time rate by carrier (% of delivered, flat 2-day SLA). Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| AVG Delivery Time Trend (days) | `68etumo08u` | period | Thời gian giao trung bình theo tuần (ngày). Chỉ tuần đã chốt dữ liệu. Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Weekly average delivery time (days). Settled weeks only. Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| AVG Delivery Time by Courier (days) | `38f5a2e4ri` | period | Thời gian giao trung bình theo hãng vận chuyển (ngày). Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | Average delivery time by carrier (days). Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |
| On-time Delivery Rate by Warehouse (%) | `e8gakuchjp` | period | Tỷ lệ đúng hạn theo kho (% trên đơn đã giao, SLA phẳng 2 ngày). Mốc thời gian = NGÀY TẠO ĐƠN. Không gồm đơn hoàn (order_type 7), kho test, và đơn seller/hệ thống huỷ trước khi vào kho (status 700/703/708 không có trong nguồn). | On-time rate by warehouse (% of delivered, flat 2-day SLA). Date basis = ORDER CREATION date. Excludes return orders (order_type 7), test warehouses, and orders cancelled before warehouse intake (status 700/703/708 are absent from the source). |

### Exception & Risk (`2aph4uahev`)

- **Mục đích:** Ngoại lệ giao hàng và lý do giao thất bại, kèm chi tiết từng vận đơn để xử lý.
- **Purpose:** Delivery exceptions and failed-delivery reasons, with shipment-level detail.
- **Kỳ mặc định:** last_30_days
- **Bộ lọc:** Country, Seller, Warehouse, Period, Courier

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Exception Type Distribution | `d8hl9jk856` | period | Tỷ trọng sự cố theo loại. ⚠ Mốc thời gian của màn này = NGÀY DỰ KIẾN GIAO, không phải ngày tạo đơn; phân loại sự cố tính tại thời điểm mở báo cáo. | Share of exceptions by type. ⚠ On this dashboard the date basis is EXPECTED DELIVERY date, not order creation; exception class is evaluated at read time. |
| Failed Delivery Reason | `48i1fjvbr7` | period | Giao thất bại theo nguyên nhân. ⚠ Mốc thời gian = NGÀY DỰ KIẾN GIAO, không phải ngày tạo đơn. | Failed deliveries by reason. ⚠ Date basis = EXPECTED DELIVERY date, not order creation. |
| Exception Detail | `18hgso3suo` | period | Chi tiết từng đơn có sự cố. ⚠ Mốc thời gian = NGÀY DỰ KIẾN GIAO, không phải ngày tạo đơn. | Order-level exception detail. ⚠ Date basis = EXPECTED DELIVERY date, not order creation. |

## Cost

### 5. Fulfillment Cost Insights (`4amp950vh0`)

- **Mục đích:** Phí dịch vụ fulfillment theo dịch vụ, loại dịch vụ, kho và tháng.
- **Purpose:** Fulfillment service fees by service, service type, warehouse and month.
- **Kỳ mặc định:** last_3_months
- **Bộ lọc:** Country, Warehouse, Service Type, Period, Seller, Order Type
- **Lưu ý:**
  - Phí sau chiết khấu, trước VAT.
  - Phí tính theo tháng; chỉ nhận mốc từ tháng trở lên.
  - Discount Detail rỗng nghĩa là seller không có khoản giảm phí.
  - Storage (CBM) = m³ lưu kho bình quân mỗi ngày; AVG Storage Fee = phí trên mỗi m³ mỗi tháng (trước VAT). Chỉ có với tháng đã chốt; tháng đang chạy để trống (sửa 08/11/2026).

| Chart | Id | Window | Mô tả (vi) | Description (en) |
|---|---|---|---|---|
| Volume Overview | `4npvgifit2` | period | Tổng quan sản lượng đơn và trọng lượng tính phí | Order volume and billed weight overview |
| Fee by Service | `2ntbckgmls` | period | Fee (sau chiết khấu, trước VAT) và Fee trung bình trên mỗi đơn vị volume theo loại dịch vụ | Fee (after discount, excl. VAT) and avg Fee per volume unit by service type |
| Fee by Service Type | `2ag26g8je5` | period | Tỷ trọng Fee (sau chiết khấu, trước VAT) theo loại dịch vụ | Share of Fee (after discount, excl. VAT) by service type |
| Fee by Warehouse | `eag46p6btg` | period | Phân bổ Fee (sau chiết khấu, trước VAT) theo kho xử lý | Fee (after discount, excl. VAT) across fulfillment centers |
| Fee Trend | `fag6kcb48v` | fixed | Fee dịch vụ Boxme (sau chiết khấu, trước VAT) theo kỳ | Boxme Fee (after discount, excl. VAT) by period |
| Service Fee detail | `8ag84pksam` | period | Chi tiết phí theo kho và dịch vụ: phí dịch vụ, điều chỉnh, phí trước chiết khấu, chiết khấu và Fee (sau chiết khấu, trước VAT) | Fee lines by warehouse and service: service fee, adjustment, fee before discount, discount and Fee (after discount, excl. VAT) |
| Avg Net Fee (ex-VAT) / Volume trend | `ccbq7qfd4s` | fixed | Phí thuần trung bình (sau chiết khấu, chưa VAT) trên mỗi đơn vị volume theo loại dịch vụ theo thời gian | Avg net fee (after discount, excl. VAT) per volume unit by service type over time |
| Cost Efficiency Overview | `46k6hbepbj` | period | NMV, tổng chi phí hậu cần, %Cost/NMV, trọng lượng tính cước và số sản phẩm bình quân/đơn. | NMV, total logistics cost, Cost/NMV%, average chargeable weight and items per order. |
| Discount Detail by Seller & Fee Type | `8adlkjspp8` | period | Chi tiet chiet khau theo khach hang va loai phi duoc chiet khau | Discount detail by seller and discounted fee type |
