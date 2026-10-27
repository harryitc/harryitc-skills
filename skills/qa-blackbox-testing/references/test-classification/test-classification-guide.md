# Test Classification Guide

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Mục đích:** Giúp gắn nhãn Test Type nhất quán. Danh mục dưới đây là taxonomy khởi đầu; dự án nên thống nhất tên trường và danh sách giá trị.

| Nhóm | Khi dùng | Ví dụ coverage |
|---|---|---|
| Functional — positive | Hành vi đúng theo luồng thành công | Thực hiện hành động hợp lệ và xác minh outcome |
| Functional — negative | Hành vi khi điều kiện/dữ liệu không thỏa | Từ chối hoặc xử lý input không hợp lệ theo spec |
| Input validation | Required, format, type, length, range | Kiểm tra dữ liệu theo validation rule |
| Business rule | Rule nghiệp vụ và tổ hợp điều kiện | Điều kiện eligibility/approval |
| Permission/authorization | Hành vi theo role/permission | Role được phép/không được phép thực hiện hành động |
| Workflow/state | Chuyển trạng thái/luồng nhiều bước | Transition hợp lệ/không hợp lệ theo spec |
| Data persistence/consistency | Dữ liệu quan sát sau create/update/delete | Dữ liệu được giữ đúng sau refresh/navigation khi yêu cầu |
| Search/filter/sort/pagination | Kết quả truy vấn và cách phân trang | Tổ hợp filter, thứ tự, trang rỗng/cuối |
| UI/content/state | Nội dung hiển thị, empty/loading/error state, feedback | Label, validation feedback hoặc trạng thái UI có spec |
| API contract (black-box) | Kiểm tra hành vi qua contract công bố | Request/response, status, schema và error contract |
| Integration behavior | Hành vi tích hợp quan sát từ biên hệ thống | Kết quả khi phụ thuộc bên ngoài đáp ứng/không đáp ứng |
| Compatibility/accessibility/performance/security-related | Chỉ khi có yêu cầu/phạm vi và test basis phù hợp | Theo tiêu chí đã xác nhận; không tự tạo tiêu chuẩn kỹ thuật |

## Quy tắc phân loại

- **Test Type** trả lời “đang kiểm tra loại mục tiêu nào?”.
- **Design Technique** trả lời “đã chọn dữ liệu/case bằng cách nào?”.
- **Execution Method** trả lời “manual hay automation?”.
- **Priority** trả lời “nên thực thi case khi nào tương đối với case khác?”.

Một case có thể có nhiều nhãn phụ nếu hệ thống cho phép, nhưng cần một quy ước chính để báo cáo không bị lẫn lộn.

Không ép case chỉ có một test type nếu mục tiêu thực sự bao trùm hai khía cạnh, nhưng tránh gắn mọi nhãn có thể.
