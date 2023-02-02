# Sử dụng Netstat quản lý mạng trên linux
- `netstat (network statistics)` là một công cụ của gói *net-tools*
## Cài đặt netstat
- Câu lệnh cài
```
yum install -y net-tools
```
## Các tùy chọn của netstat
- `-a`: hiển thị tất cả các sockets, kể cả listening và non listening
- `-l`: hiển thị các socket đang lắng nghe
- `-t`: chỉ hiển thị các kết nối tcp
- `-u`: chỉ hiển thị các kết nối udp
- `-n`: xem địa chỉ IP
- `-p`: hiển thị PID của từng socket
- `-r`: hiển thị bảng định tuyến
- `-s`: pull và hiển thị thống kê mạng được sắp xếp theo giao thức
- `-i`: hiển thị danh sách giao diện mạng