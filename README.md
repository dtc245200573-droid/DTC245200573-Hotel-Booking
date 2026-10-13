# Hệ Thống Đặt Phòng Khách Sạn (Đề Tài 6)

Kho lưu trữ: `DTC245200573-Hotel-Booking`  
Môn học: **Triển khai và Quản trị Hệ thống Phần mềm**  
Sinh viên thực hiện: **Lý Kiều Trang**  
Mã số sinh viên (MSSV): **DTC245200573**  
Lớp: **CNTT K23C**  

---

## 1. Giới thiệu hệ thống
Dự án xây dựng và triển khai hệ thống quản lý **Đặt phòng Khách sạn** (quản lý thông tin loại phòng, trạng thái phòng trống, danh sách đặt chỗ và quản lý khách hàng) chuẩn hóa hạ tầng DevOps/Containerization. 

Hệ thống bao gồm các thành phần:
- **Ứng dụng Web & CSDL**: Python/Django (hoặc Node.js) kết hợp **PostgreSQL** và **pgAdmin**.
- **Cổng kết nối**: **Nginx Reverse Proxy** bảo mật HTTPS (SSL tự ký) và HTTP Security Headers.
- **Giám sát Metrics**: **Prometheus + Grafana** (theo dõi tài nguyên container, web server, DB).
- **Quản lý Log tập trung**: **Loki + Promtail** (đẩy log container và tra cứu bằng **LogQL**).
- **An ninh hệ thống**: Áp dụng 6 biện pháp Hardening bảo vệ toàn diện.

---

## 2. Hướng dẫn khởi chạy hệ thống

```bash
# 1. Clone repository
git clone [https://github.com/dtc245200573-droid/DTC245200573-Hotel-Booking.git](https://github.com/dtc245200573-droid/DTC245200573-Hotel-Booking.git)
cd DTC245200573-Hotel-Booking

# 2. Tạo biến môi trường
cp .env.example .env

# 3. Tạo chứng chỉ SSL tự ký cho Nginx
chmod +x nginx/gen-cert.sh
./nginx/gen-cert.sh

# 4. Khởi chạy toàn bộ hệ thống bằng Docker Compose
docker compose up -d

# 5. Kiểm tra trạng thái các container
docker compose ps
#### 2. File `.gitignore`
```text
.env
.DS_Store
nginx/certs/*.key
nginx/certs/*.crt