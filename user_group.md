# User
## Đặc điểm
- Tên tài khoản user là duy nhất, có thể đặt tên chữ thường, chữ hoa
- Mỗi user có 1 mã định danh duy nhất (uid)
- Mỗi user có thể thuộc về nhiều group
- Tài khoản super user có uid=gid=0
## File /etc/passwd
- Là file văn bản chứa thông tin về các tài khoản user trên máy
- Mọi user đều có thể đọc tập tin này nhưng chỉ có user `root` mới có quyền thay đổi
### Cách đọc file /etc/passwd
- Ví dụ output của lệnh `cat /etc/passwd`như sau:
![](https://imgur.com/PNIaGek.png)
- Cấu trúc file gồm nhiều hàng, mỗi hàng là 1 thông tin của user
- Trong mỗi hàng sẽ được chia thành các cột và được ngăn cách bởi dấu `:`
- Phân tích hàng 1: là thông tin mô tả của user `root`
  - `root`: tên user
  - `x`: mật khẩu group đã được mã hóa nên là có dấu **x**
  - `0`: user id (**uid**)
  - `0`: group id (**gid**)
  - `root`: bí danh (comment) của user
  - `/root`: thư mục home của user
  - `/bin/bash`: loại shell sẽ hoạt động khi user login
- Tương tự dựa vào đó phân tích hàng được đánh số 2 trong ảnh 
## File /etc/shadow
- Là tập tin văn bản chứa thông tin về mật khẩu của các tài khoản user lưu trên máy
- Chỉ có user **root** mới có quyền đọc tập tin này
- User **root** có quyền reset mật khẩu của bất cứu user nào trên máy
- Mỗi dòng trong tập tin chứa thông tin về mật khẩu của user định dạng tương tự như file /etc/passwd
![](https://imgur.com/WHIc7CE.png)
- Ý nghĩa:
  - `root`: tên user
  - `$6$N2WfWAGkiVscBX13$ftH9I03qKlZqup6HTlbSsQF9ipQ/xYK094Em2H/mHvtW.2tF2f8e.EQIB7U06nobsnghG03Y86zV7oFnviFtq0`: mật khẩu được mã hóa
    - Nếu để trống: user không có mật khẩu
    - `*`: tài khoản bị tạm ngưng
  - Số ngày kể từ lần cuối thay đổi mật khẩu (tính từ 1/1/1970) ở ảnh trên thì user root chưa thay đổi mật khẩu lần nào
  - `0`: số ngày trước khi có thể thay đổi mật khẩu. Ở đây là giá trị `0` có nghĩa là có thể thay đổi mật khẩu bất cứ lúc nào
  - `99999`: số ngày mật khẩu có giá trị. Ở đây **99999* tức là mật khẩu có giá trị vô thời hạn
  - `7`: số ngày cảnh báo user trước khi mật khẩu hết hạn
  - Hai cột cuối lần lượt là:(ở ảnh trên là đang được để trống)
    - số ngày sau khi mật khẩu hết hạn sẽ bị khóa
    - số ngày kể từ khi tài khoản bị khóa (tính từ 1/1/1970)
## Các lệnh quản lý user
### useradd
- Tạo tài khoản user: `useradd [options] [login_name]
- Options:
  - `-c`: (**comment**) tạo bí danh
  - `-u`: set user ID(**uid**), mặc định sẽ lấy số ID tiếp theo để gắn cho user (bắt đầu từ 1000)
  - `-d`: chỉ định thư mục home cho user
  - `-g`: chỉ định group chính
  - `-G`: chính định group phụ (group mở rộng)
  - `-s`: chỉ định shell cho user sử dụng
- Ví dụ 1: Tạo user với tên testuser 
```
useradd -c testuser
```
- Mặc định nếu không chỉ định thì user được tạo sẽ thuộc về group **testuser** cùng tên với user và thư mục home cũng được tạo mặc định `/home/testuser` với quyền là 700
- Ví dụ 2: tạo user với tên là testuser2 thuộc group grouptest, trước đó ta phải có group tên là**grouptest**
```
useradd -g grouptest test
```
#### Đặt mật khẩu cho user
```
passwd [user_name]
```
- Ví dụ đặt mật khẩu cho user test vừa tạo
```
passwd test
```
### usermod
- Là lệnh sử thông tin tài khoản
```
usermod [options] [user_name]
```
- Options:
  - `-c`: tạo bí danh
  - `-d`: thay đổi thư mục home cho user
  - `-m`: di chuyển nội dung từ thư mục home cũ sang thư mục home mới(lưu ý chỉ dùng với option **-d*)
  - `-g`: chỉ định group chính
  - `-G`: chỉ định group phụ
  - `-s`:chỉ định shell cho user sử dụng
  - `-l`: đổi tên tài khoản
  - `-L`: khóa tài khoản
- Ví dụ: Đổi tên tài khoản test thành testuser1 và đổi thư mục home của user thành **/home/testuser1**
```
usermod -ltestuser1 -m -d /home/testuser1 test
```
- Thay đổi group của testuser1 thành group testuser
```
usermod -g testuser testuser1
```
### userdel
- Lệnh xóa user
```
userdel [options] [user_name]
```
- options: 
  - `-r`: xóa cả thư mục home của user
- Khi xóa tài khoản user bằng lệnh userdel, dòng mô tả tương ứng của user trong tập tin `/etc/passwd` và `/etc/shadow` cũng bị xóa.
## change
- Dùng để thiết lập chính sách (policy) cho user
```
chage [options] [user_name]
```
- Options:
  - `-d`: hoặc **--lastday** set date of last password change to
  - `-l`: xem chính sách của 1 user
  - `E`: thiết lập ngày hết hạn cho account
  - `I`: thiết lập ngày bị khóa sau khi hết hạn mật khẩu (định dạng ngày tháng là YYYY-MM-DD)
  - `-m`: thiết lập số ngày tối thiếu được phép thay đổi password
  - `-M`: thiết lập số ngày tối đa được phép thay đổi password
  - `-W`: thiết lập số ngày cảnh báo trước khi hết hạn mật khẩu
- ví dụ: 
```
chage -E 2023-02-09 -m 5 -M 90 -I 30 -W 14 testuser
```
=> Lệnh trên sẽ thiết lập mật khẩu hết hạn vào ngày `09/02/2023`. Số ngày tối thiểu được phép thay đổi mật khẩu là sau 5 ngày và số ngày tối đa được phép thay đổi mật khẩu là 90 ngày, sau 90 ngày user không được phép thay đổi mật khẩu. Các tài khoản sẽ bị khóa sau 30 ngày tính từ ngày hết hạn, và 1 tin nhắn cảnh báo sẽ được gửi ra 14 ngày trước khi hết hạn mật khẩu.
- Ví dụ 2: Tắt chính sách hết hạn mật khẩu
```
chage -I -1 -m 0 -M 99999 -E -1 testuser
```
=> Lệnh trên sẽ khiến mật khẩu không bị hết hạn(thông số -1), số ngày tối thiểu được phép thay đổi mật khẩu là 0, số ngày tối đa là vô hạn(99999), tài khoản không thông báo hết hạn (option -E = -1)
- Ví dụ 3: Thiết lập bắt buộc user đổi mật khẩu trong lần đầu đăng nhập
```
chage -d 0 testuser
```
### Lệnh id
- Xem thông tin user hiện hành
### Lệnh su
- Chuyển đổi user làm việc từ terminal
- User **root** chuyển qua user khác thì không cần phải nhập mật khẩu
- User khác chuyển qua user root thì cần phải nhập **password** của user **root**
- Câu lệnh chuyển user
```
su -l [user_name]
```
- ví dụ: chuyển từ user thường sang user root
```
su -l root
```
# Quản trị group
- Group là tập hợp của nhiều user
- Mỗi group có 1 tên duy nhất và một mã định danh duy nhất (gid)
- Khi tạo ra 1 user (không dùng option -g) thì mặc định sinh ra một group mới mang tên của user được tạo ra
## File /etc/group
- Là tập tin văn bản chứa thông tin về các group trên máy.
- Mọi user đều có quyền đọc tập tin này nhưng chỉ user root mới có quyền thay đổi
- Mỗi dòng tập tin chứa thông tin về 1 group trên máy, định dạng của dòng gồm nhiều cột giá trị, dấu `:` được sử dụng để phân cách giữa các cột
- Ý nghĩa
  - 1 - Tên group
  - 2 - Mật khẩu group được mã hóa
  - 3 - Mã nhóm (gid)
  - 4 - Danh sách các user nằm trong nhóm
## File /etc/gshadow
- Chứa thông tin password của group
- Ý nghĩa:
  - 1 - Tên group
  - 2 - Mật khẩu của group đã được mã hóa
    - Để trống: không có mật khẩu
  - 3 - Danh sách các user có quyền admin trên group này
  - 4 - Danh sách các user có trong group
## Các lệnh quản lý group
### groupadd
- Là lệnh tạo group
```
groupadd [options] [group_name]
```
- Option: 
  - `-g`: định nghĩa nhóm cùng mã nhóm (gid)
### gpasswd
- Tạo mật khẩu cho group
```
groupwd [group_name]
```
### groupmod
- Là lệnh sửa thông tin group
```
groupmod [options] [group_name]
```
- Options:
  - `-g`:sửa lại mã nhóm(gid)
  - `n`: sửa lại tên group
### groupdel
- Dùng để xóa 1 group
```
groupdel [group_name]
```
## Thay đổi thông số mặc định
- Khi sử dụng lệnh `useradd` hoặc `groupadd`, nếu chúng ta không liệt kê đầy đủ các thông số cần thiết thì hệ thống sẽ lấy theo giá trị mặc định đã được định nghĩa
- Chúng ta có thể thay đổi định nghĩa những giá trị này trong các file sau:
  - `/etc/login.defs`: file chứa thông số mặc định khi tạo user hoặc tạo group
  - `etc/skel/`: tất cả những file và thư mục con nằm trong thư mục này sẽ được copy sang thư mục home của thư mục mới tạo
## Practice and Question
- Câu 1: Tạo user có tên là test_user với group mặc định?(group ấy sẽ có tên là gì)
- Câu 2: Tạo user có tên là test_user1, và user này thuộc group **group_test**(ở đây group_test đã tồn tại)
- Câu 3: Đặt mật khẩu cho test_user1?
- Câu 4: Chỉ định cho test_user1 thuộc group test_user?
- Câu 5: Đổi tên user **test_user1** thành **test_user2** và đổi tên thư mục home nó thành của **test_user2**(lưu ý các file thư mục củ của user vẫn phải còn tồn tại sau khi đổi tên user)
- Câu 6: chỉ định shell cho **test_user2** thành /bin/sh?