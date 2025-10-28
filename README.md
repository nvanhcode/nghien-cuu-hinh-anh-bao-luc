# Hướng Dẫn Chạy Server Node.js với PM2

## 📋 Yêu cầu hệ thống

- Node.js (phiên bản 14 trở lên)
- npm hoặc yarn
- PM2 (Process Manager)

## 🚀 Cài đặt và khởi chạy

### 1. Cài đặt dependencies

```bash
# Di chuyển vào thư mục dự án
cd /Users/nguyenvananh/Downloads/nghien-cuu-phan-dong

# Cài đặt các package cần thiết
npm install
```

### 2. Cài đặt PM2 (nếu chưa có)

```bash
# Cài đặt PM2 globally
npm install -g pm2
```

### 3. Khởi chạy server với PM2

```bash
# Khởi chạy bằng ecosystem config
pm2 start ecosystem.config.js

# Hoặc khởi chạy trực tiếp
pm2 start server.js --name "nghien-cuu-phan-dong"
```

### 4. Kiểm tra trạng thái

```bash
# Xem danh sách các process
pm2 list

# Xem logs
pm2 logs nghien-cuu-phan-dong

# Xem thông tin chi tiết
pm2 show nghien-cuu-phan-dong
```

## 🔧 Các lệnh PM2 hữu ích

### Quản lý process

```bash
# Dừng process
pm2 stop nghien-cuu-phan-dong

# Khởi động lại
pm2 restart nghien-cuu-phan-dong

# Reload (zero downtime)
pm2 reload nghien-cuu-phan-dong

# Xóa process
pm2 delete nghien-cuu-phan-dong

# Dừng tất cả
pm2 stop all

# Khởi động lại tất cả
pm2 restart all
```

### Monitoring

```bash
# Xem realtime monitoring
pm2 monit

# Xem logs realtime
pm2 logs --lines 100

# Xem logs của process cụ thể
pm2 logs nghien-cuu-phan-dong --lines 50
```

### Startup và Save

```bash
# Tạo startup script để PM2 tự khởi động khi reboot
pm2 startup

# Lưu danh sách process hiện tại
pm2 save

# Khôi phục các process đã lưu
pm2 resurrect
```

## 🌐 Truy cập ứng dụng

Sau khi khởi chạy thành công, bạn có thể truy cập:

- **URL**: http://localhost:3000
- **Server sẽ serve**: file `index.html` và thư mục `images/`

## 📁 Cấu trúc dự án

```
nghien-cuu-phan-dong/
├── server.js              # Server chính
├── package.json           # Dependencies
├── ecosystem.config.js    # Cấu hình PM2
├── index.html            # Trang chính
├── images/              # Thư mục hình ảnh
└── logs/               # Thư mục logs
    ├── combined.log    # Log tổng hợp
    ├── out.log        # Log output
    └── error.log      # Log lỗi
```

## ⚙️ Cấu hình nâng cao

### Thay đổi port

Sửa file `ecosystem.config.js`:

```javascript
env: {
  NODE_ENV: 'production',
  PORT: 8080  // Thay đổi port tại đây
}
```

### Chạy nhiều instances

```javascript
instances: 'max',  // Sử dụng tất cả CPU cores
// hoặc
instances: 4,      // Chạy 4 instances
```

### Auto restart khi có thay đổi

```javascript
watch: true,
ignore_watch: ['node_modules', 'logs']
```

## 🐛 Troubleshooting

### Lỗi port đã được sử dụng

```bash
# Kiểm tra process đang dùng port 3000
lsof -i :3000

# Kill process
kill -9 <PID>
```

### Lỗi permission

```bash
# Sử dụng sudo nếu cần thiết
sudo pm2 start ecosystem.config.js
```

### Reset PM2

```bash
# Xóa tất cả process và reset
pm2 kill
pm2 resurrect
```

## 📝 Scripts có sẵn

```bash
# Chạy development mode
npm run dev

# Chạy production mode
npm start
```

## 🔄 Update và Deployment

```bash
# Update code và restart
git pull
npm install
pm2 reload nghien-cuu-phan-dong
```

---

**Lưu ý**: Đảm bảo tất cả các file hình ảnh trong thư mục `images/` có quyền truy cập phù hợp để server có thể serve chúng.