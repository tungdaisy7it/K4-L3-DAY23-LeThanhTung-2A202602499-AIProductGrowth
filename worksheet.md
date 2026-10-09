# Worksheet — Haravan AI CSKH

Họ tên: Lê Thanh Tùng · MSSV: 2A202602499 · Ngày làm: 09/10/2026

## Số đầu vào (chép từ bài Day 22: `day22_monetization_model.xlsx`, `day22_one_pager_template.docx`)

| Số | Giá trị | Ô nguồn (Day 22) | Trạng thái |
|---|---|---|---|
| Value Metric | Hybrid: $15/tháng phí nền + $0,20 / resolution | 3_Value_Metric!B30, 2_Pricing!B19 | Quyết định |
| ARPU | $155/tháng = 700 job hoàn thành × $0,20 + $15 | 4_Channel_Fit!B5 | Mô hình |
| ACV | $1.860/năm = 155 × 12 | 4_Channel_Fit!B10 | Mô hình |
| Cost/Job (hoàn thành, Biến thể A, chưa overhead) | $0,058 | 1_Cost_Job!B66 | Mô hình, chưa đo |
| Cost/Job có overhead $40/khách | $0,115 | 1_Cost_Job!B67 | Mô hình |
| Gross margin | 70,9% chưa overhead · ~42% có overhead | 2_Pricing!B21 | Mô hình |
| Containment | 70% (ước tính, **chưa đo**) | 1_Cost_Job!B10 | Ước tính |
| Breakeven containment (GM mục tiêu 60%) | 50,9% | 2_Pricing!B33 | Mô hình |
| CAC (ngân sách tối đa) | $1.319 = 155 × 70,9% × 12 tháng | 4_Channel_Fit!B9 | Mô hình |
| CAC thực tế của kênh Partner-Led | **chưa có** (chưa nói chuyện với partner) | — | ❌ |
| CAC payback mục tiêu | < 12 tháng (SMB) | 4_Channel_Fit!B8 (Bessemer, Scaling to $100M, 2024) | Mục tiêu |
| Runway | **chưa có trong hồ sơ Day 22**, không bịa; dashboard không phụ thuộc số này | — | ❌ |

> **Lưu ý trung thực:** ô 1_Cost_Job!B10 trong file xlsx đang lưu 0,82, còn ghi chú E10 và One-Pager đều nói 70%. Mọi phép tính dưới đây dùng **70%** vì $0,058 / 70,9% / 50,9% đều tính từ 70%. Cần sửa ô B10 trong file Day 22 cho khớp.

Cách ra Cost/Job (từ Tab 1): 1 job thử = 6 lượt, cache 3.500 token, fresh 1.200, output 350, giá Haiku 4.5 $1 / $5 / cache write 1,25× / cache read 0,1× (kiểm tra 08/10/2026).
LLM = 3.500×1,25/1M + 5×3.500×0,1/1M + 6×1.200×1/1M + 6×350×5/1M = $0,0238/job thử.
Chi phí biến đổi / job thử = 0,0238 (LLM) + 0,010 (infra) + 0,0019 (retry 8% × LLM) = $0,0357. QA nội bộ = 5% × 2 phút × $3/giờ ÷ 60 = $0,005/job thử. Tổng $0,0407 × 1.000 job thử = $40,7/tháng; chia cho 700 job hoàn thành = **$0,058**.

## Trạm 1 — Loại mô hình

**Câu chốt loại:** Chúng tôi là **B2B** vì tiền đến từ chủ shop online SME (ngân sách vận hành/CSKH, thay giờ nhân viên trực inbox), người dùng sản phẩm chính là chủ shop (cài app, đọc dashboard, xử lý ca escalate), còn khách mua hàng của shop chỉ nhắn qua Zalo OA/Messenger của shop, dưới thương hiệu shop: chúng tôi không có dữ liệu, tài khoản hay thương hiệu trước mặt họ. Haravan là kênh phân phối (App Store) chứ không phải người trả tiền, nên không phải B2B2C.

Ba câu hỏi: (1) Ai trả tiền: chủ shop, $15 + $0,20/resolution. (2) Ai dùng: chủ shop. (3) Chạm end-user qua đâu: không chạm trực tiếp, chỉ trả lời hộ shop trong khung chat của shop. Theo HANDBOOK §2.5 thì không chạm được = dùng bảng B2B.

**Bảng đèn §3.2 (B2B), mọi đèn:**

| Đèn | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|
| TTFV (ký → giá trị đo được đầu tiên; với SME tự cài app thì "ký" = lúc cài xong) | 🔧 | Cần log 2 mốc thời gian: lúc shop cài app và lúc có hội thoại hoàn thành đầu tiên. Hai mốc đã có trong thiết kế log từng hội thoại (3_Value_Metric!E5), cần dựng event trong 2 tuần |
| Pipeline coverage | 🔧 | Bảng tính danh sách merchant do Haravan giới thiệu × giá trị năm; chưa có target doanh thu quý để chia |
| % deal chết ở security/procurement | ❌ | SME tự quyết trong ngày, không có khâu procurement; khâu duyệt listing của partner chưa biết cách đo |
| POC → paid | 🔧 | 5 shop pilot, đếm số shop trả phí sau 4 tuần + 14 ngày (sheet tay). Có số sau 15/12/2026 |
| Sales cycle | 🔧 | Ngày từ lúc được giới thiệu đến lúc thanh toán phí nền đầu tiên, ghi tay mỗi shop |
| Usage depth | 🔧 | Đếm job hoàn thành/shop/tuần từ log hội thoại; cần dựng truy vấn |
| Chi phí triển khai ÷ ACV | 🔧 | Ghi giờ onboarding từng shop (mục tiêu < 1 giờ) × $3/giờ ÷ ACV $1.860 |
| Tập trung doanh thu | ❌ | Chưa có khách trả phí; đo được khi có ≥ 3 shop trả tiền (dự kiến 01/2027) |
| NRR | ❌ | Cần ≥ 12 tháng dữ liệu thanh toán; chưa biết có đo nổi trong khung 90 ngày hay không |
| Gross margin | 🔧 | Mô hình có (70,9%), số thực cần chi phí token thật từ log API + hoá đơn nhà cung cấp, 2 tuần |
| CAC payback | ✅/❌ | Ngân sách CAC tối đa $1.319 đã tính (✅); CAC thực của kênh Partner-Led chưa có (❌) |
| *Đèn tôi thêm:* Containment rate | 🔧 | Cần 150 hội thoại gắn nhãn tay từ 5 shop pilot (kế hoạch Day 22, hạn 15/11/2026) |
| *Đèn tôi thêm:* Cost/Job hoàn thành (p95 shop) | 🔧 | Cần log token/hội thoại theo shop; bảng §3.2 không có đèn chi phí AI trực tiếp nên tôi thêm |
| *Đèn tôi thêm:* Logo churn/tháng | ❌ | Chưa có khách trả tiền, phải có ≥ 3 tháng thanh toán |

## Trạm 2 — Thẻ đèn

**North Star:** TTFV (Time-to-first-value) — hiện tại chưa đo — mục tiêu ≤ 48 giờ. Đây là đèn bật trước của B2B (HANDBOOK §2.5).

| # | Tầng | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | **TTFV** | Số giờ từ lúc shop cài app xong đến lúc có hội thoại hoàn thành đầu tiên (khách xác nhận, hoặc không nhắn lại 24h). **Không** tính: hội thoại test của chính chủ shop, hội thoại bị escalate, "đã cài xong" chưa có khách thật | Giờ(hội thoại hoàn thành thật đầu tiên) − Giờ(cài xong) | Mỗi shop, xem hằng tuần · Tùng | Usage depth (O) → Logo churn (G) |
| 2 | L | **Containment rate** | % hội thoại AI tự xử lý xong. **Không** tính: hội thoại escalate cho chủ shop, lỗi kỹ thuật, khách bỏ ngang trước khi AI trả lời, tin nhắn test nội bộ | Hội thoại hoàn thành ÷ hội thoại thật vào bot, trên mẫu ≥ 150 hội thoại đã gắn nhãn | Hằng tuần · Tùng gắn nhãn | Cost/Job (L) → Gross margin (G) |
| 3 | L | **Cost/Job hoàn thành** *(đèn chi phí AI)* | Tổng chi phí biến đổi (LLM + infra + retry + QA nội bộ) ÷ số job hoàn thành, tính trên tuần, lấy cả mức trung bình và shop ở p95. **Không** tính: overhead $40/khách, chi phí xử lý escalate (Biến thể A khách tự chịu) | (LLM + infra + retry + QA) ÷ job hoàn thành | Hằng tuần · Tùng, từ log token | Gross margin (G) |
| 4 | O | **Job hoàn thành/shop/tuần** (median các shop go-live) | Số job hoàn thành theo định nghĩa chặt ở Tab 1 trong 7 ngày, lấy median qua các shop đã go-live ≥ 14 ngày. **Không** tính shop mới < 14 ngày, tin test | Median(job hoàn thành 7 ngày của từng shop) | Hằng tuần · Tùng | ARPU/Gross profit → Logo churn (G) |
| 5 | O | **Pilot → paid** | % shop pilot trả phí nền $15 lần đầu trong vòng 14 ngày sau khi hết 4 tuần pilot. **Không** tính shop hứa miệng, shop dùng thử miễn phí tiếp | Số shop trả phí ÷ số shop pilot đã hết 4 tuần | Mỗi đợt pilot · Tùng | Số shop trả phí → doanh thu / CAC payback |
| 6 | G | **Gross margin (COGS)** | (Doanh thu − COGS) ÷ doanh thu, doanh thu gồm phí nền + phí resolution. **Không** trừ overhead R&D/Sales $40/khách, **chưa** trừ rev-share partner (chưa thương lượng) | (Doanh thu − COGS) ÷ doanh thu | Hằng tháng · Tùng | — (kết quả) |
| 7 | G | **Logo churn/tháng** | Số shop huỷ hoặc ngừng trả phí trong tháng ÷ số shop trả phí đầu tháng. **Không** tính shop pilot chưa chuyển trả phí | Shop rời ÷ shop đầu tháng | Hằng tháng · Tùng | — (kết quả) |

Đèn chi phí AI là đèn số **3** (Cost/Job hoàn thành). Bắt được chi phí token tăng trước khi nó hiện ra ở gross margin hằng tháng. Lagging: 2/7 đèn (< 50%). Leading: 3 đèn, mỗi đèn có "báo trước cho" cụ thể.

## Trạm 3 — Ngưỡng

Ngày mở nguồn [BM]: **09/10/2026**.

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | TTFV | ≤ 48 giờ | 48 giờ – 7 ngày | > 7 ngày | [TB] | Nỗi đau xảy ra mỗi đêm 22:30–01:00 (giả định Day 22), nên nếu sau 2 đêm chưa có job hoàn thành là cấu hình/tích hợp có vấn đề, và sau 7 đêm là chắc chắn có lỗi; chưa có baseline, đo 5 shop pilot, có số ngày 15/11/2026 |
| 2 | Containment rate | ≥ 70% | 51% – 70% | < 51% | [MH] | Dưới 50,9% thì GM tụt khỏi mục tiêu 60% (Phụ lục A); 70% là mức tôi đã giả định trong mô hình nên chỉ xanh khi chứng minh được |
| 3 | Cost/Job hoàn thành | ≤ $0,067 | $0,067 – $0,080 | > $0,080 | [MH] | $0,080 là mức GM chạm 60% ở giá $0,20; $0,067 là mức giá bán còn gấp 3× cost (quy tắc giá sàn Day 22) (Phụ lục B) |
| 4 | Job hoàn thành/shop/tuần (median) | ≥ 121 | 41 – 121 | < 41 | [MH] | 121/tuần ≈ 525/tháng là mức cho ARPU ≥ $120 (KPI tháng 2–3 Day 22); dưới 41/tuần thì lãi gộp không bù nổi overhead $40 (Phụ lục C) |
| 5 | Pilot → paid | ≥ 50% (≥ 3/5 shop) | 35% – 50% (2/5) | < 35% (≤ 1/5) | [BM] | ICONIQ State of GTM 2026 nêu POC/trial → paid ≈ 50% (từ ≈ 36% năm trước); kiểm tra 09/10/2026 tại iconiq.com/growth/reports/state-of-go-to-market-2026. Với n=5 thì mỗi shop là 20 điểm %, nên 35% = dưới 2 shop |
| 6 | Gross margin (COGS) | ≥ 60% | 50% – 60% | < 50% | [MH] + [BM] | 60% là mục tiêu của mô hình (Tab 2 B32, KPI tháng 4+); 50% ứng với Cost/Job $0,10 (Phụ lục B); đối chiếu: ICONIQ State of AI 2026 nêu GM sản phẩm AI 45% (2025) → 53% (2026P), kiểm tra 09/10/2026, nên 🟡 chứa mức trung bình ngành |
| 7 | Logo churn/tháng | ≤ 8,3% | 8,3% – 10% | > 10% | [MH] | Tuổi thọ khách = 1 ÷ churn; payback mục tiêu 12 tháng nên khách phải ở ≥ 12 tháng, tức churn ≤ 8,3%; 10% là KPI tháng 2–3 của Day 22 (Phụ lục D) |

Đèn [TB] (TTFV) không có benchmark: ghi "chưa có chuẩn, đo 2 chu kỳ rồi lấy làm baseline", chu kỳ đầu từ 5 shop pilot, số đầu tiên ngày 15/11/2026.

### Phụ lục [MH] — phép tính

**[MH] A — Containment tối thiểu (đèn 2)**

```
Đầu vào (Day 22): giá P = $0,20/job hoàn thành · GM mục tiêu = 60%
  v = chi phí biến đổi / job THỬ = 0,0238 (LLM) + 0,010 (infra) + 0,0019 (retry) = $0,0357
  q = QA nội bộ / job THỬ = 5% × 2 phút × $3/giờ ÷ 60 = $0,005
  e = chi phí xử lý 1 ca escalate = 0 (Biến thể A: chủ shop tự xử lý)
Phép tính: R ≥ (v + q + e) ÷ (P × (1 − GM) + e)
           R ≥ (0,0357 + 0,005) ÷ (0,20 × 0,40) = 0,0407 ÷ 0,080 = 0,509
Kết quả → 🟢 ≥ 70% (mức mô hình đang giả định) · 🟡 51–70% · 🔴 < 51% (= 50,9% làm tròn lên)
Kiểm tra ngược: ở R = 50,9%, Cost/Job = 0,0407 ÷ 0,509 = $0,080, GM = (0,20 − 0,080) ÷ 0,20 = 60%. ✓
```

**[MH] B — Cost/Job hoàn thành tối đa (đèn 3 và đèn 6)**

```
Đầu vào: giá P = $0,20 · GM mục tiêu = 60% · hệ số giá sàn = 3× (Tab 2 B6)
Phép tính: Cost/Job tối đa để GM ≥ 60%  = 0,20 × (1 − 0,60) = $0,080
           Cost/Job tối đa để giá ≥ 3×cost = 0,20 ÷ 3        = $0,0667
           Cost/Job tại GM 50%              = 0,20 × (1 − 0,50) = $0,100
Kết quả đèn 3 → 🟢 ≤ $0,067 · 🟡 $0,067–0,080 · 🔴 > $0,080
Kết quả đèn 6 → 🔴 khi GM < 50% (Cost/Job > $0,10); hiện mô hình: $0,058 → GM 71%, đang 🟢
```

**[MH] C — Job hoàn thành/shop/tuần (đèn 4)**

```
Đầu vào: phí nền $15 · giá $0,20/job · Cost/Job $0,058 · overhead $40/khách/tháng
         KPI tháng 2–3 (Day 22): ARPU ≥ $120 · 1 tháng ≈ 4,33 tuần
Phép tính 🟢: 15 + 0,20 × n ≥ 120 → n ≥ 525 job/tháng → 525 ÷ 4,33 = 121 job/tuần
Phép tính 🔴: lãi gộp mỗi job = 0,20 − 0,058 = $0,142; cần 15 + 0,142 × n ≥ 40 (bù overhead)
              → n ≥ 25 ÷ 0,142 = 176 job/tháng → 176 ÷ 4,33 = 41 job/tuần
Kết quả → 🟢 ≥ 121 · 🟡 41–121 · 🔴 < 41
(Mô hình giả định 700 job/tháng = 162/tuần, nên 🟢 đã thấp hơn giả định.)
```

**[MH] D — Logo churn/tháng (đèn 7)**

```
Đầu vào: CAC payback mục tiêu = 12 tháng (SMB) · KPI churn Day 22 = 10%/tháng
Phép tính: tuổi thọ trung bình = 1 ÷ churn. Cần tuổi thọ ≥ 12 tháng → churn ≤ 1 ÷ 12 = 8,33%
           Ở churn 10% thì tuổi thọ = 10 tháng < 12 tháng: khách rời trước khi hoàn vốn CAC
Kết quả → 🟢 ≤ 8,3% · 🟡 8,3–10% · 🔴 > 10%
```

## Trạm 4 — 5 luật quyết định

⏹ = luật dừng (4 luật dừng: 1, 2, 4, 5). Vế NẾU dùng đúng ngưỡng 🔴 ở Trạm 3.

1. ⏹ **NẾU** TTFV > 7 ngày **TRÊN** ≥ 2 trong 3 shop pilot mới nhất **THÌ** dừng cài thêm shop mới; từ thứ Hai tuần sau, Tùng cắt phạm vi cài đặt của mọi shop xuống 1 kênh chat (Zalo OA hoặc Messenger) + 1 nhóm câu hỏi (tra đơn/vận chuyển) cho đến khi 2 shop liên tiếp đạt TTFV ≤ 48 giờ. **KHÔNG THÌ** không mở thêm kênh hay tính năng, và không giảm phí nền $15 để giữ shop ở lại (shop không bỏ vì giá, họ bỏ vì chưa thấy giá trị).

2. ⏹ **NẾU** containment < 51% **TRONG** 2 tuần liên tiếp **VÀ** mỗi tuần ≥ 150 hội thoại đã gắn nhãn **THÌ** dừng onboard shop mới và dừng việc dựng listing Haravan beta; Tùng gắn nhãn 50 ca escalate gần nhất, gom thành tối đa 3 nhóm lỗi, sửa KB/prompt trong 2 tuần, rồi đo lại. **KHÔNG THÌ** không nhận xử lý ca escalate thay chủ shop (Biến thể B làm Cost/Job lên $0,187, GM ~7%) và không đẩy tất cả sang model đắt hơn trước khi đo Cost/Job của nó.

3. **NẾU** Cost/Job hoàn thành > $0,080 (mức trung bình hoặc shop p95) **TRONG** 2 tuần liên tiếp **VÀ** ≥ 100 job hoàn thành mỗi tuần **THÌ** Tùng cắt số lượt tối đa mỗi job xuống 4, kiểm tra prompt caching còn bật, và thử một model rẻ hơn trên đúng 1 shop trong 2 tuần; với shop p95, đàm phán lại điều kiện (trần lượt/tháng hoặc mức phí resolution) trước khi kết thúc tháng. **KHÔNG THÌ** không tăng giá $0,20 cho toàn bộ shop khi chưa biết shop nào gây ra, và không cắt QA nội bộ (5%) để làm đẹp số.

4. ⏹ **NẾU** median job hoàn thành/shop/tuần < 41 **TRONG** 3 tuần liên tiếp, tính trên các shop đã go-live ≥ 14 ngày **VÀ** có ≥ 3 shop **THÌ** dừng mời shop mới vào pilot; Tùng gọi từng shop dưới ngưỡng trong 7 ngày, đọc cùng chủ shop 20 hội thoại không được xử lý, và hoàn thành việc nạp KB còn thiếu của họ. **KHÔNG THÌ** không bán thêm kênh hay gói cao hơn cho shop đó, và không tìm shop mới để bù số lượng.

5. ⏹ **NẾU** pilot → paid < 35% (≤ 1/5 shop) **TRÊN** 5 shop pilot đầu, tính sau 14 ngày kể từ hết pilot **THÌ** đóng băng việc dựng listing Haravan beta; Tùng phỏng vấn đủ 5 shop (30 phút/shop) trong 7 ngày để biết lý do không trả, và chỉ làm tiếp khi có ≥ 2 shop nói rõ họ sẽ trả nếu sửa một thứ cụ thể. **KHÔNG THÌ** không giảm giá $0,20 hay bỏ phí nền $15 để kéo chuyển đổi (giá này mới chiếm ~40% lương 1 nhân viên CSKH $350, dưới dải neo 50–70%, nên giá chưa phải rào cản đã được chứng minh).

## Trạm 5 — Cổng gác 90 ngày (nháp)

Ngày 0 = 01/11/2026 (bắt đầu pilot, theo kế hoạch Day 22). Ngày 30 = 01/12/2026 · Ngày 60 = 31/12/2026 · Ngày 90 = 30/01/2027.
| Ngày | Metric (1) | Ngưỡng | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| 30 | Containment đo thực | ≥ 55% trên ≥ 150 hội thoại gắn nhãn, ≥ 3 shop | `eval_results.md` | FIX 1 lần (41–55%) · PIVOT chỉ còn tra đơn (< 41%) |
| 60 | TTFV | ≤ 48 giờ ở ≥ 3/5 shop | `ttfv_log.csv` | FIX 1 lần (onboarding) · PIVOT chỉ nhận shop đã có Zalo OA + danh mục sản phẩm |
| 90 | Pilot → paid | ≥ 3/5 shop trả phí | Hoá đơn + `pilot_report.md` | FIX 1 lần (2/5) · KILL (≤ 1/5) |

Vì sao 55% ở cổng 30: đây là KPI tháng 1 của Day 22; ở 55%, Cost/Job = 0,0407 ÷ 0,55 = $0,074 → GM = (0,20 − 0,074) ÷ 0,20 ≈ 63%, cao hơn breakeven 50,9% khoảng 4 điểm để chừa sai số của mẫu 150 hội thoại.
Vì sao 41% ở kill criteria: Cost/Job = 0,0407 ÷ 0,41 = $0,099 → GM ≈ 50%, tức chạm 🔴 của đèn Gross margin.

Bản trình bày cuối ở `dashboard.md` / `dashboard.pdf`.

## Ghi chú về cách dùng AI

Tôi (Tùng) dùng trợ lý AI để tổng hợp số liệu Day 22 và dựng bản nháp cấu trúc; benchmark [BM] được mở lại trên nguồn gốc ngày 09/10/2026. Ngưỡng, luật và cổng cần được Tùng đọc lại, sửa bằng lời của mình trước khi nộp.
