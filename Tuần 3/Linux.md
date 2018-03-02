# Linux

## Mục lục
> ### 1.Giới Thiệu Về Hệ Điều Hành Linux
> ### 2.Kiến Trúc Về Hệ Điều Hành Linux
> ### 3.So sánh Dos/Windows và Linux
> ### 4. Một số câu lệnh cơ bản
----

## 1. Giới thiệu về hệ điều hành Linux 

![](https://www.ipvanish.com/images/a/vpnsetup/linux.png)

**Linux là hệ điều hành dạng UNIX** ( Unix-like Operating System) chạy trên máy PC với bộ điều khiển trung tâm (CPU) Intel 80386 hoặc các thế hệ sau đó, hay các bộ vi xử lý trung tâm tương thích như AMD, Cyrix. Linux ngày nay còn có thể chạy trên các máy Macsintosh hoặc Sun Sparc. linux thoả mãn chuẩn POSIX.1.  

Phiên bản Linux đầu tiên do Linus Torvalds viết vào năm 1991, lúc ông còn là một sinh viên của Đại học Helsinki tại Phần Lan. Ông làm việc một cách hăng say trong vòng 3 năm liên tục và cho ra đời phiên bản Linux 1.0 vào năm 1994. Bộ phận chủ yếu này được phát triển và tung ra trên thị trường dưới bản quyền GNU General Public License. Do đó mà bất cứ ai cũng có thể tải và xem mã nguồn của Linux.

Một cách chính xác, **thuật ngữ "Linux" được sử dụng để chỉ Nhân Linux (Linux Kernel)**, nhưng tên này được sử dụng một cách rộng rãi để miêu tả tổng thể một hệ điều hành tương tự Unix (còn được biết đến dưới tên GNU/Linux) được tạo ra bởi việc đóng gói nhân Linux cùng với các thư viện và công cụ GNU, cũng như là các bản phân phối Linux. Thực tế thì đó là tập hợp một số lượng lớn các phần mềm như máy chủ web, các ngôn ngữ lập trình, các hệ quản trị cơ sở dữ liệu, các môi trường desktop như GNOME và KDE, và các ứng dụng thích hợp cho công việc văn phòng như OpenOffice, LibreOffice.

----

## 2. Kiến trúc về hệ điều hành Linux


![](https://vnitnews.com/wp-content/uploads/2015/10/Ki%E1%BA%BFn-tr%C3%BAc-h%E1%BB%87-%C4%91i%E1%BB%81u-h%C3%A0nh-Linux.png)

### 2.1 Hat Nhân (Kernel)

- **Là trung tâm điều khiển** của hệ điều hành Linux chứa các mã nguồn điều khiển hoạt động toàn bộ của hệ thống. Hạt nhân được phát triển không ngừng, thường có **hai phiên bản** mới nhất, **một bản để phát triển và một bản ổn định***. 
- Kernel **thiết kế theo dạng module**, do vậy kích thước thật sự của Kernel rất nhỏ. Chúng **chỉ tải được những bộ phận cần thiết lên bộ nhớ**, các bộ phận khác sẽ được tải lên nếu có yêu cầu sử dụng. Do đó **không sử dụng lãng phí bộ nhớ**.

Kernel Linux có thể **truy xuất tới toàn bộ tính năng phần cứng của máy tính**. Ngoài ra, do yêu cầu của các chương trình cần nhiều bộ nhớ, trong khi hệ thống có **ít bộ nhớ, hệ điều hành sử dụng không gian hoán đổi đĩa (Swap pace)** để lưu trữ các dữ liệu xử lý của chương trình. bên cạnh đó Linux còn hổ trợ các đặc tính sau:  

* **Bảo vệ vùng nhớ giữa các tiến trình**, điều này không cho phép một tiến trình làm tắt toàn bộ hệ thống.
* **Chỉ tải các chương trình khi có yêu cầu**.  

### 2.2 Shell

- Shell **cung cấp các tập lệnh** cho người dùng thao tác với kernel để thực hiện công việc.Shell đọc các lệnh từ người dùng và xử lý.
- Ngoài ra Shell còn cung cấp các đặc tính như: **chuyển hướng xuất nhập, ngôn ngữ lệnh** để tạo các file lệnh tương tự như **file.bat** trong đó.
- Có nhiều loại Shell được dùng trong Linux. Điểm quan trọng để **phân biệt các shell** với nhau **là bộ lệnh của mỗi shell**. Ví dụ C shell sử dụng các lệnh tương tự như ngôn ngữ C, Bourne shell thì dùng ngôn ngữ lệnh khác.  
- **Shell sử dụng chính** trong Linux là **GNU Bourne Again Shell**. Shell này là shell phát triển từ Bourne shell. Là shell sử dụng chính trong hệ thống Unix, với nhiều tính năng như: **điều khiển các tiến trình, các lệnh history, tên file dài** …  

-----

## 3. So sánh Dos/Windows và Linux  

### Giống nhau:

* **Chế độ hiển thị**: Dos và Linux Console có chế độ hiển thị **là ký tự.Windows và X-Windows** có chế độ đồ hoạ.
* **Lưu trữ dữ liệu theo thư mục cấu trúc cây**: thư mục có thể chứa file hoặc các thư mục con khác. Cả hai đều có khả năng xử lý các thao tác như liệt kê, tìm kiếm, tạo, xoá, đổi tên, di chuyển file và thư mục.
* **Khởi động chương trình**: bằng dòng lệnh hoặc kích chuột vào biểu tượng.
* **Trong môi trường đồ hoạ**: có khả năg phóng to, thu nhỏ, di chuyển và đóng của sổ. Tạo các thành phần giao diện đồ hoạ thân thiện như nút nhấn, menu…  

### Khác biệt:
- Linux **phân biệt chữ hoa và chữ thường**.
- **Linux thường không đưa ra thông báo**: trong Unix và đối với một số shell diễn dịch lệnh của Linux, sau khi thực hiện xong lệnh, trình biên dịch thường trở về ngay dấu nhắc lệnh và không đưa ra thông báo gì.  
- **Dấu phân cách đường dẫn và thư mục**: Linux sử dụng dấu / trong khi Dos sử dụng \ .Linux sử dụng dấu – hoặc – làm dấu chuyển tham số trên dòng lệnh, trong khi Dos sử dụng khoá chuyển /.  
- **Đường dẫn tìm kiếm**: với hầu hết các lệnh, **Dos thường tìm thông tin về đường dẫn của file** trong biến môi trường PATH hoặc trong thư mục hiện hành. **Linux thì chỉ tìm trong biến môi trường PATH**.
- **Chương trình thực thi**: với **Dos/ Windows** thường sử dụng tên mở rộng của file như **.exe, .com, .bat** để nhận dạng chương trình thực thi trong khi Linux thì không. Mọi file trong Linux đều được xem là chương trình thực thi nếu có **thuộc tính x (execute)** cho file.  

---

## 4 Một số câu lệnh cơ bản    

![](https://image.slidesharecdn.com/linux02-101207213647-phpapp01/95/linux02-7-728.jpg?cb=1291758615)

### 1.Tắt máy:  
- Sử dụng lệnh `sudo shutdown -P 1:00`: tắt máy lúc 1h sáng.  
- Sử dụng lệnh `sudo shutdown -P +60`: tắt máy sau 60 p  
- Sử dụng lệnh `sudo shutdown -c`: để hủy lệnh.  
- Sử dụng lệnh `sudo shutdown -r now`: để khởi động lại ngay.    

### 2.	Kiểm tra RAM:  
- Sử dụng lệnh `free`: hiển thị memory trống/đã sử dụng đang có trong hệ thống.   
- Sử dụng lệnh `top`: hiển thị các process đứng đầu hệ thống (mặc định đánh giá theo mức sử dụng CPU).     

![](https://i.imgur.com/PwttDly.png)

### 3.Thông tin OS:
- Sử dụng lệnh  `lsb_r<tab> -a`  : Tên phiên bản hệ điều hành đang sử dụng  
- Sử dụng lệnh  `uname –a`  : Tên phiên bản được phát triển, thời gian phát hành    
![](https://i.imgur.com/WluD8vC.png)


### 4.Kiểm tra thông tin ổ đĩa: 
- Sử dụng lệnh  `lsblk` :Hiển thị filesize ở dạng đọc được như kb,mb,..    
- Sử dụng lệnh  `sudo fdisk –l`: hiển thị thông số theo sector     
- Sử dụng lệnh  `df –h` : hiển thị output theo dạng dễ đọc, các tệp hệ thống      

![](https://i.imgur.com/kCbsvjY.png)

### 5.	Các trình biên tập:

**a) Nano:** 
 
- Dễ dàng sử dụng và làm chủ.  
- Nano có hầu hết các phím tắt được liệt kê ở dưới cùng của cửa sổ, làm cho nó cực kỳ đơn giản để sử dụng.  
- Chức năng tìm kiếm.  
- Tìm kiếm và thay thế.  
- Lệnh "Goto line".  
- Tự động thụt lề.   
 
**b) Vi:**  

- Khó khăn để bắt đầu và làm chủ. Các chế độ chỉnh sửa và lệnh sẽ gây nhầm lẫn cho người mới bắt đầu.  
- Phục hồi phiên.  
- Màn hình chia nhỏ.  
- Mở rộng tab.  
- Lệnh hoàn thành.  
- Cú pháp tô màu.    

**c) Vim:**  

- Tương tự vi nhưng có thêm một số chức năng.  
- Vim hỗ trợ nhiều ngôn ngữ lập trình.  
- Sửa file sử dụng giao thức SSH và HTTP.  
- Sửa file không cần giải nén.  


