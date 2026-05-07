# Hệ Thống Quản Lý Nhà Hàng

Ứng dụng web hỗ trợ quản lý nhà hàng, gọi món và thanh toán theo mô hình POS. Dự án được xây dựng bằng Spring Boot, Thymeleaf và MySQL, phù hợp cho các bài tập lớn môn học hoặc demo hệ thống quản lý nhà hàng cơ bản.

## Mục tiêu dự án

- Quản lý thực đơn món ăn.
- Quản lý bàn và trạng thái bàn trong nhà hàng.
- Quản lý nhân viên theo vai trò.
- Hỗ trợ đăng nhập và phân quyền.
- Hỗ trợ mở bàn, gọi món, cập nhật số lượng món, xóa món và thanh toán.
- Hỗ trợ khách hàng tự xem menu và đặt món từ giao diện riêng.

## Công nghệ sử dụng

- Java 21
- Spring Boot 4
- Spring Web MVC
- Spring Data JPA
- Spring Security
- Thymeleaf
- MySQL
- JWT Authentication
- HTML, CSS, JavaScript
- Maven

## Chức năng chính

### 1. Xác thực và phân quyền

- Đăng nhập bằng tài khoản hệ thống.
- Sinh JWT sau khi đăng nhập.
- Phân quyền theo vai trò `ADMIN` và `STAFF`.

### 2. Quản lý món ăn

- Thêm món ăn mới.
- Cập nhật thông tin món ăn.
- Xóa món ăn.
- Xem danh sách món ăn.
- Thống kê top 5 món ăn bán chạy.

### 3. Quản lý nhân viên

- Xem danh sách nhân viên.
- Thêm nhân viên mới.
- Cập nhật thông tin nhân viên.
- Xóa nhân viên.

### 4. Quản lý bàn và gọi món

- Xem danh sách bàn.
- Mở bàn khi có khách.
- Gọi món theo hóa đơn.
- Cập nhật số lượng món trong hóa đơn.
- Xóa món khỏi hóa đơn.
- Xem danh sách hóa đơn và chi tiết hóa đơn.
- Thanh toán hóa đơn.

### 5. Giao diện khách hàng

- Xem thực đơn đang phục vụ.
- Xem danh sách bàn.
- Đặt món trực tiếp cho bàn đã chọn.
- Xem hóa đơn tạm tính của bàn.

## Giao diện hiện có

Dự án đang có sẵn các trang giao diện:

- `/` : Trang chủ
- `/login` : Trang đăng nhập
- `/admin` : Trang quản trị
- `/cashier` : Trang thu ngân / nhân viên
- `/order` : Trang khách hàng đặt món

## Cấu trúc thư mục

```text
src/
├── main/
│   ├── java/com/restaurant/
│   │   ├── config/
│   │   ├── controller/
│   │   ├── dto/
│   │   ├── entity/
│   │   ├── exception/
│   │   ├── repository/
│   │   └── service/
│   └── resources/
│       ├── static/
│       │   ├── css/
│       │   └── js/
│       ├── templates/
│       └── application.yaml
└── test/
```

## Yêu cầu môi trường

- JDK 21
- Maven 3.9+
- MySQL Server 8+

## Cách chạy dự án

### 1. Clone source code

```bash
git clone <repo-url>
cd lt_web_ptit
```

### 2. Tạo database MySQL

Ứng dụng hiện được cấu hình để kết nối tới database:

```text
restaurant_db
```

Bạn có thể tạo trước database hoặc để ứng dụng tự tạo bằng cấu hình:

```yaml
createDatabaseIfNotExist=true
```

### 3. Cập nhật cấu hình kết nối

Chỉnh sửa file `src/main/resources/application.yaml`:

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/restaurant_db?createDatabaseIfNotExist=true
    username: your_username
    password: your_password
```

Khuyến nghị không commit tài khoản hoặc mật khẩu thật lên GitHub công khai.

### 4. Chạy ứng dụng

Nếu dùng Maven Wrapper:

```bash
./mvnw spring-boot:run
```

Trên Windows:

```bash
mvnw.cmd spring-boot:run
```

Hoặc build rồi chạy:

```bash
./mvnw clean package
java -jar target/*.jar
```

### 5. Truy cập hệ thống

Sau khi chạy thành công, mở trình duyệt tại:

```text
http://localhost:8080
```

## Một số API tiêu biểu

### Xác thực

- `POST /api/auth/login`
- `POST /api/auth/logout`

### Quản lý món ăn

- `GET /api/admin/menu`
- `POST /api/admin/menu`
- `PUT /api/admin/menu/{id}`
- `DELETE /api/admin/menu/{id}`
- `GET /api/admin/menu/top-5`

### Quản lý nhân viên

- `GET /api/nhan-vien`
- `POST /api/nhan-vien`
- `PUT /api/nhan-vien/{id}`
- `DELETE /api/nhan-vien/{id}`

### POS / Thu ngân

- `GET /api/pos/ban`
- `POST /api/pos/mo-ban/{banId}`
- `POST /api/pos/goi-mon`
- `POST /api/pos/cap-nhat-so-luong`
- `DELETE /api/pos/xoa-mon/{cthdId}`
- `POST /api/pos/thanh-toan/{hoaDonId}`
- `GET /api/pos/hoa-don`
- `GET /api/pos/hoa-don/{hoaDonId}`

### Khách hàng

- `GET /api/customer/menu`
- `GET /api/customer/ban`
- `POST /api/customer/order/{banId}`
- `GET /api/customer/hoa-don/{banId}`

## Điểm nổi bật của dự án

- Có cả luồng quản trị, nhân viên và khách hàng.
- Tách rõ `controller`, `service`, `repository`, `entity`.
- Có sử dụng `Spring Security` và `JWT`.
- Có giao diện web bằng `Thymeleaf` thay vì chỉ cung cấp REST API.

## Hướng phát triển thêm

- Bổ sung upload ảnh món ăn.
- Thêm tìm kiếm, lọc và phân trang danh sách món ăn.
- Bổ sung dashboard thống kê doanh thu theo ngày/tháng.
- Gửi đơn hàng theo thời gian thực cho khu vực bếp.
- Triển khai Docker để chạy thuận tiện hơn.
- Bổ sung test cho service và controller.

## Tác giả

Bạn có thể cập nhật phần này bằng tên, lớp, mã sinh viên hoặc nhóm thực hiện của mình trước khi đưa lên GitHub.

## Giấy phép

Hiện dự án chưa khai báo license. Nếu cần public repo, bạn có thể thêm `MIT License` hoặc license phù hợp với mục đích sử dụng.
