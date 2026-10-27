# Equivalence Partitioning (EP)

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Mục tiêu:** Chia miền dữ liệu/điều kiện thành các lớp mà theo đặc tả, các phần tử trong mỗi lớp được xử lý tương tự. Chọn dữ liệu đại diện cho các lớp có ý nghĩa thay vì thử ngẫu nhiên nhiều giá trị tương tự.

## Khi nên dùng

- Trường input có nhóm giá trị hợp lệ/không hợp lệ.
- Quy tắc định dạng, kiểu dữ liệu, mã loại hoặc phạm vi được đặc tả.
- Có thể giải thích vì sao các giá trị trong cùng lớp được kỳ vọng xử lý giống nhau.

## Cách thực hiện

1. Xác định từng input/điều kiện liên quan và rule của nó.
2. Liệt kê lớp hợp lệ và lớp không hợp lệ; các lớp cần không rỗng và không chồng lấn trong mô hình đơn giản đang dùng.
3. Chia thêm lớp khi có rule khiến hai nhóm được xử lý khác nhau.
4. Chọn ít nhất một giá trị đại diện cho mỗi lớp cần kiểm tra; có thể cần nhiều hơn nếu rủi ro/điều kiện khác nhau.
5. Xác định expected result dựa vào requirement cho từng lớp.
6. Ghi coverage item để biết lớp nào đã được kiểm tra.

## Ví dụ minh họa (không phải rule của dự án)

Giả sử requirement mẫu nói rõ trường `quantity` chỉ nhận số nguyên từ 1 đến 10, bao gồm cả hai đầu mút, và từ chối giá trị không phải số nguyên.

| Partition | Ví dụ dữ liệu | Kỳ vọng theo requirement mẫu |
|---|---:|---|
| Hợp lệ: số nguyên từ 1–10 | 5 | Chấp nhận |
| Không hợp lệ: số nguyên nhỏ hơn 1 | 0 | Từ chối |
| Không hợp lệ: số nguyên lớn hơn 10 | 11 | Từ chối |
| Không hợp lệ: không phải số nguyên | 2.5 | Từ chối |
| Không hợp lệ: thiếu giá trị | empty | Cần test theo quy tắc required nếu requirement nêu rõ |

Điểm cuối không tự động là expected result nếu requirement chưa nói trường này bắt buộc; khi chưa rõ, đánh dấu cần làm rõ.

## Anti-patterns

- Tạo một partition “invalid” duy nhất dù các nhóm invalid kích hoạt rule khác nhau.
- Cho rằng mọi giá trị trong một miền đều tương đương mà không có căn cứ.
- Xem `null`, empty string, whitespace và thiếu field là một trường hợp duy nhất khi giao diện/API có thể xử lý khác nhau.
- Ghi expected result theo điều “thường gặp” thay vì theo nguồn.
