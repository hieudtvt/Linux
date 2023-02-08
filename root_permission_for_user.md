# File /etc/sudoers
- Là file cho phép người dùng được quyền sử dụng lệnh sudo để thực hiện các câu lệnh mà chỉ user root mới được phép thực hiện
- Câu lệnh
```
vi /etc/sudoers
```
- Gõ `:/Allows people in group` để tìm kiếm dòng:
```
## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL

```
- Thêm vào bên dưới nội dung sau:(giả sử ta cấp quyền cho user tên là **testuser** có quyền thực hiện câu lệnh useradd dưới quyền sudo)
```
## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL
testuser ALL=(ALL) /usr/sbin/useradd
```
- Phân tích cú pháp của nội dung vừa thêm vào
```
%GROUP HOSTNAME=(TARGET_USER) COMMAND
```
- `%GROUP` hoặc `%USER`: tên group hoặc user được cấp quyền 
- `HOSTNAME`: tên máy (có thể là địa chỉ IP) mà được áp dụng lệnh, tham số này là cần thiết vì sudo được thiết kế để bạn có thể dùng một file sudoers cho các máy khác. Lúc này, sudo sẽ xem máy đang chạy được dùng luật nào. Nói cách khác là bạn có thể thiết lập rule cho từng máy trong hệ thống. Tham số này thường để là ALL
- `TARGET-USERS`: tên người dùng đích cần mượn quyền thực thi câu lệnh với quyền root
- `COMMAND`: tên lệnh thực thi
## Group wheel trong Centos7
- Theo mặc định, Centos7 có một user group gọi là **wheel** group.
- Các thành viên của nhóm này sẽ được sử dụng quyền sudo để thực hiện các câu lệnh cần quyền root