Được. Tôi sẽ **sửa theo hướng “BA/DA review để nộp được”**, không phải chỉ sửa câu chữ.

Tôi đã đối chiếu lại bản `srs.md` hiện tại của bạn trên GitHub. Bản hiện tại có nền khá tốt nhưng đang có lỗi quan trọng ở **FR, Use Case, Business Rule, Data Model, NFR và Traceability**; ví dụ FR hiện mới dừng ở FR-01 đến FR-11 nhưng Traceability lại gọi tới FR-20, FR-21; Use Case đang nối trực tiếp các UC thay vì thể hiện rõ `<<include>>/<<extend>>`; tài xế còn bị nối với UC “Tìm tài xế”. ([GitHub](https://github.com/VuUyenThy/23730871_VuUyenThy_Cabsystem/blob/main/srs.md "23730871_VuUyenThy_Cabsystem/srs.md at main · VuUyenThy/23730871_VuUyenThy_Cabsystem · GitHub"))

Tôi đề xuất **không vá từng dòng của bản cũ**, mà chuẩn hóa lại thành cấu trúc dưới đây. Đây là phiên bản tôi sẽ dùng làm **baseline SRS mới**.

---

# SRS – CAB SYSTEM

## Nền tảng đặt xe trực tuyến

### 1. Thông tin dự án

| Thuộc tínhNội dung   |                                         |
| -------------------- | --------------------------------------- |
| Tên dự án            | CAB System – Nền tảng đặt xe            |
| Khách hàng           | Công ty ABC                             |
| Thời gian triển khai | 7 tuần                                  |
| Loại hệ thống        | Nền tảng đặt xe trực tuyến              |
| Người dùng chính     | Khách hàng, Tài xế, Nhân viên vận hành  |
| Người dùng quản trị  | Admin                                   |
| Hệ thống bên ngoài   | Payment Provider, Notification Provider |

---

# B1. BUSINESS CONTEXT & BUSINESS PROBLEM

## 1. Bối cảnh nghiệp vụ

Công ty ABC cung cấp dịch vụ đặt xe trực tuyến. Hiện tại khách hàng có thể yêu cầu xe thông qua tổng đài hoặc ứng dụng hiện có.

Tuy nhiên, quy trình vận hành còn phụ thuộc nhiều vào thao tác thủ công, đặc biệt trong việc tìm và phân công tài xế. Khách hàng chưa có khả năng theo dõi đầy đủ trạng thái chuyến đi, dữ liệu thanh toán chưa được quản lý tập trung và hệ thống hiện tại khó mở rộng khi số lượng khách hàng, tài xế và chuyến đi tăng.

Doanh nghiệp mong muốn xây dựng một **CAB System** mới nhằm tự động hóa quy trình đặt xe, tìm và phân công tài xế, thực hiện chuyến, tính cước, thanh toán, thông báo và đánh giá.

---

## 2. Business Problem

| Vấn đềẢnh hưởng                                       |                                                          |
| ----------------------------------------------------- | -------------------------------------------------------- |
| Phân công tài xế còn thủ công                         | Tốn thời gian và nhân lực                                |
| Khó tìm tài xế phù hợp                                | Khách hàng phải chờ lâu                                  |
| Tài xế từ chối/không phản hồi chưa được xử lý tự động | Khách hàng có thể phải tạo lại yêu cầu                   |
| Khách hàng khó theo dõi chuyến                        | Giảm khả năng kiểm soát và trải nghiệm                   |
| Thanh toán chưa tập trung                             | Khó tra cứu và đối soát                                  |
| Thông báo chưa linh hoạt                              | Thông tin trạng thái có thể không được cập nhật kịp thời |
| Vận hành khó theo dõi chuyến và tài xế                | Khó xử lý sự cố                                          |
| Hệ thống khó mở rộng                                  | Khó phục vụ tải tăng                                     |
| Các thành phần phụ thuộc lẫn nhau                     | Một lỗi có thể ảnh hưởng nhiều chức năng                 |
| Khó tích hợp provider mới                             | Khó phát triển trong tương lai                           |

---

# B2. BUSINESS GOALS

## BG-01 – Tự động hóa đặt xe

Tự động hóa quy trình:

> Đặt chuyến → Tìm tài xế → Phân công → Thực hiện chuyến → Tính cước → Thanh toán → Đánh giá.

## BG-02 – Nâng cao trải nghiệm khách hàng

Khách hàng có thể:

- đăng ký/đăng nhập;
- đặt chuyến;
- biết hệ thống đang tìm tài xế;
- biết tài xế đã nhận chuyến;
- xem ETA;
- theo dõi trạng thái chuyến;
- xem cước;
- thanh toán;
- xem lịch sử;
- đánh giá tài xế.

## BG-03 – Tăng hiệu quả vận hành

Nhân viên vận hành có thể:

- quản lý khách hàng;
- quản lý tài xế;
- quản lý phương tiện;
- theo dõi chuyến;
- xử lý chuyến lỗi;
- tra cứu giao dịch;
- xem báo cáo.

## BG-04 – Đảm bảo khả năng mở rộng

Hệ thống có khả năng mở rộng:

- khách hàng;
- tài xế;
- chuyến;
- dịch vụ;
- payment provider;
- notification provider;
- notification channel.

## BG-05 – Đảm bảo bảo mật và ổn định

Hệ thống phải:

- xác thực người dùng;
- phân quyền;
- bảo vệ dữ liệu;
- lưu audit log;
- cô lập lỗi giữa các thành phần quan trọng.

---

# B3. STAKEHOLDERS & ACTORS

## 1. Stakeholder

| StakeholderVai trò     |                                                 |
| ---------------------- | ----------------------------------------------- |
| Ban giám đốc           | Quyết định mục tiêu và chính sách nghiệp vụ     |
| Khách hàng             | Người đặt và sử dụng chuyến                     |
| Tài xế                 | Người nhận và thực hiện chuyến                  |
| Nhân viên vận hành     | Quản lý và hỗ trợ hoạt động                     |
| Admin                  | Quản lý quyền và các thao tác quản trị nhạy cảm |
| Payment Provider       | Xử lý thanh toán điện tử                        |
| Notification Provider  | Gửi thông báo                                   |
| BA                     | Phân tích và làm rõ yêu cầu                     |
| Development Team       | Xây dựng hệ thống                               |
| IT/Technical Operation | Vận hành kỹ thuật                               |

### Lưu ý BA

**BA và Development Team không phải Business Actor của hệ thống.**

Trong Use Case Diagram, chỉ đưa các actor tương tác trực tiếp với hệ thống.

---

# B4. SCOPE & MVP

Do thời gian dự án chỉ **7 tuần**, cần phân biệt rõ chức năng MVP và chức năng mở rộng.

## 1. In Scope – MVP

### Customer

- Đăng ký
- Đăng nhập
- Cập nhật thông tin
- Đặt chuyến
- Theo dõi chuyến
- Xem cước
- Thanh toán
- Xem lịch sử chuyến
- Đánh giá tài xế
- Nhận thông báo

### Driver

- Đăng nhập
- Cập nhật hồ sơ
- Quản lý phương tiện
- Chuyển trạng thái sẵn sàng/không sẵn sàng
- Nhận yêu cầu chuyến
- Chấp nhận/từ chối
- Cập nhật trạng thái chuyến
- Cập nhật vị trí
- Nhận thông báo

### Operator

- Quản lý khách hàng
- Quản lý tài xế
- Quản lý phương tiện
- Theo dõi chuyến
- Xử lý chuyến lỗi
- Tra cứu giao dịch

### Admin

- Quản lý tài khoản
- Phân quyền
- Quản lý role/permission
- Xem audit log

### Business/Reporting

- Số lượng chuyến
- Doanh thu
- Tỷ lệ hoàn thành
- Tỷ lệ hủy
- Hiệu quả tài xế

---

# B5. BUSINESS REQUIREMENTS

Tôi khuyên bạn **đổi toàn bộ BR cũ thành bộ mã dưới đây** để tránh trùng mã với Business Rule.

| IDBusiness Requirement |                                     |
| ---------------------- | ----------------------------------- |
| BR-01                  | Quản lý tài khoản khách hàng        |
| BR-02                  | Quản lý tài khoản tài xế            |
| BR-03                  | Đặt chuyến                          |
| BR-04                  | Tìm tài xế phù hợp                  |
| BR-05                  | Phân công tài xế                    |
| BR-06                  | Xử lý tài xế từ chối/không phản hồi |
| BR-07                  | Theo dõi chuyến                     |
| BR-08                  | Quản lý trạng thái chuyến           |
| BR-09                  | Cập nhật vị trí tài xế              |
| BR-10                  | Tính cước                           |
| BR-11                  | Thanh toán                          |
| BR-12                  | Xử lý thanh toán thất bại           |
| BR-13                  | Thông báo                           |
| BR-14                  | Quản lý lịch sử                     |
| BR-15                  | Đánh giá tài xế                     |
| BR-16                  | Quản lý vận hành                    |
| BR-17                  | Quản lý phương tiện                 |
| BR-18                  | Xử lý chuyến lỗi                    |
| BR-19                  | Báo cáo                             |
| BR-20                  | Phân quyền và bảo mật               |
| BR-21                  | Audit log                           |
| BR-22                  | Khả năng mở rộng và tích hợp        |

### Điểm quan trọng

Tôi **không đưa Hủy chuyến vào BR như một requirement đã được chốt**, vì đề bài nói rõ chính sách hủy **chưa được doanh nghiệp xác nhận**.

Thay vào đó:

> **Cancellation = Open Business Requirement / TBD**

Đây là cách làm BA đúng hơn là tự bịa chính sách.

---

# B6. BUSINESS PROCESS

## Quy trình chính

```text
Khách hàng đăng nhập
        ↓
Nhập điểm đón + điểm đến
        ↓
Chọn loại xe
        ↓
Tạo yêu cầu chuyến
        ↓
Hệ thống tiếp nhận
        ↓
Tìm tài xế phù hợp
        ↓
Có tài xế?
   ┌────┴────┐
  Không      Có
   ↓          ↓
Thông báo   Phân công
không có       ↓
tài xế      Gửi request
               ↓
       Tài xế phản hồi?
          ┌────┴────┐
        Reject    Accept
          ↓          ↓
     Tìm TX khác   Gán TX
                     ↓
              TX đến điểm đón
                     ↓
              Đã đến điểm đón
                     ↓
                Đón khách
                     ↓
              Đang di chuyển
                     ↓
                Hoàn thành
                     ↓
                 Tính cước
                     ↓
              Thanh toán
                     ↓
                Thông báo
                     ↓
              Đánh giá TX
```

---

# B7. FUNCTIONAL REQUIREMENTS

Đây là phần cần sửa mạnh nhất so với GitHub hiện tại.

## 7.1 Authentication & Account

| IDChức năng |                              |
| ----------- | ---------------------------- |
| FR-01       | Đăng ký tài khoản khách hàng |
| FR-02       | Đăng nhập                    |
| FR-03       | Đăng xuất                    |
| FR-04       | Cập nhật thông tin cá nhân   |
| FR-05       | Quản lý tài khoản tài xế     |

---

## 7.2 Booking

| IDChức năng |                        |
| ----------- | ---------------------- |
| FR-06       | Nhập điểm đón          |
| FR-07       | Nhập điểm đến          |
| FR-08       | Lựa chọn loại xe       |
| FR-09       | Tạo yêu cầu đặt chuyến |
| FR-10       | Xem thông tin chuyến   |

---

## 7.3 Driver Matching & Assignment

| IDChức năng |                                       |
| ----------- | ------------------------------------- |
| FR-11       | Xác định tài xế phù hợp               |
| FR-12       | Lọc tài xế theo trạng thái            |
| FR-13       | Lọc tài xế theo loại xe               |
| FR-14       | Tính khoảng cách/ETA                  |
| FR-15       | Ưu tiên tài xế theo tiêu chí vận hành |
| FR-16       | Gửi yêu cầu chuyến cho tài xế         |
| FR-17       | Tiếp tục tìm tài xế khi bị từ chối    |
| FR-18       | Tiếp tục tìm tài xế khi timeout       |
| FR-19       | Thông báo không tìm được tài xế       |

**Lưu ý:** tiêu chí ưu tiên cụ thể là **TBD**.

---

# 7.4 Driver

| IDChức năng |                               |
| ----------- | ----------------------------- |
| FR-20       | Cập nhật trạng thái sẵn sàng  |
| FR-21       | Nhận thông báo chuyến mới     |
| FR-22       | Chấp nhận chuyến              |
| FR-23       | Từ chối chuyến                |
| FR-24       | Cập nhật trạng thái chuyến    |
| FR-25       | Cập nhật vị trí               |
| FR-26       | Quản lý thông tin phương tiện |

---

# 7.5 Trip Tracking

| IDChức năng |                               |
| ----------- | ----------------------------- |
| FR-27       | Hiển thị trạng thái chuyến    |
| FR-28       | Hiển thị thông tin tài xế     |
| FR-29       | Hiển thị ETA                  |
| FR-30       | Hiển thị vị trí tài xế        |
| FR-31       | Lưu lịch sử trạng thái chuyến |

---

# 7.6 Fare

| IDChức năng |                                  |
| ----------- | -------------------------------- |
| FR-32       | Xác định cước chuyến             |
| FR-33       | Hiển thị số tiền phải thanh toán |
| FR-34       | Lưu thông tin cước               |

**Công thức cụ thể: TBD.**

---

# 7.7 Payment

| IDChức năng |                                    |
| ----------- | ---------------------------------- |
| FR-35       | Thanh toán tiền mặt                |
| FR-36       | Thanh toán điện tử                 |
| FR-37       | Gửi giao dịch đến Payment Provider |
| FR-38       | Nhận kết quả thanh toán            |
| FR-39       | Xử lý thanh toán thất bại          |
| FR-40       | Cho phép retry theo chính sách     |
| FR-41       | Lưu lịch sử giao dịch              |

CAB **không lưu thông tin nhạy cảm của thẻ/tài khoản thanh toán**.

---

# 7.8 Notification

| IDChức năng |                                     |
| ----------- | ----------------------------------- |
| FR-42       | Thông báo tiếp nhận yêu cầu         |
| FR-43       | Thông báo tài xế nhận chuyến        |
| FR-44       | Thông báo tài xế đến                |
| FR-45       | Thông báo hoàn thành                |
| FR-46       | Thông báo kết quả thanh toán        |
| FR-47       | Thông báo chuyến mới cho tài xế     |
| FR-48       | Retry notification khi gửi thất bại |

Thiết kế phải cho phép thêm notification channel/provider trong tương lai.

---

# 7.9 History & Rating

| IDChức năng |                                     |
| ----------- | ----------------------------------- |
| FR-49       | Xem lịch sử chuyến                  |
| FR-50       | Xem thông tin thanh toán của chuyến |
| FR-51       | Đánh giá tài xế                     |
| FR-52       | Lưu đánh giá                        |

Chỉ cho đánh giá đối với chuyến đã hoàn thành.

---

# 7.10 Operator

| IDChức năng |                         |
| ----------- | ----------------------- |
| FR-53       | Xem khách hàng          |
| FR-54       | Quản lý khách hàng      |
| FR-55       | Xem tài xế              |
| FR-56       | Quản lý tài xế          |
| FR-57       | Quản lý phương tiện     |
| FR-58       | Xem chuyến đang diễn ra |
| FR-59       | Tra cứu chuyến          |
| FR-60       | Xử lý chuyến lỗi        |
| FR-61       | Tra cứu giao dịch       |

---

# 7.11 Admin

| IDChức năng |                          |
| ----------- | ------------------------ |
| FR-62       | Quản lý tài khoản nội bộ |
| FR-63       | Quản lý role             |
| FR-64       | Quản lý permission       |
| FR-65       | Xem audit log            |

---

# 7.12 Reporting

| IDChức năng |                          |
| ----------- | ------------------------ |
| FR-66       | Báo cáo số lượng chuyến  |
| FR-67       | Báo cáo doanh thu        |
| FR-68       | Báo cáo tỷ lệ hoàn thành |
| FR-69       | Báo cáo tỷ lệ hủy        |
| FR-70       | Báo cáo hiệu quả tài xế  |

---

# B8. BUSINESS RULES

Tôi khuyên bạn **tách mã Business Rule khỏi Business Requirement**.

| IDBusiness Rule |                                                                                        |
| --------------- | -------------------------------------------------------------------------------------- |
| RULE-01         | Chỉ tài xế có trạng thái sẵn sàng mới được xem xét phân công                           |
| RULE-02         | Tài xế phải phù hợp với loại xe khách hàng yêu cầu                                     |
| RULE-03         | Tài xế không phản hồi trong thời gian quy định sẽ được xem là timeout                  |
| RULE-04         | Tài xế từ chối/timeout thì hệ thống tiếp tục tìm tài xế khác                           |
| RULE-05         | Nếu không còn tài xế phù hợp, chuyến được chuyển sang trạng thái không tìm được tài xế |
| RULE-06         | Một chuyến chỉ được gán cho một tài xế tại một thời điểm                               |
| RULE-07         | Chỉ tài xế được gán mới được cập nhật trạng thái chuyến                                |
| RULE-08         | Trạng thái chuyến phải tuân thủ thứ tự nghiệp vụ                                       |
| RULE-09         | Chỉ chuyến hoàn thành mới được tính cước cuối cùng                                     |
| RULE-10         | Thanh toán điện tử phải được xử lý thông qua Payment Provider                          |
| RULE-11         | CAB không lưu dữ liệu nhạy cảm của phương thức thanh toán                              |
| RULE-12         | Thanh toán thất bại không làm dừng quy trình đặt xe                                    |
| RULE-13         | Chỉ chuyến hoàn thành mới cho phép đánh giá                                            |
| RULE-14         | Chỉ actor có quyền phù hợp mới được thực hiện thao tác quản trị                        |
| RULE-15         | Mọi thao tác quản trị quan trọng phải được ghi audit log                               |

---

# B9. TRIP STATUS

Phần này **bắt buộc phải có**.

```text
REQUESTED
    ↓
SEARCHING_DRIVER
    ↓
DRIVER_ASSIGNED
    ↓
DRIVER_ARRIVING
    ↓
DRIVER_ARRIVED
    ↓
PASSENGER_PICKED_UP
    ↓
IN_PROGRESS
    ↓
COMPLETED
```

Ngoài ra có trạng thái kết thúc/ngoại lệ:

```text
NO_DRIVER
CANCELLED
```

`CANCELLED` hiện là **TBD – chờ khách hàng xác nhận chính sách hủy**.

Không cho phép chuyển tùy ý, ví dụ:

```text
REQUESTED → COMPLETED
```

phải bị từ chối.

---

# B10. EXCEPTION / ERROR HANDLING

| IDNgoại lệXử lý |                              |                                                          |
| --------------- | ---------------------------- | -------------------------------------------------------- |
| EX-01           | Không có tài xế              | Thông báo khách hàng                                     |
| EX-02           | Driver reject                | Tìm driver khác                                          |
| EX-03           | Driver timeout               | Tìm driver khác                                          |
| EX-04           | Payment failed               | Thông báo + retry theo policy                            |
| EX-05           | Notification failed          | Retry, không dừng trip                                   |
| EX-06           | Payment Provider unavailable | Ghi nhận lỗi, không làm sập booking                      |
| EX-07           | Mất kết nối driver           | Đồng bộ lại khi kết nối khôi phục                        |
| EX-08           | Hai driver cùng accept       | Hệ thống phải đảm bảo chỉ một assignment thành công      |
| EX-09           | Request trùng                | Không tạo duplicate trip                                 |
| EX-10           | API retry                    | Phải hỗ trợ cơ chế idempotency đối với operation phù hợp |

---

# B11. DATA MODEL

Tôi sẽ sửa mô hình hiện tại của bạn.

## Entity chính

### Customer

```text
Customer
- CustomerID
- FullName
- Phone
- Email
- PasswordHash
- Address
- Status
- CreatedAt
```

### Driver

```text
Driver
- DriverID
- FullName
- Phone
- Email
- PasswordHash
- Status
- AvailabilityStatus
- CurrentLatitude
- CurrentLongitude
- CreatedAt
```

### Vehicle

```text
Vehicle
- VehicleID
- DriverID
- VehicleType
- LicensePlate
- Brand
- Model
- Status
```

### Trip

```text
Trip
- TripID
- CustomerID
- DriverID
- VehicleID
- PickupLocation
- Destination
- VehicleType
- Status
- RequestedAt
- AssignedAt
- StartedAt
- CompletedAt
- Fare
```

### DriverAssignment

Tôi **khuyên bổ sung entity này**.

```text
DriverAssignment
- AssignmentID
- TripID
- DriverID
- OfferedAt
- RespondedAt
- Response
- Status
```

Entity này giải quyết được:

> driver A reject → driver B reject → driver C accept.

Nếu chỉ lưu `Trip.DriverID`, bạn mất lịch sử quá trình matching.

---

### PaymentTransaction

```text
PaymentTransaction
- PaymentID
- TripID
- Amount
- Method
- Status
- ProviderTransactionID
- AttemptNumber
- CreatedAt
- CompletedAt
```

Quan hệ:

```text
Trip 1 ---- N PaymentTransaction
```

---

### Rating

```text
Rating
- RatingID
- TripID
- CustomerID
- DriverID
- Rating
- Comment
- CreatedAt
```

---

### Notification

```text
Notification
- NotificationID
- RecipientID
- TripID
- Type
- Channel
- Content
- Status
- SentAt
```

---

### AuditLog

```text
AuditLog
- AuditLogID
- ActorID
- Action
- EntityType
- EntityID
- Timestamp
- Result
```

---

# B12. CARDINALITY

Các quan hệ quan trọng:

```text
Customer 1 ──── N Trip

Driver 1 ──── N Trip

Driver 1 ──── N Vehicle

Trip 1 ──── N DriverAssignment

Trip 1 ──── N PaymentTransaction

Trip 1 ──── 0..1 Rating

Trip 1 ──── N Notification
```

Đây hợp lý hơn mô hình cũ của bạn, đặc biệt vì bản hiện tại đang để **Driver 1–1 Vehicle** và **Trip 1–1 Payment**, trong khi nghiệp vụ retry payment và lịch sử assignment cần lưu nhiều record. ([GitHub](https://github.com/VuUyenThy/23730871_VuUyenThy_Cabsystem/blob/main/srs.md "23730871_VuUyenThy_Cabsystem/srs.md at main · VuUyenThy/23730871_VuUyenThy_Cabsystem · GitHub"))

---

# B13. NON-FUNCTIONAL REQUIREMENTS

Không nên tự bịa SLA khi khách hàng chưa cung cấp.

Vì vậy tôi sẽ viết theo kiểu **Requirement + TBD**.

| IDNhómRequirement |                 |                                                                                    |
| ----------------- | --------------- | ---------------------------------------------------------------------------------- |
| NFR-01            | Performance     | Hệ thống phải đáp ứng tải tăng cao và duy trì khả năng xử lý các chức năng cốt lõi |
| NFR-02            | Scalability     | Các thành phần có thể mở rộng độc lập khi tải tăng                                 |
| NFR-03            | Availability    | Lỗi Payment/Notification không được làm dừng toàn bộ booking                       |
| NFR-04            | Security        | Các chức năng yêu cầu tài khoản phải xác thực                                      |
| NFR-05            | Authorization   | Chức năng quản trị phải kiểm soát quyền                                            |
| NFR-06            | Data Protection | Dữ liệu cá nhân, vị trí và giao dịch phải được bảo vệ                              |
| NFR-07            | Auditability    | Các thao tác quan trọng phải được ghi log                                          |
| NFR-08            | Maintainability | Có thể thay đổi/thêm component mà hạn chế ảnh hưởng component khác                 |
| NFR-09            | Integration     | Có thể tích hợp Payment Provider và Notification Provider                          |
| NFR-10            | Fault Isolation | Lỗi ở một thành phần không được lan truyền làm hệ thống ngừng hoạt động            |

### Các thông số cần khách hàng xác nhận

```text
TBD-01 Peak concurrent users
TBD-02 Peak trips/hour
TBD-03 API response time
TBD-04 Availability/SLA
TBD-05 RTO
TBD-06 RPO
TBD-07 Driver location update frequency
TBD-08 Data retention period
```

Đây là cách tốt hơn việc tự ghi “500ms”, “99.9%” khi khách hàng chưa yêu cầu.

---

# B14. USE CASE

Tôi sẽ **sửa lại hoàn toàn Use Case Diagram hiện tại**.

## Customer

- UC-01 Đăng ký
- UC-02 Đăng nhập
- UC-03 Quản lý hồ sơ
- UC-04 Đặt chuyến
- UC-05 Theo dõi chuyến
- UC-06 Thanh toán
- UC-07 Xem lịch sử chuyến
- UC-08 Đánh giá tài xế

## Driver

- UC-09 Đăng nhập
- UC-10 Quản lý hồ sơ
- UC-11 Quản lý trạng thái sẵn sàng
- UC-12 Nhận yêu cầu chuyến
- UC-13 Chấp nhận chuyến
- UC-14 Từ chối chuyến
- UC-15 Cập nhật trạng thái chuyến
- UC-16 Cập nhật vị trí
- UC-17 Quản lý phương tiện

## Operator

- UC-18 Quản lý khách hàng
- UC-19 Quản lý tài xế
- UC-20 Quản lý phương tiện
- UC-21 Theo dõi chuyến
- UC-22 Xử lý chuyến lỗi
- UC-23 Tra cứu giao dịch

## Admin

- UC-24 Quản lý tài khoản nội bộ
- UC-25 Phân quyền
- UC-26 Xem Audit Log

## Management

- UC-27 Xem báo cáo

---

# B15. INCLUDE / EXTEND

Đây là chỗ bản hiện tại của bạn cần sửa rõ nhất.

### Đặt chuyến

```text
UC-04 Đặt chuyến
      |
      +-- <<include>> Tìm tài xế
      |
      +-- <<include>> Phân công tài xế
```

### Tìm tài xế

```text
UC-04 Đặt chuyến
       |
       +-- <<include>> UC-Tìm tài xế
```

Nếu driver reject:

```text
Tìm tài xế
     |
     +-- <<extend>> Xử lý tài xế từ chối
```

Nhưng cần lưu ý: **không lạm dụng** **`extend`**. Trong trường hợp hệ thống luôn phải xử lý reject/timeout như một phần của matching, có thể đặc tả trong alternative flow của UC tìm/phân công tài xế thay vì tạo quá nhiều UC con.

---

# B16. CÁC OPEN BUSINESS QUESTIONS

Đây là phần tôi muốn bạn giữ lại, vì đề bài **cố tình đưa các điểm chưa chốt**.

| IDVấn đề cần xác nhậnTrạng thái |                                |     |
| ------------------------------- | ------------------------------ | --- |
| OQ-01                           | Công thức tính cước            | TBD |
| OQ-02                           | Tiêu chí ưu tiên tài xế        | TBD |
| OQ-03                           | Thời gian driver phải phản hồi | TBD |
| OQ-04                           | Chính sách hủy chuyến          | TBD |
| OQ-05                           | Phí hủy chuyến                 | TBD |
| OQ-06                           | Số lần retry payment           | TBD |
| OQ-07                           | Xử lý mất mạng                 | TBD |
| OQ-08                           | Tần suất cập nhật vị trí       | TBD |
| OQ-09                           | Thời gian lưu trữ dữ liệu      | TBD |
| OQ-10                           | SLA/Availability               | TBD |
| OQ-11                           | Peak load                      | TBD |
| OQ-12                           | Chính sách xử lý chuyến lỗi    | TBD |

**Đây không phải thiếu sót của BA.**

Ngược lại:

> **BA ghi nhận TBD và đưa câu hỏi đến Business Owner mới là đúng.**

---

# B17. ACCEPTANCE CRITERIA

Tôi sẽ không giữ 12 AC cũ vì nó chưa phủ hết requirement. Bản mới:

| IDAcceptance Criteria |                                                                    |
| --------------------- | ------------------------------------------------------------------ |
| AC-01                 | Customer đăng ký thành công với dữ liệu hợp lệ                     |
| AC-02                 | User đăng nhập thành công với thông tin hợp lệ                     |
| AC-03                 | Customer tạo được trip với pickup, destination và vehicle type     |
| AC-04                 | Hệ thống chuyển trip sang trạng thái tìm tài xế                    |
| AC-05                 | Hệ thống chỉ xem xét driver phù hợp                                |
| AC-06                 | Driver nhận được request và có thể accept/reject                   |
| AC-07                 | Driver reject/timeout thì hệ thống tìm driver khác                 |
| AC-08                 | Không có driver thì customer nhận được thông báo                   |
| AC-09                 | Customer xem được driver và trạng thái trip                        |
| AC-10                 | Driver cập nhật được trạng thái theo đúng thứ tự                   |
| AC-11                 | Hệ thống tính được fare theo policy đã cấu hình                    |
| AC-12                 | Customer thanh toán được bằng cash/electronic                      |
| AC-13                 | Payment failure được xử lý mà không làm dừng booking               |
| AC-14                 | Customer xem được trip history                                     |
| AC-15                 | Customer đánh giá được driver sau completed trip                   |
| AC-16                 | Customer/Driver nhận được notification cần thiết                   |
| AC-17                 | Operator quản lý được customer/driver/vehicle/trip                 |
| AC-18                 | Operator xử lý được trip exception theo quyền                      |
| AC-19                 | Admin quản lý role/permission                                      |
| AC-20                 | Hệ thống ghi audit log cho thao tác quan trọng                     |
| AC-21                 | Báo cáo hiển thị đúng các chỉ số đã thống nhất                     |
| AC-22                 | Payment/Notification failure không làm toàn bộ booking system dừng |

---

# B18. TRACEABILITY MATRIX

Đây là phần phải sửa hoàn toàn.

Ví dụ:

| BRFRUCAC |          |                      |              |
| -------- | -------- | -------------------- | ------------ |
| BR-01    | FR-01–05 | UC-01–03             | AC-01, AC-02 |
| BR-03    | FR-06–10 | UC-04                | AC-03        |
| BR-04    | FR-11–15 | Tìm tài xế           | AC-04, AC-05 |
| BR-05    | FR-16    | Phân công            | AC-06        |
| BR-06    | FR-17–18 | Xử lý reject/timeout | AC-07        |
| BR-07    | FR-27–31 | UC-05                | AC-09, AC-10 |
| BR-09    | FR-32–34 | Tính cước            | AC-11        |
| BR-11    | FR-35–41 | UC-06                | AC-12, AC-13 |
| BR-13    | FR-42–48 | Notification         | AC-16        |
| BR-14    | FR-49–50 | History              | AC-14        |
| BR-15    | FR-51–52 | Rating               | AC-15        |
| BR-16    | FR-53–61 | Operator UCs         | AC-17, AC-18 |
| BR-20    | FR-62–65 | Admin UCs            | AC-19, AC-20 |
| BR-19    | FR-66–70 | UC-27                | AC-21        |

Điểm quan trọng:

> **Không được xuất hiện FR-20/FR-21 trong Traceability nếu FR-20/FR-21 không tồn tại.**

Bản GitHub hiện tại đang mắc đúng lỗi này. ([GitHub](https://github.com/VuUyenThy/23730871_VuUyenThy_Cabsystem/blob/main/srs.md "23730871_VuUyenThy_Cabsystem/srs.md at main · VuUyenThy/23730871_VuUyenThy_Cabsystem · GitHub"))

---

# B19. API TRACEABILITY

Đây là phần tôi muốn bạn thêm để SRS và API không bị tách rời.

Ví dụ:

| RequirementAPI capability |                     |
| ------------------------- | ------------------- |
| FR-02 Login               | `/auth/login`       |
| FR-09 Create Trip         | `/trips`            |
| FR-16 Driver Assignment   | Assignment service  |
| FR-22 Accept Trip         | Driver trip API     |
| FR-23 Reject Trip         | Driver trip API     |
| FR-25 Driver Location     | Driver location API |
| FR-32 Fare                | Fare API            |
| FR-36 Electronic Payment  | Payment API         |
| FR-39 Payment Failure     | Payment API         |
| FR-49 Trip History        | Trip history API    |
| FR-51 Rating              | Rating API          |
| FR-42–48 Notification     | Notification API    |

**Không nhất thiết mọi FR phải có một endpoint riêng.**

Ví dụ:

> `FR-17 Xử lý driver reject`

có thể là **business logic bên server**, không nhất thiết có endpoint `/find-next-driver`.

---

# B20. KẾT LUẬN PHIÊN BẢN SRS MỚI

Với bản sửa này, cấu trúc logic sẽ trở thành:

```text
BUSINESS PROBLEM
       ↓
BUSINESS GOALS
       ↓
STAKEHOLDERS
       ↓
BUSINESS REQUIREMENTS
       ↓
BUSINESS PROCESS
       ↓
FUNCTIONAL REQUIREMENTS
       ↓
BUSINESS RULES
       ↓
EXCEPTIONS
       ↓
DATA MODEL
       ↓
NON-FUNCTIONAL REQUIREMENTS
       ↓
USE CASE
       ↓
ACCEPTANCE CRITERIA
       ↓
TRACEABILITY
       ↓
API TRACEABILITY
```

Đây là cấu trúc **chặt hơn đáng kể so với file hiện tại**. Bản hiện tại của bạn đã có hầu hết các “khối” này, nhưng nhiều khối chưa đồng bộ với nhau. ([GitHub](https://github.com/VuUyenThy/23730871_VuUyenThy_Cabsystem/blob/main/srs.md "23730871_VuUyenThy_Cabsystem/srs.md at main · VuUyenThy/23730871_VuUyenThy_Cabsystem · GitHub"))

### Những gì tôi đã chủ động sửa

- Không để `Driver → Tìm tài xế`.
- Tách **matching → assignment → driver response**.
- Bổ sung **DriverAssignment**.
- Sửa `Driver 1–1 Vehicle` thành `Driver 1–N Vehicle`.
- Sửa mô hình payment để hỗ trợ retry/history.
- Bổ sung lịch sử, rating, notification, vehicle, operator, admin, reporting.
- Bổ sung trip state machine.
- Bổ sung cancellation dưới dạng **TBD**, không tự bịa policy.
- Bổ sung Open Questions.
- Sửa cách quản lý Business Rule.
- Làm lại FR thành một hệ thống có mã liên tục.
- Làm lại Acceptance Criteria.
- Làm lại Traceability.
- Bổ sung liên kết **SRS → API**.
- Không tự đặt các con số SLA khi khách hàng chưa cung cấp.

**Tôi sẽ lấy phiên bản này làm baseline để sửa tiếp từng UC và API, thay vì tiếp tục vá file cũ.** Đặc biệt, bước tiếp theo nên là **đặc tả chi tiết các UC-04 Đặt chuyến, Tìm & phân công tài xế, Nhận/Từ chối chuyến, Theo dõi chuyến, Thanh toán và Xử lý chuyến lỗi**, vì đây là lõi nghiệp vụ của CAB System.