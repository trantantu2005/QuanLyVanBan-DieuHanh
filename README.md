# Hệ thống Quản lý Văn bản và Điều hành

> **Đồ án phát triển ứng dụng web | Hệ thống thông tin quản lý (MIS)**  
> **Công nghệ:** Python, Django 6.0.3 (theo `requirements.txt`), Django Templates, HTML, CSS, SQLite/PostgreSQL theo cấu hình.

## 1. Tổng quan

Dự án là ứng dụng web hỗ trợ số hóa công việc quản lý văn bản và điều hành trong cơ quan/đơn vị. Các module được tổ chức theo chức năng, có quản lý tài khoản, xử lý quy trình và theo dõi thông tin.

## 2. Các module trong mã nguồn

| Module | Nội dung |
|---|---|
| Tài khoản | Đăng nhập và quản lý người dùng/quyền truy cập |
| Văn bản đến | Tiếp nhận, danh sách, chi tiết, cập nhật, chuyển tiếp, hoàn trả |
| Văn bản đi | Tạo, chỉnh sửa, theo dõi và xử lý ban hành |
| Hồ sơ văn bản | Quản lý, phân loại, liên kết hồ sơ với văn bản |
| Công việc | Tạo/giao việc, theo dõi xử lý và trạng thái công việc |
| Tổng quan | Dashboard, báo cáo/thống kê và lịch sử hoạt động |

**Lưu ý:** Tính năng có mặt trong mã nguồn không đồng nghĩa mọi luồng đã được kiểm thử hoàn chỉnh.

## 3. Cấu trúc thư mục

```text
QuanLy-VanBan-DieuHanh/
├── manage.py
├── he_thong_quan_ly_van_ban/  # Django settings, urls
├── apps/
│   ├── accounts/
│   ├── core/
│   ├── quanlyvanbanden/
│   ├── quanlyvanbandi/
│   ├── hosovanban/
│   ├── quanlycongviec/
│   ├── templates/
│   └── static/
├── requirements.txt
├── .env.example
└── README.md
```

## 4. Cài đặt trên Windows

**Yêu cầu:** Python tương thích Django 6 (Python 3.12+), PowerShell. Dự án có hỗ trợ `DATABASE_URL` cho PostgreSQL, nếu không thiết lập có thể chạy nhánh SQLite theo `settings.py`.

```powershell
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
Copy-Item .env.example .env
```

Mở `.env` và **đặt lại `SECRET_KEY` bằng khóa do bạn tự tạo**. Bạn có thể tạo khóa bằng:

```powershell
.\.venv\Scripts\python.exe -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

Thay giá trị `SECRET_KEY=...` trong `.env`. Để dùng SQLite trên máy cá nhân, bỏ/để trống biến `DATABASE_URL` và cấu hình `DEBUG=True` chỉ cho môi trường phát triển.

Sau đó chạy:

```powershell
.\.venv\Scripts\python.exe manage.py migrate
.\.venv\Scripts\python.exe manage.py check
.\.venv\Scripts\python.exe manage.py runserver
```

Mở: http://127.0.0.1:8000/

> Nếu cài đặt phụ thuộc PostgreSQL thất bại trên máy bạn, kiểm tra tương thích Python/driver. Không dùng file `.env` trong ZIP gốc vì có thể chứa cấu hình riêng.

## 5. Thiết kế, hình ảnh, kiểm thử

- Thêm sơ đồ ERD/BPMN hoặc ảnh giao diện (đã ẩn dữ liệu cá nhân) vào `docs/screenshots/`.
- Chỉ công bố những kết quả kiểm thử bạn trực tiếp chạy và lưu được log.
- Dự án gốc có thư mục media và tài liệu đầu vào: **các tệp đó đã bị loại khỏi bộ mã nguồn này** để tránh đưa nội dung người dùng lên GitHub.

## 6. Đóng góp của tôi

## 6. Vai trò và đóng góp cá nhân

**Hình thức:** Đồ án nhóm môn Lập trình Web  
**Vai trò:** Thành viên phát triển hệ thống – phụ trách module Quản lý văn bản đến và Trang chủ (Dashboard).

### Công việc thực hiện

**1. Module Quản lý văn bản đến**
- Tham gia xây dựng chức năng quản lý văn bản đến trong hệ thống.
- Phát triển các chức năng tiếp nhận, hiển thị danh sách, xem chi tiết và cập nhật thông tin văn bản đến.
- Xử lý và hoàn thiện giao diện phục vụ quá trình theo dõi, quản lý văn bản.

**2. Trang chủ (Dashboard)**
- Tham gia thiết kế và xây dựng giao diện trang chủ của hệ thống.
- Tổ chức bố cục, hiển thị các thông tin tổng quan và hỗ trợ người dùng truy cập các chức năng chính.
- Điều chỉnh giao diện nhằm nâng cao tính trực quan và thuận tiện khi sử dụng.

### Kỹ năng và kinh nghiệm tích lũy
- Phát triển ứng dụng web sử dụng Python, Django và Django Templates.
- Làm việc với giao diện HTML, CSS và dữ liệu trong ứng dụng web.
- Tìm hiểu quy trình xử lý văn bản và tổ chức chức năng trong hệ thống thông tin quản lý.
- Phối hợp phát triển phần mềm theo nhóm và tích hợp các module vào hệ thống chung.

## 7. Ghi chú bảo mật

- `SECRET_KEY` trong bản mã nguồn được chuẩn bị đã chuyển sang đọc từ môi trường, thay vì dùng một khóa cố định.
- Không commit `.env`, dữ liệu văn bản thực, file chứng thư/certificate hoặc cơ sở dữ liệu chứa thông tin cá nhân.
- Trước khi công khai, hãy kiểm tra thêm các file seed, file test và quyền sở hữu mã nguồn.

**Tình trạng:** Mã nguồn được rà soát cấu trúc tĩnh; chưa chạy kiểm thử ứng dụng trên môi trường thực tế.
