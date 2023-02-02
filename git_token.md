# Tạo token
- Cứ tài liệu chuẩn của hãng mà phang thôi
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
# Lưu token cho nhưng lần push tiếp theo
- Tạo một file `~/.netrc` file ở trong thư mục home với nội dung như sau
```
machine github.com login <login-id> password <token-password>
```

- Git push không c?n dang nh?p sau l?n th? 2
```
git config credential.helper cache
```
