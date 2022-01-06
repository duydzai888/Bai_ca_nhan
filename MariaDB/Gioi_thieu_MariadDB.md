# MariadDB
## Menu
[1. MySQL](#MySQL)

[2. MariaDB](#MariaDB)

[3. Các ưu điểm của MariaDB](#UuDiem)

`MariaDB` là hệ quản trị cơ sở dữ liệu miễn phí được phát triển từ hệ quản trị cơ sở dữ liệu mã nguồn mở `MySQL`

<a name="MySQL"></a>
### 1. MySQL
`MySQL` được công ty Thụy Điển MySQL AB phát triển. Công ty công nghệ Mỹ Sun Microsystem sau đó giữ quyền sở hữu MySQL sau khi mua lại MySQL vào năm 2008. Năm 2010, gã khổng lồ Oracle mua Sun Microsystems và MySQL thuộc quyền sở hữu của Oracle từ đó.

`MySQL` là một hệ thống quản trị cơ sở dữ liệu mã nguồn mở (gọi tắt là RDBMS) hoạt động theo mô hình client-server. Với RDBMS là viết tắt của Relational Database Management System. 

MySQL được tích hợp apache, PHP. MySQL quản lý dữ liệu thông qua các cơ sở dữ liệu. Mỗi cơ sở dữ liệu có thể có nhiều bảng quan hệ chứa dữ liệu. MySQL cũng có cùng một cách truy xuất và mã lệnh tương tự với ngôn ngữ SQL. Phiên bản đầu tiên của MySQL phát hành vào năm 1995. 

Công ty Sun Microsystems mua lại MySQL AB trong năm 2008
Năm 2010 tập đoàn Oracle thâu tóm Sun Microsystems. Ngay lúc đó, đội ngũ phát triển của MySQL tách MySQL ra thành 1 nhánh riêng gọi là MariaDB. Oracle tiếp tục phát triển MySQL lên phiên bản 5.5.
- 2013 MySQL phát hành phiên bản 5.6
- 2015 MySQL phát hành phiên bản 5.7
- MySQL đang được phát triển lên phiên bản 8.0

<a name="MariaDB"></a>
### 2. MariaDB
`MariaDB` được phát triển nhằm thay thế công nghệ cơ sở dữ liệu `MySQL`, vì thế nó tương thích và cho một hiệu suất cao hơn so với `MySQL`.

`MariaDB` được Michael “Monty” Widenius, developer hàng đầu của MySQL dẫn dắt và phát triển. Ưu điểm lớn nhất của hệ quản trị này là tương thích với nhiều hệ điều hành, bao gồm Linux CentOS, Ubuntu và Window với các gói cài đặt tar, zip, MSI, rpm cho cả 32bit và 64bit với hiệu suất cao hơn so với MySQL. 

Năm 2008, sau khi Sun mua lại MySQL AB, Michael “Monty” Widenius rời khỏi MySQL AB và tiếp tục phát triển một hệ cơ sở quản trị mới của mình.

Đầu năm 2009, Michael cùng với 1 vài đồng nghiệp khác bắt đầu tiến hành dự án chuyên sâu về công cụ lưu trữ MySQL, sau này trở thành `MariaDB`. Tên gọi MariaDB được đặt tên theo tên con gái út của Widenius – `Maria`. Sau nhiều lần nâng cấp và phát triển, hiện tại MariaDB đã ra mắt phiên bản mới nhất là MariaDB 10.1.

MariaDB được hình thành dựa trên nền tảng của MySQL, vì thế nó kế thừa được hầu hết các chức năng cơ bản cần thiết của MySQL. Bên cạnh đó, MariaDB cũng phát triển thêm nhiều tính năng mới và có sự nâng cấp hơn về cơ chế lưu trữ, tối ưu máy chủ.

Số phiên bản của MariaDB tuân theo phiên bản của MySQL đến phiên bản 5.5. Như vậy, MariaDB 5.5 cung cấp tất cả các tính năng MySQL 5.5. Có khoảng cách giữa các phiên bản MySQL từ 5.1 đến 5.5, trong khi MariaDB phát hành phiên bản 5.2 và 5.3.

Sau phiên bản 5.5, các nhà phát triển của MariaDB quyết định bắt đầu một nhánh số 10, nỗ lực để làm rõ rằng MariaDB 10.0 sẽ không nhập tất cả các tính năng từ MySQL 5.6.

**Các phiên bản của MariaDB**
![Phiên bản mariadb](https://user-images.githubusercontent.com/84270045/148376864-d75907f7-c045-4803-b21e-d352125147d8.png)


<a name="UuDiem"></a>
#### 3. Ưu điểm của MariaDB
Các ưu điểm lớn nhất của MariaDB:
- Hoàn toàn miễn phí
- Khắc phục những hạn chế của MySQL
- Bổ sung thêm nhiều Engine hơn
- Kết hợp cả SQL và NoSQL
- Hỗ trợ tiếng Việt

Hướng dẫn cài đặt MariaDB cho Centos [tại đây](https://github.com/duydzai888/Tim_hieu_linux/blob/main/MariaDB/Cai_Dat_MariaDB_tren_Centos7.md)
