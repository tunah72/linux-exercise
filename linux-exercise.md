# BÀI TẬP THỰC HÀNH LINUX CƠ BẢN

## User & Group

### Bài tập 1: Tạo và quản lý user

**Yêu cầu:** 

Tạo các user sau:

 peter và alice: thiết lập mật khẩu, thư mục home tự động và đặt shell /bin/bash mặc định cho các user này.

User bob: thiết lập mật khẩu, đặt thư mục home là /home/bob_dir và đặt shell /bin/sh mặc định cho user

Đổi tên user từ bob thành bigman và đổi thư mục home thành /home/bigman_dir và chuyển toàn bộ dữ liệu thư mục /home/bob_dir sang thư mục home mới

Xóa user alice và thư mục home của user này.

**Gợi ý:** 

Tạo user mới với cú pháp: sudo useradd [tùy chọn] [tên user]

Một số [tùy chọn]:

• -m: Tạo thư mục home cho user.

• -s: Chỉ định shell mặc định cho user (ví dụ: /bin/bash).

• -d: Chỉ định thư mục home cụ thể.

Đặt password cho user: passwd [tên user]

Xóa user và home directory: userdel -r [tên user]

Kiểm tra danh sách user: cat /etc/passwd

Đăng nhập user trên linux: su [user_name] 

Đổi tên user vào di chuyển dữ liệu sang thư mục home mới: usermod -l [user mới] [user hiện tại] -m -d [thư mục home mới]

### Bài tập 2: Tạo và quản lý group

**Yêu cầu:** 

Tạo các group mới như sau:

Tạo group tech: thêm user peter và bob vào group

Tạo group marketing: thêm user bigman vào group

Xóa group marketing.

**Gợi ý:** 

Tạo group: groupadd [tên nhóm]

Thêm user vào group: usermod -aG [tên nhóm] [tên user]

Xóa group: groupdel [tên nhóm]

Kiểm tra nhóm của user: groups [tên user]

## Phân quyền file và thư mục

### Bài tập 1: phân quyền thư mục với kí hiệu tượng trưng

**Yêu cầu:** 

Sử dụng cách phân quyền kí hiệu tượng trưng thực hiện bài tập dưới đây:

Đăng nhập vào user peter, tạo file tên practice.txt trong thư mục home user peter

Thay đổi quyền cho phép chủ sở hữu file có quyền đọc ghi một file, cho phép group và người khác đọc file.

Kiểm tra lại phân quyền file đã đúng yêu cầu hay chưa sau đó phân quyền lại cho file với owner chỉ có quyền đọc, phân quyền group và other vẫn giữ nguyên.

**Gợi ý:** 

Câu lệnh tạo file practice: touch practice.txt

Phân quyền cho file với yêu cầu trên:  chmod u=rw,g=r,o=r [tên file]

Kiểm tra phân quyền: ls -al | grep [tên file]

Phân quyền cho file với ower chỉ có quyền đọc: chmod u=r [tên file]

### Bài tập 2: Tạo và thay đổi quyền cho file bằng số học (octal)

**Yêu cầu:** 

Đăng nhập vào user peter, tạo file tên hello.sh thư mục home user peter

Tạo file hellword.sh sau đó thay đổi quyền để chủ sở hữu có quyền đọc ghi, và thực thi, còn nhóm và người khác chỉ có quyền đọc:

**Gợi ý:** 

Tạo file hello.sh với câu lệnh sau: 

cat <<EOF >hello.sh

#!/bin/bash

echo 'hello'

EOF

Câu lệnh thay đổi quyền cho file với yêu cầu bài tập: chmod 744 [tên file]

Kiểm tra phân quyền: ls -al | grep [tên file]

Kiểm tra thực chi file:./hello.sh

## Quản lý xuất nhập file

### Bài Tập 1: Tạo Và Ghi Nội Dung Vào File

**Yêu cầu:** Tạo một file mới có tên myfile.txt và ghi nội dung "Hello, Linux!" vào file đó.

**Gợi ý:** echo "Hello, Linux!" > myfile.txt

### Bài Tập 2: Xem Nội Dung File

**Yêu cầu:** Xem nội dung của file myfile.txt đã tạo ở bài tập trước.

**Gợi ý:** cat myfile.txt

### Bài Tập 3: Ghi Thêm Nội Dung Vào File

**Yêu cầu:** Thêm dòng "Welcome to Linux file management." vào cuối file myfile.txt mà không ghi đè lên nội dung cũ.

**Gợi ý:** echo "Welcome to Linux file management." >> myfile.txt

### Bài Tập 4: Đếm Số Dòng Trong File

**Yêu cầu:** Đếm số dòng trong file myfile.txt.

**Gợi ý:** wc -l myfile.txt

### Bài Tập 5: Đếm Số Từ Trong File

**Yêu cầu:** Đếm số từ có trong file myfile.txt.

**Gợi ý:** wc -w myfile.txt

### Bài Tập 6: Sao Chép File

**Yêu cầu:** Sao chép file myfile.txt sang một file mới có tên là myfile_backup.txt.

**Gợi ý:** cp myfile.txt myfile_backup.txt

### Bài Tập 7: Di Chuyển File

**Yêu cầu:** Di chuyển file myfile_backup.txt vào thư mục /tmp.

**Gợi ý:** mv myfile_backup.txt /tmp/

### Bài Tập 8: Xóa File

**Yêu cầu:** Xóa file myfile.txt.

**Gợi ý:** rm myfile.txt

### Bài Tập 9: Hiển Thị Các File Trong Thư Mục

**Yêu cầu:** Hiển thị tất cả các file và thư mục trong thư mục hiện tại, bao gồm cả các file ẩn.

**Gợi ý:** ls -al

### Bài Tập 10: Tìm Kiếm Chuỗi Trong File

**Yêu cầu:** Tìm kiếm chuỗi "Linux" trong file myfile_backup.txt ở thư mục /tmp.

**Gợi ý:** grep "Linux" /tmp/myfile_backup.txt

### Bài Tập 11: Đổi Tên File

**Yêu cầu:** Đổi tên file myfile_backup.txt thành linuxfile.txt.

**Gợi ý:** mv /tmp/myfile_backup.txt /tmp/linuxfile.txt

### Bài Tập 12: Tạo Thư Mục Và Di Chuyển File Vào Thư Mục

**Yêu cầu:** Tạo một thư mục có tên backup trong thư mục hiện tại và di chuyển file linuxfile.txt vào thư mục backup.

**Gợi ý:** 

### Bài Tập 13: Hiển Thị Nội Dung File Theo Từng Phần

**Yêu cầu:** Hiển thị nội dung của file linuxfile.txt trong thư mục backup từng trang một.

**Gợi ý:** less backup/linuxfile.txt

## Quản lý gói phần mềm

> **Lưu ý:** Các câu lệnh bên dưới dành cho hệ điều hành Ubuntu 22.04 LTS

### Bài Tập 1: Cập Nhật Danh Sách Gói Phần Mềm

**Yêu cầu:** Trước khi cài đặt gói phần mềm, cần phải cập nhật danh sách các gói phần mềm có sẵn trên hệ thống.

**Gợi ý:** sudo apt update

### Bài Tập 2: Cài Đặt Một Gói Phần Mềm

**Yêu cầu:** Cài đặt gói phần mềm vsftpd để sử dụng trong chỉnh sửa văn bản.

**Gợi ý:** sudo apt install vsftpd

### Bài Tập 3: Tìm Kiếm Gói Phần Mềm

**Yêu cầu:** Tìm kiếm một gói phần mềm có tên hoặc mô tả chứa từ khóa net-tools

**Gợi ý lệnh:** apt search net-tools

### Bài Tập 4: Hiển Thị Thông Tin Gói Phần Mềm

**Yêu cầu:** Kiểm tra thông tin chi tiết của gói phần mềm vim đã cài đặt, bao gồm phiên bản, nhà phát triển, và các gói phụ thuộc.

**Gợi ý:** apt show vsftpd

### Bài Tập 5: Gỡ Bỏ Gói Phần Mềm

**Yêu cầu:** Gỡ bỏ gói phần mềm vim khỏi hệ thống.

**Gợi ý:** apt remove vsftpd

### Bài Tập 6: Tìm Kiếm Các Gói Phần Mềm Đã Cài Đặt

**Yêu cầu:** Tìm kiếm và liệt kê tất cả các gói phần mềm đã cài đặt trên hệ thống có tên chứa từ khóa python.

**Gợi ý:** dpkg -l | grep python

### Bài Tập 7: Liệt Kê Các Gói Phụ Thuộc Của Một Gói Phần Mềm

**Yêu cầu:** Kiểm tra và liệt kê các gói phụ thuộc mà vim cần để hoạt động.

**Gợi ý:** apt depends vim

### Bài Tập 8: Kiểm Tra Các Gói Phần Mềm Bị Hỏng Hoặc Lỗi

**Yêu cầu:** Kiểm tra và sửa chữa các gói phần mềm bị lỗi hoặc hỏng trên hệ thống.

**Gợi ý:** apt --fix-broken install

### Bài Tập 9: Xóa Các Gói Phần Mềm Không Cần Thiết

**Yêu cầu:** Xóa các gói phần mềm không còn cần thiết trên hệ thống để giải phóng không gian.

**Gợi ý:** apt autoremove

## Quản lý gói dịch vụ

### Bài tập 1: Quản lý dịch vụ Nginx

**Yêu cầu:** 

Cài đặt nginx trên hệ thống và sử dụng các lệnh systemctl để:

Kiểm tra trạng thái của dịch vụ.

Khởi động và dừng dịch vụ.

**Gợi ý:** 

Cài đặt nginx: apt install nginx

Kiểm tra trạng thái nginx: systemctl status nginx

Khởi động nginx: systemctl start nginx

Dừng nginx: systemctl stop nginx

### Bài tập 2: Cấu hình tự động khởi động dịch vụ

**Yêu cầu:** Sử dụng lệnh systemctl để bật và tắt chế độ tự động khởi động của nginx khi hệ thống khởi động.

**Gợi ý:** 

Tắt chế độ tự khởi động: systemctl disable nginx

Bật chế độ tự khởi động: systemctl enable nginx

Kiểm tra lại bằng lệnh: systemctl is-enabled nginx

### Bài Tập 3: Kiểm Tra File Log Truy Cập Của Nginx

**Yêu cầu:** Kiểm tra các truy cập gần đây vào server Nginx bằng cách xem file log truy cập.

**Gợi ý:** 

Sử dụng lệnh curl vào web server mặc định nginx: curl http://localhost hoặc curl http://[ip_server]

Lệnh xem log: cat /var/log/nginx/access.log

### Bài Tập 4: Kiểm Tra File Log Lỗi Của Nginx

**Yêu cầu:** Kiểm tra các lỗi gần đây liên quan đến Nginx bằng cách xem file log lỗi.

**Gợi ý lệnh:** cat /var/log/nginx/error.log

### Bài Tập 5: Xem Log Lỗi Trong Thời Gian Thực

**Yêu cầu:** Theo dõi log lỗi của Nginx trong thời gian thực khi có truy cập.

**Gợi ý lệnh:** tail -f /var/log/nginx/error.log

## Quản lý file system

### Bài Tập 1: Kiểm Tra Không Gian Đĩa Sử Dụng

**Yêu cầu:** Kiểm tra không gian đĩa đã sử dụng và còn trống của các phân vùng hiện tại.

**Gợi ý:** df -h

### Bài Tập 2: Kiểm Tra các phân vùng trên hệ thống

**Yêu cầu:** Liệt kê tất cả các thông tin chi tiết các phân vùng đang có sẵn trong hệ thống

**Gợi ý:** fdisk -l

### Bài Tập 3: Tạo Một Phân Vùng Mới Trên Đĩa

**Yêu cầu:** Tạo một phân vùng mới trên đĩa /dev/sdb

**Gợi ý:** 

Mở trình quản lý phân vùng: fdisk /dev/sdb

Các bước trong fdisk:

Nhấn n để tạo phân vùng mới.

Nhập các giá trị như số phân vùng, sector bắt đầu và kết thúc theo hướng dẫn.

Nhấn w để ghi lại các thay đổi và thoát.

### Bài Tập 4: Định Dạng Phân Vùng Với File System

**Yêu cầu:** Định dạng phân vùng mới vừa tạo với file system xfs.

**Gợi ý:** mkfs.xfs /dev/sdb1

### Bài Tập 5: Gắn Phân Vùng Vào Hệ Thống

**Yêu cầu:** Gắn phân vùng mới /dev/sdb1 vào thư mục /mnt/new_partition.

**Gợi ý:** 

Tạo thư mục gắn phân vùng: mkdir /mnt/new_partition

Gắn phân vùng vào thư mục: mount /dev/sdb1 /mnt/new_partition

### Bài Tập 6: Gỡ Phân Vùng Ra Khỏi Hệ Thống

**Yêu cầu:** Gỡ phân vùng /dev/sdb1 vừa gắn ra khỏi thư mục /mnt/new_partition.

**Gợi ý:** umount /mnt/new_partition

### Bài Tập 7: Tự Động Gắn Phân Vùng Khi Khởi Động

**Yêu cầu:** Cấu hình để phân vùng /dev/sdb1 tự động gắn vào hệ thống tại thư mục /mnt/new_partition khi khởi động.

**Gợi ý:** 

Mở file cấu hình fstab: vi /etc/fstab

Thêm dòng sau vào cuối file: /dev/sdb1   /mnt/new_partition   xfs   defaults   0   2

### Bài tập 8: Xóa tất cả các partition đã tạo trong /dev/sdb và gỡ bỏ các cấu hình disk /dev/sdb trong /etc/fstab

**Hướng dẫn:** sử dụng lệnh fdisk /dev/sdb để xóa các phân vùng.

> **Lưu ý:** nếu đã xóa các phân vùng /dev/sdb nhưng không xóa cấu hình trong /etc/fstab thì khi reboot lại OS sẽ bị lỗi không thể khởi động thành công OS.

### Bài tập 9: Tạo và quản lý Physical Volume (PV), Volume Group (VG), và Logical Volume (LV).

**Yêu cầu:** 

Tạo Physical Volume từ phân vùng /dev/sdb.

Tạo Volume Group tên là vg_data từ Physical Volume vừa tạo.

Tạo Logical Volume tên là lv_data với kích thước 5GB từ vg_data.

Tạo hệ thống tệp ext4 trên lv_data và gắn kết vào thư mục /mnt/data.

**Hướng dẫn thực hiện:**

Tạo Physical Volume: sudo pvcreate /dev/sdb

Tạo Volume Group từ Physical Volume: sudo vgcreate vg_data /dev/sdb

Tạo Logical Volume 5GB từ Volume Group: sudo lvcreate -L 5G -n lv_data vg_data

Tạo hệ thống tệp trên Logical Volume: sudo mkfs.ext4 /dev/vg_data/lv_data

Tạo thư mục và gắn kết Logical Volume: 

sudo mkdir /mnt/data

sudo mount /dev/vg_data/lv_data /mnt/data

Kiểm tra kết quả: df -h /mnt/data

## Quản lý tác vụ tự động bằng Batch script:

 Bài Tập 1: Viết một script đơn giản để in ra dòng chữ “Hello World”.

**Yêu cầu:** 

Tạo một file Bash script có tên hello.sh

Script này sẽ in ra dòng “Hello World”.

**Gợi ý nội dung:** 

### Bài Tập 2: Viết một script để in ra ngày và giờ hiện tại của hệ thống.

**Yêu cầu:** 

Tạo một file Bash script có tên current_time.sh

Script này sẽ hiển thị ngày và giờ hiện tại.

**Gợi ý nội dung:** 

### Bài Tập 3: Viết một Bash script yêu cầu người dùng nhập hai số, sau đó tính tổng của hai số đó.

**Yêu cầu:** 

Tạo một file script sum.sh

Nhập vào hai số từ bàn phím.

In ra kết quả tổng của hai số.

**Gợi ý:** 

### Bài Tập 4: Viết một script để kiểm tra xem một file có tồn tại trong hệ thống hay không.

**Yêu cầu:** 

Tạo một file script check_file.sh

Yêu cầu người dùng nhập tên tập tin cần kiểm tra.

Kiểm tra và thông báo tập tin đó có tồn tại hay không.

**Gợi ý:** 

### Bài Tập 5: Viết một Bash script để liệt kê tất cả các file trong thư mục hiện tại.

**Yêu cầu:** 

Tạo một file script list_files.sh

Liệt kê các file trong thư mục hiện tại.

**Gợi ý:** 

### Bài Tập 6: Viết một script để in ra các số từ 1 đến 10 sử dụng vòng lặp.

**Yêu cầu:** 

Tạo một file script loop_numbers.sh

Sử dụng vòng lặp để in các số từ 1 đến 10.

**Gợi ý:** 

### Bài tập 7: Viết một script để in ra các số từ 1 đến 100 sử dụng vòng lặp.

**Yêu cầu:** 

Sao chép file loop_numbers.sh từ bài tập 8 với tên file mới là loop_numbers_100.sh

Sử dụng vòng lặp để in các số từ 1 đến 100.

**Gợi ý:** 

Sao chép file: cp loop_numbers.sh loop_numbers_100.sh

### Bài Tập 8: Viết một script để đếm số dòng của một file.

**Yêu cầu:** 

Tạo một file script count_lines.sh.

Nhập vào tên file và đếm số dòng trong file đó.

**Gợi ý:** 

### Bài Tập 9: Viết một script để sao lưu một tập tin và thêm ngày tháng vào tên tập tin sao lưu.

**Yêu cầu:** 

Tạo một file script backup_file.sh.

Nhập tên file cần sao lưu.

Tạo một bản sao của file đó với tên bao gồm ngày tháng hiện tại.

**Gợi ý:** 

### Bài Tập 10: Tạo Lệnh Crontab Để Chạy Script 5 Phút Một Lần

**Yêu cầu:** 

•Viết một Bash script tên run_script.sh in ra dòng chữ "Script dang chay" vào file output.log.

•Thiết lập một lệnh crontab để chạy script này 2 phút một lần.

**Gợi ý:** 

Tạo một script với tên run_script.sh có nội dung sau:

Cấp quyền thực thi cho script: chmod +x ~/run_script.sh

Thiết lập crontab để chạy script này mỗi 2 phút: chạy lệnh crontab -e sau đó thêm dòng sau vào cuối file: */2 * * * * /bin/bash ~/run_script.sh

Sau vài phút, kiểm tra nội dung file output.log để xem script đã chạy thành công chưa: cat ~/output.log

### Bài Tập 11: Tự Động Sao Lưu Thư Mục Hàng Ngày

**Yêu cầu:** 

Viết một script để sao lưu toàn bộ nội dung của thư mục ~/myfolder vào thư mục ~/backup.

Thiết lập crontab để sao lưu vào 2 giờ sáng hàng ngày.

**Gợi ý:** 

Tạo một script có tên backup.sh với nội dung:

Cấp quyền thực thi cho script: chmod +x ~/backup.sh

Thiết lập crontab để chạy script này chạy 2 giờ sáng hàng ngày: chạy lệnh crontab -e sau đó thêm dòng sau vào cuối file: 0 2 * * * /bin/bash ~/backup.sh

## Hướng dẫn khắc phục lỗi cơ bản network, services trên linux:

### Bài tập 1: Kiểm tra xem máy tính có kết nối Internet hay không

**Yêu cầu:** Kiểm tra kết nối đến google.com trên server

**Gợi ý lệnh:** ping -c 4 google.com

### Bài tập 2: Kiểm Tra Cấu Hình DNS

**Yêu cầu:** Kiểm tra cấu hình DNS trên server hiện tại và sửa lại cặp nameserver trỏ về 8.8.8.8 và 8.8.4.4

**Gợi ý:** 

Kiểm tra cấu hình DNS: cat /etc/resolv.conf

Dùng lệnh vi sửa file /etc/resolv.conf với cặp name server mới.

### Bài tập 3: Kiểm Tra phân giải DNS 

**Yêu cầu:** Kiểm tra domain hcmus.edu.vn có đang phân giải trên cặp nameserver 8.8.8.8 và 8.8.4.4 không

**Gợi ý lệnh:** dig hcmus.edu.vn

### Bài tập 4: Kiểm Tra RAM đang sử dụng 

**Yêu cầu:** kiểm tra tình trạng sử dụng RAM trên server

**Gợi ý lệnh:** free -m

### Bài tập 5: Kiểm Tra IP

**Yêu cầu:** kiểm tra các Ip và các interface đang có trên server

**Gợi ý lệnh:** ip addr

### Bài tập 6: Kiểm Tra IP gateway

**Yêu cầu:** Kiểm tra default gateway trên server

**Gợi ý lệnh:** ip route | grep default

### Bài tập 7: Kiểm tra RAM CPU các dịch vụ đang chạy

**Yêu cầu:** Kiểm tra RAM CPU các dịch vụ đang chạy theo thời gian thực

**Gợi ý lệnh:** top hoặc htop

### Bài tập 8: Kiểm tra các port đang lắng nghe trên server

**Yêu cầu:** Kiểm tra Nginx đang lắng nghe port nào trên server

**Gợi ý lệnh:** netstat -tlpn | grep nginx

### Bài tập 9: Kiểm tra firewall trên ubuntu

**Yêu cầu:** Kiểm tra ufw firewall trên Ubuntu có đang hoạt động hay không

**Gợi ý lệnh:** ufw status

### Bài tập 10: Thiết lập rule firewall trên ufw

**Yêu cầu:** Chỉ mở các port chiều mạng đi vào gồm port SSH(TCP 22), HTTP(TCP 80), đối với chiều mạng đi ra thì allow all

**Gợi ý các lệnh:** 

Chặn toàn bộ truy cập từ bên ngoài vào máy chủ: ufw default deny incoming

Cho phép allow kết nối từ máy chủ ra bên ngoài: ufw default allow outgoing

Mở kết nối SSH: ufw allow OpenSSH

Mở kết nối HTTP: ufw allow 80/tcp

Kiểm tra lại các rule đã thiết lập: ufw show added

kích hoạt UFW: ufw enable

Kiểm tra lại hoạt động của firewall: ufw status verbose