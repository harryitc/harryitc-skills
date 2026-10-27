# Coverage and Traceability Model

> **Owner:** QA/QC Leader (designate) · **Reference status:** Draft for pilot · **Last reviewed:** 2026-10-26


**Purpose:** Đo coverage có định nghĩa và truy ngược được, không dựa vào cảm giác “đã tạo nhiều case”.

## 1. Chuỗi truy vết

`Test Basis → Requirement/Business Rule → Coverage Item → Test Scenario → Test Case → Execution Result/Defect`

Không phải dự án nào cũng có mã đầy đủ ở mọi tầng. Khi thiếu, ghi ID tạm và đánh dấu rõ; không tạo mã giả trông như mã chính thức.

## 2. Định nghĩa trạng thái coverage

- `Covered`: có ít nhất một Test Case được thiết kế cho coverage item và expected result có căn cứ.
- `Partial`: mới kiểm tra một phần điều kiện, nhánh nghiệp vụ, role hoặc trạng thái quan trọng.
- `Gap`: đã nhận diện coverage item nhưng chưa có case phù hợp.
- `Blocked by ambiguity`: không thể thiết kế expected result đáng tin cậy do thiếu hoặc mâu thuẫn Test Basis.
- `Not applicable`: có lý do được ghi nhận để loại khỏi phạm vi.

Không xem một requirement có bất kỳ case nào là “Covered” nếu case đó không kiểm tra đúng hành vi quan trọng.

## 3. Hai chiều coverage

### Requirement coverage

Câu hỏi: mỗi requirement/rule đã có scenario và Test Case tương ứng chưa? Đây là chiều cần thiết để phát hiện yêu cầu bị bỏ sót.

### Design coverage

Câu hỏi: các điều kiện, partition, boundary, decision rule, transition, actor/role và negative path đã được xét phù hợp chưa? Không phải mỗi kỹ thuật đều áp dụng cho mọi feature.

## 4. Công thức chỉ dùng khi mẫu số rõ

`Requirement coverage (%) = số requirement in-scope có coverage đạt / tổng số requirement in-scope đã được xác định × 100`.

Phải công bố cách xác định “coverage đạt” và danh sách requirement in-scope. Nếu requirement chưa phân rã, còn ambiguity hoặc mẫu số chưa thống nhất, chỉ báo cáo danh sách gaps/trạng thái thay vì đưa ra phần trăm gây hiểu nhầm.

Coverage thiết kế theo technique chỉ nên tính khi tập coverage item/điều kiện đã được xác định trước. Không đồng nhất số Test Case với coverage.

## 5. Coverage Matrix tối thiểu

Các trường khuyến nghị: `Requirement ID`, `Requirement Summary`, `Coverage Item`, `Technique`, `Linked Test Case IDs`, `Coverage Status`, `Gap/Risk`, `Clarification Needed`.

## 6. Traceability rules

- Một Test Case có thể cover nhiều requirement nếu mối quan hệ rõ, nhưng cần tránh làm case quá rộng.
- Một requirement thường cần nhiều case nếu có nhiều rule, role, điều kiện hoặc outcome khác nhau.
- Mỗi gap cần có owner/next action khi áp dụng quy trình team.
- Sau khi requirement thay đổi, xác định case bị ảnh hưởng và chạy regression selection; không chỉ thêm case mới mà bỏ qua test cũ.
- Traceability không chứng minh Test Case đúng; vẫn phải review expected result và khả năng thực thi.

## 7. Anti-patterns

- Tuyên bố 100% coverage vì mọi chức năng đều có ít nhất một case.
- Tạo coverage denominator sau khi xem kết quả để làm số liệu đẹp hơn.
- Cho rằng link requirement tự nó chứng minh case cover requirement.
- Đếm `Blocked by ambiguity` là `Covered`.
- Để requirement bị đổi nhưng không đánh giá lại Test Case liên quan.
