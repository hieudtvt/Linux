# Log
- Là một tập hợp các bản ghi mà hệ thống duy trì để theo dõi các sự kiện quan trọng hệ điều hành, ứng dụng,...
# Các file log quan trọng
## Log messages
- Là file log chứa nhật ký hoạt động của hệ thống (System Logs). Chủ yếu được dùng để lưu trữ các thông tin liên quan đến hệ thống như mail, cron, daemon, kernel, auth,...\
- Câu lệnh xem log: `cat /var/log/messages`
## Log auth.log
- Chứa các thông tin xác thực hệ thống trong máy chủ
- Chứa các thông tin liên quan đến vấn đề ủy quyền của người dùng.
- Xác định các lần đăng nhập, các phiên ssh,
- Câu lệnh xem log: `cat /var/log/audit/audit.log`
## Log secure
- Chứa các thông tin về xác thực trên hệ thống.
- Lưu trữ các thông tin liên quan đến bảo mật, các lỗi xác thực.
- Theo dõi thông tin đăng nhập sudo, đăng nhập ssh và các lỗi khác được ghi bởi tiến trình chạy nền của dịch vụ bảo mật hệ thống.
- Câu lệnh xem log: `cat /var/log/secure` 
## Log wtmp và btmp
- Log wtmp chứa thông tin của các lần login thành công và được đọc bởi lệnh **last**
- Log btmp chứa thông tin của các lần login thất bại và được đọc bởi lệnh **lastb**
- Câu lệnh xem log login: `last -f var/log/wtmp`
- Câu lệnh xem log login fail: `lastb -f /var/log/btmp`
## Log boot.log
- Lưu trữ các thông tin liên quan đến khởi động và mọi thông báo được ghi lại trong quá trình khởi động bao gồm tập lệnh khởi tạo hệ thống,
- Giúp kiểm tra các vấn đề liên quan đến tắt máy không đúng cách, khởi động lại hoặc lỗi khởi động.
- Giúp xác định thời gian ngừng hoạt động của hệ thống do tắt máy đột xuất.
## Log dmesg
- Chứa các thông tin về bộ kernel được ghi nhận
- Chứa các thông tin liên quan đến các thiết bị phần cứng và trình điều khiển khi khởi động hệ thống.
- Dựa vào log này để  khắc phục các sự cố về phần cứng.
- Câu lệnh xem log: `cat /var/log/dmesg`
## Log cron
- Nơi lưu trữ tất cả các thông tin liên quan đến Crond
- Lưu trữ thông tin của các lần cron chạy.
## Log yum.log
- Chứa thông tn được ghi lại khi các package được cài bằng yum
- Giúp theo dõi việc cài đặt các thành phần hệ thống và gói phần mềm.
- Câu lệnh xem log: `cat /var/log/yum.log`
## File mail.log
- Lưu trữ các thông tin từ máy chủ mail đang chạy trên hệ thống 
- Theo dõi các vấn đề gửi mail thất bại, nhận thông tin về spam có thể bị ngăn chặn bới máy chủ mail. 
- Theo dõi nguồn gốc của một email.
- Câu lệnh xem log: `cat /var/log/maillog`

### Cách đọc output của lệnh last
![](https://imgur.com/5mTexZa.png)
- Cột 1: tên user hệ thống đang/đã đăng nhập vào hệ thống.
- Cột 2: thông tin về phương thức mà user đang đăng nhập như:
  - pts/0(pseudo terminal): kêt nối thông qua các chương trình remote connection như SSH, Telnet.
  - tty(teleyperwriter): kết nối thông qua local terminal.
  - shutdown/reboot: thể hiện thông tin hệ thống đã được tắt hoặc khởi động lại.
- Cột 3: thông tin hostname hoặc địa chỉ IP của máy tính kết nối đến. Nếu hiện ".0.0" hoặc không có thông tin gì thì tức là user đang kết nối local terminal như console.
- Cột 4 trở đi: thể hiện thông tin thời gian đăng nhập, thời gian thoát ra khỏi hệ thống và khoảng thời gian hoạt động của phiên kết nối đó.

