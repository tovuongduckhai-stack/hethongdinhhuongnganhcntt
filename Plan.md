# KẾ HOẠCH THỰC HIỆN ĐỀ TÀI
## XÂY DỰNG HỆ THỐNG ĐỊNH HƯỚNG NGHỀ NGHIỆP CHO SINH VIÊN NGÀNH IT

## 1. Thông tin chung
- **Sinh viên thực hiện:** Tô Vương Đắc Khải
- **Đề tài:** Xây dựng hệ thống định hướng nghề nghiệp ngành Công nghệ thông tin

## 2. Mô tả hệ thống
Hệ thống cho phép người dùng:
- Tra cứu danh mục các vị trí việc làm trong ngành IT (Web, Mobile, AI, Data...).
- Xem chi tiết yêu cầu kỹ năng, mức lương và mô tả công việc.
- Theo dõi lộ trình học tập (Roadmap) trực quan cho từng chuyên ngành.
- Quản lý và cập nhật dữ liệu thông qua giao diện Admin.

## 3. Yêu cầu hệ thống
### 3.1. Yêu cầu chức năng
- Tra cứu nghề nghiệp theo từ khóa.
- Hiển thị lộ trình học tập (Roadmap) chi tiết.
- Quản lý danh mục ngành nghề (Thêm/Sửa/Xóa).
- Gợi ý hướng đi phù hợp theo năng lực cá nhân.

### 3.2. Yêu cầu phi chức năng
- Giao diện trực quan, dễ sử dụng.
- Phản hồi dữ liệu nhanh chóng.
- Hệ thống hoạt động ổn định trên môi trường Web.

## 4. User Story
- Với vai trò là **sinh viên**, tôi muốn tra cứu nghề nghiệp để định hướng tương lai.
- Với vai trò là **sinh viên**, tôi muốn xem Roadmap để biết các kiến thức cần học.
- Với vai trò là **quản trị viên**, tôi muốn cập nhật dữ liệu để thông tin luôn chính xác.

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
