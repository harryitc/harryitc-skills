# Experience-based and Combinatorial Techniques (Supplementary)

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Status:** Hướng dẫn bổ trợ; không thay thế kỹ thuật specification-based.

## Error Guessing

Dựa vào kinh nghiệm, lịch sử defect và các điểm yếu đã biết để đề xuất test ideas. Mỗi đề xuất nên ghi rõ lý do, chẳng hạn thao tác lặp, dữ liệu rỗng, session hết hạn, lọc kết quả trống hoặc phân quyền thiếu nhất quán. Nếu không có căn cứ trong requirement, coi đây là test idea cần xác nhận/exploratory, không bịa expected result.

## Exploratory Testing

Tester đồng thời học hệ thống, thiết kế và thực thi kiểm thử. Dùng charter/goal, ghi lại đường đi, dữ liệu, quan sát, thời lượng và câu hỏi còn mở. Exploratory không có nghĩa là bỏ qua ghi chép hoặc coi hành vi hiện tại là đúng yêu cầu.

## Pairwise / Combinatorial

Có thể dùng khi nhiều tham số tạo số tổ hợp lớn và tương tác cặp là mức bao phủ có thể chấp nhận cho mục tiêu cụ thể. Phải:

1. Liệt kê tham số và giá trị hợp lệ đã xác nhận.
2. Loại tổ hợp không hợp lệ chỉ khi có rule chứng minh.
3. Giữ lại tổ hợp rủi ro cao/đã biết là quan trọng dù kế hoạch pairwise không chọn chúng.
4. Ghi rõ đây là chiến lược giảm tổ hợp; không tuyên bố bao phủ tất cả tổ hợp.

## Phân biệt

- **Technique**: cách thiết kế/đề xuất test.
- **Test Type**: loại mục tiêu kiểm thử (ví dụ functional, usability, security-related behavior).
- **Execution Method**: manual hay automation.

Không nhập ba khái niệm này thành một trường.
