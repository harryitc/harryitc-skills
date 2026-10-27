# Boundary Value Analysis (BVA)

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Mục tiêu:** Kiểm tra giá trị tại và sát giới hạn nơi lỗi thường phát sinh, theo đúng quy tắc giới hạn đã đặc tả.

## Khi nên dùng

Requirement xác định miền có thứ tự và biên rõ ràng: min/max số lượng, độ dài chuỗi, ngày tháng, tuổi, giới hạn phân trang hoặc số lần thao tác.

## Cách thực hiện

1. Xác nhận loại dữ liệu, đơn vị, biên dưới/biên trên và biên có được bao gồm hay không.
2. Xác định mức BVA phù hợp với test strategy. BVA hai giá trị và ba giá trị là các cách tiếp cận khác nhau; không trộn chúng mà không giải thích.
3. Với mỗi biên, chọn giá trị ngay ngoài biên, tại biên và ngay trong miền theo kiểu BVA đã chọn.
4. Với dữ liệu không liên tục hoặc có precision/format đặc biệt, xác định “giá trị liền kề” theo kiểu dữ liệu thực tế.
5. Kiểm tra expected result riêng cho từng giá trị và liên kết về rule.

## Ví dụ minh họa

Giả sử requirement mẫu quy định `quantity` là số nguyên từ 1 đến 10, bao gồm 1 và 10.

| Biên | Giá trị | Mục đích |
|---|---:|---|
| Dưới biên dưới | 0 | Kiểm tra ngoài miền dưới |
| Biên dưới | 1 | Kiểm tra giá trị tối thiểu được cho phép |
| Trong miền gần biên dưới | 2 | Kiểm tra ngay bên trong miền |
| Trong miền gần biên trên | 9 | Kiểm tra ngay bên trong miền |
| Biên trên | 10 | Kiểm tra giá trị tối đa được cho phép |
| Trên biên trên | 11 | Kiểm tra ngoài miền trên |

Bảng trên là bộ minh họa thực dụng quanh hai biên; team cần ghi rõ technique/coverage level được chọn. Không phải mọi chức năng đều cần đúng sáu case.

## Không được suy diễn

- Nếu tài liệu chỉ nói “độ dài tối đa 20” nhưng không nói field có thể rỗng hay không, BVA không tự xác định tính bắt buộc.
- Nếu quy tắc làm tròn, timezone hoặc precision của số chưa rõ, hỏi/ghi nhận thay vì chọn liền kề theo trực giác.
- Giá trị biên không thay thế kiểm tra format, quyền truy cập hoặc business rule khác.
