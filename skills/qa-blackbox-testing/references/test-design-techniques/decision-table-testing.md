# Decision Table Testing

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Mục tiêu:** Kiểm tra các tổ hợp điều kiện làm thay đổi quyết định hoặc kết quả nghiệp vụ. Đặc biệt hữu ích khi rule có nhiều điều kiện kết hợp.

## Khi nên dùng

- Kết quả phụ thuộc vào AND/OR giữa nhiều điều kiện.
- Có policy, eligibility, quyền, phí, trạng thái hoặc kết quả được quyết định bởi tổ hợp điều kiện.
- Việc chỉ kiểm tra từng điều kiện riêng lẻ có thể bỏ sót tương tác.

## Quy trình

1. Trích xuất các điều kiện từ nguồn đã xác nhận.
2. Trích xuất hành động/kết quả có thể xảy ra.
3. Lập cột rule cho tổ hợp điều kiện có ý nghĩa.
4. Đánh dấu `Y/N`, giá trị cụ thể hoặc `-` (không quan tâm) đúng ngữ nghĩa.
5. Xác định rule mâu thuẫn, thiếu hoặc không thể xảy ra; hỏi người phụ trách khi cần.
6. Chọn case để bao phủ các rule quan trọng; tối giản cột chỉ khi chứng minh không làm mất hành vi cần kiểm tra.

## Ví dụ minh họa

Giả sử requirement mẫu có ba điều kiện: `account_active`, `prerequisite_met`, `seat_available`. Chỉ cho phép đăng ký khi cả ba đều đúng.

| Rule | Account active | Prerequisite met | Seat available | Kết quả |
|---|---|---|---|---|
| R1 | Y | Y | Y | Cho phép đăng ký |
| R2 | N | - | - | Từ chối đăng ký |
| R3 | Y | N | - | Từ chối đăng ký |
| R4 | Y | Y | N | Từ chối đăng ký |

Bảng này chỉ đúng cho requirement minh họa. Trong sản phẩm thực tế, thông báo lý do, ưu tiên điều kiện, danh sách chờ hoặc override cần có căn cứ riêng.

## Checklist review

- Điều kiện có nguồn rõ ràng không?
- Có rule nào bị bỏ qua hoặc mâu thuẫn?
- Kết quả của mỗi rule rõ ràng và phân biệt được không?
- Dấu `-` có thực sự không ảnh hưởng kết quả không?
- Có cần kiểm tra thứ tự/ưu tiên nếu nhiều điều kiện thất bại cùng lúc không?
