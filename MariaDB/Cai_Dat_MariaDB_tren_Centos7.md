# Kết nối từ xa tới MariaDB
## Menu
[1. Cấu hình database server.](#CauHinhDatabseServer)

[2. Cài đặt phần mềm.](#CaiDatPhanMem)

[3. Tạo Database user và gán quyền cho user này trên database.](#TaoDatabaseUserVaGanQuyenChoUser)
- [3.1. Tạo Database và User trên Database](#TaoDatabaseVaUser)
- [3.2. Tìm kiếm User trong Database và kiểm tra quyền của User.](#TimKiemUser)
- [3.3. Xóa User trong Database.](#XoaUser)

## Mô hình
![remove connection](https://user-images.githubusercontent.com/84270045/148754819-c3549855-e61e-42dd-807f-326417c85d2e.png)



Trước tiên phải kiểm tra xem MariaDB đang chạy ở phiên bản nào, ta sử dụng lệnh `netstat -lutnp`
![port mariadb](https://user-images.githubusercontent.com/84270045/148676777-fdb90cd0-2f8e-43c5-b9d0-5788d5692819.png)
Hiện tại thì MariaDB đang chạy ở port 3306 và chạy trên IPv6. Nếu máy hiện đang chạy trên IPv4 thì sẽ không thể kết nối từ xa được.

<a name="CauHinhDatabseServer"></a>
### 1. Cấu hình database server.
Ta tiến hành truy cập vào MariaDB:
```
[root@duy ~]# mysql
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 15
Server version: 10.4.22-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```
Tại đây ta đưa ra câu lệnh query SELECT User, Host ở trong database mysql tương tác với bảng tới host có chữ `localhost`:

Nếu muốn có thể kết nối với MariaDB từ bất kì cái ip nào ở đường mạng `192.124.1.0/24` thì lúc này ta sử dụng câu lệnh `GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.1.%' IDENTIFIED BY 'Password' WITH GRANT OPTION;`

Dấu `%` là wildcard đại diện cho tất cả địa chỉ IP thuộc đường mạng `192.168.1.0/24` và mình quy định root database của mình bằng 1 password nào đó để tăng độ bảo mật (thay đổi Password mà bạn muốn vào "'Password'" ở câu lệnh trên).

Tại đây ta đưa ra câu lệnh query SELECT User, Host ở trong database mysql tương tác với bảng tới host có chữ `localhost`:
```
MariaDB [(none)]> SELECT User, Host FROM mysql.user WHERE Host <> 'localhost';
+---------------------+---------------+
| User                | Host          |
+---------------------+---------------+
| root                | 192.168.1.%   |
| root                | 192.168.124.% |
+---------------------+---------------+
3 rows in set (0.012 sec)
```
Sau khi hoàn thành thì đã có thể kết nối tới MariaDB từ xa.

<a name="CaiDatPhanMem"></a>
### 2. Cài đặt phần mềm 
Thực hiện kết nối từ Windows tới MariaDB. Ta tiến hành tải chương trình Navicat Premium. Sau khi cài đặt xong, ta truy cập vào Navicat và tiến hành kết nối:
![kết nối mariadb](https://user-images.githubusercontent.com/84270045/148677399-dd624f61-4086-48fa-b1e8-d18d3041cda7.png)

Xuất hiện giao diện:
![localhost](https://user-images.githubusercontent.com/84270045/148677442-9b2c941b-a072-4b4b-adb5-e23dff824142.png)

Tại đây ta tiến hành đặt 

`Connection Name: `: Đặt tùy ý

`Host: `: địa chỉ ip 
    
`Password: `: Password root database

Sau khi nhấn OK thì sẽ xuất hiện tên của kết nối ở bên trái màn hình, ta nhấn chuột phải vào và chọn `Open Connection`
![centos](https://user-images.githubusercontent.com/84270045/148677783-bdd73503-cca5-4d55-b26f-0a16243d0fd5.png)

Biểu tượng của kết nối sẽ chuyển từ màu xám sang màu vàng tức là đã mở kết nối thành công. Ta tiếp tục chuột phải vào tên của kết nối và chọn `Console...`
![console](https://user-images.githubusercontent.com/84270045/148677886-3cfdb577-9a93-4250-8f29-7af802b20aa3.png)
Sau khi chọn `Console` xong thì ta sẽ ở trong giao diện dòng lệnh điều khiển của Database Server.

<a name="TaoDatabaseUserVaGanQuyenChoUser"></a>
### 3. Tạo Database user và gán quyền cho user này trên database.

<a name="TaoDatabaseVaUser"></a>
##### 3.1. Tạo Database và User trên Database.
Ta sử dụng lệnh `CREATE database laiduy;` để tạo database có tên là `laiduy`
```
mariadb> CREATE databse laiduy;
Query OK, 1 row affected (0.02 sec)
```

Sau đó ta tạo 1 User tên là `laiduy_user` và có mật khẩu là `password`:
```
mariadb> CREATE USER 'khanhduy_user'@'localhost' IDENTIFIED BY 'password';
Query OK, 0 rows affected (0.01 sec)
```
 Và ta có thể cho User `khanhduy` có toàn quyền trên database `laiduy` bằng cách sử dụng lệnh: `GRANT ALL PRIVILEGES ON laiduy.* TO 'khanhduy_user'@'localhost';`
 ```
 mariadb> GRANT ALL PRIVILEGES ON laiduy.* TO 'khanhduy_user'@'localhost';
Query OK, 0 rows affected (0.01 sec)
```

<a name="TimKiemUser"></a>
##### 3.2. Tìm kiếm User trong Database và kiểm tra quyền của User.
Ta sử dụng lệnh: `SELECT User, Host FROM mysql.user`: chọn User và Host từ Databse Mysql.
```
mariadb> SELECT User, Host FROM mysql.user;
+---------------------+---------------+
| User                | Host          |
+---------------------+---------------+
| root'@192.168.124.% | %             |
| root                | 192.168.1.%   |
| root                | 192.168.124.% |
| khanhduy_user       | localhost     |
| laiduy_user         | localhost     |
| mariadb.sys         | localhost     |
| mysql               | localhost     |
| root                | localhost     |
| wpuser              | localhost     |
+---------------------+---------------+
9 rows in set (0.06 sec)
```
  
Để xem các quyền được cấp phát cho User vừa tạo, ta sử dụng lệnh: `SHOW GRANT FOR 'khanhduy_user'@'localhost';`
```
mariadb> SHOW GRANTS FOR 'khanhduy_user'@'localhost';
+----------------------------------------------------------------------------------------------------------------------+
| Grants for khanhduy_user@localhost                                                                                   |
+----------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `khanhduy_user`@`localhost` IDENTIFIED BY PASSWORD '*81E40896EAF96945283B847E296B16075109F08E' |
| GRANT ALL PRIVILEGES ON `laiduy`.* TO `khanhduy_user`@`localhost`                                                    |
+----------------------------------------------------------------------------------------------------------------------+
2 rows in set (0.06 sec)
```

<a name="XoaUser"></a>
##### 3.3. Xóa User trong Database.
Sử dụng lệnh: `REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'khanhduy_user'@'localhost';`
```
mariadb> REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'khanhduy_user'@'localhost';
Query OK, 0 rows affected (0.00 sec)
```

Ta có thể kiểm tra xem User đã được gỡ bỏ hay chưa bằng lệnh `SHOW GRANTS FOR 'khanhduy_user'@'localhost';` như ở trên. Ta có thể thấy kết quả mới khác với kết quả phía trên là đã bị mất đi dòng `GRANT ALL PRIVILEGES ON 'laiduy'.* TO 'khanhduy_user'@'localhost'`
```
mariadb> SHOW GRANTS FOR 'khanhduy_user'@'localhost';
+----------------------------------------------------------------------------------------------------------------------+
| Grants for khanhduy_user@localhost                                                                                   |
+----------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `khanhduy_user`@`localhost` IDENTIFIED BY PASSWORD '*81E40896EAF96945283B847E296B16075109F08E' |
+----------------------------------------------------------------------------------------------------------------------+
1 row in set (0.07 sec)
```

Để xóa User, ta sử dụng lệnh: `DROP USER 'khanhduy_user'@'localhost';`
```
mariadb> DROP USER 'khanhduy_user'@'localhost';
Query OK, 0 rows affected (0.00 sec)
```
 Ta có thể kiểm tra lại bằng lệnh: `SELECT User, Host FROM mysql.user;`
 ```
 mariadb> SELECT User, Host FROM mysql.user;
+---------------------+---------------+
| User                | Host          |
+---------------------+---------------+
| root'@192.168.124.% | %             |
| root                | 192.168.1.%   |
| root                | 192.168.124.% |
| laiduy_user         | localhost     |
| mariadb.sys         | localhost     |
| mysql               | localhost     |
| root                | localhost     |
| wpuser              | localhost     |
+---------------------+---------------+
8 rows in set (0.09 sec)
```

Vậy là ta đã kết nối từ xa tới MariaDB thành công, có thể tạo được Database và User trong Database đó.
