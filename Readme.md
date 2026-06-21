## Họ và tên: Hoàng Kim Ngọc
## MSSV: K225481006053
## Lớp: K58KTP

## BÀI TẬP LỚN
môn: phát triển ứng dụng với mã nguồn mở - tee0421
bt1: Ubuntu + Docker: DÙNG DOCKER ĐỂ BUILD myapi
bt2: django (python): WEB QUẢN LÝ TIỆM CẦM ĐỒ
bt3: wordpress (php) + mariadb + phpmyadmin (chỉ để xem các tables)
bt4: wordpress + n8n + bot telegram+gemini: auto đăng bài bằng cách chát
bt5:
  - lý thuyết: 
    + docker là gì? 
    + các keyword được sử dụng trong docker-compose.yml
      để mô tả 1 service, network, volume,...
      liệt kê + ý nghĩa của từ khoá đó + ví dụ minh hoạ
    + ưu điểm khi triển app sử dụng docker là gì?
    + dùng docker: tạo app, test app OK trên laptop cá nhân
      giờ muốn triển khai app này trên máy chủ thật ko có internet
      thì các bước cần làm là?
  - thực hành áp dụng: APP MONITOR + ALERT DATA REALTIME
    sử dụng docker compose có nhiều serivce 
    và các thành phần cần thiết để tạo thành ứng dụng:
     + nodered liên tục lấy dữ liệu từ nguồn nào đó (chứng khoán, thời tiết, giá vàng,...)
       nguồn thực tế, số liệu luôn động sau thời gian ngắn
     + nodered lưu trữ dữ liệu vào 2 database: mariadb để lưu giá trị tức thời
       lưu lịch sử vào influxdb
     + sử dụng grafana để trực quan hoá dữ liệu: vẽ biểu đồ
     + sử dụng nginx để làm webserver
       chạy 1 trang web html+js+css làm front-end
       js: lấy dữ liệu tức thời trong mariadb qua (ajax | socket) 
           gọi api (api tự build bằng Flask giống bt1)
           api trả về giá trị tức thời trong mariadb
           hiển thị lên web, auto hiển thị số mới khi thay đổi
       sử dụng iframe để gọi grafana
       hiển thị biểu đồ dữ liệu lịch sử của thông số đã lưu
     + QUAN SÁT DỮ LIỆU LỊCH SỬ => GIÁ TRỊ BẤT THƯỜNG
       (VD MIỀN A..B: OK, DƯỚI A: ALERT LOW, TRÊN B: ALERT HIGH)
     + nodered: kết hợp bot Telegram
       khi dữ liệu not OK, thì gửi tin nhắn từ bot => group trên telegram
       group đã add bot vào: (nhóm đã có 2 người), add thêm 1875746636 thành 3 người
       mỗi khi bot gửi dữ liệu vào nhóm: mọi member of group đều nhận đc
       nội dung alert: tường minh, có value gây alert

     xuất tất cả các container ra file nén.
     xoá mọi container đang chạy
     load lại các container  từ file nén để khôi phục các container đã xoá
=========
quá trình làm: chụp ảnh lại, mô tả cho ảnh
  lưu vào trong github => paste link access public của repo: vào file excel online
=====================

cả 5 bài tập:
biên tập lại xíu để phù hợp với bản print
đóng quyển, ko cần bìa xanh, ko cần giấy bóng kính
header+footer của các trang giấy: có tên + masv, bài tập lớp Môn, số trang
trang 1 có đầy đủ thông tin cá nhân.

lưu ở bm để chấm điểm.
## BÀI LÀM
6.3 Quá trình thực hiện
6.3.1 Triển khai các dịch vụ bằng Docker Compose

<img width="615" height="345" alt="image" src="https://github.com/user-attachments/assets/1530779e-df44-4c2b-9abf-f3448bb5c971" />

Hình 83 Tạo thư mục chứa project và file docker-compose.yml

<img width="617" height="347" alt="image" src="https://github.com/user-attachments/assets/d3f98d06-81a9-4501-ab21-c469dcf3ac72" />

Hình 84 Cấu hình file docker-compose.yml

<img width="600" height="337" alt="image" src="https://github.com/user-attachments/assets/cbe9c9a5-096c-4351-8542-6d725ffb2f14" />

Hình 85. Cấu hình file requirements.txt
<img width="606" height="341" alt="image" src="https://github.com/user-attachments/assets/3b32a46e-3bf2-48e2-b56b-cb96ff1c7d91" />

Hình 86. Cấu hình file Dockerfile
<img width="604" height="339" alt="image" src="https://github.com/user-attachments/assets/d6cbb527-e8bd-462b-9d83-6af46e7755f9" />

Hình 87. Cấu hình file app.py
<img width="603" height="339" alt="image" src="https://github.com/user-attachments/assets/2c793f2b-29f5-4946-b6b1-60a4da3bd463" />

Hình 88. Cấu hình file index.html
<img width="597" height="335" alt="image" src="https://github.com/user-attachments/assets/8eb65ffd-1df9-4c6a-8dc4-cc7b21647ca2" />

Hình 89. Chạy docker-compose.yml
<img width="604" height="340" alt="image" src="https://github.com/user-attachments/assets/9f6a124b-598f-4ebd-88a3-a9143e624a6a" />

Hình 90. Kiểm tra tình trạng các service
6.3.2 Xây dựng chức năng trên Nodered

Hình 91. Tải các thư viện cần thiết trên Nodered
<img width="613" height="328" alt="image" src="https://github.com/user-attachments/assets/e1e0bc55-80ce-4c2a-969b-f9c4eb96face" />

Hình 92. Các node cần thiết cho hệ thống
<img width="601" height="167" alt="image" src="https://github.com/user-attachments/assets/10ecda6d-1fc7-43b2-ab8a-e28112360250" />

Hình 93. Cấu hình node http request
<img width="327" height="420" alt="image" src="https://github.com/user-attachments/assets/881cabbc-be0f-4739-bb8f-132fb3849186" />

Hình 94. Cấu hình node function
<img width="362" height="382" alt="image" src="https://github.com/user-attachments/assets/b5a0e21a-8c0c-47f8-ac32-dd99895a93e1" />

Hình 95. Cấu hình node Mysql
<img width="359" height="465" alt="image" src="https://github.com/user-attachments/assets/e1e66284-b6f8-4ec2-93df-27a72d308c22" />

Hình 96. Cấu hình node Switch
<img width="358" height="466" alt="image" src="https://github.com/user-attachments/assets/a925c506-1a3b-4cfd-ac31-f0c0fb9acfea" />

Hình 97 Cấu hình node function 2
<img width="362" height="379" alt="image" src="https://github.com/user-attachments/assets/76361f58-9a6b-4bb4-a5f7-7782f2611217" />

6.3.3 Cấu hình Data Source InfluxDB trong Grafana
<img width="610" height="346" alt="image" src="https://github.com/user-attachments/assets/7241b209-3095-4aab-afb6-ab4d79509bb4" />

Hình 98. Cấu hình Data Source InfluxDB trong Grafana
<img width="612" height="345" alt="image" src="https://github.com/user-attachments/assets/46453689-8430-4417-957a-72b10cfca24b" />

Hình 99. Cấu hình tiếp theo trêm Grafana
<img width="626" height="335" alt="image" src="https://github.com/user-attachments/assets/509875ba-fcce-46d0-b192-e7de9d0fb15e" />

Hình 100. Kết quả trực quan dữ liệu hiển thị trên Granfana
<img width="626" height="335" alt="image" src="https://github.com/user-attachments/assets/727e7398-a4e2-4f40-bd03-5e8b4adc1773" />

Hình 101. Nhúm iframe vào trong file index.html
<img width="613" height="344" alt="image" src="https://github.com/user-attachments/assets/e811e672-0cdc-43be-a2ed-943ad2fcd0f0" />

Hình 102. Giao diện web có hiện thị biểu đồ
<img width="612" height="344" alt="image" src="https://github.com/user-attachments/assets/12236667-77be-4068-a600-1a557d240b32" />

Hình 103. Cảnh báo được hiển thị ở trong Telegram
<img width="611" height="343" alt="image" src="https://github.com/user-attachments/assets/385736c7-aa38-4753-b42a-9fb9ce89f816" />
