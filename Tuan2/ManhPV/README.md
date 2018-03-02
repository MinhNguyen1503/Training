# Báo cáo tuần 2

### Mục lục
1. [Wireshark](#wireshark-start)
	- [Cài đặt](#setup-wireshark)
	- [Bắt và phân tích gói tin](#capture-wireshark)
		- [Bắt gói tin](#capturing-packets)
		- [Màu sắc gói tin](#packets-color)
			- [Màu mặc định](#default-color)
		- [Lọc gói tin](#filter-packets)
		- [Chi tiết gói tin](#packget-detail)
2. [TCPDump](#TCPDump-start)
	- [Giới thiệu](#introduction)
	- [Cài đặt](#install-tcpdump)
	- [Cơ bản](#tcpdump-basic)
		- [Cấu trúc gói tin](#packet-struct)
	- [Tùy chọn trong TCPDump](#options-tcpdump)
	- [Một số bộ lọc cơ bản](#tcp-filters)
3. [Firewall](#Firewall-start)
	- [Nguyên lý](#Firewall-Principles)
	- [Chức năng](#Firewall-function)
	- [Ưu nhược điểm](#firewall-dis-advantages)
		- [Ưu điểm](#firewall-advantages)
		- [Nhược điểm](#firewall-disadvantages)
	- [Sử dụng HTTP Proxy để vượt Firewall](#passing-firewall-ways)
4. [Router](#router-start)
	- [Chức năng](#router-function)

<br/>-----------------------------------------------------------------------------------------------------------------------<br/>
## <a name="wireshark-start"></a>I/ Hướng dẫn sử dụng Wireshark để bắt và phân tích gói tin trong *Network*

Đây là phần mềm được dùng để bắt các gói tin được truyền trong *Network*, từ đó ta phân tích gói tin bắt được, phục vụ cho mục đích nhất định nào đấy. *Wireshark* cũng cung cấp chức năng save, giúp ta lư lại cá gói tin đã bắt được.

### <a name="setup-wireshark"></a> 1.Cài đặt
- Tải Wireshark trong link: https://www.wireshark.org/download.html
- Cài đặt như các phần mêm khác.
<br/>
### <a name="capture-wireshark"></a> 2. Bắt và phân tích gói tin bằng Wireshark
**Trước tiên là phải mở phần mềm lên đã :D**
#### <a name="capturing-packets"></a> a. Bắt gói tin:
- Chọn một *Interface* trong list *Network Interface*:

![](https://www.howtogeek.com/wp-content/uploads/2017/06/ximg_593af0b476165.png.pagespeed.gp+jp+jw+pj+ws+js+rj+rp+rw+ri+cp+md.ic.-oQ4eGr04v.png)
<br/>
Sau khi chọn, Wireshark sẽ chuyển sang màn hình hiển thị các gói tin mà nó bắt được trong *Interface* bạn chọn:

![](https://fthmb.tqn.com/5qrzPliIm9ekuq1gy_52XMZFqY8=/768x0/filters:no_upscale()/wireshark-captured-data-panes-59512e265f9b58f0fc7b1f17.png)
<br/>
- Ta có thể dừng viêc bắt gói tin của **Wireshark** bằng cách nhấn vào nút **Stop**

![](https://www.howtogeek.com/wp-content/uploads/2017/06/img_593af1eb85f89.png.pagespeed.ce.fOjs80KNB2.png)
<br/>
#### <a name="packets-color"></a> b. Màu sắc các gói tin
##### <a name="default-color"></a> Một vài màu mặc định
- Màu xanh lá cây là gói tin trong giao thức **TCP**
- Màu xanh da trời nhạt là gói tin trong giao thức **UDP**
- Màu xanh da trời đậm là gói tin trong giao thức **DNS**
- Màu đen là gói tin *có vấn đề* trong giao thức **TCP**

Ta có thể tùy chỉnh màu của các gói tin trong phần **View > Coloring Rules**

![](https://www.howtogeek.com/wp-content/uploads/2017/06/img_593af2ab6427a.png.pagespeed.ce.uiH9_sCEpL.png)
<br/>
#### <a name="filter-packets"></a> c. Lọc gói tin
Nếu bạn cần tìm các gói tin đặc biệt nào đấy, **Wireshark** có hỗ trợ chức năng *Lọc gói tin*, bạn chỉ cần gõ đúng cú pháp *lọc* của **Wireshark** là được, sau đât là 3 cú pháp đơn giản hay được dùng:
- Tìm theo IP nguồn: **ip.src == *IP nguồn***
- Tìm theo IP đích: **ip.dst == *IP đích***
- Tìm theo *Protocol*: ***Protocol cần tìm***

Ngoài những cú pháp sẵn có, bạn có thể tự tạo cú pháp *lọc* mới bằng cách vào menu **Analyze > Display Filters**

![](https://www.howtogeek.com/wp-content/uploads/2017/06/img_593af5afe5e39.png.pagespeed.ce.ZGbuilwR7w.png)
<br/>
#### <a name="packget-detail"></a> d. Kiểm tra chi tiết gói tin
Bạn có thể kiểm tra kĩ hơn các thông tin trong gói tin bằng cách chọn nó. Hai phần màn hình dưới sẽ thay đổi sang thông tin chi tiết của gói tin, bao gồm toàn bộ phần *header* và *data* của gói tin.

![](https://fthmb.tqn.com/5qrzPliIm9ekuq1gy_52XMZFqY8=/768x0/filters:no_upscale()/wireshark-captured-data-panes-59512e265f9b58f0fc7b1f17.png)
<br/><br/>
<br/>-----------------------------------------------------------------------------------------------------------------------<br/>
## <a name="TCPDump-start"></a>II/ Hướng dẫn sử dụng TCPDump để bắt và phân tích gói tin trong *Network*

### <a name="introduction"></a>1. Giới thiệu
Tương tự như *Wireshark*, *TCPDump* cũng là một phần mềm dùng để bắt các gói tin trong *Network*, có điều, công cụ này hiển thị dưới màn hình console(màn hình command line). *TCPDump* có thể lưu lại các lần bắt gói tin vào file pcap để mở lại vào lần sau, có thể dùng cả *Wireshark* để mở.

### <a name="install-tcpdump"></a> 2. Cài đặt
Với hệ điều hành Ubuntu, chạy lệnh sau để cài đặt: ```sudo apt-get install tcpdump```

### <a name="tcpdump-basic"></a> 3. Sử dụng cơ bản
Để bắt đầu bắt các gói tin bằng *TCPDump* ta chạy câu lệnh: **tcpdump**

Khi này, màn hình console sẽ hiển thị ra các gói tin mà *TCPDump* bắt được theo dòng, bao gồm các thông tin của gói tin.

*TCPDump* sẽ bắt liên tục đến khi ta yêu cầu ngắt. Khi ngắt, *TCPDump* sẽ hiện ra 3 thông báo sau:

- **Packet capture:** số lượng gói tin bắt được và xử lý.
- **Packet received by filter:** số lượng gói tin được nhận bởi bộ lọc.
- **Packet dropped by kernel:** số lượng packet đã bị dropped bởi cơ chế bắt gói tin của hệ điều hành.

#### <a name="packet-struct"></a> Cấu trúc chung của một dòng gói tin:
	time-stamp src > dst:  flags  data-seqno  ack  window urgent options
**Chú giải**
- **time-stamp:** Thời gian lúc bắt gói tin
- **src > dst:** IP nguồn và IP đích
- **Flag:**
	- **S:** (SYN) Được sử dụng trong quá trình bắt tay của giao thức TCP.
	- **.** : (ACK) Được sử dụng để thông báo cho máy gửi biết là đã gửi gói tin thành công.
	- **F:** (FIN) Được sử dụng để đóng kết nối TCP.
	- **P:** (PUSH) Thường được đặt ở cuối để đánh dấu việc truyền dữ liệu.
	- **R:** (RST) Được sử dụng khi muốn thiết lập lại đường truyền.
	- **Data-sqeno:** Số sequence number của gói dữ liệu hiện tại.
	- **ACK:** Mô tả số sequence number tiếp theo của gói tin do máy gửi truyền (số sequence number máy nhận mong muốn nhận được)
	- **Window:** Số byte có thể nhận được.
	- **Urgent:** Cho biết dữ liệu khẩn trong gói tin.

### <a name="options-tcpdump"></a>4. Một số tùy chọn trong TCPDump
- **-D :** Liệt kê các *Network Interface* trong máy có thể sử dụng.
- **-i :** Bắt các gói tin trong một *Network Interface* được chỉ định. VD: ```tcpdump -i ens33```
- **-c N :** TCPDump bắt N gói tin, sau đó dừng lại.
- **-n :** Không phân dải IP sang hostname.
- **-nm :** Tương tự **-n** và không phân giải cả portname
- **-v :** Tăng số lượng thông tin nhận được trong gói tin(Có thể dùng **-vv** hay **-vvv**).
- **-s :** Tùy chỉnh kích thước gói tin sẽ lưu lại.
### <a name="tcp-filters"></a> 5. Các bộ lọc cơ bản
- **dst A:** Bắt các gói tin có IP đích là A.
- **src A:** Bắt các gói tin có IP nguồn là A.
- **host A:** Bắt các gói tin có hostname nguồn hoặc đích là A.
- **port A:** Bắt các gói tin có port được chỉ định.
- **less A:** Bắt các gói tin có *length* nhỏ hơn A.
- **greater A:** Bắt các gói tin có *length* lớn hơn A.
- **(ether | ip) broadcast:** Bắt các gói tin *IP broadcast* hoặc *Ether broadcast*.
- **Protocol:** Bắt các gói tin theo *Protocol*.VD: ```tcpdump tcp```
<br/><br/><br/>
<br/>-----------------------------------------------------------------------------------------------------------------------<br/>
## <a name="Firewall-start"></a>III/ Firewall
**Firewall** là một hệ thống an ninh mạng, có thể dựa trên phần cứng hoặc phần mềm, sử dụng các quy tắc để kiểm soát traffic vào, ra khỏi hệ thống. **Firewall** hoạt động như một rào chắn giữa mạng an toàn và mạng không an toàn.

**Firewall** gồm các thành phần cơ bản sau:
- **Bộ lọc gói (Packet Filter):** làm nhiệm vụ lọc các packet vào / ra khỏi mạng.
- **Proxy Services:** một Server đặc biệt ở giữa Client và Server thực sự làm nhiệm vụ lọc ở mức message mức ứng dụng (application level).
- **Cổng vòng (Circuit-Level Gateway):** chuyển tiếp (relay) các kết nối TCP mà không thực hiện bất kỳ một hành động xử lý hay lọc packet nào.

### <a name="Firewall-Principles"></a> 1. Nguyên lý
**Firewall** hoạt động chặt chẽ với giao thức TCI/IP, vì giao thức này cũng làm việc theo thuật toán chia nhỏ dữ liệu thành các packets kèm địa chỉ rồi mới gửi đến đích.

Bộ lọc packet cho phép hay từ chối mỗi packet mà nó nhận đ­ợc. Nó kiểm tra toàn bộ đoạn dữ liệu để quyết định xem đoạn dữ liệu đó có thoả mãn một trong số các quy tắc của bộ lọc packet hay không. Các quy tắc lọc packet dựa trên các thông tin ở phần *Header* của packet, dùng để cho phép truyền các packet đó ở trên mạng:
- Địa chỉ IP nơi xuất phát ( IP Source address)
- Địa chỉ IP nơi nhận (IP Destination address)
- Những thủ tục truyền tin (TCP, UDP, ICMP, IP tunnel)
- Cổng TCP/UDP nơi xuất phát (TCP/UDP source port)
- Cổng TCP/UDP nơi nhận (TCP/UDP destination port)
- Dạng thông báo ICMP ( ICMP message type)
- Giao diện packet đến ( incomming interface of packet)
- Giao diện packet đi ( outcomming interface of packet)

Nếu packet thỏa mãn các quy tắc của **Firewall**, nó sẽ được cho phép đi qua **Firewall**, nếu không nó sẽ bị từ chối.

### <a name="Firewall-function"></a> 2. Chức năng
Chức năng chính của **Firewall** là kiểm soát luồng thông tin ra vào trong *Network*. Thiết lập cơ chế điều khiển dòng thông tin trong *Network*:
- Cho phép hoặc cấm  dịch vụ truy cập ra ngoài.
- Cho phép hoặc cấm dịch vụ truy cập vào trong.
- Theo dõi luồng dữ liệu mạng trong *Network*.
- Kiểm soát địa chỉ truy cập, cấm địa chỉ truy cập.
- Kiểm soát người sử dụng và việc truy cập của người sử dụng.
- Kiểm soát nội dung thông tin lưu thông trên mạng.

**Firewall** hoạt động như một thiết bị trung gian, thay mặt user để thực hiện kết nối ra bên ngoài để đảm bảo an toàn.

**Firewall** cũng có thể bảo vệ dữ liệu của user khỏi các mối đe dọa bảo mật thông qua việc kiểm soát truy cập, trạng thái gói tin.

### <a name="firewall-dis-advantages"></a> 3. Ưu nhược điểm của firewall
#### <a name="firewall-advantages"></a> a. Ưu điểm
- **Firewall** do con người cấu hình có thể che dấu mạng nội bộ bên trong, lọc dữ liệu và nội dung của dữ liệu để ngăn chặn được các ý đồ xấu từ bên ngoài như : muốn đánh cắp thông tin mật, muốn gây thiệt tê liệt hệ thống đối thủ của mình để gây thiệt hại về kinh tế…
<br/>
- **Firewall** có thể ngăn chặn các cuộc tấn công vào các server.
<br/>
- Ngoài ra **Firewall** còn có khả năng quét virus, chống spam,... khi được tích hợp những công cụ cần thiết.

#### <a name="firewall-disadvantages"></a> b. Nhược điểm

- **Firewall** không thể bảo vệ chống lại các cuộc tấn công bỏ qua tường lửa.
<br/>
- **Firewall** không thể bảo vệ chống lại các đe dọa từ bên trong nội bộ. Ví dụ như một nhân viên cố ý hoặc một nhân viên vô tình hợp tác với kẻ tấn công bên ngoài.
<br/>
- **Firewall** không thể bảo vệ, chống lại việc chuyển giao giữa các chương trình bị nhiễm virus hoặc các tâp tin. Bởi vì sự đa dạng của các hệ điều hành và các ứng dụng được hỗ trợ từ bên trong nội bộ. Sẽ không thực thế và có lẽ là không thể cho các **Firewall** quét các tập tin được gửi đến nhằm phát hiện virus.

### <a name="passing-firewall-ways"></a> 4.  Sử dụng HTTP Proxy để vượt Firewall

Sử dụng **HTTP Proxy Server** làm trung gian để gửi các yêu cầu của user ra ngoài đến máy đích khi IP máy đích bị chặn bởi **Firewall**. Như vậy, khi kiểm tra gói tin, thay vì xác nhận IP của máy đích, **Firewall** sẽ chỉ xác nhận được IP của **HTTP Proxy Server**. Điều kiện để thực hiện phương pháp này là IP của **HTTP Proxy Server** phải không bị chặn bởi **Firewall**.

<br/>-----------------------------------------------------------------------------------------------------------------------<br/>

## <a name="router-start"></a> IV/Router
Hay còn gọi là bộ định tuyến, là một thiết bị mạng máy tính dùng để **chuyển các gói dữ liệu** qua một liên mạng và đến các thiết bị đầu cuối, thông qua một tiến trình được gọi là định tuyến.

Router hoạt động ở tầng 3, trên nền giao thức IP, nên có thể tái tạo lại các packet ở tầng 3 và đọc được các thông số IP, dựa vào nó mà so sánh với bảng routing (bảng dẫn đường) để chuyển tiếp gói tin trong mạng Lan hay Wan.
Nhiệm vụ của Router đều là **định tuyến hết**. Nhưng ở Wan, thì sẽ có thêm một chức năng quan trọng hơn, đó là **kết nối các đường truyền** chạy các giao thức khác nhau, làm cho chúng hiểu được nhau.

### <a name="router-functions"></a> 1. Chức năng của Router

- Theo cách nói thông thường, một router hoạt động như một liên kết giữa hai hoặc nhiều mạng và chuyển các gói dữ liệu giữa chúng. Router đưa vào bảng định tuyến (routing table) để tìm đường đi cho gói dữ liệu.

**Bảng định tuyến được người quản trị mạng cấu hình tĩnh (static).**

> Được thiết lập một lần và thường do quản trị mạng nhập bằng tay, hoặc động (dynamic).

> Bảng tự học đường đi thông qua các giao thức định tuyến và nội dung tự động thay đổi theo sự thay đổi của tô pô mạng.

- **Phân cách** các mạng máy tính thành các segment riêng biệt để giảm hiện tượng **đụng độ**, giảm **broadcast** hay thực hiện chức năng bảo mật.

- **Kết nối** các mạng máy tính hay kết nối các user với mạng máy tính **ở các khoảng cách xa** với nhau thông qua các đường truyền thông: Điện thoại, ISDN, T1, X.25…

- Switch phát triển, Router chỉ còn phải đảm nhận việc thực hiện các kết nối truy cập từ xa **(remote access)** hay các **kết nối WAN** cho hệ thống mạng LAN.

- Do hoạt động ở tầng thứ 3 của mô hình OSI, router sẽ hiểu được các protocol quyết định phương thức truyền dữ liệu. Các địa chỉ mà router hiểu là các địa chỉ “giả” được quy định bởi các protocol. Ví dụ như địa chỉ IP đối với protocol TCP/IP, địa chỉ IPX đối với protocol IPX… Do đó tùy theo cấu hình, router quyết định phương thức và đích đến của việc chuyển các packet từ nơi này sang nơi khác. Một cách tổng quát router sẽ chuyển packet theo các bước sau:  

	- Đọc packet.
	- Gỡ bỏ dạng format quy định bởi protocol của nơi gửi.
	- Thay thế phần gỡ bỏ đó bằng dạng format của protocol của đích đến.
	- Cập nhật thông tin chuyển dữ liệu: địa chỉ, trạng thái của nơi gửi, nơi nhận.
	- Gứi packet đến nơi nhận qua đường truyền tối ưu nhất.

### <a name="router-types"></a> 2. Phân loại
#### <a name="router-type-functions"></a> a. Theo chức năng
- **Remote Access Router**
- **ISDN Router**
- **Serial router**
- **Hub**
- ...

#### <a name="router-type-struct"></a> b. Theo cấu trúc
- **Fixed configuration**
- **Modular**

### <a name="arp-protocol"></a> 3.ARP Protocol

### <a name="router-dis-advantages"></a> 4. Ưu nhược điểm của Router
#### <a name="router-advantages"></a> a.Ưu điểm
Router có thể kết nối với các **loại mạng** khác lại với nhau, từ những *Ethernet* cục bộ tốc độ cao cho đến đường dây điện thoại đường dài có tốc độ chậm.

#### <a name="router-disadvantages"></a> b.Nhược điểm
-  Router **chậm hơn** *Bridge* vì chúng đòi hỏi nhiều tính toán hơn để tìm ra cách dẫn đường cho các gói tin, đặc biệt khi các mạng kết nối với nhau không cùng tốc độ.  
- Router có đặc điểm **chuyên biệt theo giao thức**. Tức là cách một máy tính kết nối mạng giao tiếp với một router IP thì sẽ khác biệt với cách nó giao tiếp với một router Novell hay DECnet.
- Tất cả các Router thương mại đều có thể xử lý nhiều loại giao thức, thường với chi phí phụ thêm cho mỗi giao thức.

## <a name="switch-start"></a> V/ Switch
