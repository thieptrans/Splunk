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

##Cài Agent lên Server chạy Splunk để lấy log
Ở đây mình sử dụng phương pháp đẩy (Push) để lấy log từ Server.

Sử dụng Elastic Cloud để monitor và cài Auditbeat lên server.

Download và install Auditbeat version lên server.
Sau khi đăng ký elastic  bản dùng thử mk có được dòng lệnh để kết nối máy chủ với agent

$ProgressPreference = 'SilentlyContinue'
Invoke-WebRequest -Uri https://artifacts.elastic.co/downloads/beats/elastic-agent/elastic-agent-8.12.2-windows-x86_64.zip -OutFile elastic-agent-8.12.2-windows-x86_64.zip
Expand-Archive .\elastic-agent-8.12.2-windows-x86_64.zip -DestinationPath .
cd elastic-agent-8.12.2-windows-x86_64
.\elastic-agent.exe install --url=https://0cd87c8752734b4bb579362e7d2881a3.fleet.us-central1.gcp.cloud.es.io:443 --enrollment-token=NWpPQ1JZNEJ3YUUxQm1lUENnajQ6UlhYQXFWOG5SOTZlelRYWThyVDZ3Zw==

