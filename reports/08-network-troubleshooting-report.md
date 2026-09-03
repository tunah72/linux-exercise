# Báo cáo: Khắc phục lỗi cơ bản Network & Services

## Bài tập 1: Kiểm tra kết nối Internet

### Yêu cầu
Kiểm tra kết nối đến `google.com` trên server.

### Thực hiện

```bash
ping -c 4 google.com
```

- `-c 4`: gửi 4 gói ICMP rồi dừng.

📸 **Screenshot 1**: Chụp kết quả — 4 gói gửi đi, số gói nhận lại, thời gian trung bình (avg). Nếu kết nối thành công sẽ thấy `0% packet loss`.

![Screenshot 1 - Ping google.com](screenshots/08/ping-google.png)

---

## Bài tập 2: Kiểm tra cấu hình DNS

### Yêu cầu
Kiểm tra cấu hình DNS hiện tại và sửa nameserver thành `8.8.8.8` và `8.8.4.4`.

### Hướng dẫn thực hiện

#### Bước 1: Kiểm tra cấu hình DNS hiện tại

```bash
cat /etc/resolv.conf
```

📸 **Screenshot 2**: Chụp kết quả — nội dung file `resolv.conf` trước khi sửa.

![Screenshot 2 - Cấu hình DNS trước khi sửa](screenshots/08/dns-before-edit.png)

#### Bước 2: Sửa file resolv.conf

```bash
sudo vi /etc/resolv.conf
```

> Sửa nội dung thành:
> ```
> nameserver 8.8.8.8
> nameserver 8.8.4.4
> ```
> Nhấn `i` để vào chế độ insert, sửa xong nhấn `Esc` rồi gõ `:wq`.

#### Bước 3: Kiểm tra lại

```bash
cat /etc/resolv.conf
```

📸 **Screenshot 3**: Chụp kết quả — file đã có 2 dòng nameserver `8.8.8.8` và `8.8.4.4`.

![Screenshot 3 - Cấu hình DNS sau khi sửa](screenshots/08/dns-after-edit.png)

---

## Bài tập 3: Kiểm tra phân giải DNS

### Yêu cầu
Kiểm tra domain `hcmus.edu.vn` phân giải trên nameserver `8.8.8.8` và `8.8.4.4`.

### Thực hiện

```bash
dig hcmus.edu.vn @8.8.8.8
dig hcmus.edu.vn @8.8.4.4
```

> Nếu chưa có lệnh `dig`, cài đặt: `sudo apt install dnsutils -y`

📸 **Screenshot 4**: Chụp kết quả `dig` — phần `ANSWER SECTION` hiển thị IP phân giải được, `SERVER` hiển thị nameserver đã dùng.

![Screenshot 4 - Phân giải DNS hcmus.edu.vn](screenshots/08/dig-hcmus.png)

---

## Bài tập 4: Kiểm tra RAM đang sử dụng

### Yêu cầu
Kiểm tra tình trạng sử dụng RAM trên server.

### Thực hiện

```bash
free -m
```

- `-m`: hiển thị dung lượng theo MB.

📸 **Screenshot 5**: Chụp kết quả — bảng hiển thị total, used, free, shared, buff/cache, available cho cả Mem và Swap.

![Screenshot 5 - Trạng thái RAM](screenshots/08/free-ram.png)

---

## Bài tập 5: Kiểm tra IP

### Yêu cầu
Kiểm tra các IP và interface đang có trên server.

### Thực hiện

```bash
ip addr
```

📸 **Screenshot 6**: Chụp kết quả — danh sách các interface (lo, eth0/ens33,...) kèm địa chỉ IP.

![Screenshot 6 - Danh sách IP và interface](screenshots/08/ip-addr.png)

---

## Bài tập 6: Kiểm tra IP gateway

### Yêu cầu
Kiểm tra default gateway trên server.

### Thực hiện

```bash
ip route | grep default
```

📸 **Screenshot 7**: Chụp kết quả — dòng `default via X.X.X.X dev <interface>`.

![Screenshot 7 - Default gateway](screenshots/08/ip-route-gateway.png)

---

## Bài tập 7: Kiểm tra RAM, CPU các dịch vụ đang chạy

### Yêu cầu
Kiểm tra RAM, CPU các dịch vụ đang chạy theo thời gian thực.

### Thực hiện

```bash
top
```

> Hoặc nếu đã cài `htop`:
> ```bash
> htop
> ```
> Nhấn `q` để thoát.

📸 **Screenshot 8**: Chụp màn hình `top` hoặc `htop` — hiển thị load average, danh sách process với %CPU, %MEM, PID,...

![Screenshot 8 - Giám sát CPU và RAM](screenshots/08/top-htop.png)

---

## Bài tập 8: Kiểm tra các port đang lắng nghe

### Yêu cầu
Kiểm tra Nginx đang lắng nghe port nào.

### Hướng dẫn thực hiện

#### Bước 1: Đảm bảo nginx đang chạy

```bash
sudo systemctl start nginx
```

#### Bước 2: Kiểm tra port

```bash
sudo netstat -tlpn | grep nginx
```

> Nếu chưa có `netstat`, cài đặt: `sudo apt install net-tools -y`

- `-t`: chỉ hiển thị TCP
- `-l`: chỉ hiển thị port đang LISTEN
- `-p`: hiển thị PID/tên tiến trình
- `-n`: hiển thị port dạng số

📸 **Screenshot 9**: Chụp kết quả — nginx đang LISTEN trên port `80` (và có thể `443`).

![Screenshot 9 - Port nginx đang lắng nghe](screenshots/08/netstat-nginx-port.png)

---

## Bài tập 9: Kiểm tra firewall trên Ubuntu

### Yêu cầu
Kiểm tra `ufw` firewall có đang hoạt động không.

### Thực hiện

```bash
sudo ufw status
```

📸 **Screenshot 10**: Chụp kết quả — `Status: active` hoặc `Status: inactive`.

![Screenshot 10 - Trạng thái firewall](screenshots/08/ufw-status.png)

---

## Bài tập 10: Thiết lập rule firewall trên ufw

### Yêu cầu
- Chặn tất cả kết nối đi vào (incoming).
- Cho phép tất cả kết nối đi ra (outgoing).
- Chỉ mở port SSH (TCP 22) và HTTP (TCP 80) chiều vào.

### Hướng dẫn thực hiện

#### Bước 1: Thiết lập chính sách mặc định

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

#### Bước 2: Mở port SSH

```bash
sudo ufw allow OpenSSH
```

#### Bước 3: Mở port HTTP

```bash
sudo ufw allow 80/tcp
```

#### Bước 4: Kiểm tra các rule đã thêm

```bash
sudo ufw show added
```

📸 **Screenshot 11**: Chụp kết quả — danh sách các rule đã thêm (OpenSSH, 80/tcp).

![Screenshot 11 - Các rule firewall đã thêm](screenshots/08/ufw-rules-added.png)

#### Bước 5: Kích hoạt UFW

```bash
sudo ufw enable
```

> Hệ thống sẽ hỏi xác nhận — nhấn `y` rồi Enter.

#### Bước 6: Kiểm tra trạng thái chi tiết

```bash
sudo ufw status verbose
```

📸 **Screenshot 12**: Chụp kết quả — firewall `active`, default policy (deny incoming, allow outgoing), và các rule cho SSH + HTTP.

![Screenshot 12 - Firewall active chi tiết](screenshots/08/ufw-status-verbose.png)

---

## Tổng hợp Screenshot cần chụp

| # | Nội dung screenshot | Lệnh liên quan |
|---|---------------------|-----------------|
| 1 | Kết quả ping google.com | `ping -c 4 google.com` |
| 2 | DNS config trước khi sửa | `cat /etc/resolv.conf` |
| 3 | DNS config sau khi sửa | `cat /etc/resolv.conf` |
| 4 | Phân giải DNS hcmus.edu.vn | `dig hcmus.edu.vn @8.8.8.8` |
| 5 | Trạng thái RAM | `free -m` |
| 6 | Danh sách IP và interface | `ip addr` |
| 7 | Default gateway | `ip route \| grep default` |
| 8 | Tiến trình CPU/RAM realtime | `top` hoặc `htop` |
| 9 | Port nginx đang LISTEN | `sudo netstat -tlpn \| grep nginx` |
| 10 | Trạng thái firewall | `sudo ufw status` |
| 11 | Các rule firewall đã thêm | `sudo ufw show added` |
| 12 | Firewall active + chi tiết | `sudo ufw status verbose` |
