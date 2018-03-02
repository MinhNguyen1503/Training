## Sự khác biệt giữa upgrade, dist-upgrade và full-upgrade trong ubuntu

## Mục lục

> ### 1. Lệnh apt-get upgrade
> ### 2. Lệnh apt-get dist-upgrade
> ### 3. Lệnh apt full-upgrade
----

![](https://i1.wp.com/echip.pro/wp-content/uploads/2017/01/2-1.png?resize=768%2C576)

## 1. Lệnh apt-get upgrade
- khi bạn sử dụng lệnh `apt-get-upgrade` để cập nhật phần mềm. Lệnh này chỉ thực hiện nâng cấp cho những gói phần mềm cần được **cập nhật theo hình thức thay thế** những gói tin cũ bằng những gói mới hơn.
- Tuy nhiên, lệnh này **không có khả năng cập nhật cho những phần mềm cập nhật theo cách thêm mới hoặc xóa bỏ gói tin cũ trước khi nâng cấp.**

----

## 2. Lệnh apt-get dist-upgrade


![](https://i2.wp.com/echip.pro/wp-content/uploads/2017/01/change-948009_1280.jpg?resize=768%2C432)

- Đối với những gói phần mềm không thể nâng cấp bằng lệnh `apt-get-upgrade`, chúng ta cần phải sử dụng lệnh `apt-get dist-upgrade`.
-  Lệnh này sẽ thực hiện việc nâng cấp cho những gói phần mềm **theo cách thêm gói tin mới hay cần xóa những gói tin cũ** khi cập nhật phiên bản mới.
- Lệnh này thường được sử dụng trong trường hợp cập nhật những gói tin **liên quan đến kernel**.
 - Ví dụ như kernel Linux-image.

----

## 3.Lệnh apt full-upgrade
- Lệnh `apt full-upgrade` sẽ thực hiện chức năng **nâng cấp các gói tin của hệ thống và sẽ loại bỏ các gói cài đặt cũ** đang hiện có nếu điều này là cần thiết.
- Lệnh `apt full-upgrade` chỉ mới xuất hiện gần đây, đặc biệt là từ **phiên bản Ubuntu 16.04**.
- Xét về mặt tổng thể, lệnh `apt full-upgrade` có tính năng khá giống với `apt-get dist-upgrade`.


## Sự khác biệt giữa Update và Upgrate

### Upgrade (nâng cấp)
Thuật ngữ này dùng chỉ việc thay thế phần cứng, phần mềm, filmware,… bằng phiên bản mới cao cấp hơn giúp tăng khả năng hoạt động hệ thống.  

Ví dụ:  
- nâng cấp RAM từ 256MB lên 1GB  
- nâng cấp HDD từ 40GB lên 200GB  
- nâng cấp WindowsXP lên WindowsVista  

### Update (cập nhật)
Thuật ngữ này thường được dùng chỉ việc cập nhật phần mềm những bộ file sửa lỗi, bảo mật,… hay bổ sung thêm chức năng giúp đối tượng được update thích nghi tốt hơn với tình hình thực tế.  

Ví dụ:  
- cập nhật các bản vá lỗi cho Windows  
- cập nhật mã virus cho các chương trình anti-virus  