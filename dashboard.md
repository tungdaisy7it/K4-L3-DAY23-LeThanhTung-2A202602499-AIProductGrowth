# OPERATING DASHBOARD — Haravan AI CSKH

> Trợ lý AI trả lời khách của shop online ngoài giờ (Zalo OA · Messenger), bán qua Haravan App Store.
> **Lê Thanh Tùng · 2A202602499** · Cập nhật **09/10/2026** · Ngày 0 = **01/11/2026** (bắt đầu pilot 5 shop)

| Loại mô hình | North Star | Hiện tại | Mục tiêu |
|---|---|---|---|
| **B2B** — chủ shop SME vừa trả tiền vừa dùng; không chạm khách mua hàng của shop; Haravan chỉ là kênh | **TTFV** — giờ từ lúc cài app đến job hoàn thành thật đầu tiên | ⚪ chưa đo | **≤ 48 giờ** |

⚪ = chưa có số thật; số trong ngoặc là số mô hình Day 22. Nguồn: [MH] suy từ mô hình · [BM] benchmark (đã mở nguồn 09/10/2026) · [TB] tự đo baseline.

### 1 · Đèn báo sớm — Leading (hằng tuần)

| Đèn | Hiện | 🟢 | 🟡 | 🔴 | Nguồn · lý do | Báo trước cho |
|---|---|---|---|---|---|---|
| **TTFV** ⭐ | ⚪ | ≤ 48 giờ | 48 giờ – 7 ngày | > 7 ngày | [TB] Nỗi đau lặp lại mỗi đêm: 2 đêm chưa có job = lỗi cấu hình, 7 đêm = lỗi chắc chắn. Baseline từ 5 shop pilot, số đầu 15/11/2026 | Job/shop/tuần → churn |
| **Containment rate** | ⚪ (70% ước tính) | ≥ 70% | 51 – 70% | < 51% | [MH-A] Dưới 50,9% thì GM rơi khỏi mục tiêu 60%; 70% là mức mô hình đang giả định | Cost/Job → GM |
| **Cost/Job hoàn thành** · *đèn chi phí AI*, theo dõi cả trung bình và shop p95 | ⚪ ($0,058) | ≤ $0,067 | $0,067 – 0,080 | > $0,080 | [MH-B] $0,080 = GM 60% ở giá $0,20; $0,067 = giá bán còn gấp 3× cost | Gross margin |

### 2 · Đèn vận hành — Operating (hằng tuần / tháng)

| Đèn | Hiện | 🟢 | 🟡 | 🔴 | Nguồn · lý do | Báo trước cho |
|---|---|---|---|---|---|---|
| **Job hoàn thành / shop / tuần** (median) | ⚪ (162) | ≥ 121 | 41 – 121 | < 41 | [MH-C] ≥ 121 ⇔ ARPU ≥ $120 (KPI tháng 2–3); < 41 thì lãi gộp không bù overhead $40/shop | ARPU, churn |
| **Pilot → paid** | ⚪ | ≥ 50% (≥ 3/5) | 35 – 50% (2/5) | < 35% (≤ 1/5) | [BM] ICONIQ *State of GTM 2026*: POC/trial → paid ≈ 50% (2025 ≈ 36%), mở nguồn 09/10/2026 | Số shop trả phí, CAC payback |

### 3 · Đèn kết quả — Lagging (hằng tháng / quý)

| Đèn | Hiện | 🟢 | 🟡 | 🔴 | Nguồn · lý do |
|---|---|---|---|---|---|
| **Gross margin** (COGS, chưa trừ rev-share) | ⚪ (70,9%; ~42% nếu tính overhead) | ≥ 60% | 50 – 60% | < 50% | [MH-B] 60% là mục tiêu mô hình; < 50% ⇔ Cost/Job > $0,10. [BM] ICONIQ *State of AI 2026*: GM sản phẩm AI 53% (2026P), mở nguồn 09/10/2026 |
| **Logo churn / tháng** | ⚪ | ≤ 8,3% | 8,3 – 10% | > 10% | [MH-D] ≤ 8,3% ⇔ khách ở ≥ 12 tháng = CAC payback mục tiêu SMB |

### 4 · Năm luật quyết định (⏹ = luật dừng)

| # | NẾU | TRONG / TRÊN · VÀ | THÌ | KHÔNG THÌ |
|---|---|---|---|---|
| 1 ⏹ | TTFV > 7 ngày | ở ≥ 2 trong 3 shop mới nhất | **Dừng** cài shop mới; cắt phạm vi còn 1 kênh chat + nhóm câu hỏi tra đơn, đến khi 2 shop liên tiếp đạt ≤ 48 giờ | Không giảm phí nền $15, không mở thêm kênh/tính năng |
| 2 ⏹ | Containment < 51% | 2 tuần liên tiếp · mỗi tuần ≥ 150 hội thoại gắn nhãn | **Dừng** onboard và listing Haravan beta; gắn nhãn 50 ca escalate, sửa tối đa 3 nhóm lỗi KB/prompt trong 2 tuần | Không nhận xử lý escalate thay shop (GM ~7%); không đổi hết sang model đắt hơn khi chưa đo cost |
| 3 | Cost/Job > $0,080 | 2 tuần liên tiếp · ≥ 100 job/tuần | **Cắt** lượt tối đa/job còn 4, kiểm tra caching, thử model rẻ hơn trên 1 shop; **đàm phán lại** trần lượt với shop p95 | Không tăng giá toàn bộ shop; không cắt QA nội bộ 5% |
| 4 ⏹ | Median job/shop/tuần < 41 | 3 tuần liên tiếp · ≥ 3 shop đã go-live ≥ 14 ngày | **Dừng** mời shop mới; gọi từng shop dưới ngưỡng, đọc 20 hội thoại, nạp xong KB thiếu trong 7 ngày | Không bán thêm gói/kênh; không kiếm shop mới để bù số lượng |
| 5 ⏹ | Pilot → paid ≤ 1/5 | 5 shop pilot đầu, sau 14 ngày hết pilot | **Đóng băng** listing Haravan beta; phỏng vấn 5 shop trong 7 ngày, chỉ làm tiếp khi ≥ 2 shop nêu đúng 1 điều kiện sẽ trả | Không giảm $0,20 hay bỏ phí nền để kéo chuyển đổi |

### 5 · Cổng gác 90 ngày

| Ngày | Metric (1) | Ngưỡng qua cổng | Bằng chứng phải tồn tại | Nếu trượt |
|---|---|---|---|---|
| **30** · 01/12/2026 · *cổng học* | Containment đo thực | ≥ 55% trên ≥ 150 hội thoại gắn nhãn từ ≥ 3 shop (≈ GM 63%) | `eval_results.md` + sheet 150 hội thoại gắn nhãn | 41–55% và biết lỗi KB → **FIX** 1 lần · < 41% → **PIVOT** chỉ còn tra đơn |
| **60** · 31/12/2026 | TTFV | ≤ 48 giờ ở ≥ 3/5 shop pilot | `ttfv_log.csv` (mốc cài app, mốc job đầu tiên) | **FIX** 1 lần (onboarding) · trượt tiếp → **PIVOT** chỉ nhận shop đã có Zalo OA + danh mục sản phẩm sẵn |
| **90** · 30/01/2027 | Pilot → paid | ≥ 3/5 shop trả phí nền $15 | Hoá đơn 3 shop + `pilot_report.md` | 2/5 có lý do viết ra → **FIX** 1 lần · ≤ 1/5 → **KILL** |

**⛔ KILL CRITERIA:** Dừng hẳn hướng này nếu đến **30/01/2027** vẫn < 3/5 shop pilot trả phí sau đúng 1 lần FIX, **hoặc** containment đo thực < 41% (Cost/Job ≈ $0,10, GM ≈ 50%) ở 2 lần đo liên tiếp sau ngày 60.

### 6 · Chưa đo được

| Chưa có số | Cần gì để đo | Khi nào có số |
|---|---|---|
| Containment thật, tỷ lệ trả lời sai | Gắn nhãn tay 150 hội thoại của 5 shop pilot | 15/11/2026 |
| Cost/Job thật, Cost/Job shop p95 | Log token theo từng shop (chưa dựng) | 15/11/2026 |
| TTFV | Event 2 mốc trong log: cài app, job hoàn thành đầu tiên | 15/11/2026 |
| Churn, tập trung doanh thu, NRR | Khách trả phí ≥ 3 tháng (NRR cần ≥ 12 tháng, ngoài khung 90 ngày) | Churn sớm nhất 30/01/2027 |
| CAC thực, rev-share Haravan (20% đang là giả định) | Gặp partner; hiện **chưa** liên hệ | CAC sau pilot 15/12/2026 |
| Pain Moment 22:30–01:00 · Runway | Log giờ nhắn tin của 5 shop · runway chưa có trong hồ sơ Day 22 | 30/11/2026 · bổ sung trước cổng ngày 30 |
