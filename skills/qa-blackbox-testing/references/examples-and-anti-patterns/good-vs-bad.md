# Good vs. Bad Test Case Design Examples

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Lưu ý:** Ví dụ tự xây dựng để minh họa nguyên tắc; không phải business rule của bất kỳ hệ thống nào.

## Example 1 — Boundary validation

**Giả định được nêu rõ:** requirement mẫu quy định `quantity` là số nguyên từ 1 đến 10, inclusive.

**Yếu**
- Title: Test số lượng.
- Steps: Nhập số sai, bấm lưu.
- Expected: Hệ thống xử lý đúng.

**Tốt hơn**
- Title: Từ chối quantity thấp hơn giá trị tối thiểu.
- Preconditions: Form tạo item sẵn sàng; rule `quantity ∈ [1,10]` đã được xác nhận.
- Steps: Nhập `quantity = 0`; gửi form.
- Expected: Form không tạo item; giá trị không được chấp nhận theo validation rule. Nội dung message cụ thể chỉ điền nếu spec xác định.
- Technique: BVA/EP.

## Example 2 — Permission

**Yếu**
- Title: Kiểm tra sinh viên không có quyền.
- Expected: Hệ thống báo lỗi.

**Vấn đề:** chưa biết action nào bị cấm, nguồn role matrix nào áp dụng, người dùng nhìn thấy gì và dữ liệu có bị thay đổi không.

**Tốt hơn khi có role matrix đã xác nhận**
- Title: Role A không thể thực hiện action X trên resource Y.
- Preconditions: User thuộc Role A; resource Y tồn tại và ở trạng thái [S] theo test basis.
- Steps: Đăng nhập bằng user test; thử action X qua đường thao tác được hỗ trợ.
- Expected: Action bị từ chối theo rule đã xác nhận; resource giữ nguyên trạng thái/dữ liệu nếu điều đó được yêu cầu; UI/API feedback ghi đúng đặc tả.
- Requirement Reference: [ID từ role matrix].

Không suy diễn rằng mọi hệ thống phải trả HTTP 403 hoặc một câu thông báo cụ thể.

## Example 3 — State transition

**Yếu:** “Bấm duyệt và kiểm tra thành công.”

**Tốt hơn:** Nêu current state, actor/permission, event, guard, expected next state và các side effect được đặc tả. Nếu state hiện tại không được cung cấp, ghi rõ setup cần thiết hoặc hỏi thêm.

## Example 4 — Expected result không có căn cứ

Nếu requirement chỉ nói “search theo từ khóa” mà không quy định case sensitivity, tokenization hoặc search fields, không nên tự khẳng định tìm kiếm phải không phân biệt hoa thường hoặc phải match mọi trường. Tạo danh sách câu hỏi/observations cần xác nhận; vẫn có thể viết case cho hành vi đã được đặc tả rõ.

## Example 5 — Duplicate

Hai case cùng điều kiện, cùng action và cùng expected result nhưng chỉ đổi dữ liệu từ `A` sang `B` có thể là duplicate nếu A/B thuộc cùng partition và không kiểm tra boundary/rule riêng. Không gộp trước khi xác nhận giá trị đó không thuộc boundary, role hoặc business rule khác.

## Anti-patterns tổng quát

- “Kiểm tra hệ thống hoạt động đúng” làm expected result.
- Tạo Test Case từ tên chức năng mà không có căn cứ về hành vi.
- Dùng một case để kiểm tra nhiều mục tiêu độc lập khó xác định fail.
- Chỉ có happy path.
- Copy cùng một test matrix cho mọi chức năng.
- Dùng dữ liệu biên không đúng kiểu/precision.
- Gọi case là `Pass` khi chỉ mới được sinh/review.
- Tuyên bố coverage hoàn chỉnh chỉ từ số lượng Test Case.
