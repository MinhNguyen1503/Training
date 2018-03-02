# Cấu hình Apache trên Ubuntu

## 1. Khái niệm  
Apache là một phần mềm mã nguồn mở miễn phí được cài đặt trên các máy chủ web server (phần cứng) để xử lý các yêu cầu gửi tới máy chủ dưới giao thức HTTP.  

## 2. Cài đặt Apache
Trên Ubunttu sử dụng lệnh: `apt-get install apache2`  
- **Kiểm tra** Apache chạy hay chưa, mở trình duyệt nhập Url sau: **http://your_domain/** hoặc **http://server-ip/** thông tin như hình bên dưới là OK.  

![](https://www.thuysys.com/wp-content/uploads/test-apache.png)  

- Muốn chạy nhiều web site bạn tạo **Virtualhost** tương ứng với mỗi **domain**.

## 2.1 Cấu trúc thư mục cấu hình Apache trên Ubuntu
- **Thư mục chứa các thiết lập** của Apache sẽ nằm trong thư mục **/etc/apache2**. 

- Trong đó có 1 số thư mực và file cấu hình như sau:
  - **conf-available/**: Chứa các file thiết lập cấu hình sẵn của Apache trên Ubuntu, nhưng các thiết lập trong đây sẽ chưa được áp dụng vì Ubuntu không load thiết lập cấu hình trong thư mục này.  
  - **conf-enabled/**: Thư mục chứa các file thiết lập cấu hình của Apache trên Ubuntu đang được bật. Hãy hiểu là nếu thư mục này có một liên kết tượng trưng (symlink) qua một file module nào đó bên thư mục conf-available thì nó sẽ được bật.  
  - **mods-available/**: Thư mục chứa các file từng module của Apache trên Ubuntu nhưng chưa được bật.  
  - **mods-enabled/**: Thư mục chứa các file từng module của Apache trên Ubuntu đang được bật.  
  - **site-available/**: Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu nhưng chưa được bật.
  - **site-enabled/**: Thư mục chứa file cấu hình VirtualHost của Apache trên Ubuntu đang được bật.  
  - **apache2.conf**: File cấu hình Apache trên Ubuntu.
  - **envvars**: File thiết lập các biến với giá trị sẵn để sử dụng trong các file cấu hình.
  - **magic**: File thiết lập của module mod_mime_magic trên Apache.
  - **ports.conf** :File cấu hình cổng mạng của Apache (mặc định là port 80).  
 
## 2.2 Thư mục gốc chứa dữ liệu website của Apache trên Ubuntu
Mặc định, Apache trên Ubuntu sẽ sử dụng thư mục **/var/www/html** để chứa dữ liệu website gốc (load bằng IP hoặc hostname). Khi bạn vào đây sẽ thấy một file index.html, đó chính là file giao diện chào mừng mà bạn đã thấy ở trên.  

## 2.3 Use PHP

### 1. Cài đặt PHP
`root@tuananh96:~# apt-get -y install php php-cgi libapache2-mod-php php-common php-pear php-mbstring`  

### 2. Cấu hình Apache2

**root@tuananh96:~# a2enconf php7.0-cgi**:
    
    Enabling conf php7.0-cgi.  
    To activate the new configuration, you need to run:
    service apache2 reload  

`root@tuananh96:~# vi /etc/php/7.0/apache2/php.ini`
# line 912: uncomment and add your timezone
date.timezone = "Asia/Hanoi"
`root@www:~# systemctl restart apache2` 

### 3.Tạo trang kiểm tra PHP và truy cập vào nó.

**root@www:~# vi /var/www/html/index.php**  
  

      <html>   
      <body>   
      <div>   
      <?php   
        print Date("Y/m/d");  
      ?>  
      </div>  
      </body>  
      </html>    

![]()  


## 2.4 Thêm VirtualHost (thêm domain) vào Apache trên Ubuntu
Trước tiên, chúng ta cũng cần tạo cho nó một thư mục chứa dữ liệu cho domain cần thêm vào.  
> `mkdir -p /home/tuananh.com/public_html`  
> `mkdir -p /home/tuananh.com/log`  

Sau đó chúng ta cần copy file **/etc/apache2/sites-available/000-default.conf** ra một file mới chứa cấu hình của domain cần thêm vào (tuananh.com) ở **/etc/apache2/sites-available/tuananh.com.conf.**  
>`cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/thachpham.com.conf`  

**Lưu ý**: *Có thể file cấu hình mặc định của bạn không phải tên là default mà là “000-default.conf” nên tốt nhất bạn nên vào thư mục /etc/apache2/sites-available/ để xem rồi copy cho đúng.*  

Bây giờ hãy mở file **/etc/apache2/sites-available/tuananh.com.conf** lên và sửa nội dung trong đó cho nó gọn hơn như thế này: 

       <VirtualHost *:80>  
       ServerName tuananh.com  
       ServerAlias www.tuananh.com  
       ServerAdmin contact@tuananh.com  

       DocumentRoot /home/tuananh.com/public_html

       <Directory /home/tuananh.com/public_html>
               Options FollowSymLinks
               AllowOverride All
               Order allow,deny
               Allow from all
               Require all granted
       </Directory>

       # Available loglevels: trace8, ..., trace1, debug, info, notice,warn,
       # error, crit, alert, emerg.
       # It is also possible to configure the loglevel for particular
       # modules, e.g.
       LogLevel error

       ErrorLog /home/tuananh.com/log/error.log
       CustomLog /home/tuananh.com/log/access.log combined

       # For most configuration files from conf-available/, which are
       # enabled or disabled at a global level, it is possible to
       # include a line for only one particular virtual host. For example the
       # following line enables the CGI configuration for this host only
       # after it has been globally disabled with "a2disconf".
       #Include conf-available/serve-cgi-bin.conf  
       </VirtualHost>  
       # vim: syntax=apache ts=4 sw=4 sts=4 sr noet

Nhớ thay:

- **SererName** – Domain website cần thêm vào.
- **ServerAlias** – Sử dụng một tên domain khác thay thế, hay còn gọi là Parked Domain nếu bạn đã từng sử dụng qua cPanel đó.
- **DocumentRoot** – Đường dẫn tới thư mục chứa dữ liệu website của domain này mà ta đã tạo ở trên.
- **ErrorLog** – Đường dẫn tới thư mục log đã tạo ở trên cho domain này.
- **CustomLog** – Tương tự ErrorLog nhưng sẽ lưu log lại các lượt truy cập với file là access.log.  


## 3. Một số module cơ bản trên Apache
- **Module Ratelimit** : giới hạn băng thông của khách hàng.
- **Module Proxy** : Cấu hình Proxy chuyển tiếp.
- **Module Evasive** : Bảo vệ khỏi các cuộc tấn công DoS.
- **Module Sercurity** : Cấu hình Web Application Firewall.  