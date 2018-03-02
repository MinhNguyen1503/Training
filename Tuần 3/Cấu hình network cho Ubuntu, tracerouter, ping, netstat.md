# Cấu hình network cho Ubuntu

----
## Mục lục
> ### 1. Giao diện mạng
> ### 2. Cách cấu hình địa chỉ IP 
> ### 3. Sử dụng lệnh traceroute
> ### 4. Sử dụng lệnh netstat

----

## 1. Giao diện mạng
Mỗi máy tính cần có một card mạng Ethernet có dây hoặc không dây.  

- Nhận dạng bởi tên: **ethX**.
 - eth0 cho card mạng thứ nhất
 - eth1 cho card mạng thứ 2, ....
- Xem có bao nhiêu giao diện Ethernet
 `ifconfig ­a | grep eth` 
- Xem tất cả các giao diện mạng `sudo lshw ­class network`. 

----
 

## 2. Các cách cấu hình địa chỉ IP
- **Cấu hình IP tạm thời**: Sẽ mất sau khi reboot máy tính.
- **Cấu hình IP tĩnh**: Cấu hình vẫn giữ sau khi reboot máy tính.
- **Cấu hình IP động**: Nhận địa chỉ IP một cách tự động từ một DHCP server.

### Cách cấu hình IP tạm thời
- Sử dụng lệnh ifconfig để đặt địa chỉ IP
- Xem tất cả giao diện mạng `ifconfig -a`  
- Xem cấu hình hiện tại  
**ifconfig {ethX}**
`ifconfig eth0`  
- Đặt cấu hình IP mới  
**ifconfig ethX IP-address netmask net-address**  
`ifconfig eth0 192.168.1.2 netmask 255.255.255.0`  

**Thực hành**  
• Cấu hình tạm thời cho máy tính X  
– **IP**: 192.168.1.X  
– **Netmask**: 255.255.255.0  
`sudo ifconfig eth0 192.168.1.X netmask 255.255.255.0`  
• **Kiểm tra nối kết với máy tính kế bên Y**  
– ping 192.168.1.Y  

![](https://i.imgur.com/cTQb1w5.png)

### Cách cấu hình IP tĩnh
• Thông tin về cấu hình IP lưu trong file **/etc/network/interfaces:**   

- Cấu hình IP tĩnh cho giao diện eth0  
**auto eth0  
iface eth0 inet static  
address 192.168.1.2  
netmask 255.255.255.1.0  
gateway 192.168.1.1**  

• Khởi động lại dịch vụ mạng để lấy cấu hình mới  
`sudo /etc/init.d/networking restart` 
 
**Thực hành**  

• Dùng phần mềm nano để biên soạn file
/etc/network/interfaces  

`sudo nano /etc/network/interfaces`

• Bổ sung các thông tin sau:  
**auto eth0
iface eth0 inet static  
Address 172.16.19.100+X  
Netmask 255.255.255.0  
Gateway 172.16.19.1**

![](https://i.imgur.com/DaKRutS.png)  

### Cách cấu hình IP động
 
• Thông tin về cấu hình IP lưu trong file **/etc/network/interfaces:**  
- Cấu hình IP động cho giao diện **eth0**  
- Chỉ thay từ khóa static bằng **dhcp**  
**auto eth0  
iface eth0 inet dhcp**  
![](https://i.imgur.com/5mG4VsY.png)  

### Tắt/mở giao diện mạng
- Tắt giao diện eth0 `sudo ifconfig eth0 down`  
- Mở giao diện eth0 `sudo Ifconfig eth0 up` . Sẽ lấy lại cấu hình lưu trong ** /etc/network/interfaces** 

----

## 3. SỬ dụng lệnh Tracerouter

- Lệnh `tracepath` cũng tương tự như `traceroute` nhưng nó không đòi hỏi các quyền quản trị. 
- Nó cũng được cài đặt mặc định trên Ubuntu còn tracerout thì không.
- Lệnh tracepath lần dấu đường đi trên mạng tới một đích chỉ định và báo cáo về mỗi nút mạng (hop) dọc trên đường đi. Nếu gặp phải các vấn đề về mạng, lệnh tracepath có thể chỉ ra vị trí lỗi mạng.  

![](https://i.imgur.com/BMzaiJ5.png)

----
## 4.Sử dụng netstat
Câu lệnh netstat đưa ra các thống kê khác nhau cho giao diện, bao gồm các socket mở và các bảng định tuyến.
![](https://i.imgur.com/WmdUoEs.png)

- Sử dụng câu lệnh `netstat –p` để xem các chương trình đi kèm với các socket mở.  

- Xem các thống kê chi tiết cho tất cả các cổng bằng câu lệnh `netstat –s`.





