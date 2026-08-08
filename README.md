# 🖥️ RATUS — Remote Admin Trojan @ HCMUS

> **RATUS** = **R**emote **A**dmin **T**rojan + **US** (Ho Chi Minh University of Science)  
> Đồ án môn **Mạng Máy Tính** — Lớp 24TNT1TN, Khoa CNTT, ĐHKHTN – ĐHQG TP.HCM

---
## 📌 Giới thiệu

**RATUS** là hệ thống điều khiển máy tính từ xa trong mạng LAN, xây dựng trên mô hình **Client–Server** sử dụng giao thức **WebSocket** để truyền lệnh và dữ liệu theo thời gian thực.

- **Server** viết bằng **C++** (WinSock2), chạy trên máy mục tiêu (Target PC).
- **Client** là giao diện **Web** (HTML/CSS/JS), chạy trên máy điều khiển (Control PC).

---

## 👥 Thành viên

| Họ và tên | MSSV |
|---|---|
| Phạm Minh Đạt | 24120174 |
| Nguyễn Phước Khang | 24120189 |
| Huỳnh Bảo Khang | 24120507 |

**Giảng viên hướng dẫn:** Th.S Đỗ Hoàng Cường

---

## ⚙️ Chức năng chính

| Module | Chức năng |
|---|---|
| **Application Manager** | Liệt kê, khởi chạy, và dừng ứng dụng trên máy Server |
| **Process Manager** | Liệt kê tiến trình đang chạy, kết thúc theo PID |
| **Keylogger** | Bắt đầu/dừng ghi phím, truy xuất log bàn phím |
| **Live Screen** | Chụp ảnh màn hình máy Server theo yêu cầu |
| **Webcam Stream** | Quay video webcam (~10 giây) và gửi về Client |
| **System Power** | Tắt máy (Shutdown) và khởi động lại (Restart) từ xa |

---

## 🏗️ Kiến trúc hệ thống

```
[Control PC - Client]  <──WebSocket (LAN)──>  [Target PC - Server]
   index.html                                     server.exe (C++)
   console.html                                   Port 8081 (WebSocket)
   websocket.js                                   Port 8080 (HTTP file server)
   ui.js / command.js
```

- **TCP Socket** (WinSock2): nền tảng mở cổng mạng.
- **WebSocket Server**: nhận lệnh real-time từ trình duyệt.
- **HTTP Server**: phục vụ tải file video/ảnh dung lượng lớn.
- **Command Prefix Protocol**: phân loại lệnh và dữ liệu phản hồi.

---

## 🛠️ Công nghệ sử dụng

- **Server:** C++, WinSock2, Windows API, OpenCV (webcam/video), GDI (screenshot)
- **Client:** HTML5, CSS3 (Glassmorphism, Cyberpunk dark theme), Vanilla JavaScript
- **Giao thức:** WebSocket (RFC 6455), HTTP, TCP/IP

---

## 🚀 Hướng dẫn cài đặt

### Yêu cầu
- Cả hai máy phải cùng kết nối trong **một mạng LAN**.
- Tắt **Windows Defender / Antivirus** hoặc thêm thư mục vào **Exclusion list** trước khi chạy.

### Bước 1 — Tải chương trình

1. Tải file `Using.zip` từ repository này.
2. Giải nén, bạn sẽ nhận được hai thư mục: `Client/` và `Server/`.

### Bước 2 — Khởi động Server (máy bị điều khiển)

```bash
# Sao chép thư mục Server vào máy mục tiêu
# Chạy file thực thi
server.exe
```

Server sẽ tự động mở cổng lắng nghe (mặc định: **8080/8081**).

### Bước 3 — Kết nối Client (máy điều khiển)

1. Mở file `Client/index.html` bằng trình duyệt.
2. Nhấn **Launch Console** để vào trang điều khiển.
3. Nhập dải IP nội bộ (ví dụ: `192.168.1.`) → Nhấn **Scan**.
4. Chọn máy Server từ danh sách → Nhấn **Establish Connection**.

---

## 📁 Cấu trúc mã nguồn

```
.
├── Client/
│   ├── index.html          # Trang chủ (giao diện ACCESS GRANTED)
│   ├── console.html        # Trung tâm điều khiển
│   ├── about.html          # Thông tin dự án
│   ├── style.css           # Giao diện Cyberpunk dark mode
│   ├── websocket.js        # Tầng giao tiếp WebSocket & LAN scanner
│   ├── ui.js               # Xử lý hiển thị & data dispatcher
│   └── command.js          # Lớp trừu tượng hóa lệnh điều khiển
│
└── Server/
    ├── server.exe          # File thực thi (đã build sẵn)
    ├── WSServer.*          # WebSocket connection handler
    ├── ProcessManager.*    # Quản lý tiến trình
    ├── ApplicationManager.*# Quản lý ứng dụng
    ├── KeyController.*     # Keylogger module
    ├── Screenshot.*        # Chụp màn hình
    ├── Webcam.*            # Quay webcam (OpenCV)
    └── SystemControl.*     # Shutdown / Restart
```

---

## 📸 Giao diện

| Trang chủ | Command Center | Module điều khiển |
|:---:|:---:|:---:|
| ACCESS GRANTED screen | IP Scan & Connect | App / Process / Keylog / Screen / Webcam |

> Giao diện theo phong cách **Cyberpunk Dark Mode** với hiệu ứng Glassmorphism, Matrix Rain và Glitch text.

---

## 📚 Tài liệu tham khảo

- [WebSocket Protocol – RFC 6455](https://datatracker.ietf.org/doc/html/rfc6455)
- [OpenCV VideoCapture](https://docs.opencv.org/4.x/d8/dfe/classcv_1_1VideoCapture.html)
- [HTTP Protocol – MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- [Remote Administration Tool (RAT) – Research Paper](https://ijcsmc.com/docs/papers/March2014/V3I3201499a33.pdf)

---

> 🎓 **Trường Đại học Khoa học Tự nhiên – ĐHQG TP.HCM** | Khoa Công nghệ Thông tin | 24TNT1TN
