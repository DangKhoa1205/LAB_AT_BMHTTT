# LAB 4 - Khảo sát và đánh giá bề mặt mạng bằng Nmap

## 1. Thông tin sinh viên

- Họ và tên: Lê Nguyễn Đăng Khoa
- MSSV: 1150070021
- Lớp: 11_ĐH_TMĐT

## 2. Nội dung thực hiện

- Cấu hình môi trường Kali Linux và Metasploitable 2 trong mạng Host-Only.
- Kiểm tra địa chỉ IP và kết nối giữa hai máy ảo.
- Sử dụng Nmap để phát hiện các host đang hoạt động trong mạng.
- Thực hiện quét TCP bằng SYN Scan.
- Thực hiện FIN Scan, Xmas Scan và NULL Scan.
- Thực hiện ACK Scan để kiểm tra trạng thái lọc của cổng.
- Thực hiện UDP Scan trên các cổng phổ biến.
- Sử dụng `-sV` để xác định dịch vụ và phiên bản đang chạy.
- Sử dụng `-O` để nhận diện hệ điều hành.
- Thực hiện Aggressive Scan bằng `-A`.
- Sử dụng NSE Script để kiểm tra thông tin SMB và MS17-010.
- Xuất kết quả quét ra các định dạng TXT, XML và HTML.
- Thực hiện hardening bằng cách tắt dịch vụ Telnet.
- So sánh kết quả Nmap trước và sau khi hardening.

## 3. Kết quả

- Kali Linux kết nối thành công với Metasploitable 2 trong mạng Host-Only.
- Nmap phát hiện được các host đang hoạt động trong mạng.
- Phát hiện nhiều dịch vụ đang mở trên Metasploitable 2 như FTP, SSH, Telnet, HTTP, SMB, MySQL và PostgreSQL.
- `-sV` xác định được tên và phiên bản của nhiều dịch vụ đang hoạt động.
- `-O` nhận diện máy đích sử dụng hệ điều hành Linux.
- NSE Script thu thập được thông tin về dịch vụ SMB trên cổng 445.
- Kết quả quét được lưu thành công dưới dạng TXT, XML và HTML.
- Sau khi tắt dịch vụ Telnet, cổng `23/tcp` chuyển từ `open` sang `closed`.
- Kết quả before/after cho thấy việc hardening đã làm giảm bề mặt tấn công của hệ thống.
