# Create custom commands in Linux
## Method 1
- Step 1: `vi ~/.bash_profile`
- Step 2: Sửa dòng `PATH=$PATH:$HOME/bin` thành `PATH=$PATH:$HOME/bin:.`
- Step 3: `source ~/.bash_profile`
## Method 2
- Step 1: `vi ~/.bash_profile`
- Step 2: thêm dòng muốn tạo câu lệnh theo cú pháp
`alias [ten_cau_lenh]=' [command 1]; [command 2]; ,,,, [command n]'
