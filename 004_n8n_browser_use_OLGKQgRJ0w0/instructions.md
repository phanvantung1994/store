# Presequigties

- uv: https://docs.astral.sh/uv/getting-started/installation/#__tabbed_1_1
- git: https://git-scm.com/downloads
- nvm/node/npm: https://nodejs.org/en/download
- pm2: https://pm2.keymetrics.io/
- https://github.com/draphonix/browser-n8n-local

# Install browser-n8n-local

1. Clone project

```
git clone https://github.com/draphonix/browser-n8n-local.git
```

2. Vào thư mục vừa clone

```
cd <path_to_clone>
```

3. Tạo môi trường ảo bằng uv

```
uv venv --python 3.11
```

4. Activate môi trường ảo

```
source .venv/bin/activate 
```

5. Cài các thư viện

```
uv pip install -r requirements.txt
```

6. Tạo file env

```
cp .env-example .env
```

7. Chỉnh env file

8. Chạy Server

```
pm2 start "uvicorn app:app --host 0.0.0.0 --port 24006" --name browser-n8n-local-server
```
8. Chạy Server win 11
Nhớ là phải thêm PATH cho hệ thống win 11 và restart lại pc không là nó ko ăn. ví dụ ở đây là:
C:\Users\Eyeclick\Documents\Home\N8N\n8n-browser-locall\browser-n8n-local\.venv\Scripts\
Cấu hình ecosystem.config.js (Cách tốt nhất nếu dùng PM2 lâu dài) ( thêm 2 file start_uvicorn.ps1 và ecosystem.config.js) sau đó chạy lệnh:
```
pm2 start ecosystem.config.js
```
File start_uvicorn.ps1: 
```
.venv\Scripts\Activate
uvicorn app:app --host 0.0.0.0 --port 24006
```
File ecosystem.config.js:
```
module.exports = {
  apps: [
    {
      name: 'browser-n8n-local-server',
      script: 'uvicorn',
      args: 'app:app --host 0.0.0.0 --port 24006',
      interpreter: 'none',
      cwd: './',
    }
  ]
};

```

```
pm2 status
pm2 stop 0
pm2 delete 0
pm2 start 0
pm2 logs
```
### Khi shutdown PC bật lại server thì làm cách sau:
a. vào thư mục dự án
b. kích hoạt môi trường ảo:
```
.\.venv\Scripts\Activate

```
c. Nếu PM2 đã chạy trước đó, bạn có thể sử dụng lệnh sau để khôi phục các ứng dụng đã được quản lý:
```
pm2 resurrect

```
d. nếu ko thích thì chạy pm2 lại thủ công như trên.

## Install n8n-nodes-browser-use trên n8n

1. Thêm biến vào env và chạy lại n8n

```
N8N_COMMUNITY_PACKAGES_ALLOW_TOOL_USAGE=true n8n start
```

1. Cài từ giao diện n8n

```
1. Settings > Community nodes > Install Community nodes
2. n8n-nodes-browser-use
```
