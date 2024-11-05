GNS3:
-Cần tải tích hợp Router C7200, Switch Layer3
-Tích hợp VMware với GNS3 thông qua 1 máy tính làm Server trong sơ đồ mạng GNS3

VMware:
-Máy client để test bằng hệ điều hành Win10 hoặc Win7
-Máy chủ Server có hệ điều hành Win Server 2016 

Cấu hình mạng trong sơ đồ: 
Trụ sở Hà Nội và các chi nhánh Thái Bình, Đà Nẵng, Nam Định sẽ có quy mô giống nhau.
Server DHCP, DC, DNS sẽ nằm ở trụ sở Thái Bình.
Các thiết bị HOST : Được nối đến một SWITCH CORE
Router trong trụ sở mạng Internet sẽ có 2 con Router nối với Router Internet phát mạng để nếu 1 trong các con Router sập thì sẽ có backup
Các chi nhánh cũng sẽ có 1 con Router để backup nếu 1 con sập 

Quy hoạch địa chỉ IP 
1.Quy hoạch cho từng chi nhánh chính: 
Theo nhu cầu cho tổng cộng 4 chi nhánh với dải IP cấp phát là: 192.168.14.0/22, /22 sẽ có 1022 địa chỉ IP khả dụng, đủ cho mỗi chi nhánh 254 địa chỉ IP (tổng 1016)
- HÀ NỘI: 192.168.14.0/24 Wildcast: 0.0.0.255
- THÁI BÌNH: 192.168.15.0/25 Wildcast: 0.0.0.63
- ĐÀ NẴNG: 192.168.15.128/25 Wildcast: 0.0.0.63
- NAM ĐỊNH: 192.168.16.0/25 Wildcast: 0.0.0.63
- 2 con Router trong mỗi chi nhánh sẽ nối đến 1 con Switch Core và dùng cái IP trong dải địa chỉ quy định
2.Quy hoạch giữa các Router:
  Do các con Router cần nối đến nhau thông qua định tuyến nên sẽ tự cấp phát các dải mạng đại diện giữa các con Router
- Router Internet đầu tiên sẽ mang IP đại diện Internet 8.8.8.8, Router Internet nối đến R1: 1.1.1.0/24, nối đến R2: 2.2.2.0/24
- R1 -> R3: 100.0.1.0/24
- R1 -> R5: 100.0.2.0/24
- R1 -> R7: 100.0.3.0/24
- R1 -> R10: 100.0.4.0/24
- R2 -> R4: 200.0.1.0/24
- R2 -> R6: 200.0.2.0/24
- R2 -> R8: 200.0.3.0/24
- R2 -> R9: 200.0.4.0/24
3.Quy hoạch trong Server:
-IP Server: 192.168.14.8
