BÁO CÁO THỰC HÀNH LAB 3: NHẬN DIỆN VÀ ỨNG PHÓ CÁC MỐI ĐE DỌA ĐẾN AN TOÀN THÔNG TIN
I. THÔNG TIN SINH VIÊN VÀ BÀI LAB
Họ và tên: Lê Nguyễn Đăng Khoa

Mã số sinh viên (MSSV): 1150070021

Mã lớp: 11_ĐH_TMĐT

Tên bài LAB: Lab 3: Nhận diện và ứng phó các mối đe dọa đến an toàn thông tin

II. PHIÊN BẢN MÔI TRƯỜNG VÀ CÔNG CỤ
Môi trường ảo hóa: VMware Workstation Pro 26H1

Hệ điều hành máy ảo (VM): Windows 11 25H2 x64

Endpoint Protection: Microsoft Defender Antivirus (Duy trì Real-time Protection và Tamper Protection bật)

Shell: Windows PowerShell 5.1 (Run as administrator)

Bộ công cụ giám sát Sysinternals:

Sysmon: v15.22 (Schema 4.90)

Autoruns: v14.3

Process Explorer: v17.14

Công cụ phân tích mạng và lập trình:

Wireshark: v4.6.8 Stable + Npcap

Python: v3.14.7

Gói dữ liệu mẫu: LAB3_Threats_Assets.zip

III. HƯỚNG DẪN DỰNG MÔI TRƯỜNG THỰC HÀNH
Bước 1: Tạo máy ảo và khởi tạo Snapshot Clean
Dựng VM Windows 11 25H2 x64 (2 vCPU, 6 GB RAM, 64 GB Disk) trên VMware Workstation Pro 26H1.

Chuyển Network Adapter sang chế độ Host-only.

Cập nhật bản vá KB5124008 và tạo snapshot điểm chuẩn tên LAB3_CLEAN_20260914.

Bước 2: Tạo cấu trúc thư mục làm việc
Mở PowerShell dưới quyền Administrator và khởi tạo các thư mục lưu trữ:

PowerShell
$Lab = 'C:\LAB3'
New-Item -ItemType Directory -Force "$Lab\Evidence", "$Lab\Tools", "$Lab\Downloads", "$Lab\Assets" | Out-Null
Get-Date -Format 'yyyy-MM-dd HH:mm:ss zzz' | Out-File "$Lab\Evidence\start_time.txt"
Bước 3: Giải nén gói dữ liệu bài lab
Đưa file LAB3_Threats_Assets.zip vào C:\LAB3\Downloads, đối chiếu mã hash SHA-256 và giải nén:

PowerShell
Get-FileHash C:\LAB3\Downloads\LAB3_Threats_Assets.zip -Algorithm SHA256
Expand-Archive C:\LAB3\Downloads\LAB3_Threats_Assets.zip -DestinationPath C:\LAB3 -Force
Bước 4: Cài đặt Python 3.14.7 và Wireshark 4.6.8
Cài đặt bằng winget (giữ lại Npcap khi cài Wireshark):

PowerShell
winget install --id Python.Python.3.14 --exact --version 3.14.7 --accept-package-agreements --accept-source-agreements
winget install --id WiresharkFoundation.Wireshark --exact --version 4.6.8 --accept-package-agreements --accept-source-agreements
Bước 5: Tải bộ công cụ Sysinternals
Tải trực tiếp từ máy chủ Microsoft và giải nén vào C:\LAB3\Tools:

PowerShell
$D='C:\LAB3\Downloads'; $T='C:\LAB3\Tools'
Invoke-WebRequest 'https://download.sysinternals.com/files/Sysmon.zip' -OutFile "$D\Sysmon.zip"
Invoke-WebRequest 'https://download.sysinternals.com/files/Autoruns.zip' -OutFile "$D\Autoruns.zip"
Invoke-WebRequest 'https://download.sysinternals.com/files/ProcessExplorer.zip' -OutFile "$D\ProcessExplorer.zip"

Expand-Archive "$D\Sysmon.zip" -DestinationPath "$T\Sysmon" -Force
Expand-Archive "$D\Autoruns.zip" -DestinationPath "$T\Autoruns" -Force
Expand-Archive "$D\ProcessExplorer.zip" -DestinationPath "$T\ProcessExplorer" -Force

IV. BÁO CÁO KẾT QUẢ CÁC TÌNH HUỐNG (PASS / FAIL)
TH0: Baseline trước khi tạo tình huống

Trạng thái: PASS

Bằng chứng thu thập / Đã xác minh: Xuất đầy đủ các file baseline OS, Defender, Firewall, Network, Process vào C:\LAB3\Evidence\.

TH1: Xác định Tài sản, Lỗ hổng, Mối đe dọa, Rủi ro & Phân loại 5 nguồn

Trạng thái: PASS

Bằng chứng thu thập / Đã xác minh: Lập Risk Register chuẩn hóa và phân loại chính xác 5 nhóm nguồn đe dọa.

TH2: Mã độc: Kiểm chứng chu trình phát hiện bằng EICAR

Trạng thái: PASS

Bằng chứng thu thập / Đã xác minh: RealTimeProtectionEnabled = True; Defender ghi nhận detection EICAR trong Protection History và defender_eicar.txt.

TH3: Tấn công mật khẩu và nguy cơ keylogging

Trạng thái: PASS

Bằng chứng thu thập / Đã xác minh: Ghi nhận Event ID 4624/4648 cho đăng nhập đúng, Event ID 4625 cho đăng nhập sai; đổi mật khẩu thành công làm mật khẩu cũ không còn tác dụng.

TH4: Backdoor: Nhận diện Persistence và dịch vụ lắng nghe

Trạng thái: PASS

Bằng chứng thu thập / Đã xác minh: Phát hiện LAB3_Run_Demo trên Autoruns/Sysmon, kiểm tra task LAB3_Persistence_Demo; ánh xạ cổng 8080 về đúng PID python.exe bind 127.0.0.1.

TH5: Sniffing, MITM và Spoofing: HTTP vs HTTPS

Trạng thái: PASS

Bằng chứng thu thập / Đã xác minh: Capture thành công chuỗi TRAINING_ONLY trên HTTP loopback và so sánh mã hóa dữ liệu gói tin với HTTPS/TLS.

TH6: DoS, DDoS và Mail Bombing

Trạng thái: PASS

Bằng chứng thu thập / Đã xác minh: Chạy local_load_test.py trên loopback; phân tích thành công ddos_sample.csv và mailbomb_sample.csv.

TH7: Social Engineering, Phishing và Spear Phishing

Trạng thái: PASS

Bằng chứng thu thập / Đã xác minh: Phát hiện đủ 5 chỉ dấu lừa đảo trong phishing_email.txt và phân loại 6 kịch bản Social Engineering.

TH8: Cô lập, Cleanup, Phục hồi và Verify

Trạng thái: PASS

Bằng chứng thu thập / Đã xác minh: Loại bỏ toàn bộ các mục persistence, đóng HTTP server, xóa lab3user, xuất bảng hash SHA-256 các file Evidence.

V. LỖI GẶP PHẢI VÀ CÁCH KHẮC PHỤC
1. Lỗi Set-Content tạo tệp EICAR bị Defender chặn ngay lập tức
Hiện tượng: Khi chạy lệnh PowerShell để tạo file eicar.com.txt, hệ thống báo lỗi I/O do Microsoft Defender Real-time Protection phát hiện và chặn ghi tệp lập tức.

Cách khắc phục: Sử dụng khối lệnh try { ... } catch { ... } theo đúng hướng dẫn bài lab để ghi nhận lỗi vào eicar_write_error.txt. Mở Windows Security > Protection history hoặc dùng lệnh Get-MpThreatDetection để lấy thông tin detection mà không cần phục hồi tệp bị quarantine.

2. Wireshark không bắt được lưu lượng giao tiếp trên Loopback (127.0.0.1)
Hiện tượng: Mở Wireshark nhưng không thấy giao diện Loopback traffic hoặc lưu lượng bắt gói tin trên 127.0.0.1:8080 bị trống.

Cách khắc phục: Đảm bảo khi cài đặt Wireshark đã tích chọn driver Npcap. Trong giao diện Wireshark, chọn đúng card mạng Adapter for loopback traffic capture thay vì chọn card Ethernet vật lý.

3. Không tìm thấy Event ID 4624/4625/4648 trong Event Viewer
Hiện tượng: Chạy lệnh runas và gõ sai/đúng mật khẩu nhưng khi lọc Security Log không thấy sự kiện xuất hiện.

Cách khắc phục: Kích hoạt audit policy bằng GUID chính xác dưới quyền Administrator trước khi thực hiện đăng nhập:

auditpol /set /subcategory:{0CCE9215-69AE-1109-BED3-505054503030} /success:enable /failure:enable
