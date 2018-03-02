## I-Firewall: 
> Hệ thống Firewall sử dụng để tạo rào chắn cho một mạng cần được bảo vệ đối với những mạng khác. Hệ thống này sẽ giữ lại các gói tin đi vào và đi ra khỏi mạng này, phân tích chúng để cho phép chúng đi qua hoặc hủy bỏ dựa trên một chính sách bảo vệ mà mạng đã thiết lập từ trước. Có thể hiểu đơn giản Firewall dùng để bảo vệ một mạng của một tổ chức khi mạng này được kết nối với các mạng khác :D

Firewall kiểm soát sự kết nối giữa mạng cần bảo vệ với các mạng ngoài. Mục đích của Firewall là:
- Chống lại các cuộc tấn công định tuyến nguồn và gửi lại các đường dẫn định tuyến tới các site dàn xếp thông qua giao thức ICMP.
- Để giới hạn các truy cập với mạng ngoài.
- Tăng độ riêng tư và an toàn cho tài nguyên mạng.

**Chức năng của Firewall:**
1. Điều khiển truy nhập:
Firewall kiểm soát và điều khiển các truy cập, chỉ cho phép những người dùng hợp lệ có quyền truy cập đến tài nguyên của mạng mà người dùng đó cần. Firewall phải hiểu được tất cả các dịch vụ và các ứng dụng đang hoạt động trên mạng.

2. Theo dõi truy nhập: 
Firewall có thể theo dõi, hiển thị, báo cáo về những lưu thông mạng mà nó điều khiển, người dùng có thể theo dõi kết nối theo thời gian thực, ngắt hoặc chặn các kết nối đó.

3. Ghi lại quá trình làm việc:
Firewall có thể tính toán về các thông tin truy nhập hay mọi kết nối một cách chi tiết: user, service, thời gian bắt đầu kết nối, đích đến,....

4. Cảnh báo an ninh: 
Firewall có thể đưa ra nhiều tùy chọn để cảnh báo qua Email hay sử dụng giao thức SNMP để gửi các cảnh báo an ninh tới các hệ thống quản trị mạng.

5. Ngăn chặn các kiểu tấn công như:
- IP Spoofing (giả mạo địa chỉ IP): dựa trên sự giả mạo địa chỉ IP của một router hoặc máy chủ để thu được quyền truy cập tới các tài nguyên được bảo vệ.
Các Gateway sẽ ngăn chặn kiểu tấn công mạo danh IP bằng cách hạn chế truy nhập mạng dựa trên giao diện mạng của Gateway, không cho các hoạt động thu nhận tin từ giao diện đó.
- DOS-Denial of service (tấn công phong tỏa dịch vụ): đây là một tập các cuộc tấn công có chủ đích nhằm ngăn chặn một máy tính đang cung cấp các dịch vụ cho những người sử dụng hợp pháp. Firewall sẽ kiểm tra số lượng yêu cầu dịch vụ tới một máy chủ nào đó và thực hiện từ chối cung cấp dịch vụ khi số lượng này vượt quá một giới hạn cho phép nào đó.
- Tấn công mạng LAN (LAN attack): nếu kẻ tấn công gửi các gói SYN giả tạo chứa địa chỉ IP nguồn và đích cho nạn nhân, nạn nhân đó gửi các gói tin SYN-ACK cho chính bản thân mình, từ đó tạo ra các kết nối không được sử dụng chiếm khoảng trống đến khi hết thời gian. 
Firewall có thể chống lại các cuộc tấn công mạng LAN bằng cách kết hợp sự bảo vệ chống lại SYS Flood và IP Spoofing.
----

**Phân loại Firewall:**
1. Packet Filtering Firewall - Firewall lọc gói:
Đây là thế hệ đầu phân tích về tầng giao vận trong các gói tin IP của mạng. 
Firewall lọc gói cho pháp các thao tác truyền dữ liệu trên các điều khiển sau:
- Giao diện vật lý mà gói tin đã đến từ đó.
- Địa chỉ IP nguồn của gói tin.
- Địa chỉ IP đích của gói tin.
- Kiểu tầng vận chuyển: TCP, UDP, ICMP.
- Cổng nguồn & cổng đích tầng vận chuyển.
...
Việc kiểm tra gói tin trên mạng một cách đầy đủ gắn với thuật toán thông thường sau:
- Nếu không tìm thấy một quy tắc nào thích hợp thì bỏ gói tin đó.
- Nếu tìm thấy một quy tắc thích hợp, cho phép truyền thông tin ngang hàng.
- Nếu tìm thấy một quy tắc từ chối thông tin thì bỏ gói tin đó.

Firewall lọc gói không kiểm tra dữ liệu tầng ứng dụng của gói tin và không theo dõi trạng thái kết nối nên giải pháp này kém an toàn nhất trong các công nghệ Firewall. Tuy nhiên, vì nó xử lý ít hơn so với các kĩ thuật Firewall khác nên nó là công nghệ nhanh nhất hiện có và thường được thực hiện trong các giải pháp phần cứng như bộ định tuyến IP.
Các Firewall lọc gói thường thay địa chỉ cho các gói tin để luồng thông tin đi ra có địa chỉ nguồn khác với địa chỉ của máy trạm nội bộ, che giấu cách đánh địa chỉ của mạng cần bảo vệ.

Firewall lọc gói có các ưu điểm sau:
- Cài đặt và vận hành đơn giản.
- Nhanh hơn các kỹ thuật firewall khác và có thể dễ dàng thực hiện như các giải pháp phần cứng.
- Các bộ lọc gói không yêu cầu các máy tính sử dụng dịch vụ phải được cấu hình một cách đặc biệt; chúng làm tất cả các công việc này.
- Khi kết hợp với chuyển dịch địa chỉ, có thể dùng các Firewall lọc gói để che giấu các địa chỉ IP nội bộ.

Nhược điểm của Firewall lọc gói:
- Là điểm yếu cho các cuộc tấn công được chỉ định ở các giao thức cao hơn giao thức lớp mạng - giao thức duy nhất nó hiểu được.
- Không hiểu các giao thức ở tầng ứng dụng nên không hạn chế truy cập đối với giao thức lớp con cho đến cả các dịch vụ cơ bản nhất; nên kém an toàn hơn các Firewall mức kết nối và ứng dụng.
- Không thể cất giấu topo mạng riêng và phơi bày mạng riêng cho thế giới bên ngoài.
- Các bộ lọc gói không quản lý được thông tin về trạng thái và không giữ được thông tin về phiên làm việc hoặc thông tin nhận được từ ứng dụng. 
- Các bộ lọc gói bị hạn chế về khả năng xử lý thông tin trong gói tin. Do đó, nó có thể cho phép một số dịch vụ có điểm yếu bảo mật đi qua, thông qua lỗ hổng thì virus có thể làm tê liệt hệ thống.
- Các bộ lọc gói không hạn chế thông tin nào được truyền từ các máy tính nội bộ thông qua các dịch vụ máy chủ trên máy chủ Firewall. Các bộ lọc gói chỉ hạn chế thông tin nào có thể đi tới nó, vì vậy kẻ xâm nhập có thể truy cập tới dịch vụ trên máy chủ firewall.
- Kỹ thuật lọc gói có rất ít hoặc không có khả năng thống kê sự kiện và cơ chế báo động.
- Gặp khó khăn trong việc kiểm tra quy tắc chấp nhận & từ chối vì sự phức tạp trong việc hỗ trợ các dịch vụ mạng.

2. Circuit Level Firewall (Firewall mức kết nối):
Đây là thế hệ thứ 2, xác nhận tính hợp lệ của một gói tin là yêu cầu kết nối hoặc gói tin dữ liệu thuộc về một kết nối (hoặc kết nối ảo) giữa 2 tầng giao vận tương đương.
Để phê chuẩn một phiên làm việc, Firewall mức kết nối kiểm tra thiết lập kết nối để đảm bảo rằng kết nối này tạo ra một thủ tục bắt tay hợp lệ cho giao thức tầng giao vận đang được sử dụng (điển hình như TCP). Các gói tin dữ liệu sẽ không được gửi cho đến khi thủ tục bắt tay được hoàn thành. 
Mỗi lần một kết nối kết thúc thì mục chứa thông tin về kết nối này trong bảng kết nối ảo sẽ bị xóa và kết nối ảo giữa hai tầng giao vận tương đương cũng bị đóng. Khi một kết nối được thiết lập, Firewall mức kết nối thường lưu giữ các thông tin về kết nối sau:

- Nhận dạng phiên làm việc duy nhất đối với kết nối này, được sử dụng cho các mục đích theo dõi, giám sát.
- Trạng thái của kết nối: đang bắt tay, đã thiết lập hay kết thúc.
- Thông tin thứ tự của các gói tin.
- Địa chỉ IP nguồn (địa chỉ gói dữ liệu được gửi đi).
- Địa chỉ IP đích (địa chỉ đến của gói dữ liệu).
- Giao diện vật lý mà gói dữ liệu đến từ đó.
- Giao diện vật lý mà gói dữ liệu sẽ đi qua nó để đi ra.

Sử dụng thông tin này, Firewall mức kết nối kiểm tra thông tin trong phần header của mỗi gói tin để xác định xem liệu máy tính có được phép gửi dữ liệu tới máy tính nhận hay không và máy tính có quyền nhận hay không.
....
Các Firewall mức kết nối có những ưu điểm sau:
- Nhanh hơn các Firewall mức ứng dụng vì chúng thực hiện việc đánh giá gói tin ít hơn.
- Có thể bảo vệ toàn bộ mạng bằng cách ngăn các kết nối giữa địa chỉ nguồn cụ thể từ mạng Internet với các kết nối giữa địa chỉ nguồn cụ thể từ mạng Internet với các máy tính ở mạng trong.
- Bằng việc kết hợp với dịch chuyển địa chỉ, ta có thể sử dụng Firewall mức kết nối để che địa chỉ IP của mạng trong đối với người dùng mạng ngoài.

Nhược điểm của Firewall mức kết nối:
- Firewall mức kết nối không hạn chế theo các nhóm con của TCP.
- Firewall mức kết nối không thể thực hiện được kiểm tra an ninh một cách chặt chẽ đối với giao thức lớp cao hơn khi có yêu cầu.
- Do chỉ xây dựng được một số kiểu nhất định của trạng thái phiên làm việc, các Firewall mức kết nối chỉ có thể thống kê gói dữ liệu theo thuộc tính đã có từ trước của giao thức tầng ứng dụng mà không thể thống kê theo các thuộc tính bổ sung thêm về sau.
- Các Firewall mức kết nối không đưa thêm các tính năng đánh giá, bổ sung như: lưu giữ tạm thời đối tượng HTTP, lọc theo URL và tính năng xác thực. Vì chúng không hiểu các giao thức đang được sử dụng và không phân biệt các giao thức này.
- Khó có thể kiểm tra quy tắc chấp nhận - từ chối.

3. Application layer Firewall (Firewall mức ứng dụng):
Là công nghệ thế hệ thứ 3, cung cấp điều khiển tại lớp ứng dụng nên hoạt động giống như mức ứng dụng.
Với khả năng kiểm tra chi tiết sự lưu thông, độ an toàn của Firewall múc ứng dụng cao hơn so với Firewall lọc gói tin nhưng đồng thời cũng làm cho Firewall này chậm hơn. Nó kiểm tra tính hợp lệ của các gói dữ liệu tại tầng ứng dụng trước khi cho phép thực hiện một kết nối. Nó kiểm tra tất cả các gói tin tại tầng ứng dụng và duy trì thông tin về trạng thái kết nối đầy đủ và thông tin về thứ tự.
Ngoài ra, một Firewall mức ứng dụng còn có thể phê chuẩn các mục bảo vệ an ninh khác mà nó chỉ xuất hiện trong tầng ứng dụng.
...
Giống như các Firewall mức kết nối, các Firewall mức ứng dụng có thể thực hiện các kiểm tra bổ sung để đảm bảo rằng các gói tin không bị giả mạo và chúng thường thực hiện chuyển dịch địa chỉ mạng.

Các dịch vụ ủy quyền có một số ưu điểm sau:
- Dễ cấu hình hơn các Firewall lọc gói tin.
- Có thể giấu topo mạng riêng.
- Các dịch vụ ủy quyền có thể áp đặt điều khiển được đối với các giao thức lớp cao, chẳng hạn HTTP và FTP.
- Các dịch vụ ủy quyền lưu giữ các thông tin về các cuộc liên lạc thông qua server Firewall. Chúng có thể cung cấp một phần trung tâm trạng thái hoặc toàn bộ thông tin trạng thái nhận được từ các cuộc liên lạc, và một phần thông tin về phiên làm việc.
- Các dịch vụ ủy quyền có thể được sử dụng để từ chối truy cập đối với các dịch vụ nào đó, trong khi cho phép truy nhập tới các dịch vụ khác.
- Các gói dịch vụ ủy quyền có khả năng xử lý và thao tác dữ liệu gói.
- Các dịch vụ ủy quyền che giấu địa chỉ IP mạng trong đối với mạng ngoài, không cho phép liên lạc trực tiếp giữa các server bên ngoài và máy tính nội bộ.
- Có thể dẫn đường cho các dịch vụ nội bộ, cũng như các yêu cầu từ mạng ngoài đến mạng trong, hoặc tới một nơi nào đó.
- Các dịch vụ ủy quyền có thể cung cấp các tính năng bổ sung: lưu giữ tạm thời đối tượng HTTP, lọc URL, xác thực người dùng.
- Cho phép người quản trị giám sát sự cố thẻ vi phạm các chính sách bảo vệ an ninh.

Nhược điểm:
- Các dịch vụ ủy quyền yêu cầu thay đổi ngăn xếp mạng vốn có của server Firewall.
- Vì các proxy server chờ nhận trên cổng cùng với các server cung cấp dịch vụ đó nên không thể chạy các server này trên Firewall.
- Các dịch vụ ủy quyền có một độ trễ khi thực hiện. Dữ liệu phản hồi bị xử lý hai lần, bởi ứng dụng và proxy của nó.
- Các Firewall mức ứng dụng không thể cung cấp các proxy những giao thức UDP, RPC và những dịch vụ khác sử dụng giao thức này.
- Các dịch vụ ủy quyền thông thường yêu cầu một số thay đổi đối với các client hoặc các thủ tục của client, vì vậy cần phải có thêm những xử lý cấu hình.
- Các Firewall mức ứng dụng không chú ý tới thông tin chứa trong các lớp thấp hơn các gói. Nếu ngăn xếp mạng không thực hiện chính xác thì một số thông tin được sử dụng để thực hiện các phép kiểm tra an ninh mà các Firewall mức ứng dụng yêu cầu bằng cách sử dụng các lời gọi chuẩn từ các thư viện hệ điều hành có thể trả về thông tin không chính xác.
- Các Proxy server có thể yêu cầu thêm mật khẩu hoặc các thủ tục xác nhận tính hợp lệ khác làm tăng độ trễ của dịch vụ.

4. Dynamic packet filter Firewall (firewall lọc gói động):
Là công nghệ thứ tư, cho phép sửa đổi các chính sách đảm bảo an ninh dựa trên tình huống. Loại công nghệ này có ích trong việc cung cấp sự hỗ trợ nào đó đối với giao thức tầng giao vận UDP. 
Các Firewall này thực hiện chức năng liên kết tất cả các gói UDP đi qua vành đai bảo vệ an ning bằng một kết nối ảo đã được thay đổi và gói tin này được đi qua server Firewall. Thông tin kết hợp với kết nối ảo được lưu giữ trong một khoảng thời gian ngắn, và nếu không nhận được gói tin đáp ứng nào trong khoảng thời gian này, kết nối ảo là không hợp lệ.

Các Firewall lọc gói động có những ưu nhược điểm giống như các Firewall thế hệ thứ nhất trừ một điểm:
- Nó không cho phép tự động gửi các gói tin UDP vào mạng nội bộ.
Chỉ khi các gói tin UDP yêu cầu xuất phát từ mạng nội bộ gửi ra mạng ngoài, server Firewall mới cho phép các gói tin đáp ứng yêu cầu đó đi qua để đến máy trạm đã gửi các yêu cầu. Gói tin đáp ứng được phép đi qua phải có địa chỉ đích phù hợp với địa chỉ nguồn của máy. Cổng đích tầng giao vận phải phù hợp với cổng nguồn và phải cùng kiểu giao thức tầng giao vận.
Tính năng này cho phép các giao thức tầng ứng dụng hoạt động ngang qua vành đai bảo vệ an ninh. Một server DNS nội bộ phải đưa ra các yêu cầu cho các server DNS chạy trên mạng ngoài để lấy thông tin địa chỉ của các trạm mà nó không biết. Các server DNS phải tạo ra các yêu cầu này bằng cách sử dụng một kết nối TCP hoặc một kết nối ảo UDP.

---------------------------------------------------

## II-Router: 
>Router là thiết bị mạng hoạt động ở tầng 3 của mô hình OSI-tầng network. Router được chế tạo với 2 mục đích chính:
- Phân cách các mạng máy tính thành các segment riêng biệt để giảm hiện tượng đụng độ, giảm broadcast hay thực hiện chức năng bảo mật.
- Kết nối các mạng máy tính hay kết nối các user với mạng máy tính ở các khoảng cách xa với nhau thông qua các đường truyền thông như điện thoại.

Do hoạt động ở tầng thứ 3 của mô hình OSI, router sẽ hiểu được các protocol quyết định phương thức truyền dữ liệu. Các địa chỉ mà router hiểu là các địa chỉ giả được quy định bởi các protocol. Tùy theo cấu hình, router quyết định phương thức và đích đến của việc chuyển các packet từ nơi này sang nơi khác, theo các bước sau:
- Đọc packet.
- Gỡ bỏ dạng format quy định bởi protocol của nơi gửi.
- Thay thế phần gỡ bỏ đó bằng dạng format của protocol của đích đến.
- Cập nhật thông tin về việc chuyển dữ liệu: địa chỉ, trạng thái của nơi gửi, nơi nhận.
- Gửi packet đến nơi nhận qua đường truyền tối ưu nhất.

**Nguyên tắc hoạt động của Router-ARP Protocol**  
Như ta đã biết tại tầng network của mô hình OSI, chúng ta thường sử dụng các loại địa chỉ mang tính quy ước như IP, IPX,...Các địa chỉ này là các địa chỉ có hướng, nghĩa là chúng được phân thành hai phần riêng biệt là phần địa chỉ network và phần địa chỉ host.
Cách đánh số địa chỉ như vậy nhằm giúp cho việc tìm ra các đường kết nối từ hệ thống mạng này sang hệ thống mạng khác được dễ dàng hơn, có thể thay đổi theo tùy ý người sử dụng. Trên thực tế, các card mạng chỉ có thể kết nối với nhau theo địa chỉ MAC, địa chỉ cố định và duy nhất của phần cứng. Do vậy ta phải có một phương pháp để chuyển đổi các dạng địa chỉ này qua lại với nhau. Từ đó ta có giao thức phân giải địa chỉ: Address Resolution Protocol (ARP).

> ARP là một protocol dựa trên nguyên tắc: Khi một thiết bị mạng muốn biết địa chỉ MAC của một thiết bị mạng nào đó mà nó đã biết địa chỉ ở tầng network (IP, IPX…); nó sẽ gửi một ARP request bao gồm địa chỉ MAC address của nó và địa chỉ IP của thiết bị mà nó cần biết MAC address trên toàn bộ một miền broadcast. 
Mỗi một thiết bị nhận được request này sẽ so sánh địa chỉ IP trong request với địa chỉ tầng network của mình. Nếu trùng địa chỉ thì thiết bị đó phải gửi ngược lại cho thiết bị gửi ARP request một packet (trong đó có chứa địa chỉ MAC của mình).

Trong một hệ thống mạng đơn giản, ví dụ như máy A muốn gửi packet đến máy B và nó chỉ biết được địa chỉ IP của máy B. Khi đó máy A sẽ phải gửi một ARP broadcast cho toàn mạng để hỏi xem “địa chỉ MAC của máy có địa chỉ IP này là gì” Khi máy B nhận được broadcast này, có sẽ so sánh địa chỉ IP trong packet này với địa chỉ IP của nó. Nhận thấy địa chỉ đó là địa chỉ của mình, máy B sẽ gửi lại một packet cho máy B trong đó có chứa địa chỉ MAC của B. Sau đó máy A mới bắt đầu truyền packet cho B

https://imgur.com/a/hTDST

Trong một môi trường phức tạp hơn: hai hệ thống mạng gắn với nhau thông qua một router C. Máy A thuộc mạng A muốn gửi packet đến máy B thuộc mạng B. Do các broadcast không thể truyền qua router nên khi đó máy A sẽ xem router C như một cầu nối để truyền dữ liệu. 
Trước đó, máy A sẽ biết được địa chỉ IP của router C (port X) và biết được rằng để truyền packet tới B phải đi qua C. Tất cả các thông tin như vậy sẽ
được chứa trong một bảng gọi là bảng routing (routing table). Bảng routing table theo cơ chế này được lưu giữ trong mỗi máy. Routing table chứa thông tin về các gateway để truy cập vào một hệ thống mạng nào đó. Ví dụ trong trường hợp trên trong bảng sẽ chỉ ra rằng để đi tới LAN B phải qua port X của router C. Routing table sẽ có chứa địa chỉ IP của port X. Quá trình truyền dữ liệu theo từng bước sau:
- Máy A gửi một ARP request (broadcast) để tìm địa chỉ MAC của port X.
- Router C trả lời, cung cấp cho máy A địa chỉ MAC của port X.
- Máy A truyền packet đến port X của router.
- Router nhận được packet từ máy A, chuyển packet ra port Y của router. Trong packet có chứa địa chỉ IP của máy B.
- Router sẽ gửi ARP request để tìm địa chỉ MAC của máy B.
- Máy B sẽ trả lời cho router biết địa chỉ MAC của mình.
- Sau khi nhận được địa chỉ MAC của máy B, router C gửi packet của A đến B.
https://imgur.com/a/kY0eV

**Các thuật toán định tuyến**

Phân loại: Thuật toán định tuyến có thể thuộc một hay nhiều loại sau đây.
* Static hoặc Dynamic (Tĩnh hoặc Động)

 *Định tuyến tĩnh* là cơ chế trong đó người quản trị quyết định, gán sẵn protocol cũng như địa chỉ đích cho router, đến mạng nào thì phải truyền cho port nào, địa chỉ gì,... Các thông tin này được chứa trong routing table và chỉ được cập nhật hay thay đổi bởi người quản trị. Đĩnh tuyến tĩnh thích hợp cho các hệ thống đơn giản, có kết nối đơn giữa hai router, trong đó đường truyền dữ liệu đã được xác định trước.

 *Định tuyến động* dùng để tự động cập nhật các thông tin về các router xung quanh. Tùy theo dạng thuật toán mà cơ chế cập nhật thông tin của các router sẽ khác nhau. Định tuyến động thường dùng trong các hệ thống phức tạp hơn, trong đó các router được liên kết với nhau thành một mạng lưới, VD như các hệ thống router cung cấp dịch vụ Internet, hệ thống của các công ty đa quốc gia.

* SinglePath hoặc MultiPath

Thuật toán MultiPath cho phép tổng hợp dữ liệu trên nhiều liên kết khác nhau, còn thuật toán SinglePath thì không. MultiPath cung cấp một lưu lượng dữ liệu và độ tin cậy cao hơn SinglePath.

* Flat hoặc Hierachical

Thuật toán Flat dùng trong các hệ thống cấu trúc ngang hàng với nhau, được trải rộng với chức năng và nhiệm vụ như nhau. Trong khi đó thuật toán Hierachical là thuật toán phân cấp của một domain hay của một công ty. Tùy theo dạng hệ thống mà ta có thể lựa chọn thuật toán thích hợp.

* Link State hoặc Distance Vector

Thuật toán Link State (còn được gọi là thuật toán Shortest Path First) cập nhật tất cả các thông tin về cơ chế routing cho tất cả các node trên hệ thống mạng. Mỗi router sẽ gửi một phần của routing table, trong đó mô tả trạng thái của các liên kết riêng của mình lên trên mạng. Chỉ có các thay đổi mới được gửi đi.

Thuật toán Distance Vector (còn gọi là Bellman-Ford) bắt buộc mỗi router phải gửi toàn bộ hay một phần routing table của mình cho router kết nối trực tiếp với nó theo một chu kỳ nhất định.

------------------------------------------------------------------------------------------------------------

## III-Switch:

Switch (thiết bị chuyển mạch), là một thiết bị dùng để kết nối các đoạn mạng với nhau theo mô hình mạng hình sao. Trong đó, nó đóng vai trò là thiết bị trung tâm để các máy tính cùng nối về. Switch hoạt động ở tầng liên kết dữ liệu trong mô hình OSI, một số loại cao cấp hơn hoạt động ở tầng mạng.

Switch làm việc như một Bridge nhiều cổng, nhận tín hiệu vật lý, chuyển đổi thành dữ liệu, từ một cổng, kiểm tra địa chỉ đích rồi gửi tới một cổng tương ứng.

**Lợi ích của Switch:**
- Các thiết bị kết nối gián tiếp đều thông qua các port của switch.
- Switch làm cho các host có thể hoạt động ở chế độ song công (có thể đọc – ghi, nghe – nói) cùng lúc.
- Không cần phải chia sẻ băng thông. Các port của switch sẽ quyết định băng thông truyền đi như thế nào.
- Giảm tỷ lệ lỗi trong frame. Frame sẽ được kiểm tra lỗi. Các gói tin tốt khi được nhận sẽ được lưu lại trước khi chuyển đi (công nghệ store-and-forward).
- Có thể giới hạn lưu lượng truyền đi ở một mức ngưỡng nào đó.

**Chức năng của Switch**
- Switch quyết định chuyển frame dựa trên địa chỉ MAC, do đó nó được xếp vào thiết bị Lớp 2. Chính nhờ Switch có khả năng lựa chọn đường dẫn để quyết định chuyển frame nên mạng LAN có thể hoạt động hiệu quả hơn.
- Switch nhận biết máy nào kết nối với cổng của nó bằng cách học địa chỉ MAC nguồn trong frame mà nó nhận được. Khi hai máy thực hiện liên lạc với nhau.
- Switch chỉ thiết lập một mạch ảo giữa hai cổng tương ứng mà không làm ảnh hưởng đến lưu thông trên các cổng khác. Do đó, mạng LAN có hiệu suất hoạt động cao thường sử dụng chuyển mạch toàn bộ.
- Switch tập trung các kết nối và quyết định chọn đường dẫn để truyền dữ liệu hiệu quả. Frame được chuyển mạch từ cổng nhận vào đến cổng phát ra. Mỗi cổng là một kết nối cung cấp chọn băng thông cho host.
- Trong Ethernet Hub, tất cả các cổng kết nối vào một mạng chính, hay nói cách khác, tất cả các thiết bị kết nối Hub sẽ cùng chia sẻ băng thông mạng. Nếu có hai máy trạm được thiết lập phiên kết nối thì chúng sẽ sử dụng một lượng băng thông đáng kể và hoạt động của các thiết bị còn lại kết nối vào Hub sẽ bị giảm xuống. Để giải quyết tình trạng trên, Switch xử lý mỗi cổng là một đoạn mạng (segment) riêng biệt. Khi các máy ở các cổng khác nhau cần liên lạc với nhau, Switch sẽ chuyển frame từ cổng này sang cổng kia và đảm bảo cung cấp chọn băng thông cho mỗi phiên kết nối.


**Phân loại Switch**

* **Workgroup switch**: là loại switch được thiết kế nhằm để nối trực tiếp các máy tính lại với nhau hình thành một mạng ngang hàng. Như vậy, tương ứng với một cổng của switch chỉ có một địa chỉ máy tính trong bảng dịa chỉ. Giá thành thấp hơn các loại khác. Vì thế, loại này không cần thiết phải có bộ nhớ lớn cũng như tốc độ xử lý cao. 
* **Segment switch**: nối các Hub hay workgroup switch lại với nhau, hình thành một liên mạng ở tầng hai. Tương ứng với mỗi cổng trong trường hợp này sẽ có nhiều địa chỉ máy tính, vì thế bộ nhớ cần thiết phải đủ lớn. Tốc độ xử lý đòi hỏi phải cao vì lượng thông tin càn xử lý tại switch là lớn.
* **Backbone switch**: kết nối các segment switch lại với nhau. Bộ nhớ và tốc độ xử lý của switch phải rất lớn để đủ chứa địa chỉ cho tất cả các máy tính trong toàn liên mạng và hoán chuyện kịp thời dữ liệu giữa các nhánh mạng.

---------------------------------------------------------------------------
## IV-VPN:
![](https://f9official.com/wp-content/uploads/2017/10/VPN-Featured-Image.png)

VPN (Virtual Private Network) là phương pháp làm cho
một mạng công cộng (ví dụ như Internet) hoạt động giống như mạng nội bộ, có cùng các đặc tính như bảo mật và ưu tiên.

VPN cho phép thành lập các kết nối riêng với những người dùng ở xa, các văn phòng chi nhánh và đối tác đang sử dụng một mạng công cộng. Mạng WAN truyền thống yêu cầu công ty phải trả chi phí và duy trì nhiều loại đường dây riêng, song song với đầu tư thiết bị và đội ngũ cán bộ. Rào cản về chi phí cũng là nguyên nhân làm cho doanh nghiệp tuy muốn hưởng lợi ích của việc mở rộng mạng nhưng nhiều lúc lại không thể thực hiện nổi. Trong khi đó, VPN lại không bị rào cản này vì được thực hiện qua mạng công cộng.

VPN dùng việc mã hoá dữ liệu để ngăn ngừa các người dùng không được phép truy cập đến dữ liệu và bảo đảm dữ liệu không bị sửa đổi. Định hướng đường hầm (tunneling) là một cơ chế dùng cho việc đóng gói một giao thức vào trong một giao thức khác. Trong ngữ cảnh Internet, tunneling cho phép những giao thức như IPX, Apple Talk và IP được mã hoá. Trong ngữ cảnh VPN, tunneling che giấu giao thức lớp mạng nguyên thuỷ bằng cách mã hoá gói dữ liệu bằng cách mã hoá gói dữ liệu và chứa gói đã mã hoá và trong một vỏ bọc IP. 

VPN còn cung cấp các thoả thuận về chất lượng dịch vụ (QoS). 

Ta có thể định nghĩa VPN qua công thức:

**VPN = Tunneling + Bảo mật + Các thoả thuận về QoS**

Hiểu trên cơ bản, VPN như là một đường hầm mà dữ liệu được mã hóa của bạn đi qua, giúp bạn an toàn hơn và ẩn danh khi trực tuyến.



**Các mô hình kết nối VPN thông dụng**
Mục tiêu của công nghệ VPN là quan tâm đến ba yêu cầu cơ bản sau:

* Các nhân viên liên lạc từ xa, người dùng di động, người dùng từ xa của
một công ty có thể truy cập vào tài nguyên mạng của công ty họ bất cứ lúc
nào.
* Có khả năng kết nối từ xa giữa các nhánh văn phòng.
* Kiểm soát được truy cập của các khách hàng, nhà cung cấp là đối tác quan trọng đối với giao dịch thương mại của công ty.

Với các yêu cầu cơ bản như trên, ngày nay, VPN được phát triển và phân thành ba loại như sau: 

* VPN Truy cập từ xa (Remote Access VPN): cung cấp kết nối cho người dùng làm việc từ xa và di động. Nó là một sự thay thế cho các kết nối dial chuyên dụng hoặc ISDN. 
* VPN Cục bộ (Intranet VPN): kết nối trụ sở công ty, văn phòng từ xa và văn phòng chi nhánh qua một cơ sở hạ tầng chia sẻ sử dụng các kết nối chuyên dụng. 
* VPN Mở rộng (Extranet VPN): kết nối khách hàng, nhà cung cấp, đối tác, hoặc cộng đồng người sử dụng thông qua một cơ sở hạ tầng chia sẻ sử dụng kết nối chuyên dụng. 


**Các giao thức sử dụng trong VPN**
* **Point-to-Point Tunneling Protocol (PPTP)**

PPTP là sự mở rộng của giao thức Internet chuẩn Point-to-Point (PPP) và sử dụng cùng kiểu xác thực như PPP (PAP, SPAP, CHAP, MS-CHAP, EAP). Là phương pháp VPN được hỗ trợ rộng rãi nhất giữa các máy trạm chạy Windows. 

PPTP thiết lập đường hầm (tunnel) nhưng không mã hóa. Ưu điểm khi sử dụng PPTP là nó không yêu cầu hạ tầng mã khóa công cộng (Public Key Infrastructure).

* **Internet Protocol Security (IPSec)**

IPsec được tích hợp trong rất nhiều giải pháp VPN "tiêu chuẩn", đặc biệt trong các giải pháp VPN gateway-to-gateway (site-to-site) để nối 2 mạng LAN với nhau. IPsec hoạt động tại tầng Mạng (tầng 3) trong mô hình OSI.

IPSec trong chế độ đường hầm bảo mật các gói tin trao đổi giữa hai gateway hoặc giữa máy tính trạm và gateway. Như tên của nó, IPsec chỉ hoạt động với các mạng và ứng dụng dựa trên nền tảng IP (IP-based network). Giống như PPTP và L2TP, IPsec yêu cầu các máy tính trạm VPN phải được cài đặt sẵn phần mềm VPN client.

Việc xác thực được thực hiện thông qua giao thức Internet Key Exchange (IKE) hoặc với chứng chỉ số (digital certificates) đây là phương thức bảo mật hơn hoặc thông qua khóa mã chia sẻ (preshared key). IPSec VPN có thể bảo vệ chống lại hầu hết các phương pháp tấn công thông dụng bao gồm Denial of Service (DoS - tấn công từ chối dịch vụ), replay, và "man-in-the-middle".

* **Layer2 Tunneling Protocol (L2TP)**

Giao thức Layer 2 Tunneling Protocol (L2TP) là sự kết hợp các đặc điểm của cả PPTP và giao thức Layer 2 Forwarding (L2F).

Giống như PPTP, L2TP hoạt động tại tầng Liên kết dữ liệu (data link layer) của mô hình mạng OSI.

L2TP yêu cầu sử dụng chứng chỉ số (digital certificates). Xác thực người dùng có thể được thực hiện thông qua cùng cơ chế xác thực PPP tương tự như PPTP. L2TP có một vài ưu điểm so với PPTP. PPTP cho người dùng khả năng bảo mật dữ liệu, nhưng L2TP còn tiến xa hơn khi cung cấp thêm khả năng đảm bảo tính toàn vẹn dữ liệu, khả năng xác thực nguồn gốc (xác định người dùng đã gửi dữ liệu có thực sự đúng người), và khả năng bảo vệ chống gửi lại – replay protection (chống lại việc hacker chặn dữ liệu đã được gửi, ví dụ thông tin quyền đăng nhập (credentials), rồi sau đó gửi lại (replay) chính thông tin đó để bẫy máy chủ. 

Mặt khác, do liên quan đến cung cấp các khả năng bảo mật mở rộng làm cho L2TP chạy chậm hơn chút ít so với PPTP.

* **Secure Socket Layer (SSL)**

SSL còn được gọi là giải pháp "clientless". Điều này cũng có nghĩa là các giao thức có thể được xử lý bởi SSL sẽ bị hạn chế nhiều hơn. Dù sao, điều này cũng đem lại một lợi thế về bảo mật. 

Với SSL, thay vì cho phép VPN client truy xuất vào toàn bộ mạng hoặc một mạng con (subnet) như với IPsec, có thể hạn chế chỉ cho phép truy xuất tới một số ứng dụng cụ thể. Nếu một ứng dụng mà người dùng muốn họ truy cập không phải là là loại ứng dụng dựa trên trình duyệt (browser-based), thì cần phải tạo ra một plug-ins Java hoặc Active-X để làm cho ứng dụng đó có thể truy xuất được qua trình duyệt.

SSL hoạt động ở tầng Phiên – cao hơn IPsec trong mô hình OSI. Điều này cho nó khả năng điều khiển truy cập theo khối tốt hơn. SSL sử dụng chứng chỉ số (digital certificates) để xác thực server. Mặc dù các phương pháp khác cũng có thể áp dụng, nhưng sử dụng chứng chỉ số được ưa chuộng vì khả năng bảo mật cao nhất.


**Ưu điểm và nhược điểm của VPN**
Để xây dựng 1 hệ thống mạng riêng, mạng cá nhân ảo thì dùng VPN là 1 giải pháp không hề tốn kém. Môi trường Internet là cầu nối, giao tiếp chính để truyền tải dữ liệu, xét về mặt chi phí thì nó hoàn toàn hợp lý so với việc trả tiền để thiết lập 1 đường kết nối riêng với giá thành cao. Bên cạnh đó, việc phải sử dụng hệ thống phần mềm và phần cứng nhằm hỗ trợ cho quá trình xác thực tài khoản cũng không phải là rẻ. Việc so sánh sự tiện lợi mà VPN mang lại cùng với chi phí bỏ ra để bạn tự thiết lập 1 hệ thống như ý muốn, rõ ràng VPN chiếm ưu thế hơn hẳn.

Nhưng bên cạnh đó, nó có nhược điểm rất dễ nhận thấy. VPN không có khả năng quản lý Quality of Service (QoS) qua môi trường Internet, do vậy các gói dữ liệu – Data Package vẫn có nguy cơ bị thất lạc, rủi ro. Khả năng quản lý của các đơn vị cung cấp VPN là có hạn, không ai có thể ngờ trước được những gì có thể xảy ra với khách hàng của họ.

----------------------------------------------------------------------------------

## V-IDS/IPS:

IDS (Intrusion Detection System) là một hệ thống phát hiện các hành động tấn công vào một mạng. Một tính năng chính của hệ thống này là cung cấp thông tin nhận biết về những hành động không bình thường và đưa ra các báo cảnh thông báo cho quản trị viên mạng khóa các kết nối đang tấn công này. Thêm vào đó công cụ IDS cũng có thể phân biệt giữa những tấn công bên trong từ bên trong tổ chức (nhân viên hoặc khách hàng) và tấn công bên ngoài (hacker).

IPS (Intrusion Prevention Systems) là hệ thống theo dõi, ngăn ngừa kịp thời các hoạt động xâm nhập không mong muốn. Chức năng chính của IPS là xác định các hoạt động nguy hại, lưu giữ các thông tin này. Sau đó nó kết hợp với firewall để dừng ngay các hoạt động này, và cuối cùng đưa ra các báo cáo chi tiết về các hoạt động xâm nhập trái phép trên.

IDS và IPS có rất nhiều điểm chung, do đó hệ thống IDS và IPS có thể được gọi chung là IDP- Intrusion Detection and Prevention. 

Hiện nay, công nghệ của IDS đã được thay thế bằng các giải pháp IPS. 

**Chức năng cơ bản**
* Nhận diện các nguy cơ có thể xảy ra.
* Ghi nhận thông tin, log để phục vụ cho việc kiểm soát nguy cơ.
* Nhận diện các hoạt động thăm dò hệ thống.
* Nhận diện các yếu khuyết của chính sách bảo mật.
* Ngăn chặn vi phạm chính sách bảo mật.
* Lưu giữ thông tin liên quan đến các đối tượng quan sát
* Cảnh báo những sự kiện quan trọng liên quan đến đối tượng quan sát
* Ngăn chặn các tấn công (IPS)
* Xuất báo cáo.

**Phân loại IDS/IPS**
Dựa trên phạm vi giám sát, IDS được chia thành 2 loại:
* Network-based IDS (NIDS): Là những IDS giám sát trên toàn bộ mạng. Nguồn thông tin chủ yếu của NIDS là các gói dữ liệu đang lưu thông trên mạng. NIDS thường được lắp đặt tại ngõ vào của mạng, có thể đứng trước hoặc sau tường lửa. Hình 1 mô tả một NIDS điển hình.
* Host-based IDS (HIDS): Là những IDS giám sát hoạt động của từng máy tính riêng biệt. Do vậy, nguồn thông tin chủ yếu của HIDS ngòai lưu lượng dữ liệu đến và đi từ máy chủ còn có hệ thống dữ liệu nhật ký hệ thống (system log) và kiểm tra hệ thống (system audit).

Dựa trên kỹ thuật thực hiện, IDS cũng được chia thành 2 loại:
 
* Signature-based IDS: phát hiện xâm nhập dựa trên dấu hiệu của hành vi xâm nhập, thông qua phân tích lưu lượng mạng và nhật ký hệ thống. Kỹ thuật này đòi hỏi phải duy trì một cơ sở dữ liệu về các dấu hiệu xâm nhập (signature database), và cơ sở dữ liệu này phải được cập nhật thường xuyên mỗi khi có một hình thức hoặc kỹ thuật xâm nhập mới. 
* Anomaly-based IDS: phát hiện xâm nhập bằng cách so sánh (mang tính thống kê) các hành vi hiện tại với hoạt động bình thường của hệ thống để phát hiện các bất thường (anomaly) có thể là dấu hiệu của xâm nhập. Ví dụ, trong điều kiện bình thường, lưu lượng trên một giao tiếp mạng của server là vào khỏang 25% băng thông cực đại của giao tiếp. Nếu tại một thời điểm nào đó, lưu lượng này đột ngột tăng lên đến 50% hoặc hơn nữa, thì có thể giả định rằng server đang bị tấn công DoS. Để hoạt động chính xác, các IDS loại này phải thực hiện một quá trình “học”, tức là giám sát hoạt động của hệ thống trong điều kiện bình thường để ghi nhận các thông số hoạt động, đây là cơ sở để phát hiện các bất thường về sau.

**So sánh IDS và IPS**
Nếu như hiểu đơn giản, có thể xem như IDS chỉ là một cái chuông để cảnh báo cho người quản trị biết những nguy cơ có thể xảy ra tấn công. Dĩ nhiên có thể thấy rằng, nó chỉ là một giải pháp giám sát thụ động, tức là chỉ có thể cảnh báo mà thôi, việc thực hiện ngăn chặn các cuộc tấn công vào hệ thống lại hoàn toàn phụ thuộc vào người quản trị. Vì vậy yêu cầu rất cao đối với nhà quản trị trong việc xác định các lưu lượng cần và các lưu lượng có nghi vấn là dấu hiệu của một cuộc tấn công. Và dĩ nhiên công việc này thì lại hết sức khó khăn. 

Với IPS, người quản trị không nhũng có thể xác định được các lưu lượng khả nghi khi có dấu hiệu tấn công mà còn giảm thiểu được khả năng xác định sai các lưu lượng. Với IPS, các cuộc tấn công sẽ bị loại bỏ ngay khi mới có dấu hiệu và nó hoạt động tuân theo một quy luật do nhà Quản trị định sẵn.

----------------------------------------------------------------------------------------

## VI-Lệnh ping, tracert, arp

## 1. ping
Ping, viết tắt của **P**acket **I**nter**n**et **G**rouper (Groper), là một công cụ cho mạng máy tính sử dụng trên các mạng TCP/IP (chẳng hạn như Internet) để kiểm tra xem có thể kết nối tới một máy chủ cụ thể nào đó hay không và ước lượng khoảng thời gian trễ trọn vòng để gửi gói dữ liệu cũng như tỉ lệ các gói dữ liệu có thể bị mất giữa hai máy. 

Công cụ này thực hiện nhiệm vụ trên bằng cách gửi một số gói tin ICMP đến máy kia và lắng nghe trả lời.

Cú pháp: `ping <địa chỉ đích> <tham số (nếu có)>`

Các tham số của lệnh **ping**:

![](https://i.imgur.com/e0vgllh.png)

Một số thông điệp trả về khi PING:

* **Request time out**: thực hiện gửi gói thành công nhưng không nhận được gói phản hồi (Lỗi ở phía kia)
* **Destination host unreachable**: đích đến không tồn tại hoặc đang cô lập (lỗi ở phía mình)
* **Reply from 2.17.50.138: bytes=32 time=52ms TTL=58**: Gửi gói đến địa chỉ IP 2.17.50.138 với độ dài gói 32 byte, thời gian phản hồi là 52 mili giây, TTL (time to live - thời gian tồn tại của gói, chỉ số hop mà gói tin truyền thông không phải qua khi truyền từ bên gửi sang bên nhận) là 58.
* **Unknown host / Ping Request Could Not Find Host**: cho biết hostname bạn ping đến không có trên bất cứ hệ thống phân giải tên miền nào hay lý do đơn giản là bạn viết sai chính tả.

VD. `ping fox.com`

![](https://i.imgur.com/IU2rCMa.png)

## 2. tracert
Tracert là công cụ kiểm tra đường đi của gói dữ liệu, xem nó đi qua các trạm nào, mất bao lâu, trạm nào bị nghẽn, không kết nối được không? trạm đó bị nghẽn thì có con đường nào khác để đến đích hay không? Thực tế càng qua nhiều trạm thì càng chậm và càng có rủi ro bị time out (mất kết nối).

Tracert tìm đường tới đích bằng cách gửi các thông báo Echo Request (yêu cầu báo hiệu lại) Internet Control Message Protocol (ICMP) tới từng đích. Sau mỗi lần gặp một đích, giá trị Time to Live (TTL), tức thời gian cần để gửi đi sẽ được tăng lên cho tới khi gặp đúng đích cần đến.

Tracert cho phép xác định đường đi của các gói tin truyền qua mạng tới host cụ thể bạn chỉ định. Khi một gói tin đi qua một host, host sẽ giảm giá trị TTL của gói tin đi một giá trị và gửi tới host tiếp theo. Khi quá thời gian mà chưa đến đúng địa chỉ cần tìm, host nhận được gói tin sẽ loại bỏ và gửi lại thông báo thời gian quá hạn ICMP. 

Cú pháp: `tracert <tên miền>`

VD. `tracert fox.com`
![](https://i.imgur.com/KXVofz3.png)

![](http://www.mygreatname.com/how-traceroute-works/traceroute-e7.gif)

Cách đọc kết quả: `Hop RTT1 RTT2 RTT3 <name/IP address>`

* Hop: số thứ tự của hop (1 hop được tính khi gói tin đi qua 1 router)
* RTT1, RTT2, RTT3: viết tắt của *Round Trip Time* (là khoảng thời gian tính từ lúc client bắt đầu gửi request tới lúc nó nhận gói dữ liệu đầu tiên trả về, không bao gồm thời gian nhận đầy đủ dữ liệu). Có 3 RTT vì tracert gửi đi 3 goisn tin khác nhau.
* Name/IP Address: Nếu như router đó có tên miền tiên thì nó sẽ được hiển thị, thông qua tên miền của router, biết được vị trí của router ở mạng trên. Nếu router không có tên miền thì sẽ hiển thị *địa chỉ IP*.  

## 3. arp

ARP (Address Resolution Protocol) là giao thức được sử dụng để phân giải địa chỉ IP sang địa chỉ máy (MAC).

Nguyên tắc hoạt động của ARP trong mạng LAN:

* Khi một thiết bị mạng muốn biết địa chỉ MAC của một thiết bị mạng nào đó mà nó đã biết địa chỉ ở tầng Mạng, nó sẽ gửi một ARP request bao gồm địa chỉ MAC address của nó và địa chỉ IP của thiết bị mà nó cần biết MAC address trên toàn bộ một miền broadcast. 
* Mỗi một thiết bị nhận được request này sẽ so sánh địa chỉ IP trong request với địa chỉ tầng Mạng của mình. Nếu trùng địa chỉ thì thiết bị đó phải gửi ngược lại cho thiết bị gửi ARP request một gói tin (trong đó có chứa địa chỉ MAC của mình).

Cú pháp: 
`arp`: xem thông tin lệnh arp

`arp -a [inet_addr]`: hiện giá trị tại bảng ARP của giao thức ARP trong máy tính. Nếu có địa chỉ *inet_addr* thì chỉ có máy có địa chỉ tương ứng thể hiện. 

`arp -s inet_addr eth_addr`: thêm vào bảng ARP một địa chỉ IP và MAC.

`arp -d inet_addr`: xóa địa chỉ IP **inet_addr**

------------------------------------------------------------------------------------

## VII-Công cụ Netcut

NetCut là một công cụ trông có chức năng như kiểm tra tốc độ mạng, băng thông, thay đổi địa chỉ MAC, hay cắt truy cập mạng đối với bất kỳ thành viên mạng LAN nào.

Việc cắt truy cập mạng chính là chức năng hữu ích nhất dành cho người quản trị mạng LAN, vì đôi khi có những thành viên trong mạng dùng đến mức chiếm hết băng thông của người khác. Nhất là với người quản trị mạng Wi-Fi, đặc tính không dây khiến việc kiểm soát các thành viên truy cập là không dễ (ngay cả khi đặt mật khẩu).

![](https://i.imgur.com/JDW0z9c.png)

* Để xem danh sách truy cập riêng một mạng LAN cụ thể, click **Choice NetCard** và chọn card mạng mong muốn.
* Để cắt mạng truy cập của một thành viên, chọn máy tính của thành viên đó trong danh sách rồi click **Cut off**.
* Để tìm địa chỉ IP, click **Find IP** rồi nhập địa chỉ vào.
* Để xem thông tin về thiết bị đang kết nối, click **Find Type**. Lúc này, một cửa sổ của trình duyệt web sẽ hiện ra với thông tin về thiết bị.

![](https://i.imgur.com/nWDMg7g.png)

* Để thay đổi địa chỉ MAC của một thiết bị, click **Change MAC**.

* Nếu dùng NetCut bản 2.1.0 trở lên thì sẽ có lựa chọn **Protect My Computer** để chống lại lệnh cắt mạng bởi NetCut trên máy khác. Nếu chỉ đơn giản muốn không bị cắt mạng bởi NetCut thì có thể dùng công cụ chuyên biệt NetCut Defender.

![](https://i.imgur.com/T9vROsZ.png)

* Để thay đổi địa chỉ MAC, click **Change MAC**.
* Ngoài ra, ta có thể ngăn việc liên lạc giữa máy tính A với riêng máy tính B bất kỳ. Chọn máy B và bấm nút **>>** để NetCut coi máy B là cổng GateWay, sau đó chọn máy A và bấm **Cut off**. Lý do vì nguyên lý cắt mạng của NetCut là cắt liên lạc với GateWay.

![](https://i.imgur.com/eXUg1nw.png)

------------------------------------------------------------------
## IX-Proxy
### 9.1. Proxy là gì?
Proxy là một Internet server làm nhiệm vụ chuyển tiếp thông tin và kiểm soát tạo sự an toàn cho việc truy cập Internet của các máy khách, còn gọi là khách hàng sử dụng dịch vụ Internet. Trạm cài đặt proxy gọi là proxy server. Proxy hay trạm cài đặt proxy có địa chỉ IP và một cổng truy cập cố định. Ví dụ: 123.234.111.222:80. Địa chỉ IP của proxy trong ví dụ là 123.234.111.222 và cổng truy cập là 80.

### 9.2. Chức năng của Proxy

Một số hãng và công ty sử dụng proxy với mục đích: Giúp nhiều máy tính truy cập Internet thông qua một máy tính với tài khoản truy cập nhất định, máy tính này được gọi là Proxy server. Chỉ duy nhất máy Proxy này cần modem và account truy cập Internet, các máy client (các máy trực thuộc) muốn truy cập Internet qua máy này chỉ cần nối mạng LAN tới máy Proxy và truy cập địa chỉ yêu cầu. Những yêu cầu của người sử dụng sẽ qua trung gian proxy server thay thế cho server thật sự mà người sử dụng cần giao tiếp, tại điểm trung gian này công ty kiểm soát được mọi giao tiếp từ trong công ty ra ngoài Internet và từ Internet vào máy của công ty. Sử dụng Proxy, công ty có thể cấm nhân viên truy cập những địa chỉ web không cho phép, cải thiện tốc độ truy cập nhờ sự lưu trữ cục bộ các trang web trong bộ nhớ của proxy server và giấu định danh địa chỉ của mạng nội bộ gây khó khăn cho việc thâm nhập từ bên ngoài vào các máy của công ty.

Đối với các nhà cung cấp dịch vụ đường truyền Internet: Do Internet có nhiều lượng thông tin mà theo quan điểm của từng quốc gia, từng chủng tộc hay địa phương mà các nhà cung cấp dịch vụ Internet khu vực đó sẽ phối hợp sử dụng proxy với kỹ thuật tường lửa để tạo ra một bộ lọc gọi là firewall proxy nhằm ngăn chặn các thông tin độc hại hoặc trái thuần phong mỹ tục đối với quốc gia, chủng tộc hay địa phương đó. Địa chỉ các website mà khách hàng yêu cầu truy cập sẽ được lọc tại bộ lọc này, nếu địa chỉ không bị cấm thì yêu cầu của khách hàng tiếp tục được gửi đi, tới các DNS server của các nhà cung cấp dịch vụ. Firewall proxy sẽ lọc tất cả các thông tin từ Internet gửi vào máy của khách hàng và ngược lại.

