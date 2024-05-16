#!/bin/bash

# Số lượng proxy bạn muốn tạo
COUNT=150

# Cổng bắt đầu
START_PORT=30000

# Tạo cấu hình cho mỗi proxy
for ((i=0; i<COUNT; i++)); do
    PORT=$((START_PORT + i))

    # Tạo cấu hình proxy
    echo "proxy -6 -n -a -p${PORT} -i103.27.61.7 -efe80::2827:77ff:feb6:cb80"
done > /etc/3proxy/3proxy.cfg

# Thêm cấu hình chung vào tệp cấu hình
echo "daemon
maxconn 1000
nscache 65536
timeouts 1 5 30 60 180 1800 15 60
setgid 65535
setuid 65535
flush" >> /etc/3proxy/3proxy.cfg

# Khởi động 3proxy
service 3proxy start

