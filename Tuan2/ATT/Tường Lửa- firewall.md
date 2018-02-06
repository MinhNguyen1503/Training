# Tường Lửa- firewall
# Mục lục:
## 1. Khái niệm
>### 1.1 Mục đích của Firewall
>### 1.2 Chức năng của Firewall
## 2. Phân loại
>### 2.1 Firewall lọc gói( Packet Filetering Firewall)
>### 2.2. Firewall mức kết nối
>### 2.3. Firewall mức ứng dụng
>### 2.4 Firewall lọc gói động
## 3. Những hệ thống trong thực tế
>### 3.1 Các hệ thống firewall đơn giản
>### 3.2 Các hệ thống firewall phức tạp
## 4. Giải pháp triển khai Firewall cụ thể
>### 4.1 Mô hình trung tâm nhỏ
>### 4.2 Mô hình trung tâm trung bình
>### 4.3 Mô hình trung tâm lớn

----
# 1. Khái niệm
 - Hệ Thống Firewall là 1 tập hợp nhiều thành phần (gồm phần cứng và phần mềm) tạo thành "rào chắn" giữa 1 mạng cần bảo vệ với mạng khác.
 - Nó sẽ giữ lại các gói dữ liệu đi vào và ra khỏi mạng, phân tích , cho phép chúng đi qua hoặc hủy bỏ trên chích sách được thiết lập trước. 
 
## 1.1) Mục đích của Firewall:
- Bảo vệ chống lại các cuộc tấn công định tuyến nguồn và gửi lại các đường dẫn định tuyến tới cái site qua giao thức ICMP.

- Giới hạn truy cập từ trong tới mạng ngoài.

- Tăng tính riêng tư, sự an toàn cho tài nguyên trên mạng.


## 1.2) Chức năng của Firewall
- **Điều khiển truy cập**: Cho phép những người dùng hợp lệ có quyền truy cập đến tài nguyên của mạng mà người đó cần, xác định người dùng được phép và các tài nguyên nào được phép truy cập và cách truy cập.

- **Theo dõi truy cập**: Người quản trị có thể xem xét tất cả các kết nối đang kích hoạt theo thời gian thực và có thể ngắt hoặc chặn các kết nối đó.

- **Ghi lại nhật kí làm việc**: Tính toán về các thông báo truy cập, lập báo cáo phân tích chi tiết.

- **Cảnh báo an ninh**: Sử dụng nhiều tùy chọn để cảnh báo.
 -  vd : Dùng email để thông báo, sử dụng giao thức SNMP để gửi các cảnh báo .

- **Ngăn chặn các kiểu tấn công** :
  + **Giả mạo địa chỉ IP(IP spoofing)**: kỹ thuật dựa trên giả mạo địa chỉ IP của router hoặc máy chỉ để thu quyền truy cập. Lợi dụng điểm yếu  IPv4 như: định tuyến nguồn, tạo gói tin. Gateway của Firewall sẽ ngăn chặn bằng cách hạn chế truy cập và không cho thu nhận các thông tin.

   + **Gateway**: là một thiết bị điện tử có thể kết nối các loại mạng khác nhau
- **Tấn công phong tỏa dịch vụ(Dos-Denial of Service)**: là tập hợp các cuộc tấn công có chủ đích nhằm ngăn chặn 1 máy tính cung cấp dịch vụ cho người dùng. Vd: Tràn sys bằng ứng dụng SYSDefender. Firewall sẽ kiểm tra số lượng yêu cầu dịch vụ từ chối khi số lượng này vượt quá 1 giới hạn.

- **Tấn công mạng Lan(Lan attack)**: Kẻ tấn công gửi các gói SYS cho nạn nhân, nạn nhân đó gửi các gói tin SYS-ACK cho chính bản thân mình, tạo ra các kết nối không được sử dụng chiếm hết khoảng trông bảng khi hết thời gian.  

### Điểm yếu của firewall:
 - không thể ngăn chặn 1 cuộc tấn công nếu cuộc tấn công ấy không "đi qua nó".
 - Không thể chống lại cuộc tấn công trong nội bộ hoặc rò rỉ thông tin dữ liệu.
 - Không thể chống lại các cuộc tấn công bằng dữ liệu điều khiển (Dta drivent attack). Vd: Chương trình được truyền theo thư điện tử vượt qua firewall và nó sẽ bắt đầu hoặt động khi được kích hoạt.

----

# 2.  Phân loại

## 2.1. Firewall lọc gói( Packet Filetering Firewall)
- Là **thế hệ thứ nhất**, nó phân tích các thông tin về tầng giao vận trong gói tin IP của mạng.

- **Việc kiểm tra gói tin trên mạng như sau**:
  + Nếu không trong quy tắc nào thì bỏ gói tin đó.
  + Nếu không thấy 1 quy tắc cho phép truyền thông tin thì cho phép truyền ngang hàng.
  + Nếu có quy tắc từ chối từ bỏ gói tin đó.

- **Firewall lọc gói** thường thay địa chỉ cho các gói tin để luồng thông tin đi ra có địa chỉ khác với địa chỉ máy trạm. Quá trình ghi địa chỉ mới cho các gói tin được gọi là chuyển dịch địa chỉ mạng.  

### Ưu điểm của Firewall lọc gói:  

 + Cài đặt và vận hành đơn giản
 + Nhanh hơn các kĩ thuật firewall khác và dễ dàng thực hiện như các giải pháp phần cứng.
 + chỉ 1 quy tắc có thể bảo vệ toàn mạng bằng các ngăn chặn các kết nối từ 1 số máy của mạng ngoài vào các máy tính được bảo vệ.
 + Không yêu cầu sử dụng dịch vụ phải được cấu hình 1 cách đặc biệt.
 + Khi kết hợp chuyển dịch địa chỉ, dùng Firewall lọc để che giấu các địa chỉ IP nội bộ.  

### Nhược điểm của Firewall lọc gói:  
  + Là điểm yếu cho các cuộc tấn công được chỉ định ở giao thức cao hơn.
  + Không hiểu giao thức tầng ứng dụng, Kém an toàn hơn Firewall mức kết nối và mức Ứng dụng.
  + không thể cất giấu topo mạng riêng. Vì vậy phơi bày mạng riêng cho thế giới 
  + Không quản lý được các thông tin trạng thái và các thông tin về phiên làm việc => Không hiểu được ngữ cảnh kết nối.
  + Hạn chế khả năng xử lý thông tin trong gói tin => 1 số dịch vụ yếu bảo mật có thể đi qua. Vd: thư điện tử thông qua SNMP.
  + Không đưa ra các tính năng hữu dụng như: Lưu trữ tạm thời đối tượng HTTP, lọc theo URL và khả năng xác thực.
  + Không hạn chế thông tin nào được truyền từ các máy tính nội bộ thông qua các dịch vụ máy chủ => Kẻ xâm nhập có thể truy cập tới dịch vụ trên máy chủ Firewall 
  + không có khả năng thống kê sự kiện và cơ chế báo động.  

## 2.2. Firewall mức kết nối

 - Là công nghê Firewall thứ 2 , xác nhận tính hợp lệ của 1 gói tin  là yêu cầu kết nối hoặc gói dữ liệu thuộc về một kết nối giữ 2 tầng giao thức tương đương.

 - Áp dụng 1 tập quy tắc được duy trì cho kết nối TCP/IP.

 - Kiểm tra thêm để đảm bảo gói tin không bị giả mạo.

 - Firewall mức kết nối thường đề địa chỉ mới cho các gói tin lớp mạng để nguồn thông tin đi ra sẽ có địa chỉ nguồn là Firewall => Các Firewall này phát hiện 1 số kiểu dữ liệu của gói tin đã bị sử lý.

 - Duy trì thông tin về từng phiên làm việc nên có thể trả lại các gói tin đáp ứng tới máy trạm tương ứng.

 - Firewall mức kết nối thường lưu dữ các thông tin sau:
  + Nhận dạng phiên làm việc duy nhất với kết nối này => mục đích theo dõi và giám sát.
  + Trạng thái kết nối: đang bắt tay, đã thiết lập hay kết thúc.
  + Thông tin thứ tự của các gói tin.
  + Địa chỉ IP nguồn.
  + Địa chỉ IP đích.
  + Giao diện vật lý đến và qua.  
  
### Ưu điểm của Firewall mức kết nối:  
   + Kết nối nhanh hơn Firewall mức ứng dụng
   + Bảo vệ toàn bộ mạng bằng các ngăn kết nối giữ địa chỉ nguồn cụ thể với các máy tính ở trong mạng.
   + Che địa chỉ IP của mạng với người dùng ở mạng ngoài.  

### Nhược điểm: 
   + Không hạn chế theo các nhóm con của TCP.
   + Không thể kiểm tra an ninh với giao thức lớp cao.
   + Chỉ thống kê gói dữ liệu theo thuộc tính có từ trước, không thể thống kê các thuộc tính bổ sung.
   + Không đưa ra các tính năng hữu dụng như: Lưu trữ tạm thời đối tượng HTTP, lọc theo URL và khả năng xác thực.  

## 2.3. Firewall mức ứng dụng
- Là **Firewall thế hệ thứ 3**, cung cấp điều khiển tại lớp ứng dụng. Với khả năng kiểm tra chi tiết lưu thông. Nó kiểm tra tính hợp lệ của các gói dữ liệu tại tầng ứng dụng trước khi cho phép thực hiện một kết nối.
- Có phần mềm ứng dụng chuyên dụng và các dịch vụ ủy quyền.
- **Một proxy ứng dụng** yêu cầu 2 thành phần: Proxy server và proxy client.  
+ **Proxy server**:
   + hoạt động như 1 server đầu cuối cho tất cả các yêu cầu kết nối.
   + Tất cả thông tin trao đổi  giữa người dùng nội bộ và mạng ngoài phải đi qua proxy server. 
   + Sẽ kiểm tra các yêu cầu này và đưa ra quyết định chấp nhận hay từ chối
+ **Proxy cilent**: là 1 phần của ứng dụng người dùng.
- **Các dịch vụ ủy quyền** thực hiện trên tầng cao nhất của mô hình OSI và chỉ hoạt động trong không gian ứng dụng của hệ điều hành.
- Giống firewall kết nối , Firewall ứng dụng thực hiện các kiểm tra bổ sung để đảm bảo rằng các gói tin không bị giả mạo.

### Ưu điểm của các dịch vụ ủy quyền:
  + Dễ cấu hình hơn các Firewall lọc gói tin
  + Có thể giấu topo mạng riêng.
  + Có thể áp đặt điều khiển được giao thức lớp cao.
  + Lưu giữ các thông tin về cuộc liên lạc
  + Sử dụng để từ chối truy cập đối với các dịch vụ.
  + Xử lý và thao tác dữ liệu gói.
  + Không cho phép liên lạc trực tiếp giữa các server bên ngoài và máy tính nội bộ.
  + Dẫn đường cho các dịch vụ nội bộ, cũng như các yêu cầu từ mạng ngoài vào mạng trong.
  + Cung cấp các tính năng bổ sung : lữu trữ tạm thời đối tượng HTTP, lọc URL và xác thực người dùng.
  + Ghi lại các thông tin thống kê.  

### Nhược điểm của các dịch vụ ủy quyền
  + thay đổi ngăn xếp mạng vốn có của server.
  + không chạy proxy server và server cung cấp trên cùng Firewall.
  + Độ trễ khi thực hiện.
  + Người dùng phải chờ ra các Proxy cho các ứng dụng( thường là 6 tháng)
  + không thể cung cấp các proxy những giao thức UDP,RPC và những dịch vụ sử dụng giao thức này.
  + Thêm xử lý cấu hình
  + Dễ bị tấn công với hệ điều hành và các "rệp" mức ứng dụng.
  + Không chú ý tới thông tin chứa các lớp thấp hơn các gói.
  + Proxy server có thể yêu cầu thêm mật khẩu hoặc các thủ tục xác nhận làm tăng độ trễ của dịch vụ.  

## 2.4 Firewall lọc gói động

- Là Firewall thế hệ thứ 4. Cho phép sửa đổi các chính sách đảm bảo an ninh dựa trên các tình huống. Có ích trong việc cung cấp sự hỗ trợ với csac giao thức tầng giao vận UDP.

- Các firewall này thực hiện những yêu cầu chức năng của nó bằng cách liên kết tất cả các gói UDP đi qua vành đai bảo vệ an ninh bằng 1 kết nối ảo đã được thay đỏi và đi qua server firewall.

- Không cho phép tự động gửi các gói tin UDP và mạng nội bộ.

- Gói tin đi qua phải có địa chỉ đích phù hợp, cổng đích tầng giao vận phải phù hợp với cổng nguồn và phải cùng kiểu giao thức tầng giao vận.

- Cũng có thể sử dụng để cung cấp hỗ trợ cho 1 tập con nào đố của giao thức vận chuyển ICMP.  

----

# 3. Những hệ thông Firewall trong thực tế. 

- **Mạng vành đai**: Là mạng được đặt giữa một mạng được bảo vệ và một mạng bên ngoài để cung cấp thêm lớp bảo vệ an ninh, gọi tắt là DMZ(De-militarzed Zone- Vùng phi quân sự)

## 3.1 Các hệ thống firewall đơn giản
- Các hệ thông firewall đơn giản thường chỉ sử dụng 1 thiết bị để kiểm soát sự trao đổi thông tin.  

### a) Bastion Host
- Là 1 hệ thống mà bất kì 1 ngoài ngoài hoặc có thể là kẻ địch phải liên hệ để truy cập 1 hệ thống hoặc 1 dịch vụ nằm trong Firewall => bastion có sự tập trung bảo vệ cao.

- Sử dụng 1 hoặc tích hợp nhiều kiến trúc Firewall khác nhau, phổ biến nhất là lọc gói tin, proxy hoặc tích hợp của hai loại này.

- Được thiết kế theo 1 nguyên lý cơ bản: Đơn giản và có xử lí đặc biệt đối với host khi bị xâm hại.  

### b) Screening Router

![](https://i.imgur.com/HUW4hOz.png) 
 
- Hệ thống Firewall lọc gói tin sử dụng 1 router gọi là Screening router, có đầy đủ tính năng cra Firewall lọc gói tin.  
- Router biết một số thông tin phản ánh môi trường mà gói tin đi tới hoặc môi trường gói tin đi qua => Screening router lựa chọn cho phép những gói tin nào đi ra mạng ngoài và những gói tin nào đi được vào mạng trong như sau:
 + Khóa hết các kết nối từ hệ thống mạng ngoài vào mạng trong trừ kết nối SMTP.
 + Cấm tất cả kết nối đến và đi từ những hệ thống cụ thể không được phép.
 + Cho phép dịch vụ E-mail và dịch vụ FTP nhưng khoá các dịch vụ nguy
hiểm như TFTP, hệ thống Window X, RPC, các dịch vụ “r” (rsh, rcp …).  
- Xử lý bằng phần cứng nên độ an toàn cao hơn, tốc độ xử lý nhanh so với xử lý bằng dual-home host hoặc bastion host.  

### C) Dual-Home Host
![](https://i.imgur.com/u7WnEFN.png)

- Hệ thống dual-home host được xây dựng trên 1 máy tính có ít nhất 2 giao diện liên kết mạng, hoạt động như 1 bộ định tuyến giữa các mạng.
- Gói tin IP từ 1 mạng không tin cậy không được định tuyến trực tiếp tới mạng bảo vệ.
- Luồng thông tin IP giữa chúng bị khóa hoàn toàn.  

#### Ưu điểm cura Firewall dual-homed host:

+ Điều khiển đầy đủ các kết nối mạng
+ Có các ưu điểm của Firewall ứng dụng.

#### Nhược điểm: 
 + là lối duy nhất để vào mạng nội bộ nên trở thành mục tiêu duy nhất để tấn công.
 + làm giảm hiệu suất sử dụng mạng: khi cài trên 1 máy tốc độ thấp
 + Có đầy đủ nhược điểm của các firewall ứng dụng.

## 3.2 Các hệ thống firewall phức tạp

 - Phối hợp các hệ thống firewall đơn giản thành các hệ thống firewall phức tạp hơn.  

### a) Hệ thông Screened Host
![](https://i.imgur.com/sfpXTT3.png)

- Sử dụng 1 cặp một screening router và 1 bastion host theo kiểu proxy server để bảo vệ mạng nội bộ.
- Vấn đề an ninh chủ yếu được cung cấp bởi việc lọc gói tin, Screening router sẽ ngăn người sử dụng ở cả 2 mạng đi vòng qua các bastion host để tiến hành kết nối trực tiếp. Còn bastion host làm proxy Firewall cho các dịch vụ cần thiết.  

#### Ưu điểm: 
  + Mề dẻo hơn hệ thống dual- homed host.
  + An tòa hơn screening router

#### Nhược điểm:
 + Cưng cấp mức bảo vệ anh ninh mở cho mạng nội bộ, nhưng phải phụ thuộc vào khả năng phòng thủ của screening router.
 + Khó cấu hình hơn, cần phải cấu hình thêm cho screening router.
 + kẻ tấn công vẫn có thể tấn công vào mạng bằng các gửi các gói tin với địa chỉ nguồn giả mạo.  


### b) hệ thống screened Subnet
![](https://i.imgur.com/VhkKdQg.png)  

- Là hệ thống Firewall được đưa thêm một mạng vành đai vào giữa mạng nội bộ và mạng ngoài để cách ly và cô lập bastion host.
- hệ thống có 2 router, cả 2 đểu được kết nối với mạng vành đai và mạng ngoài.
- Để vào được hệ thống  kẻ tấn công phải đi qua cả 2 screening router => các trạm ở mạng trong sẽ ít bị nguye hiểm hơn.
- Tuy nhiên phải có sự khác nhau về chính sách bảo vệ an ninh giữa các lớp mạng.
+ Screening router được đặt giữa mạng trong và bastion host gọi là **Interior router**:
   - Nó bảo vệ mạng nội bộ khỏi sự tấn công mạng từ mạng ngoài vào mạng vành đai và lựa chọn các dịch vụ từ mạng nội bộ đi ra ngoài.
   - Interior router cho phép giữa bastion host và mạng không nhất thiết phải cùng với các dịch vụ nó cho phép giữa mạng ngoài và mạng trong.

+ Screening router được đặt giữa mạng ngoài và bastion host gọi là **Exterior router**:
   - Exterior route bảo vệ cả mạng vành đai và mạng bên trong khỏi sự
truy cập bất hợp pháp từ mạng ngoài.
   - Exterior router được cung cấp bởi những người quản lí mạng ngoài (ví dụ như nhà cung cấp Internet), và khi đó sự truy nhập ra mạng ngoài có thể bị hạn chế.
 - Nhiệm vụ chủ yếu của Exterior router là cấm mọi gói tin đến từ
mạng ngoài có địa chỉ nguồn giả mạo, nhưng nó không thể đưa ra rằng các gói tin đến từ mạng vành đai là giả mạo hay không. => tạo lỗ hỏng cho kẻ tấn công khi đã xâm nhập vào bastion host.  

#### Ưu điểm:
  - Có chính sách bảo vệ mềm dẻo hơn bằng việc sử dụng cả bộ lọc gói và các proxy server
  - Mức độ bảo vệ an ninh rất cao. Kẻ tấn công phải phá được sự bảo vệ của 3 thiết bị độc lập mới vào được.
  - Hỗ trợ việc che dấu mạng nội bộ.  

#### Nhược điểmm:
  + Phải có thêm nhiều thiết bị: cần có 2 screening router và 1 bastion.
  + Khó cấu hình.


### C) Hệ thống Screened Subnet với nhiều Bastion Host
![](https://i.imgur.com/AVVtZiu.png)

- là hệ thống có thể đưa thêm vào hệ thống screened subnet hai hoặc nhiều bastion host.  

- Nếu sử dụng nhiều basion host trong hệ thông screened subnet với mục đích dự phòng , nếu 1 bastion host bị lỗi thì các dịch vụ vẫn có thể được cung cấp bởi các bastion host khác.  

- Cũng có thể sử dụng nhiều basion host để lưu trữ riêng dữ liệu.  

- Bằng việc cung cấp 2 server có thể đưa ra các dữ liệu khác nhau cho khách hàng và có thể đạt được hiệu suất tốt nhất.  

### d) Hệ thống Screened Subnet với sự hợp nhất hai Screening Router
![](https://i.imgur.com/0oFwA2h.png)

- Có thể hợp nhất Exterior router và Interior router thành một screening
router khi có một screening router đủ khả năng và linh hoạt.
- hệ thống này giống hệ thống screened host sẽ làm cho mạng
trong có thể bị tổn thương nếu router hợp nhất bị xâm hại.  

### e) Hệ thống Screened Subnet với sự hợp nhất Bastion host và Exterior router.  

![](https://i.imgur.com/TdgYruY.png)  

- Đây chính là hệ thống sử dụng một dual-homed host vừa làm bastion host
vừa làm Exterior router.
- Sử dụng một dual-homed host để định tuyến luồng thông tin không có
được khả năng thực thi và tính linh hoạt như của một router chuyên dụng.
- Nếu hợp nhất bastion host và Interior router, phải thay đổi cấu hình Firewall một cách cơ bản. 
- Nếu bastion host bị xâm nhập thì
không còn có gì ngăn cách giữa bastion host và mạng nội bộ.
- Việc hợp nhất bastion host với Interior router làm cho luồng thông tin của mạng nội bộ có thể bị nhìn thấy trên basion host.
  
----

# 4 Giải pháp triển khai Firewall
## 4.1. Mô hình trung tâm nhỏ

![](https://i.imgur.com/LGO85Um.png)

- Mô hình này cho phép tăng hệ số an toàn của mạng và dễ dàng quản trị.
Khi một firewall bị lỗi vẫn không ảnh hưởng đến các kết nối trên firewall còn lại.
- Các tính năng firewall:
 + Thông lượng firewall đạt tốc độ tới 150Mbps
 + Firewall có sẵn tính năng VPN với tốc độ sử lý đến 30Mbps. Hỗ trợ cả hai
mô hình kết nối VPN client-to-site và site-to-site
 + Hỗ trợ tới 8000 kết nối đồng thời
 + Hỗ trợ khả năng sẵn sàng cao High Availability
– Các tính năng kĩ thuật:
 + Kiểm soát truy cập
 + Kiểm soát truy cập từ bên ngoài(LAN, Internet) vào bên trong mạng
 + Kiểm soát truy cập từ bên mạng ra bên ngoài (LAN, Internet)
 + Chuyển dịch địa chỉ: Dịch địa chỉ các máy bên trong mạng DMZ sang các
địa chỉ thực bên ngoài và dịch địa chỉ các máy bên trong mạng nội bộ sang
một địa chỉ duy nhất là địa chỉ card mạng bên ngoài.

## 4.2 Mô hình trung tâm trung bình

![](https://i.imgur.com/LFTMtwK.png)

- Mô hình này cho phép tăng hệ số an toàn của mạng và dễ dàng quản trị.
Khi một firewall bị lỗi vẫn không ảnh hưởng đến các kết nối trên firewall còn lại.
- Ngoài ra, firewall thứ ba sẽ làm tăng độ bảo mật của hệ thống, tạo thêm một lớp bảo vệ nữa cho các máy bên trong mạng.

-  Các tính năng firewall
  + Firewall bảo vệ bên ngoài:
  + Thông lượng firewall đạt tốc độ tới 150Mbps
  + Firewall có sẵn tính năng VPN với tốc độ sử lý đến 30Mbps. Hỗ trợ cả hai mô hình kết nối VPN client-to-site và site-to-site
  + Hỗ trợ tới 8000 kết nối đồng thời.
  Hỗ trợ khả năng sẵn sàng cao High Availability

  + Firewall bảo vệ bên trong:
  + Thông lượng firewall đạt tốc độ tới 220Mbps
  + Firewall có sẵn tính năng VPN với tốc độ xử lý đến 54 Mbps. Hỗ trợ cả
hai mô hình kết nối VPN client-to-site và site-to-site
  + Chạy trên phần cứng chuyên dụng với hệ điều hành đã được làm cứng hoá.
– Các tính năng kĩ thuật:
  + Kiểm soát truy cập
  + Kiểm soát truy cập từ bên ngoài (LAN, Internet) vào bên trong mạng
  + Kiểm soát truy cập từ bên mạng ra bên ngoài (LAN, Internet)
  + Chuyển dịch địa chỉ: Dịch địa chỉ các máy bên trong mạng DMZ sang các
địa chỉ thực bên ngoài và Dịch địa chỉ các máy bên trong mạng nội bộ
sang một địa chỉ duy nhất là địa chỉ card mạng bên ngoài
  + Chống tấn công
  + Chống lại các tấn công mới nhất tại tầng ứng dụng. Firewall lớp 2 phải có
khả năng cập nhật các mẫu tấn công mới nhất.

## 4.3 Mô hình trung tâm lớn

![](https://i.imgur.com/zkoGONe.png)

- Mô hình này cho phép tăng hệ số an toàn của mạng và dễ dàng quản trị.
Firewall thứ ba sẽ làm tăng độ bảo mật của hệ thống, tạo thêm một lớp bảo vệ nữa cho các máy bên trong mạng, các máy chủ quan trọng.

- Các tính năng firewall
   + Firewall bảo vệ bên ngoài:
   + Thông lượng firewall đạt tốc độ tới 150Mbps
   + Firewall có sẵn tính năng VPN với tốc độ sử lý đến 30Mbps. Hỗ trợ cả hai mô hình kết nối VPN client-to-site và site-to-site
   + Hỗ trợ tới 8000 kết nối đồng thời
   + Hỗ trợ khả năng sẵn sàng cao High Availability
   + Firewall bảo vệ bên trong:
   + Đảm bảo hoạt động với tốc độ cao, khả năng sẵn sàng cao
   + Thông lượng firewall đạt tốc độ tới 600Mbps
   + Firewall có sẵn tính năng VPN với tốc độ xử lý đến 200 Mbps AES/MD5

   Hỗ trợ cả hai mô hình kết nối VPN client-to-site và site-to-site
   + Chạy trên phần cứng chuyên dụng với hệ điều hành đã được làm cứng hoá.
– Các tính năng kĩ thuật:
   + Kiểm soát truy cập
   + Kiểm soát truy cập từ bên ngoài (LAN, Internet) vào bên trong mạng
   + Kiểm soát truy cập từ bên mạng ra bên ngoài (LAN, Internet)
   + Chuyển dịch địa chỉ: Dịch địa chỉ các máy bên trong mạng DMZ sang các
địa chỉ thực bên ngoài và Dịch địa chỉ các máy bên trong mạng nội bộ
sang một địa chỉ duy nhất là địa chỉ card mạng bên ngoài.
   + Chống tấn công.
   + Firewall lớp 2 phải có khả năng chống lại các tấn công mới nhất tại tầng
ứng dụng, khả năng cập nhật các mẫu tấn công mới nhất.
   + Khả năng sẵn sàng cao: Firewall lớp 2 phải gồm hai module chạy theo chế độ active- standby. Khi một module bị hỏng, module còn lại sẽ tự động thay thế mà không cần sự can thiệp của người quản trị. Khi cần có thể nâng cấp lên hoạt động với mô hình active-active.
