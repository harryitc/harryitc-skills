# Technique Selection Guide

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Purpose:** Giúp AI và tester chọn kỹ thuật Black-box phù hợp với đặc tính của requirement. **Status:** Draft for pilot.

## 1. Nguyên tắc

Bắt đầu từ câu hỏi “điều gì có thể sai trong hành vi được đặc tả?” rồi chọn kỹ thuật giúp bao phủ điều kiện/giá trị/trạng thái với tập case hợp lý. Kỹ thuật có thể kết hợp; không có một kỹ thuật duy nhất phù hợp mọi chức năng.

## 2. Bảng lựa chọn nhanh

| Dấu hiệu trong Test Basis | Technique ưu tiên | Cần xem thêm |
|---|---|---|
| Input có tập giá trị, định dạng hoặc nhóm đầu vào | Equivalence Partitioning | BVA nếu có giới hạn định lượng/thứ tự |
| Requirement nêu min/max, giới hạn ký tự, khoảng ngày, số lượng | Boundary Value Analysis | Xác nhận inclusivity và kiểu dữ liệu |
| Kết quả phụ thuộc nhiều điều kiện đồng thời | Decision Table | Quy tắc ưu tiên, điều kiện không quan tâm, tổ hợp không hợp lệ |
| Đối tượng có trạng thái và sự kiện làm đổi trạng thái | State Transition | Trạng thái đầu, sự kiện hợp lệ, guard và trạng thái đích |
| Người dùng đạt mục tiêu qua nhiều bước/nhánh | Use Case Testing | Alternate flow, exception flow và role |
| Nhiều tính năng/rule với hậu quả không đồng đều | Risk-based prioritization | Tác động, xác suất/khả năng xảy ra, độ khó phát hiện |
| Có rủi ro lỗi thường gặp hoặc thông tin chưa đầy đủ | Error guessing / exploratory | Ghi rõ căn cứ và không tự tạo expected result |
| Nhiều tham số cấu hình với số tổ hợp lớn | Pairwise/combinatorial bổ trợ | Chỉ dùng khi tương tác cặp là mục tiêu hợp lý; không thay thế tổ hợp quan trọng đã biết |

## 3. Quy trình chọn

1. Trích xuất rule, input, output, điều kiện, trạng thái và actor.
2. Xác định coverage item nào cần kiểm tra.
3. Chọn technique có quan hệ trực tiếp với coverage item.
4. Chọn dữ liệu/case đại diện.
5. Kiểm tra xem technique đã bỏ qua tương tác quan trọng nào chưa.
6. Ghi technique khi nó giải thích quyết định thiết kế; không cần gắn nhãn cho mọi case.

## 4. Lưu ý chất lượng

- Không áp dụng BVA khi biên hoặc quy tắc bao gồm biên chưa được xác nhận.
- Không lập decision table từ các điều kiện do AI tự suy diễn.
- Không tạo state transition “không hợp lệ” nếu chưa biết hệ thống phải từ chối, cảnh báo hay cho phép chuyển trạng thái.
- Không tuyên bố pairwise bao phủ toàn bộ tổ hợp.
- Technique là cách chọn test; Test Type là mục tiêu/phân loại kiểm thử. Hai trường này không đồng nghĩa.
