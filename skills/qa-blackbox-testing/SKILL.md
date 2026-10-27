---
name: qa-blackbox-testing
description: End-to-end black-box test design, coverage matrix analysis, and test case quality review based on ISTQB principles. Analyzes functional requirements, user stories, acceptance criteria, UI mockups, and API contracts without access to internal source code. Supports Equivalence Partitioning (EP), Boundary Value Analysis (BVA), Decision Table, State Transition, and Use Case testing. Automatically performs independent test review to flag unsupported assumptions, missing boundary coverage, and executability issues. Use whenever the user asks to design, generate, expand, or review manual black-box test cases or verify specification coverage.
---

# QA Black-box Testing

Goal: deliver verifiable, traceable, and executable Black-box Test Cases and quality audits based strictly on observable system behaviors and specifications, independent of internal source code implementation.

---

## Core Principles

1. **Zero Guessing / Anti-Hallucination:** Never invent business rules, error messages, user roles, or expected results.
2. **Explicit Fact Tagging:**
   - `Confirmed`: explicit in the provided specifications or approved project rules.
   - `Observed`: verified directly in the running system.
   - `Assumption`: proposed working assumption requiring stakeholder confirmation.
   - `Needs Clarification`: missing, conflicting, or ambiguous requirement.
3. **No Unearned Pass/Approval:** AI proposes findings and review statuses (`Ready for QA Lead Review`, `Needs Revision`, `Blocked by Test Basis`), never claims a test is "Approved" or "Passed" without execution evidence.
4. **Behavioral Scope:** Design tests strictly from the perspective of actors, inputs, states, and observable outputs. Do not infer code paths, branch coverage, or statement execution.

---

## Knowledge Base & References

Tra cứu tài liệu hướng dẫn kỹ thuật trong thư mục cục bộ của skill:

| Mục đích | Tài liệu tham chiếu |
|---|---|
| Danh mục & Điều phối | [`references/00-reference-index.md`](./references/00-reference-index.md) |
| Tiêu chuẩn chất lượng Test Case | [`references/testcase-quality/testcase-quality-standard.md`](./references/testcase-quality/testcase-quality-standard.md) |
| Ma trận Bao phủ & Truy vết | [`references/coverage-and-traceability/coverage-model.md`](./references/coverage-and-traceability/coverage-model.md) |
| Kỹ thuật Thiết kế Hộp đen | [`references/test-design-techniques/technique-selection-guide.md`](./references/test-design-techniques/technique-selection-guide.md)<br/>- [Equivalence Partitioning](./references/test-design-techniques/equivalence-partitioning.md)<br/>- [Boundary Value Analysis](./references/test-design-techniques/boundary-value-analysis.md)<br/>- [Decision Table](./references/test-design-techniques/decision-table-testing.md)<br/>- [State Transition](./references/test-design-techniques/state-transition-testing.md)<br/>- [Use Case Testing](./references/test-design-techniques/use-case-testing.md) |
| Đánh giá Rủi ro & Priority | [`references/risk-and-priority/risk-priority.md`](./references/risk-and-priority/risk-priority.md) |
| Ví dụ Thực hành Chuẩn | [`references/examples-and-anti-patterns/good-vs-bad.md`](./references/examples-and-anti-patterns/good-vs-bad.md) |

---

## Workflows

Tùy vào yêu cầu của người dùng, chọn quy trình phù hợp:

### Workflow A: Design & Generation (Sinh Test Case mới)

1. **Xác định Test Basis & Phạm vi:**
   - Đọc kỹ requirement, user story, API contract hoặc UI mockup được cung cấp.
   - Ghi nhận: Module, Actor/Role, Luồng chính, Phạm vi bao gồm/loại trừ.
2. **Bóc tách Requirement & Gắn Tag:**
   - Chia nhỏ thành từng quy tắc nghiệp vụ/điều kiện cụ thể.
   - Phân loại rõ ràng: `Confirmed`, `Assumption`, hay `Needs Clarification`.
3. **Lập Coverage Matrix:**
   - Xây dựng danh sách coverage items trước khi viết case chi tiết.
   - Đảm bảo bao phủ: Happy path, Negative path, Boundary conditions, Role/State transitions.
4. **Chọn Kỹ thuật Kiểm thử Phù hợp:**
   - *EP*: Nhóm dữ liệu có xử lý tương đương.
   - *BVA*: Giá trị biên (min, max, cận trên, cận dưới).
   - *Decision Table*: Tổ hợp nhiều điều kiện logic phức tạp.
   - *State Transition*: Hành vi thay đổi theo trạng thái của thực thể (Order, Account, Ticket).
   - *Use Case*: Luồng người dùng xuyên suốt từ đầu đến cuối.
5. **Sinh Scenario & Test Cases:**
   - Định dạng mặc định theo [`templates/testcase-template.csv`](./templates/testcase-template.csv):
     `Test Case ID, Module, Function, Requirement Reference, Test Scenario, Test Type, Design Technique, Title, Preconditions, Test Steps, Test Data, Expected Result, Priority, Review Status, Notes`.
   - Mỗi case có: Tiền điều kiện rõ ràng, các bước đánh số cụ thể, dữ liệu test xác thực, và kết quả mong đợi quan sát được (observable).

---

### Workflow B: Review & Quality Audit (Thẩm định Bộ Test Case có sẵn)

1. **Kiểm tra căn cứ (Basis Verification):**
   - Đối chiếu từng Test Case với tài liệu gốc. Gắn cờ `Unsupported Expected Result` nếu kết quả không có bằng chứng trong spec.
2. **Đánh giá Coverage:**
   - Phát hiện các quy tắc bị bỏ sót, thiếu negative path, thiếu kiểm tra phân quyền hoặc thiếu trường hợp biên.
3. **Kiểm tra Tính khả thi & Độc lập:**
   - Preconditions có thể thiết lập được không? Steps có mơ hồ không? Data có cụ thể không?
4. **Phát hiện Trùng lặp (Deduplication):**
   - Loại bỏ các case biến thể vô nghĩa không gia tăng giá trị kiểm thử.
5. **Phân loại Phát hiện:**
   - `Blocker`: Thiếu căn cứ nghiêm trọng, thông tin mâu thuẫn không thể kiểm thử.
   - `Major`: Bỏ sót rule trọng yếu, case không thể thực thi, expected result mơ hồ.
   - `Minor`: Naming, format hoặc chi tiết nhỏ cần chỉnh sửa.
   - `Suggestion`: Gợi ý tối ưu hóa thêm.
6. **Kết luận Review:**
   - `Ready for QA Lead Review` | `Needs Revision` | `Blocked by Test Basis`.

---

### Workflow C: End-to-End Delivery (Thiết kế + Tự Kiểm định)

Đây là chế độ mặc định khi người dùng yêu cầu: *"Hãy thiết kế test case hoàn chỉnh cho tính năng X"*:
1. Thực hiện đầy đủ **Workflow A** (Sinh ma trận coverage và test case).
2. Tự động chạy **Workflow B** (Self-review) để kiểm tra chéo các bước, phát hiện lỗ hổng coverage hoặc giả định còn tồn đọng.
3. Xuất báo cáo hoàn chỉnh gồm:
   - Phạm vi & Quy tắc đã bóc tách.
   - Điểm cần làm rõ (Needs Clarification) & Giả định (Assumptions).
   - Bảng Ma trận Bao phủ (Coverage Matrix).
   - Bảng Danh sách Test Case.
   - Ghi chú chất lượng (Quality Review Notes).

---

## Định dạng Ngôn ngữ

- Mặc định viết bằng ngôn ngữ của tài liệu hoặc ngôn ngữ người dùng yêu cầu (Tiếng Việt hoặc English).
- Giữ nguyên các thuật ngữ kỹ thuật QA chuẩn quốc tế (EP, BVA, Boundary, Preconditions, Traceability...).
