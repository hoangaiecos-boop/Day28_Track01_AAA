# Memo quyết định — VLearn AI Tutor

**AI20K · Track 1 · Day 28** · Nguyễn Tấn Hoàng — 2A202601198 · bản v2 sau kiểm tra chéo

## 1. Vấn đề và nguyên nhân gốc

VLearn AI Tutor đã triển khai nhưng học viên vẫn quay lại mở slide và hỏi TA. "Ít dùng" chỉ là triệu chứng. Hai nguyên nhân gốc:

1. **Niềm tin vỡ tại lớp trích dẫn** — chỉ 39% quote nguyên văn, groundedness 46%, nên người dùng phải làm lại việc để kiểm.
2. **AI nằm ngoài quy trình chính thức** — không có bàn giao AI → TA, không có owner chất lượng, lỗi rơi vào im lặng.

## 2. Framework đã dùng và bằng chứng

- **Gartner-Lite:** Direction đạt; Readiness và Absorption đều thiếu (corpus không có owner; không có vòng phản hồi lỗi).
- **Mollick:** tutor đang tự động ở đúng ô lẽ ra phải có người kiểm — gặp câu corpus không có căn cứ, nó vẫn trả lời.
- **ADKAR:** nghẽn ở **Desire** (không tin vì không thấy nguồn) và **Ability** (tutor không ở nơi làm việc), không phải Knowledge → thêm buổi đào tạo không giải quyết được gì.
- **Bằng chứng:** vòng eval v1 20 scenario (số liệu đã đo: quote 39%, groundedness 46%, judge TNR 100%/TPR 67%, latency p50 25,1s, gate HOLD); ba case Morgan Stanley / DWP-GDS / Klarna; mô hình đơn vị Day 25 (hoà vốn containment 20,1%).

## 3. Thay đổi sau phản biện

1. Bỏ chỉ số activity, thay bằng containment rate 24h và thời gian tới câu trả lời dùng được.
2. Thu hẹp từ rollout cả cohort xuống pilot 1 lớp; thêm cơ chế hạ cấp an toàn khi tỷ lệ kiểm chứng <90%.
3. Thêm quy trình hàng đợi TA cùng Content owner để đóng vòng học lại.

## 4. Quyết định

**SỬA — chưa mở rộng.** Pilot 1 lớp × 3 quy trình trong 30 ngày, cổng quyết định ở ngày 60. Không tăng phạm vi người dùng cho tới khi tỷ lệ kiểm chứng ≥95% và groundedness ≥90%.

## 5. Lý do, bước tiếp theo và người phụ trách

**Lý do:** cổng chất lượng đang HOLD và tổ chức chưa sẵn sàng hấp thụ; mở rộng lúc này làm hỏng niềm tin nhanh hơn là tạo giá trị.

**Ba bước tiếp theo trong 30 ngày:**

| Việc | Người phụ trách | Hạn |
|---|---|---|
| Chỉ định Content owner + lịch cập nhật corpus 2 tuần/lần | Product owner | Tuần 1 |
| Nhúng tutor vào trang lab, bật trích dẫn bấm-mở-được và nút báo sai | AI owner | Tuần 1–2 |
| Ghi mốc ban đầu: containment, thời gian tới câu trả lời, tỷ lệ quay lại cách cũ | TA lead | Tuần 1 |

**Điều kiện dừng:** containment <20,1% ở ngày 90 → thu hẹp tutor về đúng vai công cụ tra cứu có trích dẫn, bỏ vai trả lời tổng hợp.
