# Remote Development using SSH
## Step 1
- Install the **Remote-SSH** extension in VScode
## Step 2
- SSH to server using mobaxterm and follow
```
ssh-keygen -t RSA -b 2048
```
```
cd ~/.ssh
mv id_rsa.pub authorized_keys
```
## Step 3
- Copy id_rsa to your folder in local(C Drive, can't SSH when save key in other Drive)
## Step 4
- Config file ssh_config
```
Host 192.168.20.10
    Hostname 192.168.20.10
    User root
    IdentityFile C:\Users\Vanhieu\.ssh\192.168.20.10\pri_key.pem
```
## Open terminal 
```
Ctrl + Shift + `
```


