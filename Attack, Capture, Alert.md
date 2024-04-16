## Tấn công dò đoán mật khẩu

Tiến hành đăng nhập sai mật khẩu nhiều lần

Thực hiện lọc kết quả trên splunk

> index="index_name" "eventcode=4625"
| timechart span=1h count as event_count
| where event_count > 5

--> Save as --> alert

Điền các thông tin như tên alert, mô tả, chọn thời gian cảnh báo, chọn phương thức cảnh báo
* Trigger : thông báo nổi
* mail : gửi cảnh báo qua mail
