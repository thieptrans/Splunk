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
>/opt/splunk/bin/splunk start—accept-license 
![image](https://github.com/thieptrans/Splunk/assets/118431215/105a25c4-06ac-4fd9-bae1-6b60c8ec87bf)

Sau khi enter ‘y’ để xác nhận thì Splunk sẽ cho ta tạo credentials cho admin account.
![image](https://github.com/thieptrans/Splunk/assets/118431215/219c9393-6ab7-4785-82f3-beb795df8b4f)
Quá trình cài đặt hoàn tất.

Start splunk và truy cập vào web interface.
> /opt/splunk/bin/splunk start
![image](https://github.com/thieptrans/Splunk/assets/118431215/c627737f-8dc4-4b91-8ea8-c1a26bca8795)
![image](https://github.com/thieptrans/Splunk/assets/118431215/2fc023b0-6218-40f7-854d-914213da804c)

![image](https://github.com/thieptrans/Splunk/assets/118431215/b74db5ef-4357-4fa3-823d-c3e9a9a741ae)

## Cài Agent lên Server chạy Splunk để lấy log
Ở đây mình sử dụng phương pháp đẩy (Push) để lấy log từ Server.

<!-- Sử dụng Elastic Cloud để monitor và cài Auditbeat lên server.

Download và install Auditbeat version lên server.
Sau khi đăng ký elastic  bản dùng thử mk có được dòng lệnh để kết nối máy chủ với agent

>$ProgressPreference = 'SilentlyContinue'
>Invoke-WebRequest -Uri https://artifacts.elastic.co/downloads/beats/elastic-agent/elastic-agent-8.12.2-windows-x86_64.zip -OutFile elastic-agent-8.12.2-windows-x86_64.zip
>Expand-Archive .\elastic-agent-8.12.2-windows-x86_64.zip -DestinationPath .
>cd elastic-agent-8.12.2-windows-x86_64
>.\elastic-agent.exe install --url=https://0cd87c8752734b4bb579362e7d2881a3.fleet.us-central1.gcp.cloud.es.io:443 --enrollment-token=NWpPQ1JZNEJ3YUUxQm1lUENnajQ6UlhYQXFWOG5SOTZlelRYWThyVDZ3Zw== -->

### Cấu hình truy cập Splunk qua https

Sau khi đăng nhập được vào thì chọn Settings --> System --> Server settings --> General Settings

![image](https://github.com/thieptrans/Splunk/assets/118431215/1980eb41-415d-45cd-8ed2-359de6297bb3)

Khởi động lại dịch vụ và mở port 443 truy cập qua https

### Cấu hình trên máy chủ Splunk server
Tạo 2 index để nhận log đẩy về từ windows và linux
> Settings --> indexes --> New index
![image](https://github.com/thieptrans/Splunk/assets/118431215/537423c2-cbd9-46a3-979f-09d4f0005395)

Cấu hình mở **port 9998** để nhận log

Cấu hình tại Forwarding and receiving --> Recieve data

![image](https://github.com/thieptrans/Splunk/assets/118431215/925bfbbe-c79c-431d-871a-af01950b2102)

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

Tải Splunk về cho windows: https://www.splunk.com/en_us/download/splunk-enterprise/thank-you-enterprise.html
![image](https://github.com/thieptrans/Splunk/assets/118431215/e4612247-e6b8-49b0-9b8d-b4e6a2dcbbd3)

--> Customize Options
![image](https://github.com/thieptrans/Splunk/assets/118431215/5be9dd5f-d701-4b49-a40b-c5009f0b6678)

![image](https://github.com/thieptrans/Splunk/assets/118431215/f92c99b9-54d4-4dfa-9840-d8ff6a381d25)

![image](https://github.com/thieptrans/Splunk/assets/118431215/729d0818-583f-437c-aeb4-03207543e898)
