
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
<img width="1024" height="444" alt="89be509a-94e7-4118-a9a7-8cd95b5b2d6f" src="https://github.com/user-attachments/assets/3b4ffc36-59a4-424b-ba96-cf8f52f4a869" />
Hình 3.1. Biểu đồ tổng quát
- Biểu đồ Use Case trên mô tả sự tương tác giữa hai Actor chính và các chức năng của hệ thống:
1. Các Tác nhân (Actors):
Quản trị viên (Admin): Người có quyền cao nhất, thực hiện các thao tác quản lý dữ liệu lộ trình.
Sinh viên (User): Người sử dụng hệ thống để tìm kiếm và xem thông tin định hướng.
2. Các chức năng chính (Use Cases):
Nhóm chức năng hệ thống:
Đăng nhập: Chức năng bắt buộc để xác thực quyền quản trị.
Giao diện hệ thống: Điểm điều hướng chung để phân luồng vào Giao diện Admin hoặc Giao diện User.
Nhóm chức năng dành cho Quản trị viên (Phân hệ Admin):
Truy xuất dữ liệu: Hiển thị danh sách các lộ trình hiện có từ file JSON.
Cập nhật thông tin: Bao gồm các thao tác con (Include) như Thêm mới, Sửa, và Xóa dữ liệu.
Chỉnh sửa thông tin: Cho phép thay đổi chi tiết nội dung lộ trình và định vị bản ghi thông qua chức năng Tìm kiếm thông tin.
Nhóm chức năng dành cho Sinh viên (Phân hệ User):
Tra cứu nghề nghiệp: Xem danh sách các công việc IT.
Tìm kiếm lộ trình: Lọc lộ trình dựa trên từ khóa.
Xem chi tiết lộ trình: Truy xuất các bước học tập cụ thể trong Roadmap.
3. Quan hệ giữa các Use Case:
Các quan hệ <<include>> thể hiện rằng để thực hiện một chức năng lớn (như Cập nhật), hệ thống bắt buộc phải đi qua các thao tác nhỏ hơn, đảm bảo tính chặt chẽ trong luồng xử lý dữ liệu.
### 3.2. Biểu đồ Sequence (Luồng lưu trữ chức năng Cập nhật)
 3.2.1. Biểu đồ tìm kiếm
 <img width="831" height="761" alt="bieudotimkiem drawio" src="https://github.com/user-attachments/assets/4c8edd50-9896-4329-8045-f8ad670e6a25" />
 Hình 3.2.1. Biểu đồ tìm kiếm
 
- Biểu đồ mô tả quy trình truy xuất và lọc dữ liệu từ file JSON dựa trên từ khóa do người dùng nhập vào. Khác với các chức năng thay đổi dữ liệu, chức năng này tập trung vào luồng truy vấn (Read-only).
1. Các thành phần tham gia:
Quản trị viên/Sinh viên: Tác nhân khởi tạo yêu cầu.
Giao diện (Frontend): Nơi nhận từ khóa và hiển thị kết quả.
Hệ thống (FastAPI Backend): Đóng vai trò xử lý logic lọc dữ liệu.
CSDL (File JSON): Nơi lưu trữ toàn bộ dữ liệu lộ trình (Roadmaps).
2. Quy trình xử lý chi tiết:
Giai đoạn gửi yêu cầu: Người dùng nhập từ khóa vào ô Search. Giao diện gửi một yêu cầu GET kèm theo từ khóa (query string) xuống hệ thống FastAPI.
Giai đoạn xử lý tại Backend: * Hệ thống thực hiện lệnh đọc file JSON để lấy toàn bộ danh sách lộ trình.
Sau khi có dữ liệu, Backend sử dụng các hàm lọc (filter) để đối soát từ khóa với tiêu đề hoặc mô tả của từng lộ trình.
Giai đoạn phản hồi: * Những bản ghi khớp với điều kiện tìm kiếm sẽ được đóng gói dưới dạng mảng JSON và gửi ngược lại cho Giao diện.
Giao diện nhận dữ liệu và thực hiện cập nhật lại danh sách hiển thị trên màn hình, giúp người dùng thấy đúng kết quả cần tìm.
3. Đặc điểm kỹ thuật:
Luồng xử lý này không làm thay đổi nội dung file JSON, đảm bảo tính an toàn cho dữ liệu gốc.
Cơ chế tìm kiếm diễn ra nhanh chóng nhờ việc đọc file và lọc trực tiếp trong bộ nhớ (memory) của hệ thống.
 3.2.2 Biểu đồ thêm
 <img width="831" height="762" alt="biểu đồ thêm drawio" src="https://github.com/user-attachments/assets/ed5b4057-dbd8-4d0c-8486-eedc9c343b24" />
   Hình 3.2.2 Biểu đồ thêm
   
- Biểu đồ mô tả quy trình khởi tạo một lộ trình học tập mới, từ lúc Admin nhập liệu trên giao diện cho đến khi dữ liệu được lưu trữ vĩnh viễn vào hệ thống.
1. Các thành phần tham gia:
Quản trị viên: Người trực tiếp nhập liệu.
Giao diện (Form Thêm mới): Thu thập thông tin (Tiêu đề, Mô tả, Các bước).
Hệ thống (FastAPI Backend): Xử lý kiểm tra dữ liệu và tạo mã định danh (ID).
CSDL (File JSON): Lưu trữ dữ liệu mới.
2. Quy trình xử lý chi tiết:
Bước 1 (Gửi yêu cầu): Admin điền đầy đủ thông tin vào Form và nhấn nút "Lưu". Giao diện gửi một yêu cầu POST chứa dữ liệu (Body) xuống FastAPI.
Bước 2 (Xử lý tại Backend):
FastAPI nhận dữ liệu và thực hiện kiểm tra tính hợp lệ (Validate).
Hệ thống tự động tạo một ID duy nhất cho lộ trình mới để tránh trùng lặp.
Bước 3 (Ghi dữ liệu):
Backend đọc file JSON hiện tại, thêm đối tượng mới vào danh sách.
Thực hiện lệnh Ghi (Write) để cập nhật lại file JSON với bản ghi mới nhất.
Bước 4 (Phản hồi): Sau khi ghi file thành công, hệ thống gửi phản hồi (mã 201 Created) về giao diện. Một thông báo "Thêm thành công" sẽ hiển thị để xác nhận với người dùng.
3. Đặc điểm kỹ thuật:
Quy trình này đảm bảo tính toàn vẹn của dữ liệu thông qua việc kiểm tra ở Backend trước khi ghi vào file.
Việc tự động tạo ID giúp hệ thống quản lý các bản ghi một cách khoa học, phục vụ tốt cho các thao tác Sửa/Xóa sau này.
 3.2.3 Biểu đồ sửa
 <img width="831" height="762" alt="bieu do sua drawio" src="https://github.com/user-attachments/assets/9e698c0c-9ed4-4da9-a4e0-d94c51ea9c34" />
   Hình 3.2.3. Biểu đồ sửa
    
 - Biểu đồ này minh họa quy trình thay đổi nội dung của một lộ trình đã tồn tại trong hệ thống. Đây là thao tác phức tạp nhất vì đòi hỏi việc truy xuất, hiệu chỉnh và đồng bộ hóa dữ liệu.
1. Các thành phần tham gia:
Quản trị viên: Người thực hiện thay đổi.
Giao diện (Form Chỉnh sửa): Hiển thị dữ liệu cũ và nhận dữ liệu mới.
Hệ thống (FastAPI Backend): Tìm kiếm bản ghi theo ID và xử lý logic ghi đè.
CSDL (File JSON): Nơi lưu trữ và cập nhật dữ liệu.
2. Quy trình xử lý chi tiết:
Bước 1 (Lấy dữ liệu cũ): Khi Admin nhấn nút "Sửa", hệ thống gửi yêu cầu lấy thông tin của bản ghi đó theo ID. FastAPI đọc file JSON, tìm đúng bản ghi và trả về để hiển thị lên Form.
Bước 2 (Gửi yêu cầu cập nhật): Sau khi Admin sửa thông tin và nhấn "Cập nhật", Giao diện gửi yêu cầu PUT (hoặc PATCH) kèm theo dữ liệu mới xuống Backend.
Bước 3 (Xử lý Ghi đè - Overwrite): * Backend thực hiện tìm kiếm bản ghi trong danh sách dựa trên ID.
Thay thế (Update) các trường thông tin cũ bằng thông tin mới.
Thực hiện cơ chế Ghi đè toàn bộ (Overwrite) lại file JSON để đảm bảo dữ liệu trong file luôn đồng bộ với trạng thái mới nhất trên hệ thống.
Bước 4 (Phản hồi): Backend gửi thông báo thành công về Giao diện để cập nhật lại bảng hiển thị cho người dùng.
3. Đặc điểm kỹ thuật:
Cơ chế Overwrite giúp tối ưu việc quản lý file JSON đơn giản, tránh việc dữ liệu bị rác hoặc sai lệch sau nhiều lần chỉnh sửa.
Việc kiểm tra ID trước khi sửa đảm bảo tính chính xác, không ghi đè nhầm vào các lộ trình khác.
 3.2.4 Biểu đồ xóa
 <img width="831" height="762" alt="bieudoxoa drawio" src="https://github.com/user-attachments/assets/05280e0b-bebc-4fab-bcf5-528b6970c15b" />
   Hinh 3.2.4. Biểu đồ xóa
   
 - Biểu đồ mô tả quy trình loại bỏ hoàn toàn một lộ trình học tập ra khỏi hệ thống. Đây là thao tác cần sự xác nhận chính xác để tránh mất mát dữ liệu ngoài ý muốn.
1. Các thành phần tham gia:
Quản trị viên: Người ra lệnh xóa.
Giao diện (Danh sách lộ trình): Nơi chứa nút Xóa và hiển thị xác nhận.
Hệ thống (FastAPI Backend): Xử lý lọc bỏ dữ liệu dựa trên ID.
CSDL (File JSON): Nơi lưu trữ dữ liệu cần được cập nhật lại.
2. Quy trình xử lý chi tiết:
Bước 1 (Gửi yêu cầu xóa): Admin chọn một lộ trình cụ thể và nhấn nút "Xóa". Giao diện gửi một yêu cầu DELETE kèm theo ID của lộ trình đó xuống Backend.
Bước 2 (Xử lý tại Backend): * FastAPI tiếp nhận ID và thực hiện đọc file JSON hiện có để lấy danh sách lộ trình.
Hệ thống sử dụng hàm loại bỏ (ví dụ: lọc lấy các bản ghi có ID khác với ID yêu cầu xóa) để tạo ra một danh sách mới đã được lược bỏ phần tử cũ.
Bước 3 (Cập nhật lưu trữ): * Backend thực hiện Ghi đè (Overwrite) danh sách mới này vào file JSON.
Sau khi file được lưu, bản ghi cũ chính thức biến mất khỏi hệ thống.
Bước 4 (Phản hồi): Hệ thống gửi mã trạng thái thành công (200 OK hoặc 204 No Content) về Giao diện. Màn hình tự động cập nhật lại danh sách, không còn hiển thị lộ trình vừa xóa.
3. Đặc điểm kỹ thuật:
Thao tác xóa dựa trên ID đảm bảo tính chính xác tuyệt đối, không xóa nhầm các dữ liệu có tên gần giống nhau.
Việc cập nhật lại file JSON ngay lập tức giúp đảm bảo tính đồng bộ giữa dữ liệu lưu trữ và dữ liệu hiển thị trên Web.
### 3.3. Biểu đồ Lớp (Class Diagram)
<img width="461" height="371" alt="bieudoclass drawio" src="https://github.com/user-attachments/assets/e4cad92d-27df-4043-939e-a004a1c1b174" />
Hình 3.3 Biểu đồ lớp

- Biểu đồ lớp mô tả cấu trúc tĩnh của hệ thống, bao gồm các đối tượng dữ liệu, các thuộc tính và các phương thức xử lý logic cốt lõi. Hệ thống được tổ chức thành 3 thành phần chính:
1. Lớp Admin (Quản trị viên):
Vai trò: Đại diện cho thực thể người dùng có quyền quản trị hệ thống.
Thuộc tính: * username, password: Lưu trữ thông tin định danh để thực hiện quyền truy cập.
Phương thức: * login(), logout(): Xử lý việc xác thực và thoát khỏi phiên làm việc của hệ thống quản lý.
2. Lớp RoadmapController (Xử lý logic - FastAPI):
Vai trò: Đây là lớp trung tâm đóng vai trò điều hướng và xử lý mọi yêu cầu từ người dùng trước khi tác động vào dữ liệu.
Thuộc tính: * file_path: Đường dẫn trỏ tới tệp tin data.json để thực hiện các thao tác đọc/ghi.
Phương thức:
addRoadmap(): Nhận dữ liệu từ Admin và thực hiện lưu mới.
editRoadmap(): Tìm kiếm bản ghi theo ID và thực hiện ghi đè dữ liệu mới.
deleteRoadmap(): Loại bỏ bản ghi khỏi danh sách và cập nhật lại file.
searchRoadmap(): Thực hiện lọc dữ liệu dựa trên từ khóa truy vấn.
3. Lớp Roadmap (Mẫu dữ liệu):
Vai trò: Định nghĩa cấu trúc của một đối tượng lộ trình trong hệ thống.
Thuộc tính:
id: Mã định danh duy nhất cho từng lộ trình.
title: Tiêu đề của nghề nghiệp/lộ trình.
description: Mô tả tổng quan về định hướng học tập.

## 4. Phân tích cơ chế xử lý dữ liệu (Data Workflow)
Để đảm bảo hệ thống vận hành mượt mà, quy trình xử lý dữ liệu được thiết kế như sau:

1. **Tiếp nhận yêu cầu:** Frontend thu thập thông tin từ người dùng và gửi thông qua giao thức HTTP (**GET, POST, PUT, DELETE**).
2. **Xử lý tại Backend:** **FastAPI** đóng vai trò trung gian, thực hiện kiểm tra tính hợp lệ của dữ liệu trước khi thực hiện các thao tác đọc/ghi.
3. **Lưu trữ bền vững:** Dữ liệu được quản lý dưới dạng tệp tin có cấu trúc (**JSON**). Cơ chế **Overwrite (Ghi đè)** được áp dụng cho các thao tác Cập nhật để đảm bảo file dữ liệu luôn ở trạng thái mới nhất và đồng bộ hoàn toàn với giao diện Admin.
