## 1.1 Linux:
Linux là tên gọi của một hệ điều hành máy tính và cũng là tên *hạt nhân* của hệ điều hành. Nó có lẽ là một ví dụ nổi tiếng nhất của phần mềm tự do và của việc phát triển mã nguồn mở. Thuật ngữ "Linux" được sử dụng để chỉ Nhân Linux (Linux Kernel), nhưng tên này được sử dụng một cách rộng rãi để miêu tả tổng thể một hệ điều hành tương tự Unix (còn được biết đến dưới tên GNU/Linux) được tạo ra bởi việc đóng gói nhân Linux cùng với các thư viện và công cụ GNU, cũng như là các bản phân phối Linux. Thực tế thì đó là tập hợp một số lượng lớn các phần mềm như máy chủ web, các ngôn ngữ lập trình, các hệ quản trị cơ sở dữ liệu, các môi trường desktop như GNOME và KDE, và các ứng dụng thích hợp cho công việc văn phòng như OpenOffice, LibreOffice.

## 1.2. Nhân Linux
Hệ điều hành Linux có thể phân thành hai vùng: 
* Vùng người dùng (User Space) gồm các thư viện C và các phần mềm ứng dụng
* Vùng nhân (Kernel Space) gồm ba thành phần chính là System Call Interface, Kernel và Architexture/Dependent code.

![](https://www.ibm.com/developerworks/linux/library/l-linux-kernel/figure2.jpg)

Trên cùng là lớp các ứng dụng của người dùng (User Applications). Bên dưới là lớp các thư viện C (GNU C Library). Lớp thư viện phục vụ cho giao diện các lời gọi hệ thống tạo liên kết giữa các ứng dụng và nhân Linux. Giao diện này quan trọng vì nhân Linux và các ứng dụng chiếm các vùng địa chỉ bộ nhớ được bảo vệ khác nhau. Mỗi ứng dụng có vùng địa chỉ ảo riêng còn nhân có một vùng địa chỉ duy nhất.

Nhân Linux có thể chia thành ba lớp. Trên cùng là giao diện các lời gọi hệ thống thực hiện các chức năng cơ bản như đọc, ghi. Bên dưới là phần mã nhân hệ điều hành (kernel code) hoặc chính xác hơn là mã nhân độc lập với kiến trúc vi xử lý (processor). Các mã lệnh trong lớp này dùng chung cho mọi loại processor mà Linux hỗ trợ. Lớp dưới cùng là các mã lệnh phụ thuộc vào kiến trúc từng loại processor (x86, x86-64,…).

Có thể thấy nhân Linux thực ra là bộ quản lý các tài nguyên. Các tài nguyên gồm: các tiến trình (process), bộ nhớ (memory) và thiết bị phần cứng. Nhân Linux quản lý các tài nguyên đó và nó điều hành việc truy cập tài nguyên đồng thời của nhiều user.

![](https://www.ibm.com/developerworks/linux/library/l-linux-kernel/figure3.jpg)

* **System call interface – SCI**: SCI thực hiện các lời gọi hệ thống từ vùng ứng dụng vào nhân Linux. Giao diện này độc lập với kiến trúc bộ vi xử lý ngay cả trong cùng một họ vi xử lý. SCI có thể thực hiện các dịch vụ gọi hàm dồn kênh và tách kênh. Các gói liên quan được cài trong thư mục ẩn ./linux/kernel và phần độc lập với kiến trúc vi xử lý nằm trong ./linux/arch.
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

Một bản phân phối Linux (thường được gọi tắt là **distro**) là một hệ điều hành được tạo dựng từ tập hợp nhiều phần mềm dựa trên hạt nhân Linux và thường có một hệ thống quản lý gói tin. Người dùng Linux thường tải một bản phân phối Linux, trong đó có sẵn trong một loạt các hệ thống khác nhau, từ các thiết bị nhúng (VD OpenWrt) và máy tính cá nhân đến Siêu máy tính (VD Rocks Cluster Distribution).

Một bản phân phối Linux điển hình bao gồm một Linux kernel, các công cụ và thư viện GNU, các phần mềm thêm vào, tài liệu, một window system (phần lớn sử dụng X Window System), window manager và một môi trường desktop. Phần lớn các phần mềm là phần mềm tự do nguồn mở có sẵn cả file biên dịch nhị phân và mã nguồn, cho phép chỉnh sửa phần mềm gốc. Thông thường, các bản phân phối Linux tùy chọn bao gồm một số phần mềm độc quyền mà có thể không có sẵn ở dạng mã nguồn, ví dụ như các binary blob yêu cầu cho các trình điều khiển thiết bị. Hầu như tất cả các bản phân phối Linux là Unix-like, ngoại lệ đáng chú ý nhất là Android, không bao gồm một giao diện dòng lệnh và các chương trình làm cho các bản phân phối Linux điển hình.

Một bản phân phối Linux cũng có thể được mô tả như một loại riêng biệt của ứng dụng và phần mềm tiện ích (công cụ GNU khác nhau và các thư viện làm ví dụ), đóng gói cùng với các hạt nhân Linux theo cách như vậy mà khả năng của nó đáp ứng được nhu cầu của nhiều người sử dụng. Phần mềm này thường được chuyển đến phân phối và sau đó được đóng gói thành các gói phần mềm bằng cách bảo trì của phân phối. Các gói phần mềm có sẵn trực tuyến trong cái gọi là kho lưu trữ, đó là địa điểm lưu trữ thường phân bố trên toàn thế giới. Ngoài các thành phần chính, chẳng hạn như các trình cài đặt phân phối (ví dụ, Debian-Installer hay Anaconda) hoặc các hệ thống quản lý gói, còn có một số ít các gói mà ban đầu được viết từ dưới lên bởi các nhà bảo trì của một phân phối Linux.

Có khoảng sáu trăm bản phân phối Linux tồn tại, với gần năm trăm trong số đó phát triển tích cực, liên tục được sửa đổi và cải thiện. Bởi vì sự sẵn có lớn của phần mềm, phân phối đã thực hiện một loạt các hình thức, kể cả những người phù hợp để sử dụng trên máy tính để bàn, máy chủ, máy tính xách tay, netbook, điện thoại di động và máy tính bảng,cũng như môi trường tối thiểu thường để sử dụng trong các hệ thống nhúng. Có nhiều phân phối hỗ trợ thương mại, như Fedora (Red Hat), openSUSE (SUSE) và Ubuntu (Canonical Ltd.), và hoàn toàn phân phối dựa vào cộng đồng, chẳng hạn như Debian, Slackware, Gentoo hay Arch Linux. Hầu hết các bản phân phối đều sẵn sàng để sử dụng và biên dịch sẵn kèm theo một bộ hướng dẫn cụ thể, trong khi một số phân phối (như Gentoo) phân phối chủ yếu ở dạng mã nguồn và biên dịch cục bộ trong quá trình cài đặt. 

----------------------------------------------------------------
# Tổng hợp các lệnh thường dùng trên Ubuntu

# I. Các lệnh quản lí tập tin: 
## 1. Tạo tập tin và thư mục:
cp  file1 file2: chép tập tin file1 sang file2.

cp  file /folfer: chép tập tin file vào thư mục folder.

cp -r folder1 folder2: chép toàn bộ nội dung của thư mục folder1 vào folder2.

rsync -a folder1 folder2: đồng bộ nội dung thư mục «folder1»sang thư mục «folder2».

mv file1 file2: chuyển tên tập tin file1 thành tên file2.

mv folder1 folder2: chuyển tên thư mục folder1 thành folder2.

mv file folder: chuyển tập tin file vào thư mục folder.

mv file1 folder2/file2: chuyển file1 vào thư mục thư mục folder2 đồng thời đổi tên tập tin thành file2.

mkdir folder: tạo ra thư mục folder.

mkdir -p folder1/folder2: tạo ra thư mục cha folder1 và thư mục con folder2 cùng lúc.

rm file: xóa bỏ tập tin file trong thư mục hiện hành.

rmdir folder: xóa bỏ thư mục trống mang tên folder.

rm -rf folder: xóa bỏ thư mục mang tên folder với tất cả các tập tin trong thư mục.

ln -s file link: tạo ra một liên kết mang tên link đến tập tin file (nối tắt).

## 2. Di chuyển, liệt kê tập tin và thư mục: 
pwd: hiển lên tên thư mục đang làm việc hiện hành.

cd: di chuyển sang thư mục « /home/người_dùng ».

cd ~ /Desktop: di chuyển sang thư mục « /home/người_dùng/Desktop ».

cd .. : di chuyển sang thư mục cha (ngay trên thư mục hiện hành).

cd /usr/apt: di chuyển sang thư mục « /usr/apt ».

ls -l: folder liệt kê danh mục tập tin trong thư mục folder.

ls -a: liệt kê tất cả các tập tin, kể cả các tập tin ẩn (thường có tên bắt đầu bằng một dấu chấm).

ls -d: liệt kê tên các thư mục nằm trong thư mục hiện hành.

ls -t: xếp lại các tập tin theo ngày đã tạo ra, bắt đầu bằng những tập tin mới nhất.

ls -S: xếp lại các tập tin theo kích thước, từ to nhất đến nhỏ nhất.

ls -l | more: liệt kê theo từng trang một, nhờ tiện ích « more ».

dir: giống như lệnh ls dùng để liệt kê tập tin và thư mục.

# II. Các lệnh quản lí hệ thống:
## 1. Các lệnh quản lí cơ bản:

sudo command: thực hiện lệnh command với tư cách người siêu dùng (root).

sudo -k: chấm dứt chế độ dùng lệnh có chức năng của người siêu dùng.

uname -r: cho biết phiên bản của nhân Linux.

shutdown -h now: khởi động lại máy tính ngay lập tức.

lsusb: liệt kê các thiết bị usb có mặt trong máy tính.

lspci: liệt kê các thiết bị pci có trên máy tính.

clear: xoá màn hình của cửa sổ « Thiết bị cuối » (terminal).

## 2. Quản lí các gói phần mềm:
/etc/apt/sources.list: tập tin xác định nguồn các kho phần mềm để tải xuống nhằm cài mới hoặc cập nhật hệ thống.

apt-get dist-upgrade: nâng cấp phiên bản Ubuntu đang có đến phiên bản mới tiếp theo.

apt-get install soft: cài phần mềm soft đồng thời giải quyết các gói phần mềm phụ thuộc.

apt-get remove soft: loại bỏ phần mềm soft cũng như tất cả các gói phần mềm trực thuộc.

apt-get remove –purge soft: loại bỏ phần mềm soft kể cả tập tin cấu hình của phần mềm soft.

## 3. Quản lí mạng
/etc/network/interfaces: thông tin cấu hình của các bộ phần giao diện (interfaces).

uname -a: hiển thị tên của máy tính trong mạng (hostname).

ping địa chỉ IP: thử nối mạng đến máy có địa chỉ IP.

ifconfig -a: hiển thị thông tin về tất cả các giao diện mạng đang có.

ifconfig eth0 địa chỉ IP: xác định địa chỉ IP cho giao diện cạc mạng eth0.

ifdown eth0: ngưng hoạt động giao diện cạc mạng eth0.

ifconfig eth0 down

ifup eth0: kích hoạt giao diện cạc mạng eth0.

ifconfig eth0 up

poweroff -i: ngưng hoạt động tất cả các nối mạng.

route add default gw: địa chỉ IP xác định địa chỉ IP của máy làm cổng dẫn đến bên ngoài mạng cục bộ.

route del default: bỏ địa chỉ IP mặc định để ra khỏi mạng cục bộ.

-------------------------------------------------------------------------------------------------------

## Các cách cấu hình địa chỉ IP:
1. Cấu hình tạm thời: mất sau khi reboot máy tính.
2. Cấu hình IP tĩnh: vẫn giữ sau khi reboot máy tính.
3. Cấu hình IP động: nhận địa chỉ IP một cách tự động từ một DHCP server.

*1. Cấu hình tạm thời:* 
> Sử dụng lệnh ifconfig để đặt địa chỉ IP.

ifconfig -a 	Xem tất cả giao diện mạng.
ifconfig ethX	Xem cấu hình hiện tại ethX, có thể thay bằng eth0, eth1,...
sudo ifconfig ethX IP-address netmask net-address 	Đặt cấu hình IP mới.


*2. Cấu hình IP tĩnh:* 
> Sử dụng phần mềm nano để biên soạn file: sudo apt-get install nano

- Dùng nano để mở file lưu thông tin về cấu hình IP:  
sudo nano /etc/network/interfaces

- Bổ sung/sửa các thông tin:  
auto eth0  
iface eth0 inet static  
Address 172.16.19.100+X  
Netmask 255.255.255.0  
Gateway 172.16.19.1  

Sau khi edit xong:

sudo /etc/init.d/networking restart --	khởi động lại dịch vụ để lấy cấu hình mới :D  
sudo ifconfig eth0 down  
sudo ifconfig eth0 up 				--	Tải và bật lại card mạng.  
sudo reboot 						--	Restart máy và kiểm tra lại.  

*3. Cấu hình IP động:*
> Giống cấu hình IP tĩnh, chỉ thay từ khóa static bằng dhcp
auto eth0
iface eth0 inet dhcp

*4. Các câu lệnh khác về Network:* 
- Ping
> Lệnh ping gửi các gói ECHO-REQUEST tới địa chỉ chỉ định. Câu lệnh nhằm kiểm tra máy tính có thể kết nối với Internet hay một địa chỉ IP cụ thể nào đó hay không. Tuy nhiên có rất nhiều hệ thống được cấu hình để không hồi đáp với các lệnh ping. Cú pháp câu lệnh rất đơn giản: $ ping host .

Không như Windows, câu lệnh ping trên Linux sẽ duy trì gửi các gói tin cho đến khi bạn kết thúc nó. Có thể định số lượng gói tối đa gửi đi bằng cách gõ thêm tùy chọn -c. Ví dụ: ping -c google.com.

- Netstat:
> Câu lệnh netstat đưa ra các thống kê khác nhau cho giao diện, bao gồm các socket mở và các bảng định tuyến.

Sử dụng câu lệnh netstat -p để xem các chương trình đi kèm với các socket mở.
Xem các thống kê chi tiết cho tất cả các cổng bằng câu lệnh netstat -s

- Traceroute:
Lệnh traceroute là một tiện ích hữu dụng để chuẩn đoán hoạt động của mạng. Cú pháp câu lệnh giống với lệnh ping nhưng kết quả không chỉ cho biết 2 host có kết nối được với nhau không mà còn chỉ ra các thiết bị trung gian nằm giữa 2 máy. Qua đó biết được thiết bị nào cấu hình sai. Ví dụ:

> $ traceroute 192.168.1.1. 
> traceroute to 192.168.1.1 (192.168.1.1), 30 hops max, 40 byte packets. 
> 1 192.168.0.1 (192.168.0.1) 1.712 ms 2.212 ms 2.724 ms. 
> 2 192.168.1.1 (192.168.1.1) 6.437 ms 6.561 ms 6.686 ms. 

Tuy nhiên khi kết nối với một máy ở xa trên Internet, do có nhiều mạng với những tường lửa nên nhiều khi lệnh ping và traceroute không chạy nhưng trên thực chất là mạng hoạt động bình thường.
