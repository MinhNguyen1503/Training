# Bản báo cáo tuần 3


### Mục lục
1. [Linux](#linux-start)
- [Linux là gì?](#what-is-linux)
	- [Một số Distro của Linux](#linux-distro)
	- [Ưu nhược điểm của Linux](#linux-dis-advantages)
		- [Ưu điểm](#linux-advantages)
		- [Nhược điểm](#linux-disadvantages)
	- [User và Group trong Linux](#linux-user-group)
		- [User](#linux-user)
		- [Group](#linux-usergroup)
	- [Phân quyền trong Linux](#linux-user-role)
		- [Các quyền của user](#linux-roles)
		- [Cách xem quyền của File - Folder](#linux-view-role)
		- [Thay đổi quyền](#linux-change-role)
2. [Ubuntu](#ubuntu-start)
	- [Command line cơ bản](#ubuntu-basic-command)
		- [Command line quản lý file, folder](#ubuntu-file-folder-command)
		- [Command line di chuyển qua lại, liệt kê file, folder](#ubuntu-change-list-folder-command)
	- [Cấu hình mạng](#ubuntu-config-network)
		- [Cấu hình card mạng](#ubuntu-config-card-network)
			- [Cấu hình card mạng bằng file](#ubuntu-config-card-network-by-file)
		- [Cấu hình SSH](#ubuntu-setup-ssh)
***
## I/Linux
### <a name="linux-start"></a> 1. Linux là gì?
**Linux** là tên một *hệ điều hành* máy tính dựa trên **Unix** được phát triển và phân phối qua mô hình phần mềm tự do mã nguồn mở.

Đồng thời, **Linux** cũng là tên của một *nhân hệ điều hành*, ra đời bản đầu tiên vào tháng 8 năm 1991 bởi **Linus Torvalds**. Nhiều người gọi **Linux** là **GNU/Linux**, lý do là bản thân **Linux** chỉ là phần nhân hệ điều hành. Rất nhiều phần mềm, ứng dụng khác như hệ thống đồ họa, trình biên dịch, soạn thảo, các công cụ phát triển cũng cần được *gắn vào nhân* để tạo nên một HĐH hoàn chỉnh. Hầu hết những phần mềm này được phát triển bởi cộng đồng *GNU*.

**Unix** ban đầu được phát triển từ năm 1969 bởi một nhóm kỹ sư ở Bell Labs trực thuộc cty AT&T, gồm **Ken Thompson**, **Dennis Ritchies**, **Douglas Mcllroy** và **Joe Ossanna**. Bản phát hành lần đầu ra mắt năm 1970. Có vài phiên bản **Unix** trên thị trường như **Solaris Unix**, **AIX**, **HP Unix**, **BSD**... **Linux** cũng là một bản của **Unix** được cung cấp miễn phí. **Unix** có khả năng đa người dùng (vài người có thể dùng máy tính chạy **Unix** tại cùng một thời điểm) và đa nhiệm (chạy nhiều chương trình một lúc). Được viết bằng ngôn ngữ C nên **Unix** có thể cài đặt trên nhiều loại máy tính khác nhau, đây là *tính khả chuyển*.

#### <a name="linux-distro"></a> Một số Distro của Linux

- **Ubuntu**
- **Fedora**
- **LinuxMint**
- **OpenSUSE**
- **PCLinuxOS**
- **Debian**
- **Mandriva**

### <a name="linux-dis-advantages"></a> 2.Ưu nhược điểm của Linux

#### <a name="linux-advantages"></a> a. Ưu điểm
- **Linh hoạt:** **Linux** là mã nguồn mở nên ta có thể tùy ý chỉnh sửa các *hệ điều hành* sử dụng nhân **Linux** để phù hợp với nhu cầu cá nhân.
- **Bảo mật cao:** Hệ thống phân quyền của **Linux** cực tốt. Ngoài ra, vì **Linux** là mã nguồn mở nên khi có bất kì lỗi nào được phát hiện, nó sẽ được cả cộng đồng sửa lỗi.

#### <a name="linux-disadvantages"></a> b. Nhược điểm
- **Thiếu thân thiện với người dùng:** Do hầu hết các mọi việc trên **Linux** đều thực hiện qua dòng lệnh(Command line), nên việc người dùng phổ thông có thể sử dụng được **Linux** là một điều khó khăn.
- **Tính thống nhất:** Do **Linux** là mã nguồn mở nên ai cũng có thể chỉnh sửa và phát hành một phiên bản lên *Internet*. Điều này khiến người dùng phải mất một thời gian tìm hiểu để lựa chọn một phiên bản phù hợp với nhu cầu, nhất là với người dùng không có nhiều kiến thức - kinh nghiệm.
- **Phần cứng:** Có nhiều nhà sản xuất phần cứng không hỗ trợ driver chạy trên **Linux**. Do đó, sẽ có những thiết bị - phần cứng không thể chạy trên **Linux**.

### <a name="linux-user-group-start"></a> 3. User và Group trong Linux
#### <a name="linux-user"></a> a. User
User là người có thể truy cập đến hệ thống.
User có **username** và **password**.
Có hai loại user: **super user** và **regular user**.
Mỗi user còn có một định danh riêng gọi là **UID**.

**Để tạo User, ta dùng lệnh:** ```useradd [option] <username>```
- **Option:**
	- -c "Thông tin user"
	- -d <Thư mục cá nhân>
	- -m : Tạo thư mục cá nhân nếu chưa tồn tại
	- -g <nhóm của user>

**Ví dụ:** ```useradd –c "Nguyen Van A" –g serveradmin vana```

**Để thay đổi thông tin User, ta dùng lệnh:** ```usermod [option] <username>```

Các *Option* tương dự với **useradd**.
**Ví dụ:** ```usermod –g kinhdoanh vana```
Chuyển vana từ nhóm server admin sang nhóm kinh doanh.

**Để xóa một User, ta dùng lệnh:** ```userdel [option] <username>```
**Ví dụ:** ```userdel  –r  vana```

**Khóa/Mở khóa một User:**
```
passwd –l <username>  /  passwd –u <username>
usermod –L <username> /  usermod –U <username>
```

#### <a name="linux-usergroup"></a> b. Group
Group là **tập hợp nhiều user** lại.
Mỗi user luôn là **thành viên** của một group.
Khi tạo một user thì mặc định một group được tạo ra.
Mỗi group còn có một *định danh* riêng gọi là **GID**.

**Lệnh tạo group:** ```groupadd <groupname>```
**Ví dụ:** ```groupadd serveradmin```

**Lệnh xóa group:** ```groupdel <groupname>```
**Ví dụ:** ```groupdel serveradmin```


### <a name="linux-user-role"></a> 4. Phân quyền trong Linux
#### <a name="linux-roles"></a> a. Các quyền của user
- **Read(r : 4):**
	- **Files:** quyền được *xem* nội dung của *file*.
	- **Folders:** quyền được *xem* danh sách các 	*subfolder* và file bên trong *folder* đó.
- **Write(w : 2):**
	- **Files:** quyền *thêm*, *sửa* nội dung file.
	- **Folders:** quyền *thêm*, *xóa* một *subfolder* hay *file* trong *folder* đó.
- **Excute(x : 1):**
	- **Files:** cho phép thực thi *file*, nếu là *file* **program** hay **script**.
	- **Folders:** cho phép **cd** vào *folder* này.
- **Deny(- : 0):** **Không** có quyền làm một **thao tác** gì đó đối với một **file** hay **folder** xác định.

#### <a name="linux-view-role"></a> b. Xem phân quyền của file, folder
Sử dụng lệnh ```ls -la``` để liệt kê danh sách *file* và *subfolder* trong **folder** hiện hành.

![](https://viblo.asia/uploads/9958476f-bc2d-41e0-9ddf-204c8bfc50ed.png)
<br/>

##### Cách xem:
- Cột đầu gồm 10 ký tự:
	- Ký tự đầu cho biết kiểu file: **d** là *folder*, **-** là *file*.
	- 9 ký tự sau chia làm **3 phần**, mỗi phần 3 ký tự:
		- **Phần 1:** Cho biết quyền của **user** sở hữu (**Owner**).
		- **Phần 2:** Cho biết quyền của **group** sở hữu (**Owner group**).
		- **Phần 3:** Cho biết quyền của các **user** khác.
- Cột hai gồm 1 số:
	- **Folder:** Cho biết số lượng *subfolder* + *parentfolder* + chính nó.
	- **File:**  Cho biết số đường dẫn cố định đến nó.
- Cột 3: Cho biết **Owner** - người sở hữu.
- Cột 4: Cho biết **Owner group** - nhóm sở hữu.
- Cột 5: Cho biết dung lượng *file*(*folder*).
- Cột 6: Thời gian tạo.
- Cột 7: Tên *file*(*folder*).

#### <a name="linux-change-role"></a> c. Thay đổi quyền.
Chỉ *User* có quyền **root** hoặc **Owner User** mới có thể thay đổi quyền có *file*, *folder* đó.

Để thay đổi quyền của *file* hay *folder*, ta dùng lệnh:<br/> ```chmod [mode] file_name```

**Mode** có thể viết theo hai cách:
>**Symbolic:** ```chmode [group][operator][permission] file_name```

Với cách này, ta có thể phân quyền riêng biệt theo từng nhóm quyền, dễ hiểu hơn cho những người mới.

**Grouop:**

| Group Permision | Symbolic| Description   	|
| :-------------- | :------ | :---------------- |
| Owner       	  | u       | Người sở hữu		|
| Group       	  | g       | Nhóm sở hữu		|
| Other       	  | o       | Người khác		|
| All         	  | a       | Tất cả			|

**Operator:**

| Operator 		| Symbolic| Description     |
| :------------ | :------ | :-------------- |
| Add       	| +       | Thêm quyền		|
| Remove       	| -       |	Loại bỏ quyền	|
| Assign       	| =       |	Chỉ định quyền	|

**Permision:**

| Permision 	| Symbolic| Description     													|
| :------------ | :------ | :------------------------------------------------------------------ |
| Read       	| r       | Quyền đọc															|
| Write       	| w       |	Quyền ghi															|
| Excute       	| x       |	Quyền thực thi 														|
| Setuid/Setgid | s       |	Người thực thi là người sở hữu thay vì người sử dụng lệnh			|
|        		| S       |	Tương tự với Setuid/Setgid nhưng file không thể thực thi			|
| Sticky       	| t       |	**Owner User** (hoặc root) mới được phép xóa hoặc thay đổi tên file	|

> **Octal Mode:** ```chmode [octal_mode] file_name```

Cách này sẽ khó sử dụng hơn với những người mới, nhưng nếu quen rồi thì sẽ nhanh hơn so với cách thứ nhất. Với cách này, ta có thể biểu diễn quyền với tối đa 4 chữ số từ **0 đến 7**. Số nào bị thiếu sẽ được coi là 0, VD: 5 sẽ được tính là 0005. Dưới đây là ý của các số để phân quyền:

| Giá trị | Hàng thứ nhất     		 | Hàng thứ 2, 3, 4					|
| :-------| :----------------------- | :------------------------------- |
| 0       | 		       			 | Không có quyền (---) 			|
| 1       | Sticky       			 | Quyền thực thi (--x) 			|
| 2       | Setgid       			 | Quyền ghi (-w-)					|
| 3       | Setgid và Sticky       	 | Quyền ghi và thực thi (-wx)		|
| 4       | Setuid       			 | Quyền đọc (r--)					|
| 5       | Sticky và Setuid	     | Quyền đọc và thực thi (r-x)		|
| 6       | Setgid và Setuid       	 | Quyền đọc và ghi (rw-)			|
| 7       | Sticky, Setgid và Setuid | Quyền đọc, ghi và thực thi (rwx)	|

## <a name="ubuntu-start"></a> II/ Ubuntu

### <a name="ubuntu-basic-command"></a> 1. Các câu lệnh cơ bản
Để xem toàn bộ option của một câu lệnh trong **Ubuntu**, ta dùng lệnh: ```man <câu lệnh>```

**Ví dụ:** ```man ls```, ta sẽ được như hình dưới.

![](http://www.ubuntujourneyman.com/wp-content/uploads/2011/05/man-ls-output1.png)

#### <a name="ubuntu-file-folder-command"></a> a. Để quản lý files, folders

| Lệnh 								| Mô tả 												 |
| :-------------------------------- | :----------------------------------------------------- |
| cp file /folder 					| Chép file vào folder 									 |
| cp file1 file2 					| Chép file1 sang file2 								 |
| cp -r folder1 folder2 			| Chép toàn bộ nội dung của folder1 vào folder2 		 |
| rsync -a folder1 folder2 			| Đồng bộ nội dung folder1 sang folder2  				 |
| mv file1/folder1 file2/folder2	| Chuyển tên file1/folder1 thành tên file2/folder2 		 |
| mv file folder   					| Chuyển file vào folder 								 |
| mv file1 folder2/file2 			| Chuyển file1 vào folder2 đồng thời đổi tên thành file2 |
| mkdir folder 						| Tạo folder 											 |
| mkdir -p folder1/folder2 			| Tạo ra folder1 và subfolder folder2 					 |
| rm file 							| Xóa bỏ file trong folder hiện hành 					 |
| rmdir folder 						| Xóa bỏ folder trống 									 |
| rm -rf folder 					| Xóa bỏ  folder và tất cả các tập tin 					 |
| ln -s file link	 				| Tạo ra một liên kết mang tên link đến file (nối tắt) 	 |
| find folder -file_name 			| Tìm file trong folder 								 |
| diff file1 file2 					| So sánh nội dung của 2 file hoặc của 2 folder 		 |

#### <a name="ubuntu-change-list-folder-command"></a> b.Di chuyển, liệt kệ files, folders
| Lệnh 			| Mô tả 														|
| :------------ | :------------------------------------------------------------ |
| pwd       	| Hiển thị tên folder hiện hành       							|
| cd        	| Di chuyển sang folder **/home/user_folder**       			|
| cd ~ /folder	| Di chuyển sang folder **/home/user_folder/folder**       		|
| cd ..       	| Di chuyển ra folder cha       								|
| cd /usr/apt	| Di chuyển đến folder **/usr/apt**       						|
| ls -l			| Liệt kê danh sách files/folders trong folder hiện hành       	|
| ls -a			| Liệt kê danh sách files/folders(cả ẩn) trong folder hiện hành |
| ls -d			| Liệt kê tên files/folders trong folder hiện hành 				|
| ls -t			| Xếp lại files theo ngày đã tạo, theo thứ tự mới nhất ngược về |
| ls -S			| Xếp lại files theo kích thước, theo thứ giảm dần 				|
| ls -l | more	| Liệt kê theo từng trang một dần 								|
| dir			| Giống như lệnh ls dùng để liệt kê tập tin và thư mục 			|

### <a name="ubuntu-config-network"></a> 2. Cấu hình Network
#### <a name="ubuntu-config-card-network"></a> a. Cấu hình card mạng
Để xem thông tin card mạng, dùng lệnh: ```ifconfig ten_card```
- Nếu **ten_card** để trống, *terminal* sẽ hiển thị ra danh sách kèm thông tin các card mạng.

![](http://www.howtoing.com/wp-content/uploads/2016/02/Ifconfig-Command.png)
<br/>
Để gán **IP** tạm thời cho card mạng, dùng lệnh: ```ifconfig ten_card IP netmask subnet-mask```
- **Ví dụ:** ```ifconfig eth0 192.168.1.2 netmask 255.255.255.0```
- Với cách gán này, **IP** sẽ mất sau khi khởi động lại máy.

##### <a name="ubuntu-config-card-network-by-file"></a> Cấu hình card mạng bằng file
Cấu hình toàn bộ các card mạng trong **Ubuntu** được lưu trong file: **/etc/network/interfaces**

Để thêm cấu hình một card mạng mới, ta thêm vào cuối file này các dòng sau:
- auto ten_card
- iface ten_card inet static/dhcp
Nếu để **inet** là **static** thì thêm dòng dưới:
- address **IP**
- netmask **Subnet_mask**
- gateway **Default_gateway**

#### <a name="ubuntu-setup-ssh"></a> b. Cấu hình SSH
- **Bước 1:** Cài đặt **SSH**, chạy lệnh: ```sudo apt-get install openssh-server```

![](http://jtmorris.net/wp-content/uploads/cache/2013/09/Ubuntu-64-bit/733241792.png)

- **Bước 2:** Chạy **SSH** với câu lệnh: ```sudo service ssh restart```

![](https://www.howtogeek.com/wp-content/uploads/2012/07/image232.png)
