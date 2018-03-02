# Day 1: Sơ lược về OSI.

----
## What is OSI?
> Mô hình tham chiếu OSI là một cấu trúc phả hệ có 7 tầng, nó xác định các yêu cầu cho sự giao tiếp giữa hai máy tính.

Mô hình OSI phân chia chức năng của một giao thức ra thành một chuỗi các tầng cấp. Mỗi một tầng cấp có một đặc tính là nó chỉ sử dụng chức năng của tầng dưới nó, đồng thời chỉ cho phép tầng trên sử dụng các chức năng của mình.

## Các tầng của OSI:
# Tầng 1: Physical Layer (Tầng vật lý):

> Lớp vật lý định nghĩa các đặc tính vật lý của mạng chẳng hạn như kết nối, cấp điện áp và thời gian.  

**Tầng vật lý bao gồm:**
- Sóng thu phát.
- Hub.
- Repeater: bộ lặp.
- Converter: thiết bị chuyển đổi tín hiệu.
- Network Adapter: thiết bị tiếp hợp mạng.
- Host bus adapter: thiết bị tiếp hợp kênh máy chủ.

**Chức năng của tầng vật lý:**

- Thiết lập hoặc ngắt mạch kết nối điện với một môi trường truyền dẫn phương tiện truyền thông.
- Tham gia vào quy trình mà trong đó các tài nguyên truyền thông được chia sẻ hiệu quả giữa nhiều người dùng.
- Điều chế hoặc biến đổi giữa BIỂU DIỄN DỮ LIỆU SỐ của các thiết bị người dùng và các tín hiệu tương ứng được truyền qua kênh truyền thông.


# Tầng 2: Data-link layer (Tầng liên kết dữ liệu):
Tầng liên kết dữ liệu cung cấp các phương tiện có tính chức năng và quy trình để truyền dữ liệu giữa các thực thể mạng (truy cập đường truyền, đưa dữ liệu vào mạng), phát hiện và có thể sửa chữa các lỗi trong tầng vật lý nếu có.

Các lớp liên kết dữ liệu định dạng các thông điệp vào một khung dữ liệu(Frame), và thêm vào đó một header chứa các địa chỉ phần cứng nơi nhận và địa chỉ nguồn của nó.Tiêu đề này chịu trách nhiệm cho việc tìm kiếm các thiết bị đích tiếp theo trên một mạng nội bộ.

>Lớp này là chia nhỏ thành 2 lớp con: điều khiển logic liên kết (LLC) và kiểm soát truy cập media (MAC).  
Các chức năng LLC bao gồm:  
- Quản lý các khung cho các lớp trên và dưới  
- Kiểm soát lỗi.  
- Điều khiển luồng.  
Lớp con MAC mang địa chỉ vật lý của mỗi thiết bị trên mạng.Địa chỉ này là thường được gọi là địa chỉ MAC của thiết bị.Địa chỉ MAC là một địa chỉ 48 bit được ghi vào NIC trên thiết bị của nhà sản xuất.

# Tầng 3: Network Layer (Tầng mạng):
Tầng mạng cung cấp các chức năng và quy trình cho việc truyền các chuỗi dữ liệu có độ dài đa dạng, từ một nguồn tới một đích, thông qua một hoặc nhiều mạng, trong khi vẫn duy trì chất lượng dịch vụ **(quality of service)** mà tầng giao vận yêu cầu. 

Tầng mạng thực hiện chức năng định tuyến.Các thiết bị định tuyến (router) hoạt động tại tầng này — gửi dữ liệu ra khắp mạng mở rộng, làm cho liên mạng trở nên khả thi.  
Đây là một hệ thống định vị địa chỉ logic – các giá trị được chọn bởi kỹ sư mạng. Hệ thống này có cấu trúc phả hệ.

# Tầng 4: Transport Layer (Tầng giao vận): 

Tầng giao vận cung cấp dịch vụ chuyên dụng chuyển dữ liệu giữa các người dùng tại đầu cuối, nhờ đó các tầng trên không phải quan tâm đến việc cung cấp dịch vụ truyền dữ liệu đáng tin cậy và hiệu quả.

Tầng giao vận kiểm soát độ tin cậy của một kết nối được cho trước. Có nghĩa là tầng giao vận có thể theo dõi các gói tin và truyền lại các gói bị thất bại.

Ở tầng 4 địa chỉ được đánh là address ports, thông qua address ports để phân biệt được ứng dụng trao đổi.

# Tầng 5: Session Layer:
**Chức năng của Session layer:**  

- Kiểm soát các phiên hội thoại giữa các máy tính. 
- Thiết lập, duy trì và kết thúc giao tiếp với các thiết bị nhận.

Tầng này hỗ trợ hoạt động từ duplex (đơn công) - half duplex đến single và thiết lập các quy trình đánh dấu điểm hoàn thành (trì hoãn - kết thúc - khởi động lại); giúp việc phục hồi truyền thông nhanh hơn khi có lỗi xảy ra.

Tầng này có khả năng ngắt các phiên giao dịch và kiểm tra/phục hồi phiên.

# Tầng 6: Presentation Layer:
**Chức năng:**  
Lớp này trên máy tính truyền dữ liệu đảm nhiệm vai trò dịch dữ liệu được gửi từ tầng application sang định dạng chung.  
Tại máy tính nhận, lớp này lại chuyển từ định dạng chung sang định dạng của tầng application.

- Dịch các mã kí tự từ ASCII -> EBCDIC.
- Chuyển đổi dữ liệu như từ số interger sang số dấu phảy động.
- Nén dữ liệu để giảm lượng giữ liệu truyền trên mạng.
- Mã hóa và giải mã dữ liệu để đảm bảo sự bảo mật trên mạng.

# Tầng 7: Tầng ứng dụng (Application layer): 

Đây là tầng gần với người sử dụng nhất. Nó cung cấp phương tiện cho người dùng truy nhập các thông tin và dữ liệu trên mạng thông qua chương trình ứng dụng. Tầng này là giao diện chính để người dùng tương tác với chương trình ứng dụng, và qua đó với mạng.

--------------------------------------------------------------------

# Day 2: Các tầng của mô hình TCP/IP.

# Tầng 1: Network Access Layer:
Tầng truy nhập mạng bao gồm các giao thức mà nó cung cấp khả năng truy nhập đến một kết nối mạng. 
Tại tầng này, hệ thống giao tiếp với rất nhiều kiểu mạng khác nhau, cung cấp các trình điều khiển để tương tác với các thiết bị phần cứng ví dụ như Token Ring, Ethernet, FDDI… 

# Tầng 2: Internet Layer:
Nhiệm vụ của tầng mạng trên mô hình TCP/IP là giải quyết vấn đề dẫn các gói tin đi qua các mạng để đến đúng đích mong muốn. Vì vậy tại tầng này bao gồm các thủ tục cần thiết giữa các hosts và gateways để di chuyển các gói giữa các mạng khác nhau. Một gateway kết nối hai mạng, và sử dụng kết nối mạng bao gồm IP ( Internet Protocol ), ICMP ( Internet Control Message Protocol ).

# Tầng 3: Transport Layer:
Cũng giống với tầng vận chuyển của mô hình OSI, tầng vận chuyển làm nhiệm vụ phân nhỏ các gói tin có kích thước lớn khi gửi và tập hợp lại khi nhận, đảm bảo tính toàn vẹn cho dữ liệu (không lỗi,không mất, không lặp, đúng thứ tự).

Một giao thức đầu vào tại đây cung cấp một kết nối logic giữa các thực thể cấp cao.Các dịch vụ có  thể bao gồm việc điều khiển lỗi và điều khiển luồng. 

# Tầng 4: Application Layer:
Tầng này bao gồm các giao thức cấp cao mà chúng được sử dụng để cung cấp các giao diện với người sử dụng hoặc các ứng dụng. 
Do mô hình TCP/IP không có tầng nào nằm giữa tầng ứng dụng và tầng vận chuyển , nên tầng ứng dụng của mô hình TCP/IP bao gồm cả các giao thức hoạt động như tầng trình diễn và phiên trong mô hình OSI.

--------------------------------------------------------------
# 2.1) Cấu trúc gói tin TCP:

> TCP là một giao thức cần phải thiết lập liên kết logic trước khi có thể truyền dữ liệu. Giao thức này đảm bảo chuyển giao dữ liệu tới nơi nhận một cách đáng tin cậy và đúng thứ tự. TCP còn phân biệt giữa dữ liệu của nhiều ứng dụng đồng thời chạy trên cùng một máy chủ. 

Trong bộ giao thức TCP/IP, TCP là tầng trung gian giữa giao thức IP bên dưới và một ứng dụng bên trên. Các ứng dụng thường cần các kết nối đáng tin cậy kiểu đường ống để liên lạc với nhau, trong khi đó, giao thức IP không cung cấp những dòng kiểu đó, mà chỉ cung cấp dịch vụ chuyển gói tin không đáng tin cậy. TCP làm nhiệm vụ của tầng giao vận trong mô hình OSI đơn giản của các mạng máy tính.


**Một gói tin TCP bao gồm 2 phần: header và dữ liệu.** Phần header có 11 trường trong đó 10 trường là bắt buộc, trường thứ 11 là optional.
![](https://imgur.com/gi4FmmK)

**1. Source port**: Số hiệu của cổng tại máy tính gửi.

**2. Destination port**: Số hiệu của cổng tại máy tính nhận.

**3. Sequence number**: 
- Nếu cờ SYN bật thì nó là số thứ tự gói ban đầu và byte đầu tiên được gửi có số thứ tự này cộng thêm 1.
- Nếu không có cờ SYN thì đây là số thứ tự của byte đầu tiên.

**4. Acknowledgment number**:
- Nếu cờ ACK bật thì giá trị của trường chính là số thứ tự gói tin tiếp theo mà bên nhận cần.

**5. Data offset**:
- Trường có độ dài 4 bit quy định độ dài của phần header (tính theo đơn vị từ 32 bit). Phần header có độ dài tổi thiểu là 5 từ ~ 160bit và tối đa là 15 từ ~ 480 bit.

**6. Reserved**: Sử dụng trong tương lai và có giá trị là 0.

**7. Flags**: bao gồm 6 cờ.
- URG: dành cho trường Urgent Pointer.
- ACK: dành cho trường Acknowledgement.
- PSH: hàm PUSH, nhằm đẩy thêm dữ liện đệm vào ứng dụng nhận.
- RST: Thiết lập lại đường truyền.
- SYN: Đồng bộ lại số thứ tự. Chỉ gói tin đầu tiên được gửi từ mỗi đầu cho đến khi chúng được đặt cờ; một số cờ và các trường khác thay đổi ý nghĩa dựa trên cờ này, một số chỉ có giá trị khi nó được đặt, và một số khác khi nó được rõ ràng.
- FIN: Packet cuối cùng không gửi thêm số liệu. 

**8. Window size**:
- Số byte có thể nhận bắt đầu từ giá trị của trường báo nhận (ACK).

**9. Checksum**:
- 16 bít kiểm tra cho cả phần header và dữ liệu. Kết quả thu được sau khi đảo giá trị từng bít được điền vào trường kiểm tra.

**10. Urgent Pointer**:
- Nếu cờ URG bật thì giá trị trường này chính là số từ 16 bit mà số thứ tự gói tin cần dịch trái.

**11. Options**:
Đây là trường tùy chọn, là độ dài bội số của 32 bít.

++ Phần dữ liệu:
Giá trị của trường này là thông tin dành cho các tầng trên (trong mô hình 7 lớp OSI). Thông tin về giao thức của tầng trên không được chỉ rõ trong phần header mà phụ thuộc vào cổng được chọn.

----------------------------------------------------------------
# 2.2) Cấu trúc gói tin UDP:

>UDP cung cấp một giao diện rất đơn giản giữa tầng mạng bên dưới và tầng phiên làm việc hoặc tầng ứng dụng phía trên. Không đảm bảo tính tin cậy khi truyền dữ liệu và không có cơ chế phục hồi dữ liệu.Do có ít chức năng nên UDP có xu hướng chạy nhanh hơn so với TCP. Nó thường được sử dụng cho các ứng dụng đòi hỏi độ tin cậy không cao.

++ Phần header: Gồm 16 bit source port, 16 bit des port chứa thông tin về địa chỉ cổng nguồn, cổng đích, độ dài của gói và checksum.

Phần header của UDP chỉ chứa 4 trường dữ liệu, trong đó có 2 trường là tùy chọn.

![](https://imgur.com/EAQ3n3H)
**1. Source port (optional):**
- Trường này xác định cổng của người gửi thông tin và có ý nghĩa nếu muốn nhận thông tin phản hồi từ người nhận. Nếu không dùng đến thì đặt nó bằng 0.

**2. Destination port:**
- Trường này xác định cổng nhận thông tin, và trường này là cần thiết.

**3. Length:**
- Trường có độ dài 16 bit xác định chiều dài của toàn bộ datagram: phần header và dữ liệu. Chiều dài tối thiểu là 8 byte khi gói tin không có dữ liệu, chỉ có header.

**4. Checksum (optional):** 
16 bit dùng cho việc kiểm tra lỗi của phần header và dữ liệu.

Do thiếu tính tin cậy, các ứng dụng UDP nói chung phải chấp nhận mất mát, lỗi hoặc trùng dữ liệu. 

-----------------------------------------------------------------
# 2.3) ICMP
![](https://i.imgur.com/pQ8xTrQ.png)
Ví dụ gói tin ICMP type 0 code 1 có ý nghĩa là Destination Unreacheable:

**1. Type:**
- Cho biết định dạng gói tin, có 8 bit dành cho TYPE ICMP vậy nếu tính tổng có khoảng 255 dạng ICMP nhưng chỉ có 8 dạng hay dùng nhất.

**2. Code:**
- Cho biết thông tin chi tiết về dạng dói tin đó. Một gói tin ICMP được hiểu là "Destination Unreacchable" sẽ được thiết lập có code từ 1 tới 15.

**3. Checksum:**
- Ý nghĩa sử dụng để tính toán tổng cộng gói Header + data của gói ICMP.

**4. ID:**
- Thiết lập có ý nghĩa cho dạng Echo Reply.

**5. Sequence:**
- Ý nghĩa bao gồm các thông số cho quá trình trả lời Echo Reply.
-----------------------------------------------------------------
# 2.4) Cấu trúc gói tin IP datagram:
> Dữ liệu được truyền trong qua một mạng Internet bằng cách sử dụng IP được thực hiện trong các tin nhắn được gọi là IP datagram.

**Cấu trúc:**  
  
**1. Version**:
![](https://imgur.com/gthhskf)

- Xác định phiên bản của IP được sử dụng để tạo ra gói tin. Mục đích của nó nhằm đảm bảo khả năng tương thích giữa các thiết bị có thể chạy trên các phiên bản khác nhau của IP.

**2. Internet Header Length (4 bit):** 
- Định chiều dài của tiêu đề IP, tính theo đơn vị word 32 bits. Nếu không có trường này thì độ dài mặc định của phần tiêu đề là 5 từ.

**3. Type of Service (8bit):**
- Được thiết kế để mang thông tin để cung cấp chất lượng của các dịch vụ, chẳng hạn như phân phối ưu tiên cho IP Datagram.

**4. Total Length 16bit:** 
- Chỉ định tổng chiều dài của gói tin IP. Total Length = Length of Header + Length of Data.

**5.  Identification 16bit:**
- Dùng để định danh duy nhất cho một datagram trong khoảng thời gian nó vẫn còn trên liên mạng, đây là một số nguyên.

**6. Flags (3 bit):** 
- Flags kiểm soát một gói tin bị phân mảnh, theo cấu trúc sau:
0	DF 	 MF
Bit 0: reserved chưa sử dụng luôn lấy giá trị 0.
Bit 1: 
+ DF=1: Gói tin bị phân đoạn, có nhiều hơn 1 đoạn.
+ DF=0: Gói tin không bị phân đoạn.
Bit 2: 
+ MF=0: Đây là đoạn cuối cùng.
+ MF=1: Đây chưa phải đoạn cuối cùng, còn đoạn khác phía sau.

**7.  Phân mảnh bù đắp (Fragment offset-13 bit):**
- Chỉ vị trí của đoạn trong datagram, tính theo đơn vị 64bits, có nghĩa là trừ đoạn cuối cùng ra thì mỗi đoạn phải chứa một vùng dữ liệu có độ dài là bội của 64 bits; dùng để ghép lại các mảng datagram với nhau.

**8. Time to live (TTL - 8bit)**: Giải quyết vấn đề gói tin bị lặp vô hạn trên mạng.

- giá trị này được đặt lúc bắt đầu gửi gói tin, giảm dần khi đi qua 1 router.
- Gói tin này sẽ bị hủy khi giá trị =0 mà vẫn chưa đến đích.

**9. Protocol (8bit)**: Chỉ ra giao thức lớp trên, chẳng hạn như TCP hay UDP.

**10. Header Checksum:** 
- Mã kiểm soát lỗi sử dụng phương pháp CRC (cyclic redundancy check) dùng để đảm bảo thông tin về gói dữ liệu được truyền đi một cách chính xác. Nếu việc kiểm tra này thất bại, gói dữ liệu sẽ bị hủy bỏ tại nơi xác định lỗi.
- Giao thức IP không có cơ chế Error Control cho dữ liệu truyền đi, không có cơ chế kiểm soát luồng dữ liệu (flow control).

**11. Source address (32 bit)**: Địa chỉ trạm nguồn.

**12. Destination Address (32 bit)**: địa chỉ trạm đích.

**13. Option (độ dài thay đổi)**: sử dụng trong một số trường hợp, bao gồm bảo mật, chức năng định tuyến đặc biệt.

**14. Padding (độ dài thay đổi)**: Các số 0 được bổ sung vào field này để đảm bảo IP Header luôn là bội số của 32 bit.

**15. Data (độ dài thay đổi)**: Vùng dữ liệu có độ dài là bội của 8 bít, tối đa 65535 bytes.

----
Bonus: So sánh TCP và UDP:

TCP hoạt động theo hướng kết nối (connection-oriented). Trước khi truyền dữ liệu giữa 2 máy, nó thiết lập một kết nối giữa 2 máy theo phương thức “bắt tay 3 bước" (3-way handshake) bằng cách gửi gói tin ACK từ máy đích sang máy nhận, trong suốt quá trình truyền gói tin, máy gửi yêu cầu máy đích xác nhận đã nhận đủ các gói tin đã gửi, nếu có gói tin bị mất, máy đích sẽ yêu cầu máy gửi gửi lại, thường xuyên kiểm tra gói tin có bị lỗi hay ko, ngoài ra còn cho phép qui định số lượng gói tin được gửi trong một lần gửi (window-sizing), điều này đảm bảo máy nhận nhận được đầy đủ các gói tin mà máy gửi gửi đi, dẫn tới nó truyền dữ liệu chậm hơn UDP nhưng đáng tin cậy hơn UDP.

UDP hoạt động theo hướng phi kết nối (connectionless), không yêu cầu thiết lập kết nối giữa 2 máy gửi và nhận, không có sự đảm bảo gói tin khi truyền đi cũng như không thông báo về việc mất gói tin, không kiểm tra lỗi của gói tin, dẫn tới nó truyền dữ liệu nhanh hơn TCP do cơ chế hoạt động có phần đơn giản hơn, tuy nhiên lại ko đáng tin cậy bằng TCP.

TCP thường sử dụng cho các ứng mạng cần độ chính xác và tin cậy cao như mail, FTP,... Còn UDP thích hợp cho các dịch vụ hỗ trợ về mặt tốc độ nhanh như VoIP, truyền hình trực tiếp, game online,...
