# Install Nexus and push artifactory to Nexus (Linux)
:sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles::sparkles:
## Table of content
1. [Install](#install)
2. [Run as a service](#service)
<a name="install"></a>
## Install :wrench:

- Đầu tiên vào trang [sonatype](https://help.sonatype.com/repomanager3/download) để tải nexus về 

- Sau đó giải nén vào một thư mục nào đó >> Vào thư mục đã giải nén >> /home/duong/Downloads/nexus-3.17.0-01/bin >> ./nexus run

- Sau khi chạy xong vào [localhost:8081](http://localhost:8081/) ta thấy giao diện như hình
<a name="service"></a>
## Run as a service :running_man:
- Tạo một người dùng có đủ quyền để có thể chạy service trong file ***bin/nexus.rc*** ở đây e chọn root:
```run_as_user="root"``` thường thì đầu dòng có dấu # => uncomment nó.
- Sau đó symlink từ InstallDir/bin/nexus vào /etc/init.d/nexus: 
  - ```sudo ln -s /home/duong/Downloads/nexus-3.17.0-01/bin/nexus /etc/init.d/nexus```
- Tạo một file tên nexus.service trong mục etc/systemd/system. Sau đó chèn đoạn script sau:
```[Unit]
Description=nexus service
After=network.target
  
[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/home/duong/Downloads/nexus-3.17.0-01/bin/nexus start
ExecStop=/home/duong/Downloads/nexus-3.17.0-01/bin/nexus stop
User=root
Restart=on-abort
  
[Install]
WantedBy=multi-user.target
```

- Sau khi lưu lại chạy các lệnh: 
```
systemctl daemon-reload
systemctl enable nexus.service
systemctl start nexus.service
```

- Trong đó ***enable***  để service được khởi động cùng hệ thống, ***start*** để chạy service.

........Continue =>>>>>>> :notes: :notes: :notes: :notes: :notes: :notes: :notes: :notes: :notes:
