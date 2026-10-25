# LAB 7 - Thiết lập Web Proxy và kiểm soát truy cập Internet bằng Squid, E2Guardian trên pfSense

## 1. Thông tin sinh viên

- Họ và tên: Lê Nguyễn Đăng Khoa
- MSSV: 1150070021
- Lớp: 11_ĐH_TMĐT

## 2. Nội dung thực hiện

- Xây dựng mô hình mạng LAB 7 trên VMware Workstation.
- Sử dụng pfSense làm Firewall để quản lý và kiểm soát lưu lượng mạng.
- Cài đặt Ubuntu Server làm máy WEB-PROXY với địa chỉ IP `10.6.0.30`.
- Cài đặt và cấu hình Squid làm Proxy Server.
- Cài đặt và cấu hình E2Guardian để lọc nội dung và kiểm soát truy cập website.
- Cấu hình Squid hoạt động trên cổng `3128` và E2Guardian trên cổng `8080`.
- Tạo Firewall Alias để quản lý Client-A, Client-B và máy WEB-PROXY.
- Thiết lập Firewall Rules trên pfSense để kiểm soát truy cập Internet thông qua Proxy.
- Kiểm tra kết nối giữa các máy Client và WEB-PROXY.
- Kiểm thử truy cập website bình thường thông qua Proxy (Normal Allow).
- Cấu hình chính sách chặn truy cập trực tiếp HTTP/HTTPS không thông qua Proxy.
- Cấu hình E2Guardian để chặn các website thuộc nhóm Geo-Sim và Job Search.
- Cấu hình chức năng cảnh báo (Warning) và cho phép bỏ qua cảnh báo tạm thời (Temporary Bypass).
- Cấu hình chính sách cho phép truy cập các website thuộc nhóm Education.
- Tạo Schedule `LAB7_WEB_60MIN` để giới hạn thời gian truy cập Proxy.
- Thiết lập Firewall Rules `LAB7_ALLOW_PROXY_60MIN` và `LAB7_BLOCK_PROXY_OUTSIDE_SCHEDULE`.
- Cài đặt ClamAV để kiểm tra và phát hiện mã độc.
- Sử dụng file kiểm thử EICAR để kiểm tra khả năng phát hiện mã độc của ClamAV.
- Cấu hình chứng chỉ CA và bật các tùy chọn HTTPS Inspection trên E2Guardian.
- Kiểm tra E2Guardian Access Log để theo dõi các website được phép hoặc bị chặn.
- Kiểm tra Firewall Log và State Table trên pfSense để phân tích lưu lượng mạng.

## 3. Kết quả

- Xây dựng được mô hình Web Proxy kết hợp pfSense, Ubuntu Server và các máy Client.
- Cấu hình thành công máy WEB-PROXY với địa chỉ IP `10.6.0.30`.
- Cài đặt và khởi chạy thành công Squid và E2Guardian.
- Squid hoạt động trên cổng `3128` và E2Guardian hoạt động trên cổng `8080`.
- Client-A kết nối thành công đến WEB-PROXY qua cổng `8080`.
- Kiểm thử thành công việc truy cập website HTTP thông qua Proxy.
- Cấu hình được các Alias và Firewall Rules phục vụ kiểm soát truy cập.
- E2Guardian hiển thị trang thông báo chặn đối với website nằm trong danh sách cấm.
- Kiểm thử được chức năng Temporary Bypass và ghi nhận trạng thái `TRUSTED` trong nhật ký E2Guardian.
- Tạo được Schedule `LAB7_WEB_60MIN` và các Firewall Rules liên quan đến giới hạn thời gian truy cập.
- Cài đặt và khởi chạy thành công dịch vụ ClamAV.
- ClamAV phát hiện được file kiểm thử EICAR với kết quả `Eicar-Test-Signature FOUND`.
- Cấu hình được chứng chỉ CA và bật tùy chọn SSL MITM trong E2Guardian.
- E2Guardian Access Log ghi nhận các hoạt động truy cập và các website bị chặn.
- Kiểm tra được Firewall Rules, Firewall Log và State Table trên pfSense.
- Việc chặn truy cập trực tiếp, kiểm thử Education Allow và kiểm thử Schedule ngoài thời gian cho phép chưa được xác nhận đầy đủ.
- Chưa xác nhận thành công khả năng quét và chặn EICAR trực tiếp qua HTTPS Proxy.
- HTTPS Inspection đã được cấu hình nhưng chưa xác nhận thành công quá trình giải mã và kiểm tra nội dung HTTPS.
