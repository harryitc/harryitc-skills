# Risk, Priority and Severity

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


## 1. Phân biệt

- **Risk:** khả năng xảy ra vấn đề kết hợp với tác động/hậu quả trong bối cảnh cụ thể.
- **Test Priority:** thứ tự/độ ưu tiên thực thi Test Case trong chiến lược kiểm thử.
- **Defect Severity:** mức tác động của defect đã phát hiện; đây là thuộc tính của defect, không phải Test Case.

Không dùng Priority và Severity thay thế nhau.

## 2. Cách ưu tiên ở mức Test Case

Cân nhắc các yếu tố:
- Tác động nếu hành vi lỗi (nghiệp vụ, dữ liệu, người dùng, tuân thủ).
- Khả năng xảy ra dựa trên độ phức tạp, thay đổi gần đây hoặc lịch sử defect.
- Phạm vi ảnh hưởng/số vai trò hoặc luồng phụ thuộc.
- Khả năng phát hiện lỗi sau khi triển khai.
- Mức quan trọng của luồng và cửa sổ thời gian kiểm thử.

Không tự gán điểm xác suất giả chính xác nếu không có dữ liệu. Nếu cần mô hình điểm, thống nhất thang đo và ngưỡng với QA Lead.

## 3. Gợi ý thang Priority (chỉ là mặc định có thể thay đổi)

- `P1 / High`: luồng cốt lõi, quyền/dữ liệu quan trọng, rủi ro lớn hoặc cần kiểm tra sớm.
- `P2 / Medium`: chức năng quan trọng nhưng có thể xếp sau P1.
- `P3 / Low`: rủi ro/thường xuyên sử dụng thấp hơn, hoặc tối ưu có thể trì hoãn.

Các mức này không phải tiêu chuẩn phổ quát. Nếu team đã có P0/P1/P2/P3 hoặc quy ước khác, dùng quy ước đó.

## 4. Quy tắc

- Priority phải có lý do ngắn nếu không hiển nhiên.
- Không suy ra priority chỉ từ test type.
- Test âm hoặc permission không mặc định low priority; có thể rất quan trọng.
- Đừng đặt tất cả case P1; nếu mọi thứ đều cao, priority không còn hỗ trợ quyết định.
- Severity được gán sau khi có defect evidence và impact, theo quy trình defect management.
