# MỤC LỤC

## 1. Linux
### 1.1. Linux là gì?
### 1.2. Nhân Linux

## 2. Windows

## 3. Ubuntu
### 3.1. Cài đặt Ubuntu
### 3.2. Cấu hình network 
### 3.3. Tạo, sửa, xóa user, group
### 3.4. Cài đặt, xóa các phần mềm trên Ubuntu
### 3.5. Sự khác nhau giữa update, upgrade và dist-upgrade
### 3.6. Các lệnh cơ bản

***

# 1. Linux
## 1.1. Linux là gì?
Linux là tên gọi của một hệ điều hành máy tính và cũng là tên *hạt nhân* của hệ điều hành. Nó có lẽ là một ví dụ nổi tiếng nhất của phần mềm tự do và của việc phát triển mã nguồn mở.

Phiên bản Linux đầu tiên do Linus Torvalds viết vào năm 1991, lúc ông còn là một sinh viên của Đại học Helsinki tại Phần Lan. Ông làm việc một cách hăng say trong vòng 3 năm liên tục và cho ra đời phiên bản Linux 1.0 vào năm 1994. Bộ phận chủ yếu này được phát triển và tung ra trên thị trường dưới bản quyền GNU General Public License. Do đó mà bất cứ ai cũng có thể tải và xem mã nguồn của Linux.

Một cách chính xác, thuật ngữ "Linux" được sử dụng để chỉ Nhân Linux (Linux Kernel), nhưng tên này được sử dụng một cách rộng rãi để miêu tả tổng thể một hệ điều hành tương tự Unix (còn được biết đến dưới tên GNU/Linux) được tạo ra bởi việc đóng gói nhân Linux cùng với các thư viện và công cụ GNU, cũng như là các bản phân phối Linux. Thực tế thì đó là tập hợp một số lượng lớn các phần mềm như máy chủ web, các ngôn ngữ lập trình, các hệ quản trị cơ sở dữ liệu, các môi trường desktop như GNOME và KDE, và các ứng dụng thích hợp cho công việc văn phòng như OpenOffice, LibreOffice.

## 1.2. Nhân Linux
Hệ điều hành Linux có thể phân thành hai vùng: 
* Vùng người dùng (User Space) gồm các thư viện C và các phần mềm ứng dụng
* Vùng nhân (Kernel Space) gồm ba thành phần chính như hình sau

![](https://www.ibm.com/developerworks/linux/library/l-linux-kernel/figure2.jpg)

Trên cùng là lớp các ứng dụng của người dùng (User Applications). Bên dưới là lớp các thư viện C (GNU C Library). Lớp thư viện phục vụ cho giao diện các lời gọi hệ thống tạo liên kết giữa các ứng dụng và nhân Linux. Giao diện này quan trọng vì nhân Linux và các ứng dụng chiếm các vùng địa chỉ bộ nhớ được bảo vệ khác nhau. Mỗi ứng dụng có vùng địa chỉ ảo riêng còn nhân có một vùng địa chỉ duy nhất.

Nhân Linux có thể chia thành ba lớp. Trên cùng là giao diện các lời gọi hệ thống thực hiện các chức năng cơ bản như đọc, ghi. Bên dưới là phần mã nhân hệ điều hành (kernel code) hoặc chính xác hơn là mã nhân độc lập với kiến trúc vi xử lý (processor). Các mã lệnh trong lớp này dùng chung cho mọi loại processor mà Linux hỗ trợ. Lớp dưới cùng là các mã lệnh phụ thuộc vào kiến trúc từng loại processor (x86, x86-64,…).

Có thể thấy nhân Linux thực ra là bộ quản lý các tài nguyên. Các tài nguyên gồm: các tiến trình (process), bộ nhớ (memory) và thiết bị phần cứng. Nhân Linux quản lý các tài nguyên đó và nó điều hành việc truy cập tài nguyên đồng thời của nhiều user.

![](https://www.ibm.com/developerworks/linux/library/l-linux-kernel/figure3.jpg)

* **Giao diện lời gọi hệ thống (System call interface – SCI)**: SCI thực hiện các lời gọi hệ thống từ vùng ứng dụng vào nhân Linux. Giao diện này độc lập với kiến trúc bộ vi xử lý ngay cả trong cùng một họ vi xử lý. SCI có thể thực hiện các dịch vụ gọi hàm dồn kênh và tách kênh. Các gói liên quan được cài trong thư mục ẩn ./linux/kernel và phần độc lập với kiến trúc vi xử lý nằm trong ./linux/arch.
*  **Quản lý tiến trình (Process management)**: đảm bảo việc thực hiện các tiến trình. Trong vùng nhân Linux, mỗi tiến trình được gọi là một mạch lệnh (thread) và được thể hiện thành một vi xử lý ảo (gồm mã lệnh, dữ liệu, các ngăn xếp và các thanh ghi của CPU). Trong vùng ứng dụng thì chỉ dùng từ tiến trình mặc dù Linux không phân biệt hai khái niệm này (threads và processes). Nhân cung cấp một giao diện lập trình ứng dụng (API) để tạo tiến trình mới (fork, exec hoặc các hàm POSIX), ngừng tiến trình (kill, exit) và thông tin, đồng bộ giữa các tiến trình (signal hoặc các cơ cấu POSIX).

Quản lý tiến trình còn dùng để chia sẻ CPU giữa các mạch lệnh đang hoạt động. Nhân thực hiện một thuật toán lập lịch cố định bất kể đến các mạch lệnh đang tranh chấp quyền sử dụng CPU. Lịch này cũng hỗ trợ cả chế độ đa xử lý đối xứng (Symmetric MultiProcessing – SMP). Các gói liên quan được cài trong thư mục ẩn ./linux/kernel và phần độc lập với kiến trúc vi xử lý nằm trong ./linux/arch.

* **Quản lý bộ nhớ (Memory management)**: Một tài nguyên quan trọng khác mà nhân Linux quản lý là bộ nhớ. Để sử dụng bộ nhớ hiệu quả theo cách mà phần cứng quản lý bộ nhớ ảo, bộ nhớ được chia thành các trang (mỗi trang là 4KB đối với phần lớn loại vi xử lý). Linux có các cơ cấu quản lý lượng bộ nhớ khả dụng và các cơ cấu phần cứng để mapping giữa bộ nhớ vật lý và bộ nhớ ảo.

Việc quản lý bộ nhớ còn làm nhiều hơn là chỉ quản lý các trang 4KB. Linux dùng một sơ đồ định vị lát (slab allocator) lên trên mỗi trang. Sơ đồ này dùng trang 4KB làm cơ sở nhưng tạo một cấu trúc bên trong, theo dõi trang nào đầy, trang nào mới dùng một phần, trang nào còn trống.

Khi nhiều user sử dụng bộ nhớ, dung lượng có thể không đủ. Khi đó các trang nhớ được chuyển sang ổ cứng. Quá trình này được gọi là trao đổi (swapping) giữa bộ nhớ và ổ cứng. Các gói phần mềm liên quan đến quản lý bộ nhớ đặt trong thư mục ./linux/mm.

* **Hệ thống file ảo (Virtual file system)**: Hệ thống file ảo (VFS) là một khía cạnh hay của nhân Linux, cung cấp một giao diện trừu tượng hoá chung cho hệ thống file. VFS tạo nên một lớp chuyển đổi giữa SCI và các hệ thống file của Linux.

![](https://www.ibm.com/developerworks/linux/library/l-linux-kernel/figure4.jpg)

Nằm trên cùng của VFS là lớp các API các chức năng như mở, đóng, đọc, viết file. Dưới cùng của VFS là lớp trừu tượng hệ thống file xác định các chức năng lớp trên thực hiện như thế nào. Đó là các plug-in đối với một hệ thống file cho trước (có trên 50 plug-in như vậy). Các phần mềm liên quan đến VFS nằm trong thư mục ./linux/fs.
Bên dưới lớp file hệ thống là bộ đệm cache (buffer cache) gồm các chức năng chung cho mọi hệ thống file (không phụ thuộc vào một kiểu hệ thống file riêng biệt nào). Lớp cache này tối ưu hoá việc truy cập vào các thiết bị vật lý bằng cách giữ dữ liệu trong một thời gian ngắn (hoặc đọc trước sao cho dữ liệu luôn có khi cần). Dưới bộ đệm cache là các driver thiết bị là giao diện của các thiết bị vật lý cụ thể.

* **Các ngăn xếp mạng (Network stack)**:Các ngăn xếp mạng được thiết kế theo một kiến trúc lớp mô phỏng theo đúng kiến trúc lớp của các giao thức. IP là giao thức lớp mạng lõi nằm bên dưới giao thức vận chuyển (thường là TCP). Bên trên TCP là lớp socket được gọi đến qua SCI.

Lớp socket là API chuẩn của hệ thống con network, tạo nên một giao diện cho các giao thức mạng khác nhau. Lớp socket quy định một cách quản lý kết nối và di chuyển dữ liệu chuẩn hoá giữa các điểm đầu cuối. Tài nguyên mạng nằm ở thư mục ./linux/net.

* **Các driver thiết bị (Device drivers)**: Phần lớn mã nguồn của nhân Linux là các driver để điều khiển các thiết bị phần cứng. Cây thư mục của mã nguồn nhân Linux có một thư mục con driver trong đó có các thư mục con ứng với các thiêt bị khác nhau. Mã nguồn driver nằm ở ./linux/drivers.

* **Mã lệnh phụ thuộc kiến trúc vi xử lý (Architecture-dependent code)**: Phần lớn Linux độc lập với kiến trúc vi xử lý, nhưng cũng có những bộ phận cần phải theo đúng từng kiến trúc cụ thể để hoạt động được và hiệu quả. Thư mục con ./linux/arch chứa các mã nguồn phụ thuộc kiến trúc đó.

## 1.3. Bản phân phối Linux (distro)

Một bản phân phối Linux (thường được gọi tắt là **distro**) là một hệ điều hành được tạo dựng từ tập hợp nhiều phần mềm dựa trên hạt nhân Linux và thường có một hệ thống quản lý gói tin. Người dùng Linux thường tải một bản phân phối Linux, trong đó có sẵn trong một loạt các hệ thống khác nhau, từ các thiết bị nhúng và máy tính cá nhân đến siêu máy tính.

Một bản phân phối Linux điển hình bao gồm một Linux kernel, các công cụ và thư viện GNU, các phần mềm thêm vào, tài liệu, một window system (phần lớn sử dụng X Window System), window manager và một môi trường desktop. Phần lớn các phần mềm là phần mềm tự do nguồn mở có sẵn cả file biên dịch nhị phân và mã nguồn, cho phép chỉnh sửa phần mềm gốc. Thông thường, các bản phân phối Linux tùy chọn bao gồm một số phần mềm độc quyền mà có thể không có sẵn ở dạng mã nguồn. Hầu như tất cả các bản phân phối Linux là Unix-like, ngoại lệ đáng chú ý nhất là Android, không bao gồm một giao diện dòng lệnh và các chương trình làm cho các bản phân phối Linux điển hình.

Một bản phân phối Linux cũng có thể được mô tả như một loại riêng biệt của ứng dụng và phần mềm tiện ích (công cụ GNU khác nhau và các thư viện làm ví dụ), đóng gói cùng với các hạt nhân Linux theo cách như vậy mà khả năng của nó đáp ứng được nhu cầu của nhiều người sử dụng. Phần mềm này thường được chuyển đến phân phối và sau đó được đóng gói thành các gói phần mềm bằng cách bảo trì của phân phối. Các gói phần mềm có sẵn trực tuyến trong cái gọi là kho lưu trữ, đó là địa điểm lưu trữ thường phân bố trên toàn thế giới. Ngoài các thành phần chính, chẳng hạn như các trình cài đặt phân phối (ví dụ, Debian-Installer hay Anaconda) hoặc các hệ thống quản lý gói, còn có một số ít các gói mà ban đầu được viết từ dưới lên bởi các nhà bảo trì của một phân phối Linux.

Có khoảng sáu trăm bản phân phối Linux tồn tại, với gần năm trăm trong số đó phát triển tích cực, liên tục được sửa đổi và cải thiện. Bởi vì sự sẵn có lớn của phần mềm, phân phối đã thực hiện trên một loạt các hình thức, kể cả những người phù hợp để sử dụng trên máy tính để bàn, máy chủ, máy tính xách tay, netbook, điện thoại di động và máy tính bảng, cũng như môi trường tối thiểu thường để sử dụng trong các hệ thống nhúng. Có nhiều phân phối hỗ trợ thương mại, như Fedora (Red Hat), openSUSE (SUSE) và Ubuntu (Canonical Ltd.), và hoàn toàn phân phối dựa vào cộng đồng, chẳng hạn như Debian, Slackware, Gentoo hay Arch Linux. Hầu hết các bản phân phối đều sẵn sàng để sử dụng và biên dịch sẵn kèm theo một bộ hướng dẫn cụ thể, trong khi một số phân phối (như Gentoo) phân phối chủ yếu ở dạng mã nguồn và biên dịch cục bộ trong quá trình cài đặt. 

**Bản phân phối phổ biến**

* Debian, Một bản phân phối phi thương mại và là một trong những bản phân phối ra đời sớm nhất, duy trì bởi một cộng đồng phát triển tình nguyện với một cam kết mạnh mẽ cho nguyên tắc phần mềm miễn phí và quản lý dự án dân chủ.
 * Raspbian, một hệ điều hành cho Raspberry Pi.
 * Knoppix, bản phân phối Live CD cho phép khởi động từ những thiết bị lưu trữ di động mà không cần phải cài đặt vào ổ cứng, bắt nguồn từ Debian.

 * Ubuntu, một bản phân phối phổ biến cho máy tính để bàn và máy chủ bắt nguồn từ Debian, duy trì bởi một công ty của Anh, Canonical Ltd
   * Kubuntu, phiên bản KDE của Ubuntu
   * Linux Mint, một bản phân phối dựa trên và tương thích với Ubuntu. Hỗ trợ nhiều môi trường desktop, trong số những phân nhánh khác nhau của GNOME Shell là Cinnamon và GNOME 2 là MATE
   * Trisquel, một bản phân phối dựa trên Ubuntu dựa trên Linux kernel và bao gồm toàn bộ phần mềm miễn phí
   * Elementary OS, một bản phân phối dựa trên Ubuntu tập trung mạnh vào các trải nghiệm hình ảnh mà không ảnh hưởng tới hiệu suất
* Fedora, một bản phân phối cộng đồng được đỡ đầu bởi một công ty của Mỹ, Red Hat. nó được tạo ra nhằm kiểm thử các công nghệ cho một bản phân phối thương mại khác của Red Hat, nơi mà các phần mềm nguồn mở mới được tạo lập, phát triển và kiểm thử trong môi trường cộng đồng trước khi được đưa vào Red Hat Enterprise Linux
  * Red Hat Enterprise Linux (RHEL), một phát sinh của Fedora, duy trì và và hỗ trợ thương mại bởi Red Hat. Nó tìm cách cung cấp các thử nghiệm, an toàn, ổn định cho các máy chủ và máy trạm Linux hỗ trợ cho các doanh nghiệp.
    * CentOS, một bản phân phối bắt nguồn từ mã nguồn tương tự được sử dụng bởi Red Hat, duy trì bởi một cộng đồng tình nguyện tận tâm của các nhà phát triển với cả hai phiên bản 100% tương thích với Red Hat và một phiên bản nâng cấp không phải luôn tương thích ngược 100%.
    * Oracle Linux, cũng phát sinh từ Red Hat Enterprise Linux, duy trì và hỗ trợ thương mại bởi Oracle
    * Scientific Linux, một bản phân phối phát sinh từ mã nguồn tương tự của Red Hat,duy trì bởi Fermilab
* Mandriva Linux là một phân phối bắt nguồn từ Red Hat, phổ biến ở một vài quốc giaChâu Âu và Brazil,Hỗ trợ bởi một công ty Pháp cùng tên.nó đã bị thay thế bởi OpenMandriva Lx.
  * Mageia, một phân nhánh cộng đồng của Mandriva Linux bắt đầu từ 2010
  * PCLinuxOS, một phân nhánh của Mandriva, phát triển từ một nhóm các gói tin do ccoongj đồng tự phát triển và phân phối
* openSUSE một phân phối cộng đồng chủ yếu được tài trợ bởi Novel.
  * SUSE Linux Enterprise, phân nhánh từ openSUSE, duy trì và hỗ trợ thương mại bởi Novel

# 2. Windows

# 3. Ubuntu
## 3.1 Cài đặt Ubuntu

## 3.2. Cấu hình network 

Cấu hình địa chỉ IP

* Cấu hình IP tạm thời: mất sau khi reboot máy tính
* Cấu hình IP tĩnh: giữ nguyên sau khi reboot máy tính
* Cấu hình IP động: nhận địa chỉ IP một cách tự động từ một DHCP server

**Cấu hình IP tạm thời**

* Xem tất cả giao diện mạng: `ifconfig -a`
* Xem cấu hình hiện tại: `ifconfig enp0s3`
* Đặt cấu hình IP mới: `sudo ifconfig ethX IP-address netmask net-address`

`sudo ifconfig enp0s3 192.168.1.2 netmask 255.255.255.0`

**Sử dụng lệnh route để thiết lập đường đi**

* Xem đường đi hiện tại: `route -n`
* Đặt default gateway: `sudo route add default gw ip-getway {interface-name}`

`sudo route add default gw 192.168.1.1 enp0s3`

**Cấu hình IP tĩnh**

* Thông tin về cấu hình IP lưu trong file `/etc/network/interfaces`
* Cấu hình IP tĩnh cho giao diện enp0s3

Dùng nano (`sudo nano /etc/network/interfaces`) để thêm các thông tin sau:

`auto enp0s3`

`iface enp0s3 inet static`

`address 192.168.1.2`

`netmask 255.255.255.0`

`gateway 192.168.1.1`

* Sau đó reboot hoặc restart dịch vụ mạng:

`sudo reboot`

`sudo /etc/init.d/networking restart`

**Cấu hình IP động**

Thông tin về cấu hình IP lưu trong file /etc/network/interfaces
* Cấu hình IP động cho giao diện `enp0s3` (chỉ thay từ khóa `static` bằng `dhcp`)

`auto enp0s3`

`iface enp0s3 inet dhcp`

**Tắt/mở giao diện mạng**

* Tắt giao diện `enp0s3`: `sudo ifconfig enp0s3 down`
* Mở giao diện `enp0s3`: `sudo ifconfig eth0 up`


## 3.3. Tạo, sửa, xóa user, group

**User là gì ?**

* User là người có thể truy cập đến hệ thống.
* User có username và password.
* Có hai loại user: super user và regular user.
* Mỗi user còn có một định danh riêng gọi là **UID**.
* Định danh của người dùng bình thường sử dụng giá trị bắt đầu từ 500.

**Group là gì ?**

* Group là tập hợp nhiều user lại.
* Mỗi user luôn là thành viên của một group.
* Khi tạo một user thì mặc định một group được tạo ra.
* Mỗi group còn có một định danh riêng gọi là **GID**.
* Định danh của group thường sử dụng giá trị bắt đầu từ 500.

**Quản lý user**
`useradd`: tạo user

`-c`: comment (chú thích)

`-d`: home directory (thư mục cá nhân)

`-G`: đưa user vào group

`-M`: không tạo thư mục cá nhân

`-n`: không tạo primary group, user tạo ra sẽ được đưa vào group users

`-s`: chỉ định shell

`passwd`: đặt password cho user

`-l`: lock user

`-u`: unlock user

`-d`: disable passwd

`userdel`: xóa user

`-r`: xóa luôn thư mục các nhân

VD. Tạo user mới dr1 với password "111".

`sudo useradd dr1`

`sudo passwd dr1` 

**Quản lý group**

`groupadd`: tạo group
`groupdel`: xóa group

VD.Tạo group kinhdoanh: `groupadd kinhdoanh`

Tạo user kd1, kd2 và đưa vào group kinhdoanh đã tồn tại

`useradd –G kinhdoanh kd1`
`useradd –G kinhdoanh kd2`

Xem id và group của user kd1: `id kd1`

## 3.4. Cài đặt, xóa các phần mềm trên Ubuntu

**Dùng Ubuntu Software Center**

Đây là cách cài đặt và gỡ phần mềm đơn giản nhất trong Ubuntu.

Các bước cài đặt một phần mềm:

* Mở Ubuntu Software Center
* Viết tên phần mềm cần cài đặt
* Chọn phần mềm cần cài đặt và nhấn Install
* Nhập mật khẩu root và đợi nó cài đặt xong

Các bước gỡ phần mềm vừa cài đặt:

* Trong Ubuntu Software Center, chọn tab Installed.
* Danh sách phần mềm đã được cài đặt hiện lên
* Bạn chọn Remove để gỡ cài đặt.
* Nhập mật khẩu root và đợi quá trình hoàn thành.

**Sử dụng apt-get trên Terminal**
Để cài đặt 1 gói phần mềm trên Ubuntu sử dụng Terminal theo cách online, cần có kết nối Internet. Tìm kiếm trên Google tên những gói phần mềm cần cài đặt rồi làm theo những bước sau:

* Mở Terminal: Ctrl Alt T
* `sudo apt-get install ten_goi1 ten_goi2 ten_goi3`
* Nhập mật khẩu và đợi cài đặt xong

Các bước gỡ cài đặt:

* Mở Terminal: Ctr Alt T
* `sudo apt-get remove ten_goi1 ten_goi2 ten_goi3`
* Nhập mật khẩu và chờ đợi

Trong quá trình cài đặt và gỡ phần mềm trên Ubuntu, việc sinh ra rác là điều không tránh khỏi. Để bỏ đi những thứ không cần thiết:

* Mở Terminal
* `sudo apt-get autoremove` và nhập mật khẩu
* `sudo apt-get autoclean` (nhập mật khẩu nếu cần)

**Cài đặt Offline**
Cần tải gói phần mềm về (vì không có kết nối Internet). Các gói phần mềm thường có đuôi là: .deb, .rpm, .bin và dạng nén tarball (.tar, .tar.gz, .tgz,…).

**Cài đặt file .deb**: click vào file, tự nó sẽ cài đặt – sử dụng Ubuntu Software Center.

**Cài đặt file .rpm**

* Mở Terminal
* Cài đặt gói alien với câu lệnh: sudo apt-get install alien
* Convert file từ .rpm thành .deb với câu lệnh: sudo alien -k filename.rpm
* Sau bước trên bạn đã có một tệp tin là filename.deb, tiếp tục click vào để cài đặt.

**Cài đặt phần mềm từ tarball**

*Giải nén tarball*:

Cách 1: click vào file, nhấn chuột phải, chọn "Extract here".

Cách 2: Dùng dòng lệnh:

`$ tar zxvf file.tar.gz`

`$ tar zxf file.tar.gz`

`$ tar zxf file.tgz`

`$ tar jxf file.tar.bz2`

`$ tar jxf file.tbz2`

Các tùy chọn chúng ta cung cấp cho tar được mô tả bên dưới:

* `z`: lệnh cho tar chạy file này thông qua gzip để giải nén (sử dụng `j` cho các file bzip)
* `x`: bung các file
* `v`: cho “verbose”, để chúng ta có thể thấy danh sách các file đang bung
* `f`: cho lệnh cho tar rằng chúng ta đang làm việc với một file

*Configure*:

* Mở terminal lên, dùng lệnh cd để di chuyển tới nơi đã bung file ở bước trước 
* Gõ `./configure`, mục đích là để kiểm tra xem hệ thống có đầy đủ các phần mềm để cài đặt chưa, nếu thiếu thì ta phải cài đặt các phần mềm đó trước
* Gõ `make`, chờ cho tới khi hoàn thành rồi đến bước tiếp theo
* Gõ `sudo make install`: đợi cho tới khi kết thúc là hoàn thành cài đặt.

## 3.5. Sự khác nhau giữa update, upgrade và dist-upgrade

`apt-get update`: cập nhật danh sách các gói sẵn có và các phiên bản của chúng, nhưng nó không cài đặt hoặc nâng cấp bất kỳ gói nào. 

`apt-get upgrade`: cài đặt các phiên bản mới hơn của các gói bạn có. Sau khi cập nhật danh sách, công cụ quản lý gói biết về các bản cập nhật có sẵn cho phần mềm bạn đã cài đặt. Đây là lý do tại sao trước tiên bạn phải cập nhật (update) trước đã. 

`apt-get dist-upgrade`: ngoài việc thực hiện các chức năng của lệnh `apt-get upgrade`, nó còn loại bỏ các gói cài đặt cũ đang hiện có nếu điều này là cần thiết.

## 3.6. Các lệnh cơ bản

**Các lệnh quản lí tập tin**


Các lệnh quản lí tập tin

|Lệnh|Mô tả| 
|---|---|
|`cp file /folfer`|Chép tập tin vào folder|
|`cp file1 file2`|Chép tập tin file1 sang file2|
|`cp -r folder1 folder2`|Chép toàn bộ nội dung của thư mục folder1 vào folder2|
|`rsync -a folder1 folder2`|Đồng bộ nội dung thư mục folder1 sang thư mục folder2|
|`mv file1 file2`|Chuyển tên tập tin file1 thành tên file2|
|`mv folder1 folder2`|Chuyển tên thư mục folder1 thành folder2|
|`mv file folder`|Chuyển tập tin file vào thư mục folder|
|`mkdir folder`|Tạo ra thư mục folder|
|`mkdir -p folder1/folder2`|Tạo ra thư mục cha folder1 và thư mục con folder2 cùng lúc|
|`rm file`|Xóa bỏ tập tin file trong thư mục hiện hành|
|`rmdir folder`|Xóa bỏ thư mục trống mang tên folder|
|`rm -rf folder`|Xóa bỏ thư mục mang tên folder với tất cả các tập tin trong thư mục|
|`ln -s file link`|Tạo ra một liên kết mang tên link đến tập tin file (lối tắt)|
|`find folder -name`|file Tìm tập tin mang tên file trong thư mục folder kể cả trong các thư mục con|
|`diff file1 file2`|So sánh nội dung của 2 tập tin hoặc của 2 thư mục|

Di chuyển, liệt kê tập tin và thư mục

|Lệnh|Mô tả| 
|---|---|
|`pwd`|Hiển lên tên thư mục đang làm việc hiện hành|
|`cd`|Di chuyển sang thư mục «/home/người_dùng»|
|`cd ~ /Desktop`|Di chuyển sang thư mục «/home/người_dùng/Desktop»|
|`cd ..`|Di chuyển sang thư mục cha (ngay trên thư mục hiện hành)|
|`cd /usr/apt`|Di chuyển sang thư mục «/usr/apt»
|`ls -l`|Folder liệt kê danh mục tập tin trong thư mục folder|
|`ls -a`|Liệt kê tất cả các tập tin, kể cả các tập tin ẩn (thường có tên bắt đầu bằng một dấu chấm)|
|`ls -d`|Liệt kê tên các thư mục nằm trong thư mục hiện hành|
|`ls -t	`|Xếp lại các tập tin theo ngày đã tạo ra, bắt đầu bằng những tập tin mới nhất|
|`ls -S`|Xếp lại các tập tin theo kích thước, từ to nhất đến nhỏ nhất|
|`ls -l l more`|Liệt kê theo từng trang một, nhờ tiện ích «more»|
|`dir`|Giống như lệnh ls dùng để liệt kê tập tin và thư mục|

**Các lệnh quản lí hệ thống**

|Lệnh|Mô tả| 
|---|---|
|`sudo command`|Thực hiện lệnh command với quyền root|
|`gksudo command`|Giống với sudo nhưng dùng cho các ứng dụng đồ hoạ|
|`sudo -k`|	Chấm dứt chế độ dùng lệnh của quyền root|
|`uname -r`|Cho biết phiên bản của nhân Linux|
|`shutdown -h now`|Tắt máy tính ngay lập tức|
|`lsusb`|Liệt kê các thiết bị usb có mặt trong máy tính|
|`lspci`|Liệt kê các thiết bị pci có trên máy tính|
|`time command`|Cho biết thời gian cần thiết để thực hiện xong lệnh command|
|`command1 l command2`|Chuyển kết quả của lệnh command1 làm đầu vào của lệnh command2|
|`clear`|Xoá màn hình của cửa sổ Terminal|

**Phím tắt trong Terminal**

|Lệnh|Mô tả| 
|---|---|
|Ctrl + L|Xoá toàn bộ màn hình, giống lệnh clear|
|Ctrl + D|Exit session, giống lệnh exit|
|Ctrl + R|Tìm một lệnh đã chạy trước đây, nhấn Ctrl + R sau đó bắt đầu gõ một phần của câu lệnh, hệ thống sẽ tự hoàn tất phần còn lại dựa trên các câu lệnh đã được thực hiện trước đó|
|Tab|Hiện gợi ý về câu lệnh|
|Ctrl + Shift + V|Dán (paste) nội dung đã copy vào terminal|
