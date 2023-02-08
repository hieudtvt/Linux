# Sao lưu và đồng bộ dự liệu trên Linux
- Rsync (Remote Sync) là một công cụ hữu hiệu để sao lưu và đồng bộ dữ liệu trên Linux.
## Cú pháp 
```
rsync options source destination
```
- Các option
  - `-v`: verbose
  - `r`: sao chép dữ liệu theo cách đệ quy (không bảo tồn mốc thời gian và permistion trong quá trình truyền dữ liệu)
  - `a`: chế độ lưu trữ cho phép các tệp đệ quy và giữ các liên kết, quyền sở hữu, nhóm và mốc thời gian
  - `-z`: nén dữ liệu
  - `-h`: định dạng số
## Cài đặt
```
yum install rsync
```
## 1 Sao lưu, đồng bộ file trên local
- Để copy file backup.tar sang thư mục /tmp/backups/ ta làm như sau:
```
rsync -zvh backup.tar /tmp/backups/
```
## 2 Sao lưu, đồng bộ file từ server về local
- Từ local lên server(Ví dụ bạn có 1 thư mục chứa ảnh trên local images/ và bạn muốn đồng bộ lên server có IP 192.168.20.10)
```
rsync -avz images/ root@192.168.20.10:/home/
```
- Từ server về local (Ví dụ bạn có 1 thư mục chứa ảnh trên server là images/ và bạn muốn đồng bộ về máy local)
```
rsync -avzh root@192.168.20.10:/home/images /home/images/
```
## 3 rsync qua SSH
- Sử dụng SSH khi truyền tải file để đảm bảo file của bạn được bảo mật và không ai có thể đọc được dữ liệu khi dữ liệu được truyền tải qua internet.
- Bạn cần cấp quyền user/root mật khẩu để hoàn thành tác vụ copy file từ Remote Server về local với SSH
- Thêm option `-e` khi sử dụng SSH với rsync để truyền tải file
```
rsync -avzhe ssh root@192.168.20.10:/root/install.log
```
- 