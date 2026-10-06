# LAB 5 - Thiết lập mô hình tường lửa pfSense

## 1. Thông tin sinh viên

- Họ và tên: Lê Nguyễn Đăng Khoa
- MSSV: 1150070021
- Lớp: 11_ĐH_TMĐT

## 2. Nội dung thực hiện

- Cài đặt và cấu hình pfSense CE 2.7.2 trên VMware.
- Cấu hình 3 card mạng cho pfSense gồm WAN, LAN và DMZ.
- Cấu hình WAN sử dụng NAT để kết nối ra Internet.
- Cấu hình LAN sử dụng mạng VMnet1 với địa chỉ `10.0.0.1/8`.
- Cấu hình DMZ sử dụng mạng VMnet2 với địa chỉ `172.16.0.1/16`.
- Truy cập và quản trị pfSense thông qua WebGUI tại `https://10.0.0.1`.
- Kiểm tra Dashboard và trạng thái các interface WAN, LAN và DMZ.
- Kiểm tra cấu hình Automatic Outbound NAT cho mạng LAN và DMZ.
- Cấu hình và kiểm thử các Firewall Rule trên LAN và DMZ.
- Thực hiện Reset States sau khi thay đổi Firewall Rule để loại bỏ các state cũ.
- Thực hiện tình huống chặn ICMP nhưng vẫn cho phép truy cập Web/DNS.
- Thực hiện tình huống chỉ cho phép host `10.0.0.2` truy cập Internet và chặn các host LAN còn lại.
- Sử dụng Kali Linux với địa chỉ `10.0.0.3/8` làm máy LAN-Test để kiểm tra Firewall Rule.
- Thực hiện kiểm thử cô lập vùng DMZ khỏi mạng LAN.
- Kiểm tra kết nối trước và sau khi áp dụng rule Block DMZ → LAN.
- Kiểm tra hoạt động của các rule bằng các lệnh `ping`, `nslookup` và `curl`.
- Thực hiện bật/tắt các Firewall Rule và kiểm tra ảnh hưởng đến kết nối mạng.

## 3. Kết quả

- Cài đặt và khởi động pfSense CE 2.7.2 thành công trên VMware.
- Cấu hình thành công 3 interface WAN, LAN và DMZ.
- LAN hoạt động với địa chỉ gateway `10.0.0.1/8`.
- DMZ hoạt động với địa chỉ gateway `172.16.0.1/16`.
- Các máy trong LAN có thể kết nối đến pfSense thông qua VMnet1.
- Máy trong DMZ có thể kết nối đến pfSense thông qua VMnet2.
- Automatic Outbound NAT nhận diện và tạo rule NAT cho các mạng nội bộ.
- Rule Block ICMP chặn thành công lưu lượng ping theo yêu cầu kiểm thử.
- DNS và HTTPS vẫn có thể hoạt động khi chỉ chặn giao thức ICMP.
- Host `10.0.0.2` được phép truy cập Internet khi sử dụng rule Pass riêng.
- Host `10.0.0.3` bị chặn truy cập Internet bởi rule Block LAN.
- Thứ tự Firewall Rule được kiểm chứng có ảnh hưởng trực tiếp đến kết quả lọc lưu lượng.
- Rule Block DMZ → LAN cô lập thành công vùng DMZ khỏi mạng LAN.
- Việc Reset States sau khi thay đổi rule giúp kết quả kiểm thử phản ánh đúng ruleset mới.
- Mô hình pfSense đã thực hiện được chức năng phân vùng mạng, NAT và kiểm soát truy cập bằng Firewall Rule.
