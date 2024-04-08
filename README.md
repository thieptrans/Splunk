# Splunk
## Giới thiệu
Phần mềm Splunk cho phép người dùng thu thập, lưu trữ, phân tích và trực quan hóa dữ liệu từ nhiều nguồn khác nhau. Hỗ trợ tìm kiếm, giám sát và trích suất thông tin giá trị từ dữ liệu. Splunk được ứng dụng rộng rãi trong an toàn hệ thống để nâng cao ứng dụng, bảo mật, các chính sách, phân tích web.
## Cài đặt
Để cài đặt Splunk mk sử dụng môi trường ubuntu desktop
Tải Splunk tại https://www.splunk.com/

Sau khi đăng kí và nhập thông tin thì mình có đường link 
>wget -O splunk-9.2.0.1-d8ae995bf219-linux-2.6-amd64.deb "https://download.splunk.com/products/splunk/releases/9.2.0.1/linux/splunk-9.2.0.1-d8ae995bf219-linux-2.6-amd64.deb"

![image](https://github.com/thieptrans/Splunk/assets/118431215/bdf0ff74-16a0-4a42-ba80-7bc3c7509d92)

Sau khi tải xong, cài các package bằng lệnh **apt install**.
![image](https://github.com/thieptrans/Splunk/assets/118431215/13dcd6dc-f36d-41ba-998e-3e8ee524108f)

Splunk sẽ được cài vào thư mục **/opt/splunk**.

Chạy lệnh sau để accept license
>/opt/splunk/bin/splunk start --accept-license

![image](https://github.com/thieptrans/Splunk/assets/118431215/fa7edf21-0b87-458a-b4d5-d67170875b53)

Sau khi enter ‘y’ để xác nhận thì Splunk sẽ cho ta tạo credentials cho admin account.
![image](https://github.com/thieptrans/Splunk/assets/118431215/219c9393-6ab7-4785-82f3-beb795df8b4f)

Quá trình cài đặt hoàn tất.

Start splunk và truy cập vào web interface.
> /opt/splunk/bin/splunk start

![image](https://github.com/thieptrans/Splunk/assets/118431215/c627737f-8dc4-4b91-8ea8-c1a26bca8795)
![image](https://github.com/thieptrans/Splunk/assets/118431215/2fc023b0-6218-40f7-854d-914213da804c)

![image](https://github.com/thieptrans/Splunk/assets/118431215/b74db5ef-4357-4fa3-823d-c3e9a9a741ae)

## Cài Agent lên Windows server rồi đẩy log về Splunk
Ở đây mình sử dụng phương pháp đẩy (Push) để lấy log từ Server.

### Cấu hình truy cập Splunk qua https

Sau khi đăng nhập được vào thì chọn Settings --> System --> Server settings --> General Settings

![image](https://github.com/thieptrans/Splunk/assets/118431215/1980eb41-415d-45cd-8ed2-359de6297bb3)

Khởi động lại dịch vụ và mở port 443 truy cập qua https

### Cấu hình trên máy chủ Splunk server
Tạo 2 index để nhận log đẩy về từ windows và linux
> Settings --> indexes --> New index

![image](https://github.com/thieptrans/Splunk/assets/118431215/62661ba6-4b16-4af3-89f5-5b6997e305e0)

Cấu hình mở **port 9997** để nhận log

Setting --> Forwarding and receiving --> Recieve data

![image](https://github.com/thieptrans/Splunk/assets/118431215/4f1cf5eb-4b85-458f-802b-24f86520daed)

### Đẩy Log từ windows về

Bật Success/Failure audit log tại Administrator Tools → Local security policy → Local Policy → Audit Policy

Chỉnh sửa các chính sách sau: 
 - Audit account logon events
 - Audit account management
 - Audit logon events
 - Audit Policy change
 - Audit Privilege use
 - Audit system event

![image](https://github.com/thieptrans/Splunk/assets/118431215/34377ebd-3b85-4399-a390-f9ebd9ebf976)

Tải Universal Forwarder về cho windows: 
https://www.splunk.com/en_us/download/universal-forwarder.html

![image](https://github.com/thieptrans/Splunk/assets/118431215/fb8ecfcd-6bf3-473d-a6d0-41710530b270)

--> Check thi box to accept the License Agreement
--> Customize Options

![image](https://github.com/thieptrans/Splunk/assets/118431215/8e6a4723-c6b6-46d3-872e-d98bd576b4df)

--> next 
![image](https://github.com/thieptrans/Splunk/assets/118431215/b5ddef35-fcb8-481f-8baf-e8e80f919364)

Cài đặt ssl, nếu có Browse đến đường dẫn chứa tập tin public và private, sau đó nhập password và Browse đường dẫn SSL root CA. Nếu không sử dụng tính năng này có thể Next sang bước tiếp theo

![image](https://github.com/thieptrans/Splunk/assets/118431215/68550be4-7c96-4d08-942f-b2d9dfa1a68d)
--> next

![image](https://github.com/thieptrans/Splunk/assets/118431215/0f66ba3c-c796-439d-a567-df742a60e8f4)

Tích chọn các log cần đẩy về để giám sát

![image](https://github.com/thieptrans/Splunk/assets/118431215/567949e0-a4f7-4738-bf31-ef799efef399)

Nhập tài khoản và mật khẩu cho app

--> next 

Nhập ip Splunk Server và port mặc định sử dụng là 8089

![image](https://github.com/thieptrans/Splunk/assets/118431215/eca9a3b3-ea61-4476-80dc-e498d0e5bb04)

Nhập ip server và port nhận log từ client đẩy về.

![image](https://github.com/thieptrans/Splunk/assets/118431215/f83d9108-3192-4b23-baea-8552d4f46ea1)

![image](https://github.com/thieptrans/Splunk/assets/118431215/3202964d-beaa-453e-865b-e3b9fd0ff362)
--> Install

![image](https://github.com/thieptrans/Splunk/assets/118431215/8603212b-cac6-459c-9149-39c37c7e2862)

Quá trình cài đặt hoàn tất.

Thay đổi cấu hình log đẩy về chỉnh sửa tại path C:\Program Files\SplunkUniversalForwarder\etc\apps\SplunkUniversalForwarder\localinputs.conf

![image](https://github.com/thieptrans/Splunk/assets/118431215/82f26348-a5c8-4321-9bfc-22a2f214612c)

Thêm dòng index = <tên index> vào dưới mỗi luồng

Bật cửa sổ service và restart lại Splunk Forwarder

![image](https://github.com/thieptrans/Splunk/assets/118431215/4740c746-39dd-4db2-9759-5221b7ba0d4f)

Restart lại splunk sau khi thay đổi cấu hình.

Trên splunk server, Chọn Setting --> Data inputs --> Forwarded input --> Windows Event Log

![image](https://github.com/thieptrans/Splunk/assets/118431215/d4e55016-b78f-4cb9-b8b1-f647e2f11d2f)

Chọn tên máy thực hiện chuyển tiếp tại mục available host và nhập tên vào class name --> next
Bước tiếp theo chọn các mục đã tích khi cài universal Forwarder, mục index nhấp chọn index vừa tạo tại indexes, ở đây của mình là windows_server.

Trở về trang chủ splunk server --> search and reporting

![image](https://github.com/thieptrans/Splunk/assets/118431215/ae0a64b1-eff6-4bfb-b1d4-a6fc4e71f5b8)

## Cài đặt agent lên ubuntu
### Cài đặt splunk forwarder trên máy ubuntu
Đăng nhập vào tài khoản root và tạo user mới là splunkfwd và thêm vào group splunkfwd

Tạo thư mục chứa Splunk

>export SPLUNK_HOME="/opt/splunkforwarder"
>mkdir $SPLUNK_HOME

Tải splunk universal forwarder về từ link 

>wget -O splunkforwarder-9.2.1-78803f08aabb-linux-2.6-amd64.deb "https://download.splunk.com/products/universalforwarder/releases/9.2.1/linux/splunkforwarder-9.2.1-78803f08aabb-linux-2.6-amd64.deb"

Cài đặt splunk bằng lệnh

>dpkg -i splunkforwarder-9.2.1-78803f08aabb-linux-2.6-amd64.deb 

Cấp quyền cho tài khoản splunkfwd
>chown -R splunkfwd:splunkfwd $SPLUNK_HOME

Khởi chạy 
>$SPLUNK_HOME/bin/splunk start --accept-license

Nhập thông tin tài khoản mật khẩu
![image](https://github.com/thieptrans/Splunk/assets/118431215/b26c5403-1e93-434e-b53a-f20946cf6257)

==> Quá trình cài đặt hoàn tất.
### Cấu hình file universal forwarder
