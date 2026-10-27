# Use Case Testing

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Mục tiêu:** Kiểm tra một actor đạt mục tiêu qua luồng tương tác với hệ thống, bao gồm luồng chính, luồng thay thế và xử lý ngoại lệ đã được đặc tả.

## Khi nên dùng

- Chức năng có nhiều bước liên tiếp.
- Cần kiểm tra kết quả nghiệp vụ cuối luồng, không chỉ từng field riêng.
- Vai trò, precondition hoặc trạng thái ban đầu làm thay đổi luồng.

## Khung phân tích

- **Actor/role:** ai thực hiện?
- **Goal:** mục tiêu cần đạt?
- **Preconditions:** điều gì phải đúng trước khi bắt đầu?
- **Trigger:** sự kiện bắt đầu?
- **Main flow:** các bước thành công?
- **Alternative flows:** nhánh khác khi điều kiện khác nhau?
- **Exception flows:** lỗi/hệ thống từ chối nào đã được mô tả?
- **Postconditions:** trạng thái/dữ liệu/kết quả sau luồng?

## Cách chuyển thành Test Case

- Mỗi luồng/nhánh có ý nghĩa trở thành scenario.
- Steps đi theo trình tự đủ tái lập.
- Expected Result có thể xuất hiện tại bước kiểm tra và ở kết quả cuối.
- Setup dữ liệu, role và trạng thái phải rõ.
- Nếu một scenario quá rộng và xác minh nhiều mục tiêu độc lập, tách case; nếu các bước chỉ là một luồng business cần kiểm tra từ đầu đến cuối, giữ chúng cùng case.

## Anti-patterns

- Chỉ kiểm tra đường thành công.
- Tạo một case duy nhất cho mọi nhánh khiến kết quả khó định vị.
- Tạo từng case cho mỗi bước đơn lẻ làm mất kiểm tra tính liên tục của workflow.
- Tự thêm luồng lỗi chưa có trong requirement mà không đánh dấu là exploratory idea.
