# Hệ Thống Đặt Phòng Khách Sạn (Đề Tài 6)

Kho lưu trữ: `DTC245200573-Hotel-Booking`  
Môn học: Triển khai và Quản trị Hệ thống Phần mềm

---

## 1. Giới thiệu và thông tin sinh viên

- **Sinh viên thực hiện:** Lý Kiều Trang
- **Mã số sinh viên (MSSV):** DTC245200573
- **Lớp:** CNTT K23C
- **Email:** DTC245200573@ictu.edu.vn
- **Mô tả đề tài:** Dự án xây dựng và triển khai hệ thống phần mềm Quản lý Đặt phòng Khách sạn phục vụ khách hàng và quản lý phòng nghỉ theo chuẩn DevOps. Hệ thống được đóng gói dạng Microservices/Containerized trên Docker Compose, tích hợp cổng Nginx Reverse Proxy bảo mật HTTPS, giám sát số liệu thời gian thực (Prometheus & Grafana), quản lý log tập trung và áp dụng các biện pháp Hardening bảo vệ toàn diện.

---

## 2. Hướng dẫn khởi chạy hệ thống

Triển khai hệ thống theo trình tự chuẩn hóa các bước dưới đây:

```bash
# Bước 1: Sao chép mã nguồn dự án từ GitHub
git clone [https://github.com/dtc245200573-droid/DTC245200573-Hotel-Booking.git](https://github.com/dtc245200573-droid/DTC245200573-Hotel-Booking.git)

# Bước 2: Di chuyển vào thư mục dự án
cd DTC245200573-Hotel-Booking

# Bước 3: Tạo file cấu hình biến môi trường và điền mật khẩu
cp .env.example .env
chmod 600 .env

# Bước 4: Tự động khởi tạo chứng chỉ SSL tự ký cho Nginx HTTPS
chmod +x nginx/gen-cert.sh
./nginx/gen-cert.sh

# Bước 5: Khởi chạy toàn bộ hệ thống dịch vụ bằng Docker Compose
docker-compose up -d

# Bước 6: Kiểm tra trạng thái toàn bộ container hoạt động bình thường
docker compose ps



## 7. Cấu trúc thư mục dự án

DTC245200573-Hotel-Booking/
├── docker-compose.yml          # Cấu hình khởi chạy các container dịch vụ & networks
├── .env.example                # File mẫu biến môi trường (không chứa mật khẩu thật)
├── .gitignore                  # Khai báo loại trừ file bí mật (.env, private keys, log)
├── README.md                   # Tài liệu hướng dẫn triển khai và kiến trúc hệ thống
├── db/
│   └── init.sql                # Khởi tạo schema CSDL đặt phòng, cấp quyền và dữ liệu mẫu
├── web/
│   ├── Dockerfile              # Dockerfile đóng gói ứng dụng Đặt phòng Khách sạn
│   ├── security.ini            # Cấu hình bảo mật ứng dụng
│   └── src/                    # Mã nguồn ứng dụng Web Đặt phòng Khách sạn
├── nginx/
│   ├── nginx.conf              # Cấu hình Reverse Proxy, HTTPS, Security Headers, Rate Limit
│   ├── gen-cert.sh             # Script tự động tạo chứng chỉ SSL tự ký
│   └── certs/                  # Thư mục lưu trữ chứng chỉ SSL (server.crt, server.key)
├── prometheus/
│   └── prometheus.yml          # Cấu hình targets cào metrics định kỳ cho Prometheus
├── grafana/
│   └── provisioning/           # Cấu hình nạp tự động Datasource, Dashboards và Alerting
├── loki/
│   └── loki-config.yaml        # Cấu hình dịch vụ lưu trữ log Loki
├── promtail/
│   └── promtail-config.yaml    # Cấu hình thu thập log container gửi về Loki
└── scripts/
    └── hardening_evidence.sh   # Script tự động kiểm tra và xuất bảng chứng 6 biện pháp Hardening