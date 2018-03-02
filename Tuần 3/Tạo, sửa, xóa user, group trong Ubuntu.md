# Tạo, sửa, xóa user, group trong Ubuntu

----

## Mục lục
> ### 1. User
> ### 2. Group

------

## 1. User

Ubuntu là hệ điều hành đa người dùng vì thế mỗi người muốn sử dụng được máy đều phải có một account . Một account bao gồm Username và password.
  
- Có **2 loại user** là **super user và regular user**. Để tạo một người dùng mới, thay đổi thuộc tính của một người dùng hay xóa bỏ một người dùng chỉ khi có quyền của một super user. Mỗi user có một định danh riêng là **UID**.   
- Cách **kiểm tra UID** ta gõ lệnh `sudo cat /etc/passwd`. File này lưu trữ tất cả các thông tin về user như sau:
 
![](https://i.imgur.com/bFWz3J0.png)

**Trong đó:**  

- Mỗi user nằm trên một dòng bao gồm các trường:  
`Tên tài khoản:Mật khẩu(đã được mã hóa):UID:GID:Tên đầy đủ của người sử dụng: thư mục home và shell đăng nhập`.  

- Một số **UID đặc biệt** : **UID = 0** (được gán cho *tài khoản root* là **super user**), **UID = 65534** (là *tài khoản người dùng*), **UID từ 1 đến 99** (Được dùng cho các *tài khoản dịch vụ*).
  
### 1.1 Để tạo một user mới ta dùng cú pháp:  
 `useradd [tùy chọn] "tên người dùng"`
  
- **Các tùy chọn**:  
 - `-d/home_directory`: **tạo thư mục** home cho người dùng.  
 - `-g group`: xác định **tài khoản người dùng thuộc nhóm** người dùng nào trên hệ thống.  
 - `-e date`: xác định **ngày mà tài khoản bị vô hiệu hóa** trên hệ thống.  
 - `-G groups`: xác định tài khoản người dùng thuộc những nhóm người dùng nào trên hệ thống.  
 - `-s shell`: xác định **shell mặc định của người dùng khi đăng nhập** vào hệ thống.  
 - `-u uid`: xác định **số user id** của người dùng.  

### 1.2  Để xóa một tài khoản người dùng
`userdel [tùy chọn] "tên người dùng"`  

- Trong câu lệnh xóa ta có thể thêm tùy chọn "option -r" để xóa thư mục home của người dùng và các file trong thư mục home.  
- Chỉnh sửa một tài khoản ta sử dụng cú pháp: `usermod [tùy chọn] "tên người dùng"`. Ta dùng các tùy chọn như phần **useradd** để sửa những thông số tương ứng như thư mục home, ngày tài khoản bị vô hiệu hóa,....  

----

## 2. Group
  
- Thông tin lưu trữ nhóm người dùng xem bởi lệnh:   `sudo cat /etc/group`  

![](https://i.imgur.com/98IDhh4.png)  

- Mỗi group nằm trên 1 dòng bào gồm:  
`nhóm người dùng : mật khẩu: số group id: các thành viên của nhóm được lưu trữ trong file này.`  

### 2.1 Tạo group dùng lệnh

`sudo groupadd [tùy chọn] "tên nhóm người dùng"`  

- **các tùy chọn:**  
 - `-g gid`: Đặt số group id cho nhóm người dùng.  
 - `-f`: Bắt câu lệnh chạy mà không thông báo lỗi nếu đã có một nhóm trên hệ thống trùng với tên nhóm đinh tạo .  

### 2.2 Xóa group  
`sudo groupdel "tên nhóm"` 

### 2.3 Chỉnh sửa nhóm 
`sudo groupmod [tùy chọn] "tên nhóm"`

- Chức năng của lệnh groupmod giống chức năng của usermod.
