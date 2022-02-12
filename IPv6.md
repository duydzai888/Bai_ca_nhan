# IPv6
## Menu
[1. Cách biểu diễn địa chỉ IPv6.](#CachBieuDien)

[2. Phân loại IPv6.](#PhanLoai)
- [2.1. Địa chỉ Unicast.](#Unicast)
- [2.2. Địa chỉ Multicast.](#Multicast)
- [2.3. Địa chỉ Anycast.](#Anycast)




<a name="CachBieuDien"></a>
### 1. Cách biểu diễn địa chỉ IPv6.
Địa chỉ IPv6 không được trình bày ở dạng thập phân như địa chỉ IPv4 mà ở dạng thập lục phân, do IPv6 có chiều dài 128 byte nên IPv6 được quy ước chia thành 8 nhóm, mỗi nhóm gồm 2 byte và cách nhau bởi dấu ":" (hai chấm).

                            X:X:X:X:X:X:X:X

Trong đó: X là 2 byte ở dạng thập lục phân

VD: 2031:3051:130F:E0F1:90CD:9C0A:876A:130B

Đối với những nhóm có giá trị 0 ở đầu thì có thể lược bỏ đi.

VD:
2031:0517:130F:E0F1:90CD:0C0A:876A:130B

-> 2031:517:130F:E0F1:90CD:C0A:876A:130B

Đối với những nhóm có giá trị 0 liên tiếp, có thể rút gọn lại là "::".

VD: 2031:2517:0000:0000:0000:1C0A:876A:130B

-> 2031:2517::1C0A:876A:130B

Nhưng cách rút gọn này chỉ được 1 lần thực hiện.

VD: 2031:0517:0000:0000:A5C7:0000:0000:130B

-> 2031:0517::A5C7::130B (Sai)

-> 2031:517::A5C7:0:0:130B (Đúng)

<a name="PhanLoai"></a>
### 2. Phân loại IPv6.
IPv6 có 3 loại địa chỉ chính: Unicast, Multicast và Anycast.

<a name="Unicast"></a>
##### 2.1. Địa chỉ Unicast
Địa chỉ Unicast là địa chỉ định danh cho một thiết bị (interface hay card mạng). Một gói tin được gửi đến địa chỉ Unicast là được chuyển đến interface định danh bởi địa chỉ đó. Địa chỉ Unicast có 2 loại:

`Link local`: Địa chỉ link local cho phép kết nối các thiết bị nội bộ với nhau, địa chỉ này không có khả năng định tuyến và chỉ sử dụng trong cùng một lớp mạng. Địa chỉ local prefix có dạng như sau: `FE80::/10`

![link local](https://user-images.githubusercontent.com/84270045/152124532-26406622-5c8e-4b26-aab0-f114b1a28082.png)

![ipv6](https://user-images.githubusercontent.com/84270045/152124246-ea2fbd50-93cf-486c-be5c-3af63afe27a9.png)

`Global Unicast`: Địa chỉ này tương tự như địa chỉ Public IPv4, nghĩa là địa chỉ này được định tuyến và sử dụng trên internet.
![Screenshot_2](https://user-images.githubusercontent.com/84270045/152125889-b28f7553-08f1-47b9-ac6c-44ec516a6c67.png)

- `Registry`: định danh các vùng.
- `ISP Prefix`: định danh các nhà cung cấp dịch vụ.
- `Site Prefix`: định danh các doanh nghiệp, tổ chức.
- `Subnet Prefix`: định dạng mạng nhỏ hơn trong doanh nghiệp, tổ chức.

3 byte đầu tiên được gán giá trị 001. Do đó, địa chỉ Global Unicast thường có dạng `2001::/3`.

<a name="Multicast"></a>
##### 2.2. Địa chỉ Multicast.
Địa chỉ Multicast định danh nhiều host/interface. Một gói tin khi gửi đến địa chỉ này có nghĩa nó sẽ được gửi đến các host/interface tương ứng. Địa chỉ Multicast thường có Prefix là `FF00::/8`

**Cấu trúc của địa chỉ Multicast**
- 8 bit đầu là 1111 1111: định danh của địa chỉ Multicast.
- 4 bit tiếp theo là Flags: 3 bit đầu thường không được sử dụng, bit cuối. Bit thứ 4: 0 là giá trị được gán bởi IANA và 1 địa chỉ tạm thời, sử dụng trong nội bộ.
- 4 bit kế tiếp là Scope: quy định phạm vi của địa chỉ Multicast.
- 112 bit còn lại: định danh nhóm các host/interface có cùng địa chỉ Multicast.

<a name="Anycast"></a>
#### 2.3. Địa chỉ Anycast.
Địa chỉ Anycast là địa chỉ được gán cho một nhóm các host/interface không cùng một node mạng. Khi một gói tin được gửi đến địa chỉ Anycast, nó sẽ được gửi đến host/interface nghĩa là đó chính là địa chỉ Anycast. Địa chỉ Anycast về mặt cấu trúc thì không khác gì so với địa chỉ Unicast vì nó được cấp phát từ không gian địa chỉ Anycast. Việc gán địa chỉ Unicast cho nhiều hơn 1 host/interface nghĩa là đó chính là địa chỉ Anycast


