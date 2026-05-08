# End-to-End Encrypted Chat Application (Web Chat E2EE)

[![React](https://img.shields.io/badge/Frontend-React%20%2B%20TypeScript-61DAFB?style=flat-square&logo=react&logoColor=black)](https://reactjs.org/)
[![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![MongoDB](https://img.shields.io/badge/Database-MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![E2EE](https://img.shields.io/badge/Security-E2E%20Encryption-FF9900?style=flat-square&logo=letsencrypt&logoColor=white)]()

> **Đồ án:** Môn học Mạng máy tính và Truyền thông dữ liệu
> **Giảng viên hướng dẫn:** TS. Trần Thanh Nam
> **Đơn vị:** Khoa Công nghệ thông tin - Trường Đại học Tôn Đức Thắng (TDTU)

## 📝 Giới thiệu
Dự án xây dựng một ứng dụng nhắn tin thời gian thực trên nền tảng Web theo mô hình **Zero-Knowledge Architecture**. Hệ thống áp dụng cơ chế **Mã hóa đầu - cuối (End-to-End Encryption - E2EE)**, đảm bảo nội dung tin nhắn chỉ có thể được giải mã tại thiết bị của người dùng. Máy chủ chỉ đóng vai trò định tuyến các bản mã (ciphertext) và hoàn toàn không có khả năng truy cập vào nội dung gốc hay khóa bí mật.

## 👥 Nhóm phát triển
| MSSV | Họ và tên |
| :--- | :--- |
| **52200292** | Nguyễn Văn Hậu |
| **52200319** | Võ Mạnh Cường |

## 🚀 Tính năng nổi bật
- [x] **Mã hóa đầu-cuối (E2EE):** Bảo mật toàn diện cho cả hội thoại cá nhân (1-1) và hội thoại nhóm.
- [x] **Hỗ trợ đa thiết bị (Multi-device Support):** Mỗi thiết bị tự sinh và quản lý cặp khóa riêng biệt. Không cần chia sẻ private key giữa các thiết bị.
- [x] **Giao tiếp thời gian thực:** Đồng bộ trạng thái và tin nhắn tức thời với độ trễ thấp thông qua giao thức WebSocket.
- [x] **Xử lý ngoại tuyến (Offline Support):** Cơ chế "Pending Session Keys" lưu trữ tạm thời khóa phiên an toàn khi người nhận không trực tuyến.
- [x] **Bảo vệ khóa cục bộ:** Private key được mã hóa bằng thuật toán dẫn xuất khóa từ mã PIN (PBKDF2) trước khi lưu vào IndexedDB.

## 🧠 Kiến trúc & Bảo mật
Hệ thống kết hợp sức mạnh của nhiều chuẩn mật mã công nghiệp thông qua **Web Cryptography API**:
1. **Bảo mật nội dung (AES-256-GCM):** Mã hóa xác thực nội dung tin nhắn, đảm bảo tính bí mật và tính toàn vẹn (chống giả mạo, replay attack).
2. **Trao đổi khóa (RSA-2048 OAEP & PSS):** - *RSA-OAEP:* Bao gói an toàn khóa phiên đối xứng (Session Key).
   - *RSA-PSS:* Ký số (Digital Signature) xác thực nguồn gốc khóa, chống tấn công Man-in-the-Middle (MITM).
3. **Định danh thiết bị (SHA-256):** Băm public key thành Fingerprint để nhận diện và áp dụng cơ chế *Trust On First Use (TOFU)*.
4. **Bảo mật mật khẩu & xác thực:** Bcrypt cho mật khẩu, JSON Web Token (JWT) cho phiên làm việc.

## 🛠 Công nghệ sử dụng
* **Frontend:** React 19, TypeScript, Vite, Zustand, Socket.io-client.
* **Backend:** Python, FastAPI, WebSockets, python-jose, bcrypt.
* **Database:** MongoDB (kết hợp với Beanie ODM cho thao tác Async).
* **Kiểm thử:** Vitest (Frontend), Pytest (Backend) với độ bao phủ 108 Test Cases.

## 💻 Hướng dẫn cài đặt

### 1. Backend (FastAPI)
```bash
# Tạo môi trường ảo và kích hoạt
python -m venv venv
source venv/bin/activate  # Linux/Mac
# .\venv\Scripts\activate # Windows

# Cài đặt thư viện
pip install -r requirements.txt

# Khởi chạy server
uvicorn app.main:app --reload --port 8000
```

### 2. Frontend (React/Vite)
```bash
# Cài đặt các gói phụ thuộc
npm install

# Khởi chạy môi trường phát triển
npm run dev
```

### 3. Cấu hình biến môi trường (.env)
Tạo file `.env` tại thư mục backend chứa các biến cần thiết:
```env
MONGO_URI=mongodb://localhost:27017/chat_e2ee
JWT_SECRET=your_super_secret_key
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE=30
CORS_ORIGINS=http://localhost:5173
```

---
*Dự án thực hiện tại TP. Hồ Chí Minh – 2025*
