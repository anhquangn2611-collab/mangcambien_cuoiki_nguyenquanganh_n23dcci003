# ĐỀ TÀI: PHÁT HIỆN TRẠNG THÁI NẮP CHAI BẰNG CÔNG NGHỆ TINYML

**Tiểu luận môn học:** Mạng cảm biến
**Giảng viên hướng dẫn:** Hồ Nhựt Minh

## 1. Thành viên thực hiện
* **Họ và tên:** Nguyễn Quang Anh
* **MSSV:** N23DCCI003
* **Lớp:** D23CQCI01-N

## 2. Giới thiệu dự án
Dự án xây dựng một hệ thống thị giác máy tính hoạt động cục bộ trên thiết bị biên (Edge AI) để nhận diện và phân biệt theo thời gian thực 2 trạng thái của chai nước:
* **closed**: Trạng thái nắp chưa mở.
* **opened**: Trạng thái nắp đã mở (miệng chai trống).
Mô hình sử dụng thuật toán nhận diện vật thể siêu nhẹ FOMO (Faster Objects, More Objects) được tối ưu hóa lượng tử hóa Int8 bằng nền tảng Edge Impulse, xuất bản dưới dạng WebAssembly để chạy mượt mà ngay trên trình duyệt web.

## 3. Mô tả thư mục (Cấu trúc Source Code)
* `index.html`: Giao diện ứng dụng Web tĩnh dùng để hiển thị Camera và kết quả nhận diện (Bounding Box) theo thời gian thực.
* `edge-impulse-standalone.wasm`: Lõi mạng nơ-ron định dạng nhị phân WebAssembly chứa các ma trận trọng số đã được huấn luyện.
* `edge-impulse-standalone.js`: Thư viện JavaScript cầu nối để giao tiếp với file `.wasm`.
* `run-impulse.js`: Chứa thuật toán tiền xử lý ảnh đầu vào (resize về 96x96, chuẩn hóa) và đưa vào lõi học máy.
* `server.py`: Mã nguồn Python dùng để khởi tạo một local server giả lập (nếu cần thiết).

## 4. Hướng dẫn cài đặt và chạy thử nghiệm
Để chạy thực nghiệm mô hình phân loại qua Camera, bạn có thể sử dụng 1 trong 2 cách sau:

**Cách 1: Chạy trực tiếp qua Local Server (Khuyên dùng để tránh lỗi bảo mật CORS)**
1. Tải toàn bộ mã nguồn về máy tính.
2. Mở cửa sổ dòng lệnh (Terminal/Command Prompt) tại thư mục vừa giải nén.
3. Gõ lệnh: `python server.py` (hoặc `python3 server.py`).
4. Mở trình duyệt web, truy cập vào đường dẫn: `http://localhost:8000`
5. Nhấn **Allow (Cho phép)** khi trình duyệt yêu cầu quyền truy cập Camera. Đưa chai nước vào trước ống kính để hệ thống nhận diện.

**Cách 2: Mở file trực tiếp**
1. Tải toàn bộ mã nguồn về máy tính.
2. Click đúp chuột vào file `index.html` để mở bằng trình duyệt (Chrome, Edge, Safari...).
3. Cấp quyền truy cập Camera cho ứng dụng web.

## 5. Các phụ thuộc (Dependencies)
Dự án chạy hoàn toàn độc lập (Standalone) bằng mã web tĩnh, không yêu cầu cài đặt framework phức tạp. Tuy nhiên, hệ thống yêu cầu môi trường thực thi sau:
* Trình duyệt web hiện đại có hỗ trợ lõi tính toán **WebAssembly** và API phần cứng **WebRTC/MediaDevices** (để gọi Camera).
* (Tùy chọn): Môi trường **Python 3.x** cài đặt sẵn trên máy tính nếu muốn khởi chạy qua file `server.py`.
