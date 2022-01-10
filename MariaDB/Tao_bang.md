# Tạo bảng trong MariaDB
## Menu
[1. Truy cập MariaDB.](#TruyCapMariaDB)

[2. Sử dụng Database để làm nơi lưu trữ bảng.](#SuDungDatabaseDeLuuTru)

[3. Tạo bảng.](#TaoBang)






<a name="TruyCapMariaDB"></a>
### 1. Truy cập MariaDB.
Sử dụng câu lệnh `mysql` để truy cập vào MariaDB.
```
[root@duy ~]# mysql
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 18
Server version: 10.4.22-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

<a name="SuDungDatabaseDeLuuTru"></a>
### 2. Sử dụng Database để làm nơi lưu trữ bảng.
Sử dụng lênh `show databses;` để xem các databases hiện có:
```
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| laiduy             |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.001 sec)
```
Sau đấy ta lựa chọn Database bằng lệnh `use 'ten_database'`. Ở đây mình dùng database `laiduy`:
```
MariaDB [(none)]> use laiduy
Database changed
MariaDB [laiduy]>
```

<a name="TaoBang"></a>
### 3. Tạo bảng.
Sử dụng câu lệnh `create table 'ten_bang'`:
```
MariaDB [laiduy]> create table tkb (
    -> Ten_mon nVarchar(30),
    -> So_tin_chi Int,
    -> Ngay_bat_dau Date,
    -> Giang_vien nVarchar(30)
    -> );
Query OK, 0 rows affected (0.054 sec)
```
Vậy là ta đã tạo bảng thành công. Để hiển thị lên bảng vừa tạo, ta sử dụng lệnh `describe 'ten_bang'`:
```
MariaDB [laiduy]> describe tkb;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| Ten_mon      | varchar(30) | YES  |     | NULL    |       |
| So_tin_chi   | int(11)     | YES  |     | NULL    |       |
| Ngay_bat_dau | date        | YES  |     | NULL    |       |
| Giang_vien   | varchar(30) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
4 rows in set (0.016 sec)
```