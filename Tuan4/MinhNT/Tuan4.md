# I-Cấu hình Webserver:
## 1.1 Cài đặt Web Server Apache:
- B1: Update Ubuntu Server:
    
        sudo apt-get update

- B2: Cài đặt Apache: 

        sudo apt-get install apache2

- B3: Sau khi cài đặt, truy cập: http://localhost để kiểm tra. Nếu trình duyệt hiện Default Page của Apache2 "It works !!!" nghĩa là quá trình cài đặt hoàn tất.

![](https://thachpham.com/wp-content/uploads/2015/01/ubuntu-apache-welcome.jpg)

**Bonus: Thiết lập Virtual Hosts:**

- B1: Tạo thư mục dưới đường dẫn file */var/www :*

        sudo mkdir -p /var/www/abc.com/public_html

- B2: Thiết lập Ownership & Permissions:

        sudo chown -R $USER:$USER /var/www/abc.com/public_html/

- B3: Thiết lập quyền read cho www:

        sudo chmod -R 755 /var/www/

- B4: Tạo một trang sample cho Virtual Hosts:

        sudo nano /var/www/abc.com/public_html/index.html


*Trong trang này, bổ sung đoạn sau:*

     <html>
     <head>
     <title>abc.com</title>
     </head>
     <body>
     <h1>Can you say something ???</h1>
     </body>
     </html>

Save và đóng lại. Lưu ý ưu tiên dùng **sudo nano** hoặc **sudo gedit** để chỉnh sửa trang tiện hơn.

- B5: Tạo file của Virtual Hosts:

        sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/abc.com.conf

Sau đó mở file **.conf** vừa được tạo 

    sudo nano /etc/apache2/sites-available/abc.com.conf

và thay đổi/bổ sung thông tin như sau:

        ServerAdmin admin@abc.com
        ServerName abc.com
        ServerAlias www.abc.com
        DocumentRoot /var/www/abc.com/public_html

Tiến hành disable cấu hình mặc định và enable cấu hình mới:

     sudo a2dissite 000-default.conf .
     sudo a2ensite abc.com.conf .

Khởi động lại apache (nên nhớ):

     sudo service apache2 restart .

- B6: Kiểm tra Virtual Hosts:

Sửa đổi file host: 

    sudo nano /etc/hosts .

Thêm vào domain:

    [...]
    127.0.1.2  abc.com

- B7: Mở trình duyệt gõ: **https://abc.com** và kiểm tra kết quả.


## 1.2) Cài đặt MySQL Server:

    sudo apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql

Trong khi cài đặt, MySQL sẽ hiển thị một request để bạn nhập mật khẩu root cho MySQL

![](https://thachpham.com/wp-content/uploads/2015/01/ubuntu-mysql-rootpass.jpg)

Cài xong, kích hoạt nó bằng lệnh: 

    sudo mysql_install_db

Bạn có thể cài đặt bảo mật cho MySQL Server và đổi lại mật khẩu root:

    sudo /usr/bin/mysql_secure_installation

## 1.3) Cài đặt PHP:
- B1: Nhập lệnh:

        sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt

- B2: Nhập tiếp 

        sudo nano /etc/apache2/mods-enabled/dir.conf 

Thêm **index.php** ngay sau **DirectoryIndex** để nó ưu tiên index file .php thay vì .html

    <IfModule mod_dir.c>
          DirectoryIndex index.php index.html index.cgi index.pl index.php index.xhtml index.htm
    </IfModule>

- B3: Đừng quên khởi động lại apache2

        sudo service apache2 restart

- B4: Tìm tới thư mục var chứa tên miền 

![](https://i.imgur.com/LrAPozF.jpg)

Tạo một file **info.php** trong thư mục này và thêm nội dung:

        <?php phpinfo(); ?>

- B5: Truy cập và kiểm tra kết quả

![](https://thachpham.com/wp-content/uploads/2015/01/ubuntu-phpinfo.jpg)

## 1.4) Cài đặt, cấu hình NGinX:
- B1: Cài đặt: 

        sudo apt-get -y install nginx

- B2: Cấu hình NGinX

Sửa file sau

      sudo nano /etc/nginx/sites-available/default

Tìm đến dòng thứ 38, bổ sung: 

      server_name www.srv.world;

Lưu và thoát ra. Nhập tiếp lệnh:

      sudo systemctl start nginx 
      sudo systemctl enable nginx 

- B3: Truy cập trang mặc định của NGinX và kiểm tra kết quả (ảnh)


II - Tìm hiểu về DNS:
2.1) DNS là gì ?

DNS là từ viết tắt trong tiếng Anh của Domain Name System, là Hệ thống phân giải tên được phát minh vào năm 1984 cho Internet, chỉ một hệ thống cho phép thiết lập tương ứng giữa địa chỉ IP và tên miền. Hệ thống tên miền (DNS) là một hệ thống đặt tên theo thứ tự cho máy vi tính, dịch vụ, hoặc bất kỳ nguồn lực tham gia vào Internet. Nó liên kết nhiều thông tin đa dạng với tên miền được gán cho những người tham gia. Quan trọng nhất là, nó chuyển tên miền có ý nghĩa cho con người vào số định danh (nhị phân), liên kết với các trang thiết bị mạng cho các mục đích định vị và địa chỉ hóa các thiết bị khắp thế giới.

Phép tương thường được sử dụng để giải thích hệ thống tên miềnlà, nó phục vụ như một “Danh bạ điện thoại” để tìm trên Internet bằng cách dịch tên máy chủ máy tính thành địa chỉ IP 

Ví dụ, www.example.com dịch thành 208.77.188.166.

Hệ thống tên miền giúp cho nó có thể chỉ định tên miền cho các nhóm người sử dụng Internet trong một cách có ý nghĩa, độc lập với mỗi địa điểm của người sử dụng. Bởi vì điều này, World-Wide Web (WWW) siêu liên kết và trao đổi thông tin trên Internet có thể duy trì ổn định và cố định ngay cả khi định tuyến dòng Internet thay đổi hoặc những người tham gia sử dụng một thiết bị di động. Tên miền internet dễ nhớ hơn các địa chỉ IP như là 208.77.188.166 (IPv4) hoặc 2001: db8: 1f70:: 999: de8: 7648:6 e8 (IPv6).

Mọi người tận dụng lợi thế này khi họ thuật lại có nghĩa các URL và địa chỉ email mà không cần phải biết làm thế nào các máy sẽ thực sự tìm ra chúng.

Hệ thống tên miền phân phối trách nhiệm gán tên miền và lập bản đồ những tên tới địa chỉ IP bằng cách định rõ những máy chủ có thẩm quyền cho mỗi tên miền. Những máy chủ có tên thẩm quyền được phân công chịu trách nhiệm đối với tên miền riêng của họ, và lần lượt có thể chỉ định tên máy chủ khác độc quyền của họ cho các tên miền phụ. Kỹ thuật này đã thực hiện các cơ chế phân phối DNS, chịu đựng lỗi, và giúp tránh sự cần thiết cho một trung tâm đơn lẻ để đăng ký được tư vấn và liên tục cập nhật. Nhìn chung, Hệ thống tên miền cũng lưu trữ các loại thông tin khác, chẳng hạn như danh sách các máy chủ email mà chấp nhận thư điện tử cho một tên miền Internet. Bằng cách cung cấp cho một thế giới rộng lớn, phân phối từ khóa – cơ sở của dịch vụ đổi hướng , Hệ thống tên miền là một thành phần thiết yếu cho các chức năng của Internet. Các định dạng khác như các thẻ RFID, mã số UPC, ký tự Quốc tế trong địa chỉ email và tên máy chủ, và một loạt các định dạng khác có thể có khả năng sử dụng DNS.

2.2) Chức năng của DNS

Mỗi Website có một tên (là tên miền hay đường dẫn URL:Universal Resource Locator) và một địa chỉ IP. Địa chỉ IP gồm 4 nhóm số cách nhau bằng dấu chấm(Ipv4). Khi mở một trình duyệt Web và nhập tên website, trình duyệt sẽ đến thẳng website mà không cần phải thông qua việc nhập địa chỉ IP của trang web. Quá trình "dịch" tên miền thành địa chỉ IP để cho trình duyệt hiểu và truy cập được vào website là công việc của một DNS server. Các DNS trợ giúp qua lại với nhau để dịch địa chỉ "IP" thành "tên" và ngược lại. Người sử dụng chỉ cần nhớ "tên", không cần phải nhớ địa chỉ IP (địa chỉ IP là những con số rất khó nhớ).[1]

2.3) Nguyên tắc làm việc của DNS

-Mỗi nhà cung cấp dịch vụ vận hành và duy trì DNS server riêng của mình, gồm các máy bên trong phần riêng của mỗi nhà cung cấp dịch vụ đó trong Internet. Tức là, nếu một trình duyệt tìm kiếm địa chỉ của một website thì DNS server phân giải tên website này phải là DNS server của chính tổ chức quản lý website đó chứ không phải là của một tổ chức (nhà cung cấp dịch vụ) nào khác.

INTERNIC (Internet Network Information Center) chịu trách nhiệm theo dõi các tên miền và các DNS server tương ứng. INTERNIC là một tổ chức được thành lập bởi NFS (National Science Foundation), AT&T và Network Solution, chịu trách nhiệm đăng ký các tên miền của Internet. INTERNIC chỉ có nhiệm vụ quản lý tất cả các DNS server trên Internet chứ không có nhiệm vụ phân giải tên cho từng địa chỉ.

DNS có khả năng tra vấn các DNS server khác để có được một cái tên đã được phân giải. DNS server của mỗi tên miền thường có hai việc khác biệt. Thứ nhất, chịu trách nhiệm phân giải tên từ các máy bên trong miền về các địa chỉ Internet, cả bên trong lẫn bên ngoài miền nó quản lý. Thứ hai, chúng trả lời các DNS server bên ngoài đang cố gắng phân giải những cái tên bên trong miền nó quản lý. - DNS server có khả năng ghi nhớ lại những tên vừa phân giải. Để dùng cho những yêu cầu phân giải lần sau. Số lượng những tên phân giải được lưu lại tùy thuộc vào quy mô của từng DNS.

2.4) Cách sử dụng DNS

Do các DNS có tốc độ biên dịch khác nhau, có thể nhanh hoặc có thể chậm, do đó người sử dụng có thể chọn DNS server để sử dụng cho riêng mình. Có các cách chọn lựa cho người sử dụng. Sử dụng DNS mặc định của nhà cung cấp dịch vụ (internet), trường hợp này người sử dụng không cần điền địa chỉ DNS vào network connections trong máy của mình. Sử dụng DNS server khác (miễn phí hoặc trả phí) thì phải điền địa chỉ DNS server vào network connections. Địa chỉ DNS server cũng là 4 nhóm số cách nhau bởi các dấu chấm.
