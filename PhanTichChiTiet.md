
# PHẦN 2: PHÂN TÍCH CHI TIẾT HỆ THỐNG TECHROUTE
## 1. Tổng quan mục tiêu phân tích
Hệ thống TechRoute được thiết kế nhằm hỗ trợ sinh viên định hướng lộ trình học tập IT một cách trực quan. Việc phân tích chi tiết tập trung vào cơ chế quản trị dữ liệu thông qua FastAPI và tương tác của người dùng để đảm bảo tính logic, minh bạch và khả năng mở rộng.

## 2. Đặc tả các Use Case (Trường hợp sử dụng)
Hệ thống được chia làm 2 phân hệ chức năng chính dựa trên vai trò của người dùng (Actors):

### 2.1. Phân hệ dành cho Người dùng
* **Tra cứu nghề nghiệp:** Hiển thị danh sách các vị trí việc làm từ file dữ liệu hệ thống.
* **Tìm kiếm lộ trình:** Lọc nhanh thông tin dựa trên từ khóa quan tâm.
* **Xem chi tiết Roadmap:** Truy xuất nội dung các bước học tập (Steps) cho một nghề nghiệp cụ thể.

### 2.2. Phân hệ dành cho Quản Trị Viên
Đây là phân hệ trọng tâm xử lý các thao tác dữ liệu (CRUD) trực tiếp xuống file JSON:
* **Truy xuất dữ liệu (GET):** Kiểm soát toàn bộ danh sách nghề nghiệp hiện có.
* **Tìm kiếm thông tin (GET):** Định vị nhanh bản ghi cần chỉnh sửa thông qua mã định danh (ID) hoặc tên.
* **Thêm mới (POST):** Khởi tạo và lưu trữ các nghề nghiệp/lộ trình mới vào hệ thống.
* **Chỉnh sửa thông tin (PUT/PATCH):** Hiệu chỉnh các thông tin hành chính (Tên nghề, mức lương).
* **Cập nhật nội dung (PUT):** Nâng cấp nội dung chuyên môn của Roadmap. 
    * *Cơ chế xử lý:* Nhận ID -> Tìm bản ghi -> Ghi đè (Overwrite) toàn bộ nội dung các bước học tập mới vào file dữ liệu.
* **Xóa dữ liệu (DELETE):** Loại bỏ các bản ghi không còn giá trị sử dụng.

## 3. Thiết kế sơ đồ hệ thống (Diagrams)

### 3.1. Biểu đồ Use Case tổng quát
*(Ghi chú: Thể hiện sự tương tác giữa Sinh viên, Admin và các chức năng cốt lõi của hệ thống).*
> **[CHÈN ẢNH USE CASE TẠI ĐÂY]**

### 3.2. Biểu đồ Sequence (Luồng lưu trữ chức năng Cập nhật)
*(Ghi chú: Minh họa quy trình từ lúc Admin nhập dữ liệu trên Form -> FastAPI xử lý logic -> Ghi đè dữ liệu vào file JSON).*
> **[CHÈN ẢNH SEQUENCE TẠI ĐÂY]**

### 3.3. Biểu đồ Lớp (Class Diagram)
*(Ghi chú: Mô tả cấu trúc các lớp Career và Roadmap trong mã nguồn).*
> **[CHÈN ẢNH CLASS DIAGRAM TẠI ĐÂY]**

## 4. Phân tích cơ chế xử lý dữ liệu (Data Workflow)
Để đảm bảo hệ thống vận hành mượt mà, quy trình xử lý dữ liệu được thiết kế như sau:

1. **Tiếp nhận yêu cầu:** Frontend thu thập thông tin từ người dùng và gửi thông qua giao thức HTTP (**GET, POST, PUT, DELETE**).
2. **Xử lý tại Backend:** **FastAPI** đóng vai trò trung gian, thực hiện kiểm tra tính hợp lệ của dữ liệu trước khi thực hiện các thao tác đọc/ghi.
3. **Lưu trữ bền vững:** Dữ liệu được quản lý dưới dạng tệp tin có cấu trúc (**JSON**). Cơ chế **Overwrite (Ghi đè)** được áp dụng cho các thao tác Cập nhật để đảm bảo file dữ liệu luôn ở trạng thái mới nhất và đồng bộ hoàn toàn với giao diện Admin.
