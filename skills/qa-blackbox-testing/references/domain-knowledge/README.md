# Project Domain Knowledge

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


Thư mục này dành cho kiến thức đã được xác nhận riêng của từng sản phẩm/dự án. Bản toolkit hiện tại không chứa business rule của hệ thống cụ thể.

## Cách khởi tạo

1. Sao chép `project-rule-register-template.md` thành file dự án (ví dụ `project-a-rule-register.md`).
2. Đính kèm nguồn, người xác nhận và ngày xác nhận.
3. Giữ trạng thái `Draft` cho đến khi người có thẩm quyền review.
4. Tạo các file riêng cho role-permission matrix, workflow/state table, glossary và dữ liệu mẫu nếu cần.
5. Bảo vệ thông tin nội bộ; chỉ đưa dữ liệu tối thiểu cần thiết vào prompt/agent.

## Quy tắc cho AI

- Không suy diễn business rule chỉ từ tên role hoặc nhãn UI.
- Không dùng hành vi quan sát hiện tại làm bằng chứng duy nhất cho hành vi đúng.
- Khi hai tài liệu mâu thuẫn, liệt kê cả hai nguồn và đề nghị phân xử.
- Tài liệu `Draft` chỉ là đầu vào tham khảo, không phải policy đã phê duyệt.
