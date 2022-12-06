# Zip
- Cài đặt chương trình zip/unzip
```
yum install -y zip unzip
```
- Nén file/thư mục:
```
zip -r ten_file.zip file/thu_muc_can_nen
```
- Nén file / thư mục có mật khẩu bảo vệ được mã hóa
```
zip -er ten_file.zip file_can_nen
```
- Nén file/thư mục và xóa thư mục gốc
```
zip -m -r newfile.zip file/thu_muc_can_nen
```
- Thêm một file vào thư mục nén
```
zip -u -r newfile.zip newfile_add
```
# Unzip
- Giải nén file
```
unzip file.zip
```
- Giải nén vào một thư mục cụ thể
```
unzip -d thu_muc file.zip
```

