### Cấu hình ip tĩnh
 # 1. TOPO LAB
- Giả lập trên VMware Workstation.
- Centos 7 Minimal-2009 Server 64 bit và Ubuntu 20.04
- Cần có ít nhất 2 máy để ping địa chỉ IP qua lại: máy vật lí, máy ảo và ubunbu
# 2. Mô hình
![ip tĩnh](https://user-images.githubusercontent.com/84270045/141457434-0ba23097-3f35-4412-b98d-cbbdb86c0b92.png)
# 3. Tiến hành cấu hình ip tĩnh
### 3.1. Cấu hình ip trên Centos 7.
- Kiểm tra card mạng tương ứng: Ta sử dụng lệnh `ip link show`.

![ip link show](https://user-images.githubusercontent.com/84270045/141282521-13359b2b-d0b8-4e70-8a35-3bb9c606d9a3.png)
- Giờ ta có card mạng `ens33` thì ta cần tạo 1 file cấu hình có tên tiền tố là `ifcfg-<tên card mạng>` trong thư mục `/etc/sysconfig/network-scripts/`. Ví dụ dưới đây thì ta sẽ tạo file `ifcfg-ens33`.
```
[root@client ~]# vi /etc/sysconfig/network-scripts/ifcfg-ens33
```
![Screenshot_1](https://user-images.githubusercontent.com/84270045/141282981-4dad87e7-ff26-4a7a-809c-82eee146e3eb.png)
- Sau khi đã hoàn tất cấu hình IP tĩnh như trên thì ta sẽ khởi động lại dịch vụ network trên CentOS 7.
```
[root@client ~]# systemctl restart network
```
 **Vậy là bạn đã hoàn tất các thao tác để có thể tự cài đặt địa chỉ IP tĩnh trên CentOS 7 rồi.**
 ### 3.2 Cấu hình ip tĩnh trên Ubuntu20.
 - Chuột phải và chọn Open Terminal.
 
 ![mở terminal](https://user-images.githubusercontent.com/84270045/141457781-d4ff3533-473c-4dcd-9f0b-3933ba11b25a.png)
 - Sử dụng lệnh `nmcli dev show` để kiểm tra địa chỉ Gateway của máy.
 
 ![gateway](https://user-images.githubusercontent.com/84270045/141458087-bc6d4cc1-30fb-48a6-81c9-04643c07428e.png)
 - Tiếp theo sử dụng lệnh `nm-connection-editor` để mở bảng Network Connections.
 
 ![Network](https://user-images.githubusercontent.com/84270045/141458603-faf8435e-0824-4f58-b96f-fad11445deb5.png)
 
 #### Đặt địa chỉ ip mới:
 B1: Chọn IPv4 Settings
 
 B2: Tại dòng Method chọn Manual
 
 B3: Ấn vào `Add` để thêm địa chỉ IP
 
 B4: Nhập địa chỉ IP mới, Subnetmask và địa chỉ Gateway (địa chỉ Gateway phải trùng với Gateway của máy)
 
 B5: Nhập địa chỉ DNS
 
 B6: Ấn `Save`
 
 ![ip mới của ubuntu](https://user-images.githubusercontent.com/84270045/141461420-1e960dc2-1e51-47db-97c5-c7a5cd138c4b.png)
  ## Vậy là đã hoàn thành công việc đặt địa chỉ IP tĩnh.
