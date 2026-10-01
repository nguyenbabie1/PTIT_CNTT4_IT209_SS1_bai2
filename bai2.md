# Session 02 - Exercise 2: Create User and Configure Sudoers

## 1. Mục tiêu

Tạo user thường `devops`, thêm user vào nhóm `sudo`, sao chép SSH Key từ root sang user `devops` và cấu hình quyền truy cập SSH.

## 2. Tạo user devops

```bash
adduser devops
```

Kiểm tra:

```bash
id devops
```

## 3. Thêm devops vào nhóm sudo

```bash
usermod -aG sudo devops
```

Kiểm tra:

```bash
groups devops
```

Kết quả có nhóm:

```text
sudo
```

## 4. Sao chép SSH Key

```bash
rsync --archive --chown=devops:devops /root/.ssh /home/devops/
```

## 5. Phân quyền SSH

```bash
chmod 700 /home/devops/.ssh
chmod 600 /home/devops/.ssh/authorized_keys
chown -R devops:devops /home/devops/.ssh
```

Kiểm tra:

```bash
ls -ld /home/devops/.ssh
ls -l /home/devops/.ssh/authorized_keys
```

Kết quả:

```text
.ssh              -> 700
authorized_keys   -> 600
owner             -> devops:devops
```

## 6. Kiểm tra SSH Login

Từ máy cá nhân:

```bash
ssh -i /path/to/private_key devops@<IP_ADDRESS_DROPLET>
```

Sau khi đăng nhập:

```bash
whoami
```

Kết quả:

```text
devops
```

## 7. Kiểm tra quyền sudo

```bash
sudo whoami
```

Sau khi nhập mật khẩu của user `devops`, kết quả:

```text
root
```

## 8. Kết luận

User `devops` đã được tạo thành công, được thêm vào nhóm `sudo`, có thể đăng nhập bằng SSH Key và có thể thực hiện các lệnh quản trị thông qua `sudo`.
