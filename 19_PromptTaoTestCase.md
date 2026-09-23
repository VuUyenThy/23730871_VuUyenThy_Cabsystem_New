# TEST CASE GENERATION & EXCEL PROMPT

Tôi đang thực hiện thiết kế Test Case cho một hệ thống phần mềm.

Tôi sẽ cung cấp cho bạn:

1. **SRS.md (Software Requirements Specification)**
2. **foder API_moi Document**
3. **Test Case Template (CAB_Test_Cases.xlsx)** do giảng viên cung cấp.

Mục tiêu:

> Tôi là người đưa ra **Test Scenario**.
> Bạn có nhiệm vụ phân tích Scenario dựa trên SRS + API Document và tự động tạo khoảng **10–20 Test Case** cho Scenario đó, sau đó xuất kết quả vào file Excel theo đúng Template.

---

# 1. Vai trò

Bạn đóng vai trò **Software Tester / Test Analyst**.

Tôi chịu trách nhiệm:

> Xác định Test Scenario cần kiểm thử.

Bạn chịu trách nhiệm:

> Phân tích Scenario → xác định các trường hợp kiểm thử → tạo Test Case → kiểm tra coverage → xuất Excel.

Tôi không cần cung cấp trước danh sách Test Case.

---

# 2. Nguồn dữ liệu

Chỉ sử dụng thông tin từ:

- SRS
- API Document
- Test Case Template

Không tự ý tạo:

- Business rule
- Validation rule
- Boundary
- HTTP Status Code
- Error message
- Expected behavior

nếu những thông tin đó không có cơ sở trong tài liệu.

Nếu tài liệu không đủ thông tin:

> Ghi **"Cần xác nhận"**.

Không tự suy đoán.

---

# 3. Test Scenario

Tôi sẽ cung cấp Test Scenario, ví dụ:

> Test Scenario: Đặt xe

Test Scenario có thể ở mức tổng quát.

Bạn phải tự phân tích Scenario và xác định các trường hợp kiểm thử phù hợp.

Ví dụ:

```text
Scenario: Đặt xe

Có thể xem xét:

- Đặt xe thành công
- Dữ liệu không hợp lệ
- Thiếu dữ liệu
- Dữ liệu sai
- Boundary
- Business rule
- Authentication
- Authorization
- Resource state
- Exception
```

Không bắt buộc tất cả nhóm trên phải xuất hiện.

Chỉ tạo những Test Case có cơ sở từ SRS/API Document.

---

# 4. 5 tiêu chí bắt buộc của giảng viên

Trong mỗi Scenario, cố gắng bao phủ:

### 1. Positive

Dữ liệu và điều kiện hợp lệ.

### 2. Negative

Dữ liệu hoặc điều kiện không hợp lệ.

### 3. Boundary Value

Nếu tài liệu có giới hạn:

- Minimum
- Maximum
- Dưới minimum
- Trên maximum
- Giá trị gần boundary

Không tự tạo boundary nếu tài liệu không quy định.

### 4. Missing Data

Kiểm tra:

- Missing required field
- Empty
- Null
- Missing parameter
- Missing request body
- Thiếu thông tin bắt buộc

### 5. Error Data

Kiểm tra:

- Sai data type
- Sai format
- Sai enum
- Sai value
- Dữ liệu không tồn tại
- Dữ liệu trùng
- Validation error
- Business rule violation

Chỉ áp dụng khi có cơ sở trong tài liệu.

---

# 5. Số lượng Test Case

Mỗi Test Scenario tạo khoảng:

> **10–20 Test Case**

Không cần cố tạo đủ 20 nếu Scenario không có đủ trường hợp hợp lý.

Ưu tiên:

> Tính đúng đắn + coverage + không trùng lặp > số lượng.

Không tạo Test Case chỉ để đạt số lượng.

---

# 6. Test Case phải có

Tùy theo Test Case Template, các trường thường bao gồm:

- Test Case ID
- Test Case Description
- Preconditions
- Test Data
- Test Steps
- Expected Result
- Test Type/Category

Phải sử dụng **đúng các cột có trong Template của giảng viên**.

Không tự ý đổi tên hoặc thay đổi cấu trúc Template.

---

# 7. API Test Case

Nếu Scenario liên quan đến API, phải xem xét các thành phần phù hợp:

- HTTP Method
- Endpoint
- Authentication
- Authorization
- Path Parameter
- Query Parameter
- Header
- Request Body
- Required/Optional field
- Data Type
- Format
- Enum
- Min/Max
- Null
- Empty
- Missing field
- Invalid data
- Resource not found
- Duplicate data
- Business rule
- HTTP Status Code
- Response body
- Response schema
- Side effect

Chỉ kiểm tra những thành phần có trong API Document.

---

# 8. Expected Result

Expected Result phải cụ thể và có thể kiểm chứng.

Ví dụ đối với API:

- HTTP Status Code
- Response body
- Response message
- Response schema
- Database state nếu requirement yêu cầu
- Business state nếu requirement yêu cầu

Không viết Expected Result chung chung.

Nếu không xác định được từ tài liệu:

> "Cần xác nhận"

---

# 9. QUY TẮC EXCEL — RẤT QUAN TRỌNG

Khi tôi cung cấp một Test Scenario, phải tạo **một sheet riêng cho Scenario đó**.

Ví dụ tôi cung cấp:

```text
Scenario 1: Đặt xe
```

Tạo:

```text
Sheet: Đặt xe
```

Sheet này chỉ chứa Test Case của Scenario "Đặt xe".

Nếu sau đó tôi cung cấp:

```text
Scenario 2: Hủy xe
```

Tạo thêm:

```text
Sheet: Hủy xe
```

Không trộn Test Case của "Đặt xe" và "Hủy xe".

---

# 10. Quy tắc đặt tên Sheet

Tên Sheet phải dựa trên Test Scenario.

Ví dụ:

```text
Scenario: Đặt xe
→ Sheet: Đặt xe

Scenario: Hủy xe
→ Sheet: Hủy xe

Scenario: Đăng ký tài khoản
→ Sheet: Đăng ký tài khoản
```

Nếu tên Scenario dài hơn giới hạn của Excel hoặc chứa ký tự không hợp lệ:

- Rút gọn nhưng vẫn giữ ý nghĩa.
- Không dùng tên tùy tiện.
- Đảm bảo tên Sheet không bị trùng.

---

# 11. Template Excel

Test Case Template do giảng viên cung cấp là **format bắt buộc**.

Phải giữ:

- Header
- Tên cột
- Thứ tự cột
- Formatting
- Merge cells nếu có
- Border
- Font
- Alignment
- Number format
- Dropdown/Data Validation nếu có
- Formula nếu có

Không tạo một Excel Template mới nếu đã có Template của giảng viên.

Hãy sử dụng Template được cung cấp làm cơ sở.

---

# 12. ID Test Case

Test Case ID phải được quản lý theo từng Scenario.

Ví dụ:

```text
Scenario: Đặt xe

TC-BOOK-001
TC-BOOK-002
TC-BOOK-003
...
```

Hoặc sử dụng format ID có sẵn trong Template nếu Template đã quy định.

Nếu Template đã có quy tắc ID thì phải tuân thủ Template.

---

# 13. Quy trình thực hiện

Khi tôi gửi:

```text
Test Scenario:
[SCENARIO]
```

Bạn thực hiện:

### Bước 1

Xác định Requirement / Use Case / API liên quan.

### Bước 2

Phân tích Scenario.

### Bước 3

Tự xác định các trường hợp kiểm thử có thể phát sinh.

### Bước 4

Đảm bảo coverage:

- Positive
- Negative
- Boundary
- Missing Data
- Error Data

### Bước 5

Tạo khoảng 10–20 Test Case.

### Bước 6

Review Test Case.

### Bước 7

Tạo một Sheet Excel riêng cho Scenario.

### Bước 8

Đưa Test Case vào đúng Template.

### Bước 9

Kiểm tra lại file Excel trước khi hoàn thành.

---

# 14. Khi tôi đưa nhiều Scenario

Nếu tôi cung cấp nhiều Scenario cùng lúc:

```text
Scenario 1: Đặt xe
Scenario 2: Hủy xe
Scenario 3: Thanh toán
```

Tạo:

```text
Excel File
│
├── Sheet: Đặt xe
│   └── 10–20 Test Case
│
├── Sheet: Hủy xe
│   └── 10–20 Test Case
│
└── Sheet: Thanh toán
    └── 10–20 Test Case
```

Mỗi Scenario độc lập.

---

# 15. Review trước khi xuất file

Trước khi hoàn thành file Excel, kiểm tra:

- Test Case có đúng Scenario không?
- Có Test Case nằm ngoài phạm vi Scenario không?
- Có Test Case trùng nhau không?
- Có Positive không?
- Có Negative không?
- Có Boundary nếu áp dụng không?
- Có Missing Data không?
- Có Error Data không?
- Expected Result có kiểm chứng được không?
- Có tự suy diễn requirement không?
- Có tuân thủ SRS không?
- Có tuân thủ API Document không?
- Có đúng Template không?
- Có đúng Sheet tương ứng với Scenario không?
- Có đủ khoảng 10–20 Test Case nếu Scenario cho phép không?

Nếu phát hiện vấn đề, sửa trước khi xuất file.

---

# 16. Output

Sau khi hoàn thành, cung cấp:

### 1. Tóm tắt

```text
Test Scenario: [Tên Scenario]
Số Test Case: [Số lượng]
Sheet: [Tên Sheet]
```

### 2. File Excel

Xuất file `.xlsx` hoàn chỉnh.

Tên file nên có dạng:

```text
TestCase_[Scenario].xlsx
```

Nếu tôi đã có một file Test Case tổng, hãy cập nhật thêm Sheet mới vào file đó thay vì tạo file mới, nếu phù hợp với yêu cầu hiện tại.

Không xuất Test Case dưới dạng bảng Markdown thay cho file Excel nếu tôi đã yêu cầu tạo file Excel.
