# Reference Quality Standard

**Mục tiêu:** Bảo đảm tài liệu trong `references/` giúp AI và tester đưa ra quyết định test design có căn cứ, áp dụng đúng điều kiện và có thể review. Đây là chuẩn nội bộ đề xuất cho toolkit, không phải tài liệu chứng nhận của ISTQB.

> **Owner:** QA/QC Leader hoặc người được ủy quyền · **Status:** Draft for pilot · **Last reviewed:** 2026-10-26

## 1. Reference tốt phải trả lời được gì?

1. Tài liệu này hỗ trợ quyết định QA nào?
2. Áp dụng khi nào, không áp dụng khi nào?
3. Người/AI cần làm theo các bước nào?
4. Cần đầu vào gì và phải tạo ra đầu ra gì?
5. Ví dụ nào minh họa đúng kỹ thuật? Ví dụ nào thể hiện lỗi thường gặp?
6. Điều gì phải lấy từ nguồn dự án, không được AI tự suy diễn?
7. Căn cứ nào hỗ trợ các khẳng định kỹ thuật?
8. Evals nào sẽ phát hiện nếu nội dung này bị hiểu sai?

Không nhất thiết mọi tài liệu ngắn phải có mọi heading y hệt, nhưng các mục phù hợp phải được đề cập.

## 2. Metadata bắt buộc

Mỗi Reference thực hành nên có:

- `Owner`: vai trò chịu trách nhiệm, không nhất thiết tên cá nhân.
- `Status`: `Draft`, `Reviewed`, hoặc `Deprecated`.
- `Last reviewed`: ngày kiểm tra nội dung.
- `Scope`: loại dự án/feature hoặc bối cảnh áp dụng.
- `Sources`: nguồn chính xác nếu có khẳng định chuẩn tắc/kỹ thuật từ bên ngoài.

Tài liệu domain-specific bổ sung người xác nhận, nguồn nội bộ và ngày xác nhận rule.

## 3. Nội dung chất lượng

### A. Tính chính xác
- Phân biệt yêu cầu chính thức, hướng dẫn tổng quát, ví dụ minh họa và giả định.
- Không gán ý kiến của toolkit cho ISTQB hoặc tiêu chuẩn ngoài.
- Không trích lại dài nội dung có bản quyền; diễn giải bằng lời riêng và dẫn nguồn.
- Nếu không chắc phiên bản nguồn hoặc nội dung đã thay đổi, ghi nhận và kiểm tra lại trước khi nâng trạng thái.

### B. Khả năng áp dụng
- Có điều kiện kích hoạt/không kích hoạt.
- Có quy trình lựa chọn/thực hiện, không chỉ định nghĩa.
- Có ví dụ đầu vào → cách phân tích → output mong đợi.
- Nêu các lỗi áp dụng phổ biến và cách tránh.
- Expected Result trong ví dụ phải bắt nguồn từ rule được nêu ngay trong ví dụ.

### C. Tính an toàn trước suy diễn
- Ghi rõ phần nào phải xác nhận từ requirement/owner.
- Không biến convention của một dự án thành quy tắc phổ quát.
- Khi thiếu nguồn, chỉ ghi câu hỏi/coverage idea; không bịa behavior cụ thể.

### D. Khả năng đánh giá
- Liên kết các lỗi hiểu sai thường gặp với một hoặc nhiều eval cases.
- Nếu thay đổi hướng dẫn có thể đổi output, chạy eval liên quan trước khi merge.

## 4. Review gate trước khi đổi `Draft` thành `Reviewed`

| Gate | Câu hỏi |
|---|---|
| Purpose & scope | Người đọc hiểu tài liệu giải quyết vấn đề gì và giới hạn ở đâu? |
| Provenance | Nguồn ngoài/nội bộ đã được dẫn và không bị trình bày sai? |
| Operational guidance | Có hướng dẫn áp dụng và tiêu chí đầu ra rõ? |
| Worked example | Có ví dụ đúng, nhất quán với rule đầu vào? |
| Anti-patterns | Có chỉ ra những lỗi dễ xảy ra? |
| Uncertainty | Có ngăn AI tự suy diễn nơi nguồn chưa đủ? |
| Eval coverage | Có eval phù hợp và đã chạy nếu tài liệu tác động đến output? |
| Owner approval | Người được ủy quyền đã review chưa? |

Nếu còn lỗi trọng yếu hoặc nguồn chưa xác thực, giữ `Draft`.

## 5. Change control

1. Tạo branch/đề xuất thay đổi.
2. Ghi lý do và mục tiêu thay đổi.
3. Xác định Skill/template/eval nào bị ảnh hưởng.
4. Chạy eval tương ứng và so sánh output trước/sau.
5. Review bằng con người; cập nhật `CHANGELOG.md`.
6. Chuyển status chỉ sau khi được duyệt.

Không tối ưu Reference chỉ để tăng số Test Case. Ưu tiên độ chính xác, coverage có ý nghĩa, khả năng thực thi và giảm unsupported assumptions.
