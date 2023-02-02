# Cron là gì?
- Là một chương trình dùng để chạy các tác vụ ngầm theo một lịch trình cụ thể
- Ví dụ: sao lưu, đồng bộ file, chạy batch,...
- Một khi được khởi động, nó sẽ chạy ngầm mãi mãi
# Cài đặt Cron
- Bước 1: kiểm tra cron đã được cài đặt hay chưa
```
systemctl status crond
```
- Cấu trúc
```
* * * * * command được thực hiện
- - - - -
| | | | |
| | | | +----- ngày trong tuần (0 - 6) (Sunday=0)
| | | +------- tháng (1 - 12)
| | +--------- ngày trong tháng (1 - 31)
| +----------- giờ (0 - 23)
+------------- phút (0 - 59)
```
- Chú thích:
  - `*`: tất cả các giá trị
  - `-`: khoảng giá trị: VD: 6-8 ở cột giờ tức là thực hiện lúc 6h, 7h, 8h
  - `,`: liệt kệ các giá trị: VD 10,20,30 ở cột phút thì sẽ thực hiện ở các phút 10, phút 20, phút 30. 
  - `/`: bước nhảy giá trị: VD: */15 * * * * sẽ thực hiện 15 phút một lần
  Hoặc */15 8-10/2 * * * sẽ thực hiện vào 8h00, 8h15, 8h30, 8h45, 10h00, 10h15, 10h30, 10h45
## Lab
- Để mở crontab nhập câu lệnh
```
crontab -e
```
- Một số ví dụ :
`* * * * *`: tức là chạy command mỗi phút
`0 4 * * *`: chạy command mỗi ngày 4 giờ sáng
`0 4 * * 2-4`: chạy command vào 4 giờ chiều thứ 3, thứ 4, thứ 5
`20,40 */8 * 7-12 *`: chạy command vào phút 20 và 40 mỗi 8h vào tháng 7 đến tháng 12

- Một số mẫu crond đặc biệt:
  - `@yearly`: tức là chạy một lần mỗi năm tương đương `0 0 1 1 *`
  - `@mouthly`: chạy mỗi tháng một lần `0 0 1 * *`
  - `@weekly`: chạy mỗi tuần một lần `0 0 * * 0`
  - `@daily`: chạy mỗi lần mỗi ngày `0 0 * * *`
  - `@hourly`: chạy mỗi lần mỗi giờ `0 * * * *`
- Xem các crontab bằng câu lệnh
```
crontab -l
```
- Xóa hết crontab bằng câu lệnh
```
crontab -r
```
- Sửa crontab bằng câu lệnh
```
crontab -e
```
- Quản lý user nào được phép sử dụng crontab với các file 
`cron.allow` và file `cron.deny` 
- `cron.allow`: cho phép những user được list trong file mới được edit crontab.
- `cron.deny`: hạn chế những user được list trong file edit crontab
