# Báo cáo: Quản lý File System

> **Lưu ý quan trọng:** Các bài tập từ 3–9 yêu cầu có đĩa `/dev/loop0` (thường là đĩa phụ trong VM). Đảm bảo VM đã được thêm đĩa phụ trước khi thực hiện. Các lệnh thao tác trên đĩa cần quyền `root` hoặc `sudo`.

## Bài tập 1: Kiểm tra không gian đĩa sử dụng

### Yêu cầu
Kiểm tra không gian đĩa đã sử dụng và còn trống.

### Thực hiện

```bash
df -h
```

- `-h`: hiển thị dung lượng dạng human-readable (GB, MB).

📸 **Screenshot 1**: Chụp kết quả — bảng hiển thị các phân vùng, dung lượng đã dùng, còn trống, % sử dụng.

![Screenshot 1 - Không gian đĩa](screenshots/06/df-h-disk-space.png)

---

## Bài tập 2: Kiểm tra các phân vùng trên hệ thống

### Yêu cầu
Liệt kê thông tin chi tiết các phân vùng.

### Thực hiện

```bash
sudo fdisk -l
```

📸 **Screenshot 2**: Chụp kết quả — danh sách tất cả đĩa và phân vùng (Disk /dev/sda, /dev/loop0,...), kích thước, loại phân vùng.

![Screenshot 2 - Danh sách phân vùng](screenshots/06/fdisk-list-partitions.png)

---

## Bài tập 3: Tạo phân vùng mới trên đĩa

### Yêu cầu
Tạo một phân vùng mới trên đĩa `/dev/loop0`.

### Hướng dẫn thực hiện

```bash
sudo fdisk /dev/loop0
```

Trong giao diện fdisk, thực hiện lần lượt:
1. Nhấn `n` → tạo phân vùng mới (new)
2. Nhấn `p` → chọn loại primary
3. Nhấn `Enter` để chấp nhận số phân vùng mặc định (1)
4. Nhấn `Enter` để chấp nhận sector bắt đầu mặc định
5. Nhấn `Enter` để chấp nhận sector kết thúc mặc định (dùng toàn bộ đĩa)
6. Nhấn `w` → ghi thay đổi và thoát (write)

*(Quan trọng đối với ổ đĩa ảo)* Cập nhật lại bảng phân vùng để hệ thống nhận diện phân vùng mới:

```bash
sudo partprobe /dev/loop0
```

Kiểm tra:

```bash
sudo fdisk -l /dev/loop0
```

📸 **Screenshot 3**: Chụp toàn bộ quá trình tương tác trong fdisk (từ lúc nhấn `n` đến `w`) và kết quả `fdisk -l` sau khi tạo.

![Screenshot 3 - Tạo phân vùng mới](screenshots/06/fdisk-create-partition.png)

---

## Bài tập 4: Định dạng phân vùng với file system

### Yêu cầu
Định dạng phân vùng `/dev/loop0p1` với file system `xfs`.

### Thực hiện

```bash
sudo mkfs.xfs /dev/loop0p1
```

📸 **Screenshot 4**: Chụp kết quả — thông tin format thành công (data blocks, naming,...).

![Screenshot 4 - Định dạng xfs](screenshots/06/mkfs-xfs-format.png)

---

## Bài tập 5: Gắn phân vùng vào hệ thống

### Yêu cầu
Gắn (mount) phân vùng `/dev/loop0p1` vào thư mục `/mnt/new_partition`.

### Thực hiện

```bash
sudo mkdir -p /mnt/new_partition
sudo mount /dev/loop0p1 /mnt/new_partition
```

Kiểm tra:

```bash
df -h | grep loop0p1
```

📸 **Screenshot 5**: Chụp kết quả `df -h` — phân vùng `/dev/loop0p1` đã mount vào `/mnt/new_partition`.

![Screenshot 5 - Mount phân vùng](screenshots/06/mount-loop0p1.png)

---

## Bài tập 6: Gỡ phân vùng ra khỏi hệ thống

### Yêu cầu
Gỡ (unmount) phân vùng `/dev/loop0p1`.

### Thực hiện

```bash
sudo umount /mnt/new_partition
```

Kiểm tra:

```bash
df -h | grep loop0p1
```

📸 **Screenshot 6**: Chụp kết quả — `grep loop0p1` không trả về kết quả, chứng tỏ đã unmount thành công.

![Screenshot 6 - Unmount phân vùng](screenshots/06/umount-loop0p1.png)

---

## Bài tập 7: Tự động gắn phân vùng khi khởi động

### Yêu cầu
Cấu hình phân vùng `/dev/loop0p1` tự động mount vào `/mnt/new_partition` khi boot.

### Hướng dẫn thực hiện

#### Bước 1: Mở file fstab

```bash
sudo vi /etc/fstab
```

#### Bước 2: Thêm dòng sau vào cuối file

```
/dev/loop0p1   /mnt/new_partition   xfs   defaults   0   2
```

> Nhấn `i` để vào chế độ chỉnh sửa, thêm dòng, nhấn `Esc` rồi gõ `:wq` để lưu và thoát.

#### Bước 3: Kiểm tra cấu hình

```bash
cat /etc/fstab
```

📸 **Screenshot 7**: Chụp nội dung file `/etc/fstab` — dòng cấu hình mới nằm ở cuối file.

![Screenshot 7 - Cấu hình fstab](screenshots/06/fstab-config.png)

#### Bước 4: Test mount bằng fstab

```bash
sudo mount -a
df -h | grep loop0p1
```

📸 **Screenshot 8**: Chụp kết quả — phân vùng đã được mount thành công thông qua fstab.

![Screenshot 8 - Mount qua fstab](screenshots/06/mount-a-fstab-test.png)

---

## Bài tập 8: Xóa partition và gỡ cấu hình fstab

### Yêu cầu
Xóa tất cả partition trên `/dev/loop0` và xóa cấu hình tương ứng trong `/etc/fstab`.

> ⚠️ **CẢNH BÁO:** Nếu xóa partition mà không xóa cấu hình fstab, hệ thống sẽ **KHÔNG THỂ KHỞI ĐỘNG** khi reboot!

### Hướng dẫn thực hiện

#### Bước 1: Unmount trước khi xóa

```bash
sudo umount /mnt/new_partition
```

#### Bước 2: Xóa partition bằng fdisk

```bash
sudo fdisk /dev/loop0
```

Trong fdisk:
1. Nhấn `d` → xóa phân vùng (delete)
2. Nhấn `w` → ghi thay đổi và thoát

#### Bước 3: Xóa dòng cấu hình trong fstab

```bash
sudo vi /etc/fstab
```

> Tìm dòng `/dev/loop0p1   /mnt/new_partition   xfs   defaults   0   2` và xóa nó. Trong vi: di chuyển con trỏ đến dòng đó, nhấn `dd` để xóa, sau đó `:wq` để lưu.

#### Bước 4: Kiểm tra

```bash
sudo fdisk -l /dev/loop0
cat /etc/fstab
```

📸 **Screenshot 9**: Chụp kết quả fdisk (không còn partition) và nội dung fstab (dòng loop0p1 đã bị xóa).

![Screenshot 9 - Xóa partition và fstab](screenshots/06/delete-partition-fstab.png)

---

## Bài tập 9: Tạo và quản lý LVM (Physical Volume, Volume Group, Logical Volume)

### Yêu cầu
- Tạo Physical Volume từ `/dev/loop0`.
- Tạo Volume Group `vg_data`.
- Tạo Logical Volume `lv_data` 5GB.
- Format ext4 và mount vào `/mnt/data`.

### Hướng dẫn thực hiện

#### Bước 1: Tạo Physical Volume

```bash
sudo pvcreate /dev/loop0
```

📸 **Screenshot 10**: Chụp kết quả — "Physical volume ... successfully created".

![Screenshot 10 - Tạo Physical Volume](screenshots/06/pvcreate.png)

#### Bước 2: Tạo Volume Group

```bash
sudo vgcreate vg_data /dev/loop0
```

📸 **Screenshot 11**: Chụp kết quả — "Volume group \"vg_data\" successfully created".

![Screenshot 11 - Tạo Volume Group](screenshots/06/vgcreate.png)

#### Bước 3: Tạo Logical Volume 5GB

```bash
sudo lvcreate -L 5G -n lv_data vg_data
```

📸 **Screenshot 12**: Chụp kết quả — "Logical volume \"lv_data\" created".

![Screenshot 12 - Tạo Logical Volume](screenshots/06/lvcreate.png)

#### Bước 4: Format ext4

```bash
sudo mkfs.ext4 /dev/vg_data/lv_data
```

📸 **Screenshot 13**: Chụp kết quả — thông tin format ext4 thành công.

![Screenshot 13 - Format ext4](screenshots/06/mkfs-ext4-lv.png)

#### Bước 5: Mount và kiểm tra

```bash
sudo mkdir -p /mnt/data
sudo mount /dev/vg_data/lv_data /mnt/data
df -h /mnt/data
```

📸 **Screenshot 14**: Chụp kết quả `df -h` — logical volume đã mount vào `/mnt/data` với kích thước ~5GB.

![Screenshot 14 - Mount Logical Volume](screenshots/06/mount-lv-data.png)

---

## Tổng hợp Screenshot cần chụp

| # | Nội dung screenshot | Lệnh liên quan |
|---|---------------------|-----------------|
| 1 | Không gian đĩa hiện tại | `df -h` |
| 2 | Danh sách phân vùng | `sudo fdisk -l` |
| 3 | Quá trình tạo partition + kết quả | `sudo fdisk /dev/loop0` + `sudo fdisk -l /dev/loop0` |
| 4 | Format xfs thành công | `sudo mkfs.xfs /dev/loop0p1` |
| 5 | Mount partition thành công | `df -h \| grep loop0p1` |
| 6 | Unmount thành công | `df -h \| grep loop0p1` |
| 7 | Nội dung fstab có dòng mới | `cat /etc/fstab` |
| 8 | Mount thông qua fstab | `sudo mount -a` + `df -h` |
| 9 | Xóa partition + xóa fstab | `sudo fdisk -l /dev/loop0` + `cat /etc/fstab` |
| 10 | Tạo PV thành công | `sudo pvcreate /dev/loop0` |
| 11 | Tạo VG thành công | `sudo vgcreate vg_data /dev/loop0` |
| 12 | Tạo LV thành công | `sudo lvcreate -L 5G -n lv_data vg_data` |
| 13 | Format ext4 thành công | `sudo mkfs.ext4 /dev/vg_data/lv_data` |
| 14 | LV mount vào /mnt/data | `df -h /mnt/data` |
