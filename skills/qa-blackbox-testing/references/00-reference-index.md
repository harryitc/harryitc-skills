# Reference Index — Nguồn kiến thức chuẩn

**Owner đề xuất:** QA/QC Leader · **Trạng thái:** Draft for pilot · **Phiên bản:** 0.1.0

## 1. Mục đích và cách dùng

Thư mục `references/` là knowledge base của QA Black-box Testing AI. Tài liệu ở đây phải hướng dẫn AI lựa chọn và áp dụng phương pháp, không chỉ mô tả thuật ngữ. Mỗi tài liệu nên có mục đích, điều kiện áp dụng, quy trình, ví dụ, anti-patterns và nguồn tham khảo khi phù hợp.

AI cần đọc theo nhu cầu, không phải nhồi tất cả tài liệu vào mỗi lượt:

| Nhiệm vụ | Reference cần đọc |
|---|---|
| Mọi hoạt động tạo/review | `testcase-quality/testcase-quality-standard.md`; `coverage-and-traceability/coverage-model.md` |
| Chọn technique | `test-design-techniques/technique-selection-guide.md` và tài liệu kỹ thuật tương ứng |
| Xét mức ưu tiên | `risk-and-priority/risk-priority.md` |
| Xác định loại test | `test-classification/test-classification-guide.md` |
| Kiểm tra ví dụ | `examples-and-anti-patterns/good-vs-bad.md` |
| Xác minh thuật ngữ/nguồn | `standards-and-glossary/glossary.md`; `standards-and-glossary/source-register.md` |
| Dự án cụ thể | Các file được QA Leader xác nhận trong `domain-knowledge/` hoặc tài liệu dự án cung cấp |

## 2. Quy tắc ưu tiên nguồn

1. Requirement/business rule của dự án đã được phê duyệt quyết định hành vi cụ thể của sản phẩm.
2. Hợp đồng giao tiếp/API, thiết kế UI và tài liệu sản phẩm đã được xác nhận là nguồn chi tiết cho phạm vi tương ứng.
3. Quan sát hệ thống là bằng chứng về hành vi hiện tại, không tự động chứng minh hành vi hiện tại là đúng yêu cầu.
4. Reference QA tổng quát dùng để thiết kế kiểm thử; không được thay thế business rule dự án.
5. Giả định do AI đề xuất không phải quy tắc chính thức cho đến khi người có thẩm quyền xác nhận.

Nếu hai nguồn xung đột, tạo finding `Contradiction`, ghi rõ cả hai nguồn và yêu cầu giải quyết; không tự chọn nguồn tiện lợi hơn.

## 3. Chuẩn metadata cho mỗi reference

Mỗi tài liệu nên ghi:

- `Purpose`: tài liệu dùng để giải quyết quyết định nào.
- `Scope`: phạm vi áp dụng và ngoại lệ.
- `Status`: Draft / Reviewed / Deprecated.
- `Owner` và `Last reviewed`.
- `Sources`: URL/tên tài liệu và ngày truy cập.
- `Examples`: dữ liệu minh họa được đánh dấu rõ là ví dụ, không phải rule của sản phẩm.

## 4. Cách quản lý chất lượng

- Reference thay đổi phải có lý do và entry trong `CHANGELOG.md`.
- Thay đổi kỹ thuật thiết kế phải chạy eval cases phù hợp trong `evals/`.
- Chỉ QA Leader hoặc người được ủy quyền chuyển nội dung dự án từ Draft thành Reviewed.
- Không copy toàn văn tài liệu có bản quyền vào reference. Tóm tắt bằng lời của team, trích dẫn nguồn và dùng ví dụ tự xây dựng.
- Tránh các câu tuyệt đối như “mọi chức năng đều phải có 20 Test Case” nếu chưa có chính sách có căn cứ.

## 5. Danh mục tài liệu

- `test-design-techniques/technique-selection-guide.md`: cách chọn technique.
- `test-design-techniques/equivalence-partitioning.md`: phân vùng tương đương.
- `test-design-techniques/boundary-value-analysis.md`: phân tích giá trị biên.
- `test-design-techniques/decision-table-testing.md`: bảng quyết định.
- `test-design-techniques/state-transition-testing.md`: chuyển trạng thái.
- `test-design-techniques/use-case-testing.md`: kiểm thử use case/luồng nghiệp vụ.
- `test-design-techniques/experience-based-and-combinatorial.md`: error guessing, exploratory và pairwise ở mức bổ trợ.
- `reference-quality-standard.md`: chuẩn chất lượng và quy trình review References.
- `REFERENCE_TEMPLATE.md`: mẫu để tạo Reference mới có nguồn, scope, ví dụ và anti-pattern.
- `testcase-quality/testcase-quality-standard.md`: tiêu chuẩn Test Case.
- `coverage-and-traceability/coverage-model.md`: coverage và traceability.
- `test-classification/test-classification-guide.md`: phân loại test.
- `risk-and-priority/risk-priority.md`: risk, priority, severity.
- `domain-knowledge/README.md` và `domain-knowledge/project-rule-register-template.md`: quản lý kiến thức dự án.
- `examples-and-anti-patterns/good-vs-bad.md`: ví dụ tốt/xấu.
- `standards-and-glossary/glossary.md`, `source-register.md`: thuật ngữ và nguồn.
