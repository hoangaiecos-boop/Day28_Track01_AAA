# Day 28 · Track 01 — AI Adoption & Change Management

**Dashboard Hành Động Cho Áp Dụng AI — v2** · Sản phẩm được chẩn đoán: **VLearn AI Tutor**

## 1. Thành viên

| Họ tên | MSSV | Phần phụ trách | Góp ý đã đưa cho nhóm bạn |
|---|---|---|---|
| Nguyễn Tấn Hoàng *(Leader)* | 2A202601198 | `<<CẦN ĐIỀN>>` | `<<CẦN ĐIỀN>>` |
| Nguyễn Minh Đức | 2A202601946 | `<<CẦN ĐIỀN>>` | `<<CẦN ĐIỀN>>` |

**Nhóm được phản biện:** `<<CẦN ĐIỀN — tên nhóm mà nhóm mình đã góp ý ở chặng 3>>`

## 2. Phạm vi

1 sản phẩm AI: **VLearn AI Tutor** — trợ giảng AI trả lời câu hỏi học viên trên corpus khoá AI20K.
1 nhóm người dùng chính: **học viên Track 1** đang làm lab hằng ngày (người dùng phụ: TA/trợ giảng).
3 quy trình: **W1** tự học ngoài giờ · **W2** tra cứu khi đang làm lab · **W3** hàng đợi TA.

## 3. Nguyên nhân gốc

**(1) Niềm tin vỡ ngay tại lớp trích dẫn** — câu trả lời không kiểm chứng được tại chỗ nên người dùng phải làm lại việc để kiểm. **(2) AI nằm ngoài quy trình chính thức** — không có bàn giao AI→TA, không có owner chất lượng, lỗi rơi vào im lặng.
**Framework:** Gartner-Lite (Direction đạt, Readiness + Absorption thiếu) · Mollick (tutor đang tự động ở ô lẽ ra phải người kiểm) · ADKAR (nghẽn ở Desire và Ability, không phải Knowledge).
**Bằng chứng:** đo nội bộ — vòng eval v1 20 scenario của chính sản phẩm (quote nguyên văn 39%, groundedness nhãn người 46%, judge TNR 100%/TPR 67%, latency p50 25,1s, gate HOLD); 3 case tham khảo Morgan Stanley / DWP-GDS / Klarna; mô hình đơn vị Day 25 (hoà vốn containment 20,1%).

## 4. Cách làm mới

**Nguồn kiểm chứng:** trích dẫn bấm mở đúng section + hiển thị ngày cập nhật trong mọi câu trả lời.
**Người chịu trách nhiệm:** TA trực chịu trách nhiệm câu trả lời; Content owner chịu trách nhiệm corpus, cập nhật 2 tuần/lần.
**Xử lý khi AI không chắc:** tutor từ chối và chuyển giao — tự động tạo ticket cho TA kèm transcript, không đoán.

## 5. Chỉ số

| Loại | Chỉ số | Baseline | Target | Nguồn | Owner |
|---|---|---|---|---|---|
| Product | Containment rate 24h | chưa đo (đo tuần 1) | ≥25% D30 · ≥39% D90 (hoà vốn 20,1%) | Log hội thoại ⋈ ticket TA | Product owner |
| Product | Tỷ lệ câu trả lời kiểm chứng được | 39% (7/18, eval v1) | ≥95% | `code_checks.py` nightly / 100 log thật | Eval owner |
| Workflow | W2 · Thời gian tới câu trả lời dùng được (p80) | đo tuần 1 | ≤2 phút cho 80% câu | Log tác vụ (hỏi → bấm "Đủ rõ") | TA lead |
| Workflow | W3 · Đóng escalation trong SLA & đưa lại corpus | 0% (chưa có quy trình) | 90% SLA 4h · ≥60% sinh cập nhật corpus | Ticket tracker + changelog corpus | TA trực + Content owner |

Bộ đầy đủ 8 chỉ số kèm cột **hành động khi chỉ số xấu**: xem `dashboard/dashboard_hanh_dong_v2.xlsx`.

## 6. Quyết định

**SỬA — chưa mở rộng.** Lý do: cổng chất lượng đang HOLD (trích dẫn 39%, groundedness 46%) và Gartner-Lite cho thấy readiness lẫn absorption đều thiếu, nên tăng lượt dùng lúc này chỉ làm hỏng niềm tin nhanh hơn.
**Hai thay đổi so với v1:** (1) bỏ chỉ số activity ("số câu hỏi/tuần", "% học viên đã dùng"), thay bằng containment rate 24h và thời gian tới câu trả lời dùng được; (2) thu hẹp từ rollout cả cohort xuống pilot 1 lớp × 3 quy trình, cổng quyết định dời sang ngày 60, thêm cơ chế hạ cấp an toàn. *(Thay đổi thứ ba: thêm quy trình W3 hàng đợi TA + Content owner để đóng vòng học lại.)*

---

## Cấu trúc repo

```
├── README.md
├── dashboard/
│   ├── dashboard_hanh_dong_v2.xlsx   ← bản v2 sau kiểm tra chéo
│   ├── dashboard_hanh_dong_v2.html   ← bản web tương tác (bổ sung)
│   └── dashboard_hanh_dong_v2.md
├── memo/
│   └── memo_quyet_dinh.md            ← 5 phần
└── v1/
    └── dashboard_hanh_dong_v1.xlsx   ← bản trước phản biện, để đối chiếu
```
