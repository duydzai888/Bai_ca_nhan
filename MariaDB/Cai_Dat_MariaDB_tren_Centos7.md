# Cài đặt MariaDB trên Centos7
## Menu
[1. Cấu hình Repo của MariaDB](#CauHinhRepo)

[2.Cài đặt và thiết lập bảo mật MariaDB](#CaiDatVaThietLap)




<a name="CauHinhRepo"></a>
### 1. Cấu hình Repo của MariaDB
Trước khi cài đặt Mariadb bạn cần chú ý là hệ điều hành chưa có cài đặt Mysql hoặc Mariadb nào trước đó để tránh việc mất dữ liệu hoặc gây ra lỗi sau khi cài đặt.

Trong hướng dẫn này mình sẽ hướng dẫn cài đặt MariaDB trên CentOS7 với yum từ repo MariaDB.

Bạn có thể cấu hình các repo dựa theo hệ điều hành mà bạn sử dụng, MariaDB có thể cài đặt trên nhiều hệ điều hành khác nhau không phải chỉ cài được trên CentOS7.

Hoặc có cách khác đơn giải hơn là sử dụng tập lệnh cấu hình repo của MariaDB bằng lệnh sau: `curl -sS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | bash -s -- --mariadb-server-version="mariadb-10.4"`. Sau khi nhập lệnh ta ấn Enter và để quá trình cài đặt tự chạy. 


<a name="CaiDatVaThietLap"></a>
### 2. Cài đặt và thiết lập bảo mật MariaDB
Sau khi cài đặt repo hoàn tất ta có thể cài đặt MariaDB bằng lệnh: `yum install MariaDB-server MariaDB-client -y`

```
[root@duy ~]# yum install MariaDB-server MariaDB-client -y
Loaded plugins: fastestmirror
Determining fastest mirrors
 * base: mirrors.cloudfly.vn
 * extras: mirrors.cloudfly.vn
 * updates: mirrors.bkns.vn
base                                                                                                                                   | 3.6 kB  00:00:00
extras                                                                                                                                 | 2.9 kB  00:00:00
mariadb-main                                                                                                                           | 3.4 kB  00:00:00
mariadb-maxscale                                                                                                                       | 2.5 kB  00:00:00
mariadb-tools                                                                                                                          | 2.9 kB  00:00:00
updates                                                                                                                                | 2.9 kB  00:00:00
(1/8): base/7/x86_64/group_gz                                                                                                          | 153 kB  00:00:00
(2/8): extras/7/x86_64/primary_db                                                                                                      | 243 kB  00:00:01
(3/8): mariadb-main/updateinfo                                                                                                         | 5.7 kB  00:00:03
(4/8): base/7/x86_64/primary_db                                                                                                        | 6.1 MB  00:00:04
(5/8): mariadb-main/primary_db                                                                                                         |  61 kB  00:00:04
(6/8): mariadb-tools/primary_db                                                                                                        |  17 kB  00:00:04
(7/8): mariadb-maxscale/primary_db                                                                                                     | 7.1 kB  00:00:05
(8/8): updates/7/x86_64/primary_db                                                                                                     |  13 MB  00:00:06
...
Replaced:
  mariadb-libs.x86_64 1:5.5.68-1.el7

Complete!
```
Sau khi nhận được thông báo cài đặt `Complete!` chúng ta sẽ khởi động MariaDB server và bắt đầu thiết lập bảo mật  cho Mariadb bằng các lệnh sau:
- `systemctl enable mariadb`: Cho phép MariaDB khởi động khi reboot server

- `systemctl start mariadb`: Khởi động Mariadb

- `mysql_secure_installation`: Thiết lập bảo mật cho Mariadb

Sau khi chạy lệnh `mysql_secure_installation` thì sẽ xuất hiện các lựa chọn, ta tiến hành chọn như sau:
```
Enter current password for root (enter for none): Nhấn phím Enter
Switch to unix_socket authentication [Y/n]: n
Change the root password? [Y/n]: Y
New password: Nhập password root các bạn muốn tạo
Re-enter new password: Nhập lại password root
Remove anonymous users? [Y/n] : Y
Disallow root login remotely? [Y/n]: Y
Remove test database and access to it? [Y/n] : Y
Reload privilege tables now? [Y/n]: Y
```
Kết quả:
```
[root@duy ~]# mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password or using the unix_socket ensures that nobody
can log into the MariaDB root user without the proper authorisation.

You already have your root account protected, so you can safely answer 'n'.

Switch to unix_socket authentication [Y/n] n
' ... skipping.

You already have your root account protected, so you can safely answer 'n'.

Change the root password? [Y/n] n
You already have your root account protected, so you can safely answer 'n'.

Change the root password? [Y/n] n
 ... skipping.

By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] Y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] Y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] Y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] Y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```

Như vậy là đã cài đặt hoàn tất, bạn có thể dùng lệnh sau để truy cập MariaDB để kiểm tra hoạt động: `mysql -u root -p`

Lưu ý: ***Sau khi gõ lệnh trên hệ thống sẽ yêu cầu bạn nhập mật khẩu root Mariadb mà bạn đã khởi tạo trong phần `mysql_secure_installation` trước đó.***
```
[root@duy ~]# mysql -u root -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 8
Server version: 10.4.22-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> 
```
Hoặc ta có thể sử dụng lệnh `mysql -v`

Sau khi hoàn tất bạn chỉ cần gõ lệnh `mysql` để truy cập vào MariaDb
