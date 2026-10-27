# Test Case Quality Standard

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Purpose:** Chuẩn tối thiểu để một Test Case có thể được hiểu, thực thi, xác minh, truy vết và bảo trì. **Status:** Draft for pilot; QA Leader cần điều chỉnh theo template thực tế.

## 1. Tiêu chí bắt buộc

### A. Căn cứ và traceability
- Có requirement/business rule/coverage item tham chiếu nếu đã có nguồn.
- Nếu chưa có nguồn, gắn nhãn `Needs Clarification` hoặc `Exploratory Idea`.
- Không trình bày giả định như yêu cầu đã được phê duyệt.

### B. Title
- Nêu hành vi/điều kiện cần xác minh.
- Tránh tên chung như `Test chức năng`, `Kiểm tra dữ liệu`.
- Không nhồi toàn bộ steps vào title.

### C. Preconditions
- Chỉ ghi điều kiện cần để case chạy đúng.
- Bao gồm role, trạng thái ban đầu và dữ liệu phụ thuộc khi cần.
- Không phụ thuộc setup không được mô tả hoặc trạng thái khó tái lập.

### D. Test Steps
- Đánh số và sắp theo trình tự.
- Mỗi bước có hành động cụ thể, actor/context rõ.
- Tránh chỉ dẫn mơ hồ như “xử lý như bình thường”, “kiểm tra hợp lệ”.
- Nếu cần quan sát tại từng bước, nêu rõ checkpoint.

### E. Test Data
- Nêu giá trị cụ thể, dataset/reference hoặc cách tạo dữ liệu.
- Ghi chính xác kiểu/format, khoảng giá trị và điều kiện liên quan.
- Không sử dụng dữ liệu thật nhạy cảm nếu không cần thiết; ưu tiên test data giả lập.

### F. Expected Result
- Có thể quan sát hoặc xác minh được qua UI, API contract, phản hồi hoặc nguồn dữ liệu được phép.
- Phù hợp với requirement/đặc tả.
- Nêu giá trị/trạng thái/kết quả cần thấy khi chúng quan trọng.
- Không dùng câu chung như “hệ thống hoạt động chính xác”, “không có lỗi” khi chưa xác định điều gì là đúng.
- Không ghi thông báo chính xác nếu chưa có căn cứ về nội dung thông báo.

### G. Granularity và independence
- Mỗi case có một mục tiêu kiểm chứng chính.
- Có thể có nhiều bước và checkpoint nếu chúng cùng phục vụ một luồng end-to-end.
- Tránh ghép nhiều mục tiêu độc lập vào một case làm khó xác định nguyên nhân fail.
- Giảm phụ thuộc thứ tự giữa case; nếu phụ thuộc là cần thiết, ghi rõ setup/cleanup.

## 2. Các trường khuyến nghị

`Test Case ID`, `Module`, `Function`, `Requirement Reference`, `Test Scenario`, `Test Type`, `Design Technique`, `Title`, `Preconditions`, `Test Steps`, `Test Data`, `Expected Result`, `Priority`, `Review Status`, `Notes`.

Nếu test management tool đã định nghĩa trường khác, mapping theo schema hiện hành của team thay vì tạo schema cạnh tranh.

## 3. Quy ước ID và trạng thái

- ID phải duy nhất và ổn định; không tái sử dụng ID case đã loại bỏ.
- Nếu chưa có quy ước ID dự án, có thể dùng mã tạm có prefix như `BB-TC-001`, nhưng không tự khẳng định đó là chuẩn công ty.
- Review Status và Execution Status là hai vòng đời riêng.
- Gợi ý Review Status: `Draft`, `Needs Review`, `Approved`, `Rejected`.
- Gợi ý Execution Status: `Not Run`, `Pass`, `Fail`, `Blocked`, `Not Applicable`.
- AI có thể đề xuất `Ready for QA Lead Review`, nhưng không được tự set `Approved`.

## 4. Chất lượng Expected Result — checklist

1. Có thể biết pass/fail từ kết quả quan sát không?
2. Có chỉ ra đúng trạng thái/giá trị/hành vi cần xác minh không?
3. Có căn cứ trong requirement/contract/approved rule không?
4. Có phân biệt kết quả mong đợi với thông báo hoặc chi tiết chưa được đặc tả không?
5. Có kiểm tra đúng điểm sau thao tác không (ngay lập tức, sau reload, sau điều hướng hoặc sau một điều kiện khác)?

## 5. Mẫu so sánh

**Yếu:** “Nhập số lượng không hợp lệ và kiểm tra hệ thống xử lý đúng.”

**Tốt hơn (khi rule đã xác nhận):** “Nhập `quantity = 0`, gửi form; hệ thống không tạo bản ghi và hiển thị validation theo rule `quantity >= 1`.”

Nếu requirement không xác định hành vi khi `quantity = 0`, không được khẳng định nội dung thông báo hoặc trạng thái bản ghi; đánh dấu phần đó cần làm rõ.

## 6. Điều không nên dùng làm thước đo duy nhất

- Số lượng Test Case.
- Số lượng dòng steps.
- Có đủ tất cả loại Test Type hay không.
- Độ dài title.
- Điểm số do AI tự chấm mà không có bằng chứng.

Đánh giá phải dựa vào coverage, căn cứ, khả năng thực thi, tính chính xác, độ trùng lặp và rủi ro bị bỏ sót.

## Liên quan đến quản trị Reference

Khi sửa tài liệu này, áp dụng `../reference-quality-standard.md` và chạy các eval có tiêu chí về tính thực thi/expected result trong `../../evals/blackbox-eval-cases.json`.
