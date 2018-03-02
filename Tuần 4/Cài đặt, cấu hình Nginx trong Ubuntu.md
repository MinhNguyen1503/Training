# Nginx trong Ubuntu

## 1. Khái niệm

Nginx là một máy chủ proxy ngược mã nguồn mở (open source reverse proxy server) sử dụng phổ biến giao thức HTTP, HTTPS, SMTP, POP3 và IMAP , cũng như dùng làm cân bằng tải (load balancer), HTTP cache và máy chủ web (web server).
- Dự án Nginx tập trung vào việc phục vụ **số lượng kết nối đồng thời lớn (high concurrency)**, **hiệu suất cao và sử dụng bộ nhớ thấp**. Nginx được biết đến bởi sự ổn định cao, nhiều tính năng, cấu hình đơn giản và tiết kiệm tài nguyên.

-----

## 2. Cài đặt Nginx
`sudo apt-get install nginx`

File config nginx : **/etc/nginx/nginx.conf**  

---

## 3. Cấu hình Virtual Hostings

### 3.1 Cấu hình Virtual Host

Ở đây mình thêm 1 domainame **"virtual.host"**
- Tạo file cấu hình host ảo cho **virtual.host**  

**root@tuananh96:~#   vi /etc/nginx/sites-available/virtual.host**
  
    create new
    server{
	listen	80;
	server_name www.virtual.host;

	lacation / {
		root /var/www/virtual.host;
		index index.html index.htm;
	  }
    }

**root@tuananh96:~# mkdir /var/www/virtual.host**  
**root@tuananh96:~# cd /etc/nginx/sites-enabled**  

 - Muốn nginx đọc được file cấu hình bạn phải tạo một symbolic link đến sites-enabled  
 `ln -s /etc/nginx/sites-available/virtual.host.còn ./`  

 - Khởi động lại nginx
 `sudo systemctl resstart nginx`  

Tạo trang kiểm tra để đảm bảo hoạt động bình thường. 
 
**root@tuananh96:~# vi /var/www/virtual.host/index.html** 


    <html>
    <body>
    <div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;"
    Nginx Virtual Host Test Page
    </div>
    </body>
    </html>  


 ![](https://www.server-world.info/en/Ubuntu_16.04/nginx/img/2.png)

### 3.2 Bật Userdir

 Bật Userdir cho người dùng thông thường để mở trang web của họ trong thư mục Home directories.

#### Bước 1: Cấu hình Nginx

 **root@tuananh96:~# vi /etc/nginx/sites-available/default**

    # add into "server" section
         location ~ ^/~(.+?)(/.*)?$ {
            alias /home/$1/public_html$2;
            index  index.html index.htm;
            autoindex on;
        }

**root@tuananh96:~# systemctl restart nginx**   

#### Bước 2: Tạo trang thử nghiệm để đảm bảo hoạt động  

**ubuntu@tuananh96:~$ chmod 711 /home/ubuntu**
**ubuntu@tuananh96:~$ mkdir ~/public_html**   
**ubuntu@tuananh96:~$ chmod 755 ~/public_html**   
**ubuntu@tuananh96:~$ vi ~/public_html/index.html**

    <html>
    <body>
    <div style="width: 100%; font-size: 40px; font-weight: bold; text-align: center;">
    Nginx UserDir Test Page
    </div>
    </body>
    </html>

![]()  

### 3.3 Enable Basic Authentication

Bật xác thực cơ bản để hạn chế quyền truy cập vào các trang web cụ thể.  

#### Bước 1: Đặt Basic Auth dưới thư mục "/ auth-basic"  

**root@tuananh96:~# apt-get -y install apache2-utils**
**root@tuananh96:~# vi /etc/nginx/sites-available/default**

    # add into "server" section
        location /auth-basic {
            auth_basic            "Basic Auth";
            auth_basic_user_file  "/etc/nginx/.htpasswd";
        }

**root@tuananh96:~# htpasswd -c /etc/nginx/.htpasswd ubuntu** 
 
> **New password**:     # set password  
> **Re-type new password**:  
> Adding password for user ubuntu  

**root@tuananh96:~# mkdir /var/www/html/auth-basic** 
**root@tuananh96:~# systemctl restart nginx**


#### Bước 2:
 Truy cập trang kiểm tra với trình duyệt Web trên máy khách và xác thực với người dùng được thêm vào với htpasswd  

![](https://www.server-world.info/en/Ubuntu_16.04/nginx/img/5.png)  
![](https://www.server-world.info/en/Ubuntu_16.04/nginx/img/6.png)

---

### 3.4 Cài đặt PHP-FPM  
#### Bước 1: Cài đặt PHP và PHP-FPM
 `root@tuananh96:~# apt-get -y install php php-fpm`  

#### Bước 2: Cấu hình PHP-FPM và Nginx  

 **root@tuananh96:~# vi /etc/nginx/sites-available/default**

    # add follows in "server" section
        location ~ \.php$ {
               include snippets/fastcgi-php.conf;
               fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        }

**root@tuananh:~# systemctl restart php7.0-fpm nginx**  

### Bước 3: Tạo trang kiểm tra

`root@tuananh96:~# echo "<?php phpinfo() ?>" > /var/www/html/info.php`  
 
![](https://www.server-world.info/en/Ubuntu_16.04/nginx/img/11.png)