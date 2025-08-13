# N8N với Cloudflare Tunnel

Dự án này triển khai [n8n](https://n8n.io/) - một nền tảng automation workflow mạnh mẽ - kết hợp với Cloudflare Tunnel để tạo ra một giải pháp automation có thể truy cập từ bên ngoài một cách an toàn.

## 🚀 Tính năng

- **N8N**: Nền tảng automation workflow với giao diện web trực quan
- **Cloudflare Tunnel**: Tạo kết nối an toàn từ internet đến n8n instance
- **Docker Compose**: Triển khai dễ dàng với containerization
- **Persistent Storage**: Dữ liệu được lưu trữ bền vững
- **Production Ready**: Cấu hình tối ưu cho môi trường production

## 📋 Yêu cầu hệ thống

- Docker và Docker Compose
- Cloudflare account với Tunnel token
- Domain name (tùy chọn)

## 🛠️ Cài đặt

### 1. Clone repository

```bash
git clone https://github.com/vuongmanhnghia/n8n-compose.git
cd n8n
```

### 2. Tạo file môi trường

Tạo file `.env` trong thư mục gốc với các biến môi trường sau:

```env
# Cloudflare Tunnel
TUNNEL_TOKEN=your_cloudflare_tunnel_token

# Domain Configuration
SUBDOMAIN=your-subdomain
DOMAIN_NAME=your-domain.com

# Timezone
GENERIC_TIMEZONE=Asia/Ho_Chi_Minh
```

### 3. Khởi chạy services

```bash
docker-compose up -d
```

## 🔧 Cấu hình

### Cloudflare Tunnel

1. Đăng nhập vào Cloudflare Dashboard
2. Tạo một tunnel mới trong phần "Zero Trust" > "Access" > "Tunnels"
3. Copy tunnel token và thêm vào file `.env`

### N8N Configuration

Các biến môi trường chính:

- `N8N_HOST`: Hostname của n8n instance
- `N8N_PROTOCOL`: Protocol (https)
- `N8N_RUNNERS_ENABLED`: Bật tính năng runners
- `WEBHOOK_URL`: URL cho webhooks

## 📁 Cấu trúc dự án

```
.
├── README.md
├── compose.yaml          # Docker Compose configuration
├── .gitignore           # Git ignore rules
├── .env                 # Environment variables (tạo thủ công)
└── local-files/         # Thư mục chia sẻ với n8n
```

## 🌐 Truy cập

Sau khi khởi chạy thành công:

- **N8N Web Interface**: `https://your-subdomain.your-domain.com`
- **Local Access**: `http://127.0.0.1:5678`

## 🔒 Bảo mật

- N8N chỉ có thể truy cập từ localhost (127.0.0.1)
- Cloudflare Tunnel tạo kết nối an toàn từ internet
- Dữ liệu được mã hóa trong quá trình truyền tải
- File permissions được enforce

## 📊 Monitoring

### Kiểm tra trạng thái services

```bash
docker-compose ps
```

### Xem logs

```bash
# Tất cả services
docker-compose logs

# Chỉ n8n
docker-compose logs n8n

# Chỉ cloudflared
docker-compose logs cloudflared
```

## 🛠️ Troubleshooting

### N8N không khởi động

- Kiểm tra logs: `docker-compose logs n8n`
- Đảm bảo các biến môi trường được cấu hình đúng
- Kiểm tra quyền truy cập thư mục `local-files`

### Cloudflare Tunnel không hoạt động

- Kiểm tra TUNNEL_TOKEN có hợp lệ không
- Xem logs: `docker-compose logs cloudflared`
- Đảm bảo tunnel đã được tạo trong Cloudflare Dashboard

## 📝 Lưu ý

- Dữ liệu n8n được lưu trong Docker volume `n8n_data`
- Backup dữ liệu thường xuyên để tránh mất mát
- Cập nhật images định kỳ để có các tính năng mới nhất
