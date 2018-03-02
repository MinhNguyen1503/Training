# Các phím tắt và câu lệnh cơ bản trong Ubuntu

----

## Mục lục
> ## A) Các lệnh cơ bản
> ### 1. Các lệnh quản lí tập tin
> ### 2. Các lệnh quản lí hệ thống
> ### 3. Quản lí tiến trình
> ### 4. Quản lí mạng
> ## B) Các phím tắt
---

## A) Các lệnh cơ bản
### 1. Các lệnh quản lí tập tin
### Tạo tập tin và thư mục

| Lệnh | Mô tả |   
| ------------- |:-------------:|    
| cp file /folfer | Chép tập tin file vào thư mục folder |    
| cp file1 file2 | Chép tập tin file1 sang file2 |    
| cp -r folder1 folder2 | Chép toàn bộ nội dung của thư mục folder1 vào folder2 |  
|rsync -a folder1 folder2|Đồng bộ nội dung thư mục «folder1» sang thư mục «folder2»|  
|mv file1 file2|Chuyển tên tập tin file1 thành tên file2|  
|mv folder1 folder2|Chuyển tên thư mục folder1 thành folder2|  
|mv file folder|Chuyển tập tin file vào thư mục folder|  
|mv file1 folder2/file2|Chuyển file1 vào thư mục thư mục folder2 đồng thời đổi tên tập tin thành file2|  
|mkdir folder|Tạo ra thư mục folder|  
|mkdir -p folder1/folder2|Tạo ra thư mục cha folder1 và thư mục con folder2 cùng lúc|  
|rm file|Xóa bỏ tập tin file trong thư mục hiện hành|
|rmdir folder|Xóa bỏ thư mục trống mang tên folder
|rm -rf folder|Xóa bỏ thư mục mang tên folder với tất cả các tập tin trong thư mục|  
|ln -s file link|Tạo ra một liên kết mang tên link đến tập tin file (nối tắt)|  
|find folder -name|file Tìm tập tin mang tên file trong thư mục folder kể cả trong các thư mục con|
|diff file1 file2|So sánh nội dung của 2 tập tin hoặc của 2 thư mục|  

----

### Xem và chỉnh sửa nội dung các tập tin văn bản

|Lệnh|Mô tả|  
|---|--|  
|cat file|Xem nội dung của tập tin file trên màn hình ở dạng mã ASCII|      
|more file|Xem nội dung của tập tin file trên màn hình theo chế độ từng trang một : ấn phím «Enter» để xuống 1 dòng; ấn phím «Space» để sang thêm 1 trang ; ấn phím «q» để thoát.|  
|less file|«less» giống như «more», nhưng cho phép dùng phím Page Down|  
|head -n file|Xem số n dòng đầu tiên của tập tin file|  
|tail -n file|Xem số n dòng cuối cùng của file|  
|vi file|Soạn tập tin file dùng trình soạn vi|  
|nano file|Soạn tập tin file dùng trình soạn nano|  
|gedit file|Soạn tập tin file dùng trình soạn gedit|  
|grep keyword file|Tìm và hiển thị các dòng chứa từ keyword trong tập tin file|  
|grep -r string folder|Tìm nội dung string trong tất cả các tập tin có trong thư mục folder|  
|lệnh > file|Ghi kết quả của lệnh trong tập tin file|  
|lệnh >> file|Bổ sung kết quả của lệnh ở phần cuối của tập tin file|  

### Di chuyển, liệt kê tập tin và thư mục

|Lệnh|Mô tả|  
|---|---|  
|pwd|Hiển lên tên thư mục đang làm việc hiện hành|  
|cd|Di chuyển sang thư mục «/home/người_dùng»|cd ~ /Desktop|Di chuyển sang thư mục «/home/người_dùng/Desktop»|  
|cd ..|Di chuyển sang thư mục cha (ngay trên thư mục hiện hành)|  
|cd /usr/apt|Di chuyển sang thư mục «/usr/apt»|  
|ls -l|Folder liệt kê danh mục tập tin trong thư mục folder|  
|ls -a|Liệt kê tất cả các tập tin, kể cả các tập tin ẩn (thường có tên bắt đầu bằng một dấu chấm)|  
|ls -d|Liệt kê tên các thư mục nằm trong thư mục hiện hành|  
|ls -t|Xếp lại các tập tin theo ngày đã tạo ra, bắt đầu bằng những tập tin mới nhất|  
|ls -S|Xếp lại các tập tin theo kích thước, từ to nhất đến nhỏ nhất|  
|ls -l l more|Liệt kê theo từng trang một, nhờ tiện ích «more»|  
|dir|Giống như lệnh ls dùng để liệt kê tập tin và thư mục|  

### Nén và giải nén tập tin và thư mục


|Lệnh|Mô tả|  
|---|---|
|tar xvf archive.tar|Giải phóng các tập tin có trong tập tin « archive.tar », đồng thời hiển thị các tên tập tin|  
|tar xvfz archive.tar.gz|Giải nén các tập tin có trong tập tin « archive.tar.gz » dùng «gzip» và «tar»|  
|tar jxvf archive.tar.bz2|Giải nén các tập tin có trong tập tin «archive.tar.bz2» dùng « bzip » và «tar»|  
|tar cvf archive.tar file1 file2|Tạo ra một tập tin archive.tar chứa các tập tin file1, file2|  
|tar cvfz archive.tar.gz folder|Tạo một tập tin «archive.tar.gz» dùng «gzip» để chứa toàn bộ thư mục folder|  
|gzip file.txt|Tạo tập tin nén «file.txt» sang «file.txt.gz»|  
|gunzip file.txt.gz|Giải nén tập tin «file.txt.gz»|  
|bzip2 file.txt|Tạo tập tin nén «file.txt.bz2»|  
|bunzip2 file.txt.bz2|Giải nén tập tin «file.txt.bz2»|  

### Thiết lập quyền truy cập tập tin thư mục

|Lệnh|Mô tả|  
|---|---|  
|chown username|File xác định người chủ của tập tin file là người dùng mang tên « username »|  
|chown -R username folder|Xác định người chủ của thư mục folder, kể cả các thư mục con (-R) là người dùng « username»|  
|chgrp group file|Chuyển tập tin file thành sở hữu của nhóm người dùng mang tên group|  
|chmod u+x file|Giao (+) quyền thực thi (x) tập tin file cho người dùng (u)|  
|chmod g-w|File loại bỏ (-) quyền ghi (w) file của nhóm (g)|  
|chmod o-r l file|Loại bỏ (-) quyền đọc (r) tập tin file của những người dùng khác (o)|  
|chmod a+rw file|Giao (+) quyền đọc (r) và ghi (w) file cho mọi người (a)|  
|chmod -R a+rx folder|Giao (+) quyền đọc (r) và vào bên trong thư mục (x) folder, kể cả tất cả các thư mục con của nó (-R), cho tất cả mọi người (a)|  

-----

### 2. Các lệnh quản lí hệ thống

|Lệnh|Mô tả| 
|---|---|
|sudo command|Thực hiện lệnh command với quyền root|
|gksudo command|Giống với sudo nhưng dùng cho các ứng dụng đồ hoạ|
|sudo -k|	Chấm dứt chế độ dùng lệnh của quyền root|
|uname -r|Cho biết phiên bản của nhân Linux|
|shutdown -h now|Tắt máy tính ngay lập tức|
|lsusb|Liệt kê các thiết bị usb có mặt trong máy tính|
|lspci|Liệt kê các thiết bị pci có trên máy tính|
|time command|Cho biết thời gian cần thiết để thực hiện xong lệnh command|
|command1 l command2|Chuyển kết quả của lệnh command1 làm đầu vào của lệnh command2|
|clear|Xoá màn hình của cửa sổ Terminal|

-----

## 3. Quản lí tiến trình


|Lệnh|Mô tả|
|---|---|
|ps -ef|Hiển thị tất cả các tiến trình đã được thực hiện (pid et ppid)|
|ps aux|Hiển thị chi tiết các tiến trình|
|ps aux l grep soft|Hiển thị các tiến trình liên quan đến chương khởi động soft|
|kill pid|Báo chấm dứt tiến trình mang số pid|
|kill -9 pid|Yêu cầu hệ thống chấm dứt tiến trình pid
|xkill|Chấm dứt một ứng dụng theo dạng đồ hoạ (ấn chuột vào cửa sổ của ứng dụng)|

-----

## 4. Quản lí mạng

|Lệnh|Mô tả|  
|---|---|  
|/etc/network/interfaces|Thông tin cấu hình của các bộ phần giao diện (interfaces)|  
|uname -a|Hiện thị tên của máy tính trong mạng (hostname)|  
|ping địa chỉ IP|Thử nối mạng đến máy có địa chỉ IP|  
|ifconfig -a|Hiển thị thông tin về tất cả các giao diện mạng đang có|  
|ifconfig eth0 địa chỉ IP|Xác định địa chỉ IP cho giao diện cạc mạng eth0|  
|ifdown eth0|Ngưng hoạt động giao diện cạc mạng eth0|  
|ifconfig eth0 down|  	
|ifup eth0|Kích hoạt giao diện cạc mạng eth0|  
|ifconfig eth0 up|  	
|poweroff -i|Ngưng hoạt động tất cả các nối mạng|  
|route add default gw địa chỉ IP|Xác định địa chỉ IP của máy làm cổng dẫn đến bên ngoài mạng cục bộ|  
|route del default|Bỏ địa chỉ IP mặc định để ra khỏi mạng cục bộ|  

-----

# B) Phím tắt trong Terminal

|Lệnh|Mô tả| 
|---|---|
|Ctrl + L|Xoá toàn bộ màn hình, giống lệnh clear|
|Ctrl + D|Exit session, giống lệnh exit|
|Ctrl + R|Tìm một lệnh đã chạy trước đây, nhấn Ctrl + R sau đó bắt đầu gõ một phần của câu lệnh, hệ thống sẽ tự hoàn tất phần còn lại dựa trên các câu lệnh đã được thực hiện trước đó|
|Tab|Hiện gợi ý về câu lệnh|
|Ctrl + Shift + V|Dán (paste) nội dung đã copy vào terminal|
