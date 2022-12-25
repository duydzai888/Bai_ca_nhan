# Đổi port ssh 
### B1: Kiểm tra Port ssh
Để kiểm tra porh ssh hiện tại ta sử dụng lệnh `netstat` để kiểm tra
```
[root@laiduy ~]# netstat -nltp | grep sshd
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      877/sshd
tcp6       0      0 :::22                   :::*                    LISTEN      877/sshd
```
Nếu chưa có `netstat` ta có thể cài đặt nó bằng lệnh: `yum install net-tool -y`

Như kết quả phía trên, ta có thể thấy port ssh là port 22. Giờ ta sẽ tiến hành thay đổi sang một port khác.
### B2: Thay đổi Port ssh
File cấu hình ssh có tên `sshd_config` và nằm tại đường dẫn `/etc/ssh/sshd_config`. Ta có thể mở file này lên bằng lệnh `vi`, `vim`, hoặc `nano`. Tại đây mình sẽ sử dụng lẹnh `vi` để chỉnh sửa file.
```
vi /etc/ssh/sshd_config
```
Khi đã mở được file lên, ta tìm dòng `#port 22` sau đó bỏ dấu `#` và thay số `22` thành port mà ta muốn đổi. Ở đây mình chọn port ssh là `222`.
```
[root@laiduy ~]# vi /etc/ssh/sshd_config
#       $OpenBSD: sshd_config,v 1.100 2016/08/15 12:32:04 naddy Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/local/bin:/usr/bin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

# If you want to change the port on a SELinux system, you have to tell
# SELinux about this change.
# semanage port -a -t ssh_port_t -p tcp #PORTNUMBER
#
Port 222
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::
```
![alt](https://huongdan.azdigi.com/wp-content/uploads/2021/01/Screenshot-2021-01-19-at-20.30.36.gif)

Sau khi thay xong port mới, ta lưu lại cấu hình và khởi động lại dịch vụ ssh để nhận port mới.
```
[root@laiduy ~]# systemctl restart sshd.service
```
Để kiểm tra xem sever đã được đổi sang port mới hay chưa thì ta sử dụng lệnh `semanage port -l | grep ssh`.
```
[root@laiduy ~]# semanage port -l | grep ssh
ssh_port_t                     tcp      222, 22
```
Trường hợp máy bạn chưa có `semanage`thì chúng ta phải cài đặt trước. Sử dụng lệnh `yum install policycoreutils-python`để tạo. Sau khi tạo xong tiến hành kiểm tra như trên.
Cuối cùng là mở port mới cho dịch vụ ssh trên firewall
```
[root@laiduy ~]# firewall-cmd --permanent --add-port=222/tcp
```
Khởi động lại firewall để có hiệu lực:
```
[root@laiduy ~]# firewall-cmd --reload
```




# Cấu hình đăng nhập bằng người dùng
Ta truy cập file `sshd_config` và tìm dòng `#PermitRootLogin yes`. Sau đó ta xóa bỏ dấu `#` và sửa `yes` thành `no`. Lưu và thoát file.

Sau đó ta dùng lệnh `systemctl restart sshd` để reset SSH.

Lưu ý: Phải tắt SELinux.
