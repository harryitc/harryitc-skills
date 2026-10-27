# Evaluation Guide — Black-box Toolkit

## Mục tiêu

Đo chất lượng của Skill/Reference qua tình huống chuẩn, không chỉ xem output có nhiều Test Case hay không. Bộ eval hiện là v0.1.0, cần được bổ sung từ các chức năng thực tế đã được QA Leader duyệt.

## Cách chạy eval thủ công

1. Chọn case trong `blackbox-eval-cases.json`.
2. Đưa `input` cùng System Prompt và Generation Skill vào agent.
3. Lưu output nguyên bản, kèm phiên bản model/skill/reference/date.
4. Đối chiếu `expected_coverage_checkpoints`, `forbidden_assumptions` và `acceptance_criteria`.
5. Chạy Review Skill trên output và đánh giá xem nó phát hiện đúng điểm thiếu không.
6. Ghi điểm và finding vào bảng kết quả ngoài (CSV/issue tracker); không sửa eval “để output mới trông tốt hơn” nếu chưa có căn cứ.

## Thang đánh giá đề xuất

Chấm từng chiều 0–2:
- **0 — Fail:** bỏ sót hoặc làm sai trọng yếu.
- **1 — Partial:** có một phần nhưng thiếu coverage/chi tiết đáng kể.
- **2 — Pass:** đáp ứng tiêu chí với căn cứ rõ.

Các chiều: requirement fidelity, coverage, expected-result quality, executability, traceability, ambiguity handling, duplicate control. Tổng điểm có thể hữu ích để so sánh phiên bản, nhưng không thay thế blocker gates.

## Blocker gates

Bất kể điểm tổng, không đạt nếu AI:
- Tự tạo expected result nghiệp vụ không có căn cứ và trình bày như đã xác nhận.
- Bỏ sót một điều kiện trọng yếu được nêu rõ trong input.
- Khẳng định đã thực thi/pass hoặc đã phê duyệt khi chưa có bằng chứng.
- Làm lộ secrets/PII không cần thiết từ input.

## Theo dõi thay đổi

Với mỗi lần sửa Reference, ghi:
- File thay đổi và lý do.
- Evals đã chạy.
- Regression mới phát hiện.
- Quyết định giữ/rollback và người review.

Không coi một bộ eval nhỏ là chứng minh thống kê rằng Skill tốt trên mọi dự án. Tăng dần số case bằng tình huống thật đã được làm sạch thông tin nhạy cảm.
