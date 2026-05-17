# KẾ HOẠCH THỰC HIỆN ĐỀ TÀI
## XÂY DỰNG HỆ THỐNG ĐỊNH HƯỚNG NGHỀ NGHIỆP CHO SINH VIÊN NGÀNH IT CỦA TECHROUTE

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
- Xem danh sách các thẻ nghề nghiệp (Card layout)..
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
- Hệ thống cung cấp các công cụ quản trị dữ liệu độc lập, đảm bảo tính chính xác và kịp thời của thông tin:
  Truy xuất dữ liệu : Xem danh sách tổng thể tất cả các nghề nghiệp và lộ trình hiện có trong hệ thống dưới dạng bảng hoặc danh sách chi tiết.
  Tìm kiếm thông tin : Cho phép Admin lọc nhanh dữ liệu theo tên nghề nghiệp hoặc mã ngành để tiết kiệm thời gian khi quản lý kho dữ liệu lớn.
  Chỉnh sửa thông tin : Thay đổi các thông số nhỏ như: tên nghề, mức lương, hoặc mô tả ngắn mà không làm thay đổi cấu trúc lộ trình.
  Thêm mới dữ liệu : Tạo mới hoàn toàn một thẻ nghề nghiệp và lộ trình đi kèm.
  Xóa dữ liệu : Loại bỏ dữ liệu không còn sử dụng.
  Cập nhật dữ liệu : Xem danh sách tổng thể tất cả các nghề nghiệp và lộ trình hiện có trong hệ thống dưới dạng bảng hoặc danh sách chi tiết.
  
## 5. Kế hoạch thực hiện

### Tuần 1: Phân tích và Thiết kế hệ thống (Từ 11/05 đến 15/05)
- Khảo sát yêu cầu: Chốt đề tài TechRoute, xác định các đối tượng người dùng
- Phân tích logic: Đặc tả các chức năng chính như tra cứu Roadmap, quản lý dữ liệu qua API.
- Thiết kế kỹ thuật: Hoàn thiện sơ đồ tổng quát để định hình luồng dữ liệu.
- Quản lý mã nguồn: Khởi tạo Repository trên GitHub và đẩy bản kế hoạch sơ bộ.
  
### Tuần 2: Phát triển giao diện và Cơ sở dữ liệu (Từ 16/05 đến 20/05)
- Thiết kế Database: Xây dựng cấu trúc file JSON hoặc SQLite để lưu trữ thông tin nghề nghiệp và các bước trong Roadmap.
- Xây dựng Frontend (Giao diện người dùng): * Thiết kế trang chủ chuyên nghiệp theo phong cách TechRoute.
- Làm giao diện các "Card" nghề nghiệp và trang hiển thị lộ trình chi tiết.
- Xây dựng giao diện Admin: Tích hợp Swagger UI để kiểm thử và quản lý các phương thức GET/POST/PUT/DELETE.
  
### Tuần 3: Lập trình Backend và Kết nối hệ thống (Từ 21/05 đến 25/05)
- Phát triển API với FastAPI: Viết các hàm xử lý logic để trả về dữ liệu Roadmap khi người dùng yêu cầu.
- Xử lý Logic định hướng: Code chức năng tìm kiếm và lọc nghề nghiệp theo từ khóa.
- Kết nối Front-Back: Sử dụng JavaScript (Fetch API) để lấy dữ liệu từ Backend và hiển thị lên giao diện đã thiết kế.
- Hỗ trợ từ AI: Sử dụng GitHub Copilot để tối ưu hóa các đoạn code xử lý dữ liệu phức tạp.

### Tuần 4: Kiểm thử, Viết báo cáo và Hoàn thiện (Từ 26/05 đến 30/05)
- Kiểm thử (Testing): Chạy thử hệ thống, sửa các lỗi về đường dẫn dữ liệu hoặc giao diện bị lỗi trên trình duyệt.
- Viết báo cáo thực tập: Soạn thảo file Word chi tiết (mô tả quá trình làm, các kỹ năng đạt được, hướng dẫn sử dụng hệ thống).
- Chuẩn bị thuyết trình: Làm Slide PowerPoint tóm tắt các điểm nổi bật của dự án TechRoute.
- Nộp bài: Đóng gói toàn bộ mã nguồn, báo cáo đề tài để nộp đúng hạn ngày 30/05.
## 6. Công nghệ sử dụng
- Ngôn ngữ lập trình: Python (Ngôn ngữ chính để xử lý logic định hướng).
- Backend Framework: FastAPI (Dùng để xây dựng các API truy xuất dữ liệu nghề nghiệp và lộ trình học tập).
- Frontend: HTML5, CSS3, JavaScript (Dùng để thiết kế giao diện người dùng trực quan).
- Database: JSON hoặc SQL Server (Lưu trữ danh mục nghề nghiệp, kỹ năng và Roadmap).
- Draw.io: Là công cụ thiết kế sơ đồ hệ thống trực tuyến mã nguồn mở, hỗ trợ đầy đủ các thư viện ký hiệu theo chuẩn UML
## 7. Công cụ hỗ trợ:
- Visual Studio Code: Môi trường lập trình chính.
- GitHub Copilot: AI hỗ trợ tối ưu hóa mã nguồn và xử lý lỗi.
- Postman: Công cụ để kiểm thử các cổng API của FastAPI.
- GitHub: Quản lý phiên bản và lưu trữ mã nguồn dự án.
