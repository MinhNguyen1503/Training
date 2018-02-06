# Cấu trúc của ICMP

----
## ICMP là gì?
see [Wikipedia](https://en.wikipedia.org/wiki/ICPM)

> ICMP (Internet Control Message Protocol) là một giao thức của bộ giao thức TCP/IP. Nó được các thiết bị mạng như router dùng để gửi đi các thông báo lỗi chỉ ra một dịch vụ có tồn tại hay không, hoặc một địa chỉ host hay router có tồn tại hay không.
----
## Gói tin ICMP gồm 2 phần:
- **Header**.
- **Data**.

### Header
![](https://i.imgur.com/pQ8xTrQ.png)

- 32 bit đầu tiên (4 byte đầu) của một gói tin ICMP là giống nhau cho mỗi loại thông điệp, nội dung các byte còn lại sẽ lệ thuộc vào trường type và trường code:

 1. **TYPE (8bit)**: là một số nguyên 8bit để xác định thông điệp.

 2. **CODE (8bit)**: cung cấp thêm thông tin về kiểu thông điệp.

 3. **CheckSum (16bit)**: ICMP sử dụng thuật checksum như IP, nhưng ICMP checksum chỉ tính đến thông điệp ICMP.

- Các thông điệp ICMP **thông báo lỗi** luôn luôn bao gồm **phần đầu và 64bit đầu tiên của packet** gây nên lỗi. 


 - Một số thông báo đáng chú ý:
 ![](https://i.imgur.com/vUPRGlc.png)  

 ### Data

 - Thông thường, data là header của gói tin IP và là 64 bit đầu tiên của nó.

----
## Các loại ICMP mesenger thường thấy
## 1. ICMP echo mesenger

Có 2 loại là echo request và echo reply messenger tương ứng với các trường:

+ Type=0 => echo request, code=0

+ Type=8 => echo reply, code=0

Ngoài ra còn có 2 trường( size là 16bit/field) là ID và sequence Number dùng để nhận biết giữa các cặp reply/ request.

## 2.  ICMP Destination Unreachable messenger

- Nếu bị Destination Unreachable, thiết bị trung gian sẽ gửi về một Destination Unreachable messenger về sender.
- Destination Unreachable có nhiều loại ứng với các nguyên nhân khác nhau và chúng sẽ có các cặp giá trị code khác nhau.

## 3. ICMP Parameter Problem messenger 
- Vấn đề xảy ra khi có một vài error trong header của datagram( ở một vài octet) và không thể chuyển nó đi tiếp được. Khi đó thiết bị trung gian gửi một ICMP Parameter Problem messenger cho sender với các trường như sau:

Type=12 
Code=0-2 
Thêm một trường poiter(8 bit) để chỉ vị trí của octet lỗi.

- **Control messenger**:

  không mang các lost packet hoặc error conditions. Control messenger báo cho host biết các điều kiện như đang có congestion hoặc có gateway phù hợp hơn cho host.

## 4.ICMP Redirect/ Change Request messenger

Là một loại control messenger, nó chỉ được gửi đi bởi một default gateway và nó báo cho host nhận biết là có best path cho mi đọc nếu có các điều kiện sau xảy ra: 

+ Tại Interface mà packet đã đi vào sau đó routed lại đi ra. 
+ Tại subnet/network của địa chỉ IP nguồn cùng subnet/network của nexthop.

+ Khi host được để mặc định là gửi ICMP Redirect messenger.

Có thể bỏ default này bằng command:” **no ip redirect**”

## 5.ICMP Timestamp request messenger
- Dùng để đồng bộ thời gian cho các ứng dụng giữa nơi chuyển và nơi nhận.
- Ngoài ra còn có 2 trường có size là 16 bit là ID và sequence Number dùng để nhận biết giữa các cặp reply/request.

## 6.ICMP Information Request and Reply Messenger

- Để xác định số network được sử dụng.
- Ngoài ra còn có 2 trường có size là 16 bit là ID và sequence Number dùng để nhận biết giữa các cặp reply/request.

## 7. ICMP Address Mask Request messenger
- Để host tìm subnetmask của mình khi không được cấu hình bằng tay.
- có 2 trường có size là 16 bit là ID và sequence Number dùng để nhận biết giữa các cặp reply/request
- 1 trường 32 bit dành cho Address Mask( với request messenger thì nó được cho về not use còn với reply messenger thì nó là Address mask correct của host)

## 8.ICMP Router Discover messenger
- ICMP Router Solicitation messenger Được dùng khi sender mất default gateway 

## 9.ICMP Source Quench messenger 
- Được dùng để báo cho sender biết có congestion và hỏi sender xem có giảm tốc độ gửi packet đi không. Nó thuộc loại Flow- Control messenger.
