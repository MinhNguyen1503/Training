# MySQL, PHP

## Cài đặt PHP

Để cài đặt PHP và các module PHP cho Apache trên Ubuntu, hãy gõ lệnh sau:  
`sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt`  

- Thiết lập cấu hình để nó ưu tiên index file index.php thay vì index.html bằng cách sửa file **/etc/apache2/mods-enabled/dir.conf** thành dưới đây (thêm index.php):

<IfModule mod_dir.c>
          DirectoryIndex index.php index.html index.cgi index.pl index.php index.xhtml index.htm
</IfModule>

- Sau đó khởi động lại apache
- Kiểm tra cách tạo file **info.php** trong thư mục với nội dung như sau: `<?php phpinfo(); ?>`




## Cài đặt MySQL
Trên Ubuntu sử dụng lệnh : `apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql`    


## Một số lệnh Transact-SQL (T-SQL) căn bản  
Trong cơ sở dữ liệu SQL, để tương tác với dữ liệu hay đối tượng cơ sở dữ liệu bạn cần sử dụng các đoạn lệnh được cung cấp bằng hệ quản trị cơ sở dữ liệu (CSDL). Trong bài viết này mình sẽ nói đến các lệnh T-SQL trong SQL Server. Cũng tương tự nhưng ở các hệ quản trị CSDL khác, thì nó cũng được chia thành 2 loại là loại ngôn ngữ thao tác với dữ liệu (DML – Data manipulation language), thường được các lập trình viên sử dụng và loại ngôn ngữ định nghĩa dữ liệu, tương tác với đối tượng trong CSDL (DDL – data definition language) thường được các nhà quản trị csdl (DBA) sử dụng.  

## 1. Các nhóm lệnh thao tác dữ liệu -DML

![](https://tuandc.com/wp-content/uploads/2017/06/DML-SQL.png)
Đây là nhóm lệnh phổ biến được dùng nhiều trong các phần mềm để thao tác đến các dữ liệu. Nhóm này bao gồm 4 lệnh cơ bản sau:  

### Lệnh SELECT trong SQL Server 

- Lệnh được sử dụng để truy xuất các tập kết quả của các cột hay các hàng trong CSDL.
 Cú pháp: `SELECT tên_cột FROM Tên_bảng.`
- Trong lệnh select bạn có thể tạo ra các trường tính toán hoặc nối các bảng dữ liệu lại với nhau để truy vấn. ví dụ mình có 2 bảng sinh_vien và diem mình sẽ nối như sau:  
 `SELECT * FROM sinh_vien join diem ON sinh_vien.id = diem.id_sinhvien`.
- Trong SELECT còn có 2 phép Join là **Inner join** (chỉ hiển thị các dòng có các trường bằng nhau) và **outer join** (hiển thị cả những dòng không có trường bằng nhau).  
- Trong phần tên_cột bạn có thể thêm AS để đặt trên cho cột đó ví dụ:   `SELECT (toan+ly) AS diemtoanly FROM sinh_vien join diem ON sinh_vien.id = diem.id_sinhvien.`  

### Lệnh INSERT trong SQL Server 

- Để thêm dữ liệu vào CSDL bạn cần một câu lệnh để làm việc này và đó là lệnh INSERT.
- Cú pháp: `INSERT INTO Tên_bảng (tên_các_trường) VALUES (giá_trị_thêm)`.
- Trong lệnh này nếu muốn thêm vào dữ liệu có hỗ trợ chữ tiếng việt có đấu bạn phải thêm chữ N phía trước. Ví dụ:  
 `INSERT INTO sinh_vien (ten_sinh_vien, tuoi) VALUES (N"Tuấn",18).`

### Lệnh UPDATE trong SQL Server  

- Để cập nhật, thay đổi dữ liệu cần sử dụng một câu lệnh có tên UPDATE.
- Cú pháp: `UPDATE Tên_bảng SET tên_trường = giá_trị WHERE điều kiện.`
- Với lệnh này bạn thường phải đưa ra điều kiện để xác định, thông thường là trường ID, ví dụ:  
 `UPDATE sinh_vien SET ten = N"Tuấn ĐC" WHERE id=1.`

### Lệnh DELETE trong SQL Server

 - Mặc dù lệnh DELETE rất ít được sử dụng trong các vấn đề yêu cầu sự toàn vẹn và không để mất mát dữ liệu, nhưng lệnh này cũng được đưa ra như một vấn đề tất yếu.
- Cú pháp: `DELETE FROM tên_bảng WHERE điều_kiện.`
- Trong lệnh này bạn không cần đưa vào trường nhưng bạn cần đưa vào điều kiện để xóa. Nếu không có điều kiện dữ liệu trong bảng có thể bị xóa hết.  

### Tạo Procedure trong SQL Server

- Procedure là thủ tục được lưu trữ sẵn trong csdl. Nó được sử dụng để hạng chế phần mềm truy vấn thẳng để các bảng hay trường của csdl, thay vào đó chỉ cần truyền đến các thông số hoặc gửi yêu cầu.
- Cú pháp: `CREATE PROCEDURE tên_thủ_tục @Tham_số [kiểu_dữ_liệu] AS Lệnh_DML.`
- Cú pháp thực thi: `EXEC tên_thủ_tục 'Tham số'.`
- ví dụ: `CREATE PROCEDURE lay_du_lieu_sv @so_luong int AS SELECT TOP @so_luong FROM sinh_vien.`

----

## 2. Các nhóm lệnh định nghĩa dữ liệu – DDL
![](https://tuandc.com/wp-content/uploads/2017/06/DDL-SQL.png)
Các nhóm lệnh này rất ít được sử dụng bởi các phần mềm, tuy nhiên chúng là những lệnh rất quan trọng có thể làm thay đổi csdl ở mức lớn nhất. Nhóm lệnh này thường chỉ được sử dụng bởi các Database Admin (DBA).  

### Lệnh CREATE DATABASE trong SQL Server

- Trong một hệ quản trị csdl có chứa rất nhiều csdl. các hệ hỗ trợ những đoạn lệnh khác nhau để tạo ra một database. Trong SQL Server cũng có câu lệnh để làm việc này.
- Cú pháp: `CREATE DATABASE tên_csdl;`

### Lệnh CREATE TABLE trong SQL Server

- Chúng ta đã biết trong một database sẽ có nhiều bảng (table), để tạo ra các bảng ta có câu lệnh để tạo bảng.
- Cú pháp: `CREATE TABLE tên_bảng (tên_cột_1 [kiểu_dữ_liệu],  tên_cột_2 [kiểu_dữ_liệu],....);`

### Lệnh ALTER TABLE trong SQL Server

- SQL hỗ trợ các lệnh thay đổi bảng sau khi đã tạo như thêm (ADD) các trường (cột), Xóa (DROP) các trường, Sửa (ALTER) các trường.
- Cú pháp thêm cột vào bảng: `ALTER TABLE Tên_bảng ADD Tên_cột [kiểu_dữ_liệu];`
- Cú pháp xóa một cột trong bảng: `ALTER TABLE Tên_bảng DROP COLUMN Tên_cột;`
- Cú pháp sửa một cột trong bảng: `ALTER TABLE Tên_bảng ALTER COLUMN Tên_cột [kiểu_dữ_liệu];`

### Lệnh DROP DATABASE trong SQL Server

- Bạn có thể sử dụng lệnh DROP để xóa đi một database trong SQL. Tuy nhiên đây là lệnh hạn chế sử dụng nhất.
- Cú pháp: `DROP DATABASE Tên_bảng;`

### Lệnh DROP TABLE trong SQL Server

- Mặc dù không khuyến khích nhưng nó vẫn thường xuyên được sử dụng để loại bỏ đi các bảng thừa. Mặc dù có thể dùng Management studio (SSMS) để thực hiện việc này nhanh hơn nhưng với lệnh bạn có thể thao tác nhanh hơn.
- Cú pháp: `DROP TABLE Tên_bảng;`

---