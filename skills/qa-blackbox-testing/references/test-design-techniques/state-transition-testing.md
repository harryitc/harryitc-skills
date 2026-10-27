# State Transition Testing

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Mục tiêu:** Kiểm tra hành vi phụ thuộc trạng thái hiện tại và sự kiện/hành động, gồm cả chuyển đổi hợp lệ và xử lý chuyển đổi không được phép theo đặc tả.

## Khi nên dùng

- Một entity có lifecycle (ví dụ draft/submitted/reviewed/published).
- Hành động bị giới hạn bởi trạng thái.
- Lỗi có thể xảy ra do bỏ qua bước, lặp thao tác hoặc gọi sự kiện sai thời điểm.

## Cách thực hiện

1. Trích xuất danh sách state, event, guard/điều kiện, transition và kết quả từ requirement.
2. Xác định state khởi đầu và cách thiết lập nó.
3. Lập bảng `Current State + Event/Action + Guard → Expected State/Outcome`.
4. Bao phủ các transition quan trọng và các transition bị cấm nếu hành vi khi bị cấm đã được mô tả.
5. Kiểm tra tác dụng phụ có thể quan sát được (ví dụ record, notification hoặc lịch sử) khi requirement đề cập.
6. Xác định case riêng cho event lặp, stale state hoặc concurrent update chỉ khi phù hợp với rủi ro/phạm vi.

## Ví dụ minh họa

Với workflow minh họa `Draft → Submitted → Reviewed`, yêu cầu mẫu xác nhận không được chuyển thẳng `Draft → Reviewed`.

| Trạng thái hiện tại | Hành động | Kết quả mong đợi theo ví dụ |
|---|---|---|
| Draft | Submit | Chuyển sang Submitted |
| Submitted | Review/Approve | Chuyển sang Reviewed nếu người dùng có quyền |
| Draft | Review/Approve | Từ chối transition hoặc phản hồi theo hành vi đã được xác nhận |

Dòng cuối chỉ chứng minh transition không hợp lệ; thông báo cụ thể, mã lỗi hoặc UI behavior cần requirement khác.

## Anti-patterns

- Tự tạo state hoặc transition chỉ vì phổ biến trong sản phẩm cùng loại.
- Gộp trạng thái nghiệp vụ với trạng thái UI mà không có mô tả liên kết.
- Chỉ kiểm tra transition hợp lệ trong khi rule nêu rõ transition bị cấm.
- Kiểm tra thông báo/cảnh báo cụ thể chưa được định nghĩa.
