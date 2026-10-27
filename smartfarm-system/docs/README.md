


# Hệ thống Giám sát và Xử lý Log Thiết bị

## Hướng dẫn chạy script

bash

```
# Cập nhật quyền thực thi
chmod +x scripts/process_log.sh

```

## Checklist kiểm tra thiết bị

- [X]   Kiểm tra trạng thái kết nối mạng giữa trung tâm và các trạm cảm biến
- [ ]  Xác minh dung lượng lưu trữ khả dụng trên máy chủ thu thập log
- [ ] Kiểm tra phiên bản phần mềm và quyền truy cập dịch vụ giám sát
- [ ]  Đo băng thông thực tế đường truyền tại các trạm từ xa

## Bảng thông số phần cứng

|Tên thiết bị|Đơn giá (VNĐ)|Loại lưu trữ|
|-|-|-| 
|Bộ điều khiển trung tâm CNTT-01|8.500.000|SSD NVMe 512GB |
| Module thu thập dữ liệu trạm từ xa|2.350.000|eMMC 32GB tích hợp|
|Thiết bị ghi log chuyên dụng|4.100.000|HDD 2TB SATA 3.5"|

## Phân tích hệ thống

### Luồng xử lý lọc loG

|Thành phần|Mô tả|
|-|-|
|**Input**|Tệp log thô (định dạng `.log`/`.txt`), dấu thời gian, mức độ cảnh báo, mã thiết bị, nội dung thông báo lỗi|
|**Process**|Đọc luồng tệp => chuẩn hóa định dạng thời gian => lọc theo điều kiện (mức lỗi, khoảng ngày, mã trạm) 
|**Output**|Tệp log đã lọc sạch, bảng thống kê số lỗi theo thiết bị, tóm tắt xu hướng sự cố, báo cáo cảnh báo vượt ngưỡng| 

### Phân loại theo mô hình DIKW



|Tầng DIKW|HÀNH ĐỘNG 
|-|-
|**Wisdom (Trí tuệ)**| Hành động/quyết định dựa trên kiến thức đã phân tích, bao gồm thời gian thực hiện|
|**Data (Dữ liệu)**|Quan sát thô, giá trị riêng lẻ chưa xử lý ngữ cảnh|
|**Information (Thông tin)**|Dữ liệu đã được tổng hợp, có so sánh, gắn bối cảnh|
|**Knowledge (Kiến thức)**|Liên kết nguyên nhân-kết quả, rút ra quy luật và hướng giải quyết|

## Bẫy phần cứng  Tính thời gian tải log

### Phép quy đổi

-   Đơn vị đường truyền: **Mbps** = Megabit/giây
-   Đơn vị dung lượng tệp: **MB** = Megabyte
-   Hệ số quy đổi: **1 Byte = 8 bit** ⇒ `Tốc độ (MB/s) = Tốc độ (Mbps) ÷ 8`

### Tính toán

1.  Tốc độ thực tế:

100 Mbps ÷ 8 = 12,5 MB/giây


2.  Thời gian tải:

Thời gian = Dung lượng ÷ Tốc độ
          = 500 MB ÷ 12,5 MB/s
          = 40 giây

**Kết quả:** Tải tệp log 500 MB qua đường truyền 100 Mbps cần **40 giây**
