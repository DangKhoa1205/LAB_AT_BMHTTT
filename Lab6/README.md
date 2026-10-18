# LAB 6 - Xác thực Active Directory và thiết lập chính sách truy cập trên pfSense

## 1. Thông tin sinh viên

- Họ và tên: Lê Nguyễn Đăng Khoa
- MSSV: 1150070021
- Lớp: 11_ĐH_TMĐT

## 2. Nội dung thực hiện

- Xây dựng mô hình mạng LAB 6 trên VMware Workstation.
- Cấu hình pfSense với 4 interface: WAN, MGMT, LAN và DMZ.
- Cài đặt Windows Server và cấu hình Active Directory Domain Services (AD DS), DNS với domain `lab6.test`.
- Tạo các tài khoản người dùng `sv_a`, `sv_b` và tài khoản dịch vụ `svc_pfsense_ldap`.
- Tích hợp pfSense với Active Directory thông qua LDAP.
- Kiểm tra xác thực tài khoản bằng Diagnostics → Authentication.
- Cấu hình Captive Portal trên LAN để xác thực người dùng bằng tài khoản Active Directory.
- Tạo Firewall Alias cho Client-A, Client-B, nhóm máy trạm và các website mô phỏng.
- Cấu hình Schedule `LUNCH_WINDOW` và `WORK_HOURS` để kiểm soát truy cập theo thời gian.
- Cấu hình Ubuntu Server trong DMZ với các website GENERAL_SITE, JOB_SITE, SOCIAL_SITE và RESTRICTED_SITE.
- Thiết lập Firewall Rules để cho phép hoặc chặn truy cập theo địa chỉ IP, cổng và thời gian.
- Kiểm thử các chính sách chặn JOB_SITE, RESTRICTED_SITE và giới hạn truy cập SOCIAL_SITE.
- Kiểm thử truy cập HTTP/HTTPS trong giờ làm việc và cô lập mạng DMZ khỏi LAN.
- Kiểm tra Firewall Log và State Table để phân tích kết quả.
- Sao lưu cấu hình pfSense bằng Diagnostics → Backup & Restore.

## 3. Kết quả

- Xây dựng được mô hình pfSense với 4 interface WAN, MGMT, LAN và DMZ.
- Cấu hình Active Directory và kết nối LDAP với pfSense.
- Captive Portal chuyển hướng người dùng chưa đăng nhập đến trang xác thực và cho phép truy cập sau khi đăng nhập thành công.
- Tạo được các Alias và Schedule phục vụ chính sách kiểm soát truy cập.
- Client-A bị chặn khi truy cập JOB_SITE.
- Client-A và Client-B bị chặn khi truy cập RESTRICTED_SITE.
- Client-B được phép truy cập SOCIAL_SITE trong thời gian cho phép và bị chặn ngoài thời gian quy định.
- Client-A và Client-B truy cập thành công GENERAL_SITE.
- Kiểm thử thành công kết nối HTTPS khi lịch cho phép truy cập web đang hoạt động.
- Firewall chặn kết nối khởi tạo từ DMZ đến LAN.
- Firewall Log ghi nhận các kết nối bị chặn theo rule đã cấu hình.
- State Table hiển thị thông tin các kết nối mạng được thiết lập.
- Xuất được file sao lưu cấu hình pfSense để phục vụ nộp bài và khôi phục hệ thống.

