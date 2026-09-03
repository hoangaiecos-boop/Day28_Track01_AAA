# Dashboard Hành Động Cho Áp Dụng AI — v2

**Sản phẩm:** VLearn AI Tutor
**Khoá:** AI20K · Track 1 · Day 28 — AI Adoption & Change Management
**Bản:** v2 (sau kiểm tra chéo) · **Quyết định:** SỬA — chưa mở rộng

**Nhóm thực hiện:**

| # | Họ tên | MSSV | Vai trò |
|---|---|---|---|
| 1 | Nguyễn Tấn Hoàng | 2A202601198 | Leader |
| 2 | Nguyễn Minh Đức | 2A202601946 | Thành viên |

---

## 0. Trạng thái — bốn con số quyết định bản v2

| Chỉ số | Hiện tại | Ngưỡng | Trạng thái |
|---|---:|---:|---|
| Trích dẫn nguyên văn (quote_verbatim) | **39%** (7/18) | 95% | Dưới ngưỡng |
| Groundedness (nhãn người) | **46%** (6/13) | 90% | Dưới ngưỡng |
| Containment rate 24h | chưa đo | hoà vốn 20,1% | Phải đo tuần 1 |
| Critical-regression | **0 fail** (2/2 pass) | 0 fail | Đạt |

**Mức độ ứng dụng hiện tại:** Usage → Pilot → **Deployment (đang ở đây)** → Adoption → Normalization.
Tutor đã sẵn sàng và ai cũng truy cập được, nhưng công việc, trách nhiệm và cách kiểm soát đều chưa đổi — nên mọi con số về lượt dùng đều không nói lên điều gì.

---

## 1. Phạm vi (Bước 1)

- **Sản phẩm:** VLearn AI Tutor — trợ giảng AI trả lời câu hỏi học viên, chỉ trên corpus khoá AI20K (slide + tài liệu tham chiếu), trả về JSON `scope · answer · sources · 3 followup`.
- **Người dùng chính:** học viên Track 1 đang làm lab hằng ngày. **Phụ:** TA/trợ giảng đang gánh hàng đợi câu hỏi trong nhóm chat.
- **Ba quy trình trong phạm vi:**
  - **W1 — Tự học ngoài giờ:** hỏi khái niệm, ôn trước checkpoint.
  - **W2 — Tra cứu khi đang làm lab:** định vị đúng phần nội dung để đi tiếp. *(Quy trình giá trị cao nhất, cũng là nơi tutor vắng mặt.)*
  - **W3 — Hàng đợi TA:** nhận câu tutor không chắc, trả lời, rồi đưa kiến thức đó trở lại corpus.
- **Vấn đề quan sát/đo được:** học viên hỏi vài lần rồi quay lại mở slide tự tìm hoặc hỏi TA trong nhóm chat. Quan sát được: câu hỏi vẫn dồn về TA. Đo được: chất lượng trích dẫn của tutor mới 39%.

---

## 2. Chẩn đoán (Bước 2)

### 2.1 Gartner-Lite — khả năng hấp thụ

| Thành phần | Kết luận | Căn cứ |
|---|---|---|
| **Direction** | ĐẠT | Mục tiêu rõ: giảm thời gian tra cứu, giảm tải TA. Đã có mô hình đơn vị ($0,1238/câu được kiểm chứng). |
| **Readiness** | THIẾU | Corpus chưa có người phụ trách và lịch cập nhật; phạm vi tài liệu chưa chốt nên tutor trả lời cả câu corpus không có căn cứ. |
| **Absorption** | THIẾU | Không ai chịu trách nhiệm chất lượng câu trả lời; không có nút báo sai; không có vòng học lại từ lỗi. |

### 2.2 Mollick — chia việc người / AI

| Ô | Nội dung |
|---|---|
| **AI làm** | Tìm & trích: định vị section, trả trích đoạn nguyên văn kèm ngày cập nhật. Rủi ro thấp, referent kiểm được bằng code. |
| **AI làm, người kiểm** | Tổng hợp nhiều nguồn; câu "đòi con số" → phải qua TA duyệt. |
| **Người giữ quyền** | Chấm bài, đánh giá năng lực, câu ngoài corpus, quyết định ship. |
| **LỆCH hiện tại** | Tutor đang **tự động** ở đúng ô lẽ ra phải "người kiểm": gặp câu không có căn cứ so sánh trong corpus, nó vẫn trả lời thay vì từ chối. |

### 2.3 ADKAR — người dùng kẹt ở đâu

| Giai đoạn | Trạng thái | Nội dung |
|---|---|---|
| Awareness | Cần làm | Học viên không biết tutor chỉ phủ corpus khoá → hỏi ra ngoài phạm vi rồi kết luận "nó dở". |
| **Desire** | **NGHẼN** | Không tin câu trả lời vì trích dẫn bị ghép "…", phải tự mở slide kiểm lại — mất luôn phần thời gian đáng lẽ tiết kiệm. |
| Knowledge | Cần làm | Chưa biết cách hỏi; câu kiểu "đoạn này giải thích lại" thường trượt. |
| **Ability** | **NGHẼN** | Tutor không nằm ở nơi học viên đang làm việc (trang lab), phải đổi tab mới dùng được. |
| Reinforcement | Cần làm | Không có nút báo sai, không ai theo dõi hành vi mới. |

> Nghẽn ở **Desire** và **Ability**, không phải ở Knowledge → thêm buổi đào tạo sẽ không giải quyết được gì.

### 2.4 Hai nguyên nhân gốc

1. **Niềm tin vỡ ngay tại lớp trích dẫn.** Câu trả lời không kiểm chứng được tại chỗ: 39% quote nguyên văn, groundedness 46%. Người dùng buộc phải làm lại việc để kiểm — nên quay về cách cũ. *Đây là nguyên nhân, không phải "học viên lười".*
2. **AI nằm ngoài quy trình chính thức.** Không có bước bàn giao AI → TA, không có owner cho chất lượng câu trả lời, không có đường để một câu sai được phát hiện và học lại. Lỗi rơi vào im lặng nên hệ thống không bao giờ tốt lên.

*Triệu chứng (không phải nguyên nhân): "ít lượt dùng", "học viên không chịu dùng".*

### 2.5 Bằng chứng

- **E1 — Đo nội bộ, vòng eval v1 (20 scenario).** quote nguyên văn 7/18 (39%) · schema 18/20 (90%) · groundedness nhãn người 6/13 kết luận được (46%) · judge TNR 100% / TPR 67%, agreement 89% · latency p50 25,1s (max 52,5s) · chi phí $0,108/20 câu. Kết luận gate: **CHƯA SHIP**. Dẫn: `evidence/results-v1.jsonl`, `code-checks-v1.txt`, `calibration-v1.txt` (Lab21).
- **E2 — Case tham khảo.** Morgan Stanley: chốt độ tin cậy trước khi mở rộng. DWP/GDS: cách đo quyết định độ tin cậy — ước tính thận trọng có nhóm so sánh đáng tin hơn số tự khai. Klarna: khối lượng tự động hoá không thay thế được chất lượng và quy trình.
- **E3 — Mô hình đơn vị (Day 25).** Chi phí $0,1238/câu trả lời được kiểm chứng; giá đề xuất $0,60; hoà vốn khi containment đạt **20,1%**, kịch bản thận trọng 39%. → Việc áp dụng chỉ có giá trị kinh tế khi containment thật vượt 20,1%; đó là ngưỡng đặt vào dashboard.

---

## 3. Thiết kế lại quy trình W2 (Bước 3a)

| | AS-IS (hôm nay) | TO-BE (sau thiết kế lại) |
|---|---|---|
| 1 | Học viên vướng ở một bước trong lab | Hỏi tutor **ngay trong trang lab**, không đổi tab |
| 2 | Mở lại slide/PDF, Ctrl+F mò từ khoá | Tutor trả lời kèm **trích dẫn bấm mở đúng section + ngày cập nhật** |
| 3 | Không thấy → hỏi trong nhóm chat | Học viên bấm **"Đủ rõ"** hoặc **"Chưa đủ / Báo sai"** |
| 4 | Chờ TA rảnh (hàng giờ), lab đứng lại | Báo sai / tutor tự nhận không chắc → **ticket cho TA trực** kèm transcript |
| 5 | TA trả lời thủ công; câu trả lời trôi mất trong chat | TA trả lời trong SLA 4h; câu trả lời được **đưa lại corpus** |
| 6 | Tutor tồn tại song song, dùng vài lần rồi bỏ | Hằng tuần QA mẫu 20% số câu judge đánh fail |

**Ba thay đổi bắt buộc:** ① nguồn kiểm chứng (trích dẫn mở được + ngày cập nhật); ② người chịu trách nhiệm (TA trực cho câu trả lời, Content owner cho corpus); ③ cách xử lý khi AI không chắc (chuyển giao, không đoán).

---

## 4. Lộ trình 30–60–90 (Bước 3b) — ba cổng quyết định

**Ngày 0–30 · Chứng minh vấn đề**
- Khoá pilot: 1 lớp Track 1, ba quy trình W1–W3.
- Chỉ định **Content owner** cho corpus + lịch cập nhật 2 tuần/lần.
- Nhúng tutor vào trang lab; bật nút "Đủ rõ / Báo sai".
- Ghi mốc ban đầu tuần 1: containment, thời gian tới câu trả lời, tỷ lệ quay lại cách cũ.
- **Qua cổng khi:** có baseline thật cho cả ba chỉ số hành vi (không phải ước lượng) và corpus đã có owner tên cụ thể.

**Ngày 31–60 · Chứng minh chất lượng**
- Bật trích dẫn bấm-mở-được; cấm ghép quote "…" trong system prompt.
- Chạy judge nightly trên 50 log thật + audit tay 20% câu fail.
- Mở hàng đợi TA với SLA 4h; mỗi câu escalate phải sinh 1 cập nhật corpus.
- Thêm 2 ví dụ "pass sát ranh" vào judge prompt để nâng TPR 67%.
- **Qua cổng khi:** trích dẫn nguyên văn ≥95%, groundedness ≥90%, containment ≥20,1%, 0 fail critical-regression. Thiếu bất kỳ điều kiện nào → không mở rộng.

**Ngày 61–90 · Quyết định mở rộng**
- So kết quả với mục tiêu; đối chiếu chi phí thực với $0,1238/câu.
- Chốt owner vận hành thường trực (không còn là người làm pilot).
- Kiểm governance: phạm vi corpus, quyền truy cập, thời gian lưu log.
- Ra quyết định: mở rộng / sửa tiếp / dừng.
- **Điều kiện dừng:** containment <20,1% ở ngày 90 → thu hẹp tutor về đúng vai "công cụ tra cứu có trích dẫn", bỏ vai trả lời tổng hợp.

---

## 5. Dashboard chỉ số (Bước 4)

### Mức sản phẩm

| Chỉ số | Mốc đầu | Mục tiêu | Nguồn dữ liệu | Phụ trách | Khi chỉ số xấu |
|---|---|---|---|---|---|
| **Containment rate 24h** — % câu hỏi được tutor giải quyết trọn, không phát sinh ticket TA trong 24h | chưa đo (đo tuần 1) | ≥25% (D30) · ≥39% (D90) · hoà vốn 20,1% | Log hội thoại ⋈ ticket TA, join theo học viên trong cửa sổ 24h | Product owner | <20,1% tại cổng ngày 60 → không mở rộng. Đọc 20 transcript escalate gần nhất, phân loại nguyên nhân trước khi đổi bất cứ thứ gì. |
| **Tỷ lệ câu trả lời kiểm chứng được** — citation tồn tại + quote nguyên văn liền mạch | **39%** (7/18, eval v1) | ≥95% | `code_checks.py` nightly trên 100 log thật | Eval owner | <90% → tắt chế độ trả lời tổng hợp, hạ cấp an toàn về "trích đoạn + link nguồn", thông báo cho lớp. |
| **Chi phí / câu trả lời được kiểm chứng** — guardrail kinh tế khi mở rộng | $0,1238 (mô hình Day 25) | ≤$0,15 | Log token gateway + hoá đơn | Product owner | >$0,20 → cắt vòng tool-calling lặp, cache câu hỏi trùng, xem lại lựa chọn model. |

### Mức quy trình

| Chỉ số | Mốc đầu | Mục tiêu | Nguồn dữ liệu | Phụ trách | Khi chỉ số xấu |
|---|---|---|---|---|---|
| **W2 · Thời gian tới câu trả lời dùng được (p80)** — từ lúc vướng đến khi học viên bấm "Đủ rõ" | đo tuần 1 (tutor p50 25,1s + tự kiểm slide 3–5 phút) | ≤2 phút cho 80% câu | Log tác vụ: timestamp hỏi → timestamp xác nhận | Chủ quy trình (TA lead) | p80 >5 phút → giảm số vòng tool-call của tutor và kiểm lại vị trí nhúng trong trang lab. |
| **W1 · Tỷ lệ quay lại cách cũ** — % câu hỏi cùng nội dung được đăng lại vào nhóm chat trong 24h sau khi đã hỏi tutor | đo tuần 1 | ≤20% (D60) | Ticket + chat log gắn nhãn theo chủ đề | TA lead | >35% → phỏng vấn 5 học viên, xác định đang nghẽn ở Desire hay Ability rồi sửa đúng chỗ đó. Không mặc định thêm buổi đào tạo. |
| **W3 · Đóng escalation trong SLA & đưa lại corpus** — % ticket đóng ≤4h giờ hành chính · % câu escalate sinh 1 cập nhật corpus | 0% (chưa có quy trình) | 90% đóng SLA · ≥60% sinh cập nhật | Ticket tracker + changelog corpus | TA trực + Content owner | <70% → thu hẹp phạm vi pilot hoặc tăng người trực, hoãn cổng ngày 60. Đây là vòng học lại của hệ thống; nó hỏng thì chất lượng không tự tốt lên. |

### Chất lượng & rủi ro

| Chỉ số | Mốc đầu | Mục tiêu | Nguồn dữ liệu | Phụ trách | Khi chỉ số xấu |
|---|---|---|---|---|---|
| **Groundedness pass rate** — judge tự động gắn cờ + người audit 20% câu fail | **46%** (nhãn người, eval v1) | ≥90% câu in_scope | `judge.py` nightly trên 50 log thật; judge đã calibrate (TNR 100%) | Eval owner | <80% → HOLD toàn bộ việc mở rộng, quay lại sửa system prompt và retrieval trước khi bàn tiếp về lượt dùng. |
| **Critical-regression** — xin đáp án bài chấm điểm · prompt injection lộ hạ tầng | 0 fail (2/2 pass, eval v1) | 0 fail tuyệt đối | Bộ regression chạy mỗi lần đổi prompt hoặc model | AI owner | 1 fail → rollback ngay và chặn ship, bất kể các chỉ số khác đẹp đến đâu. |

---

## 6. Kiểm tra chéo — ba góp ý đã sửa vào v2

> Cần điền tên nhóm/người phản biện trước khi nộp.

| # | Góp ý về bản v1 | Thay đổi trong v2 |
|---|---|---|
| 01 | V1 lấy "số câu hỏi/tuần" và "% học viên đã từng dùng tutor" làm chỉ số chính. Đó là activity, không phải giá trị — hai số này tăng vẫn không chứng minh được công việc đã đổi. | Thay bằng **containment rate 24h** (giá trị) và **thời gian tới câu trả lời dùng được** (năng suất), cả hai join được từ log tác vụ và ticket. Gắn thẳng ngưỡng hoà vốn 20,1% để chỉ số có nghĩa kinh tế. |
| 02 | V1 đặt mục tiêu groundedness 90% ngay từ ngày 30 và rollout cả cohort. Readiness chưa đạt — corpus chưa có người phụ trách — mở rộng lúc này sẽ khoá luôn niềm tin của học viên. | Thu hẹp còn **pilot 1 lớp × 3 quy trình trong 30 ngày**, cổng quyết định dời sang ngày 60. Thêm **cơ chế hạ cấp an toàn**: khi tỷ lệ kiểm chứng <90%, tutor chỉ trả trích đoạn + link. |
| 03 | V1 có chỉ số chất lượng nhưng không có ai đứng tên corpus, và không có đường đi cho câu trả lời sai. Thiếu vòng học lại thì chỉ số chất lượng chỉ để báo cáo. | Thêm quy trình **W3 — hàng đợi TA** thành một dòng có chỉ số riêng (SLA 4h, ≥60% escalate sinh cập nhật corpus). Chỉ định **Content owner** + lịch cập nhật 2 tuần/lần, hiển thị **ngày cập nhật** trong mọi câu trả lời. |

---

## 7. Memo quyết định

Xem [NguyenTanHoang_Day28_memo.md](NguyenTanHoang_Day28_memo.md).
