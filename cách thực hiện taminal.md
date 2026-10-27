# CÁCH THỰC HIỆN TERMINAL  POWERSHELL
### Tạo thư mục gốc + 4 thư mục con (1 dòng lệnh duy nhất)

powershell

```
mkdir smartfarm-system; cd smartfarm-system; mkdir docs, scripts, data, backup

```

### 2. Tạo tệp `.env` ở thư mục gốc từ trong `data/` — dùng đường dẫn tương đối

powershell

```
cd data; "DB_PASSWORD=demo_123456" | Out-File -FilePath ../.env -Encoding utf8

```

### 3. Đặt thuộc tính Ẩn cho tệp `.env`

powershell

```
Set-ItemProperty -Path ../.env -Name Attributes -Value Hidden

```

----------

## Phiên bản gộp toàn bộ trong 1 chuỗi lệnh liên tiếp

powershell

```
mkdir smartfarm-system; cd smartfarm-system; mkdir docs, scripts, data, backup; cd data; "DB_PASSWORD=demo_123456" | Out-File -FilePath ../.env -Encoding utf8; Set-ItemProperty -Path ../.env -Name Attributes -Value Hidden

```

----------

## Kiểm tra kết quả  Cấu trúc thư mục



```
smartfarm-system/
docs/
 scripts/
 data/
  backup/
  .env   Tệp ẩn, nội dung: DB_PASSWORD=demo_123456

```


