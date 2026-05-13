# KẾ HOẠCH THỰC HIỆN ĐỀ TÀI
## XÂY DỰNG HỆ THỐNG ĐỊNH HƯỚNG NGHỀ NGHIỆP CHO SINH VIÊN NGÀNH IT

## 1. Thông tin chung
- **Sinh viên thực hiện:** Tô Vương Đắc Khải
- **Đề tài:** Xây dựng hệ thống định hướng nghề nghiệp ngành Công nghệ thông tin

## 2. Mô tả hệ thống
Hệ thống cho phép người dùng:
- Tra cứu danh mục các vị trí việc làm trong ngành IT (Lập trinh viên, Kiểm thử phần mềm ).
- Xem chi tiết yêu cầu về kỹ năng, mô tả công việc và mức lương tham khảo cho từng vị trí trong ngành.
- Cung cấp lộ trình học tập để sinh viên tự tin phát triển bản thân
- Tích hợp công cụ quản trị dữ liệu tập trung, cho phép cập nhật thông tin nghề nghiệp nhanh chóng

## 3. Yêu cầu hệ thống
### 3.1. Yêu cầu chức năng
Đối với sinh viên: 
- Xem danh sách các thẻ nghề nghiệp (Card layout).
- Hiển thị chi tiết Roadmap học tập và mức lương tham khảo
- Tìm kiếm nghề nghiệp trong ngành theo từ khóa nhanh.
Đối với Quản trị viên:
- Thêm mới, sửa thông tin hoặc xóa các lộ trình cũ (CRUD qua API).
- Cập nhật dữ liệu trực tiếp vào hệ thống thông qua giao diện Swagger UI.
### 3.2. Yêu cầu phi chức năng
- Giao diện tối giản, sạch sẽ, chia khối rõ ràng theo phong cách chuyên nghiệp.
- Phản hồi dữ liệu từ file JSON ngay lập tức nhờ hiệu năng cao của Python FastAPI.
- Hoạt động tốt trên môi trường trình duyệt Web hiện đại.

## 4. Thiết kế giao diện (Mô tả Layout)
Giao diện User:
- Sử dụng bố cục Boxed Layout (khung hộp).
- Thông tin được trình bày trong các Cards đối xứng để sinh viên dễ so sánh giữa các nghề.
Giao diện Admin:
- Sử dụng giao diện chuẩn Swagger UI.
- Hiển thị danh sách các phương thức (GET, POST, PUT, DELETE) một cách khoa học để quản lý file dữ liệu.
## 5. Kế hoạch thực hiện

### Tuần 1: Phân tích & Thiết kế
- Khởi tạo repository trên GitHub để quản lý dự án.
- Phân tích yêu cầu và đặc tả các chức năng hệ thống.
- Thiết kế cơ sở dữ liệu (JSON/SQLite) và giao diện UI/UX sơ bộ.

### Tuần 2: Phát triển hệ thống (Có hỗ trợ từ AI)
- Thiết lập môi trường lập trình Python (Streamlit/Flask).
- Xây dựng Backend xử lý dữ liệu (Sử dụng GitHub Copilot hỗ trợ viết code).
- Kết nối dữ liệu và xây dựng giao diện hiển thị danh mục, Roadmap.
- Hoàn thiện các chức năng quản lý cốt lõi.

### Tuần 3: Kiểm thử & Hoàn thiện
- Kiểm thử toàn bộ chức năng và sửa lỗi (Fix bug).
- Tối ưu hóa giao diện và trải nghiệm người dùng.
- Sử dụng AI để kiểm tra và tối ưu hóa đoạn mã.

### Tuần 4: Báo cáo & Demo
- Hoàn thiện báo cáo dự án chi tiết.
- Chuẩn bị slide thuyết trình và quay video demo sản phẩm.
- Tổng kết và nộp bài đúng hạn.

## 6. Công nghệ sử dụng
- Ngôn ngữ lập trình: Python (Ngôn ngữ chính để xử lý logic định hướng).
- Backend Framework: FastAPI (Dùng để xây dựng các API truy xuất dữ liệu nghề nghiệp và lộ trình học tập).
- Frontend: HTML5, CSS3, JavaScript (Dùng để thiết kế giao diện người dùng trực quan).
- Database: JSON hoặc SQLite (Lưu trữ danh mục nghề nghiệp, kỹ năng và Roadmap).
## 7. Công cụ hỗ trợ:
- Visual Studio Code: Môi trường lập trình chính.
- GitHub Copilot: AI hỗ trợ tối ưu hóa mã nguồn và xử lý lỗi.
- Postman: Công cụ để kiểm thử các cổng API của FastAPI.
- GitHub: Quản lý phiên bản và lưu trữ mã nguồn dự án.
