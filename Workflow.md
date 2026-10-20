1. Workflow Tổng Thể (Business Workflow)
Mục tiêu

Trả lời câu hỏi:

"Hệ thống được sử dụng như thế nào trong thực tế?"

Những gì NÊN có

✅ Actor nào tham gia

✅ Luồng nghiệp vụ chính

✅ Trình tự các hoạt động lớn

✅ Tương tác giữa các actor

✅ Vòng đời hoàn chỉnh của nghiệp vụ

Ví dụ:

Plain Text
Admin tạo tài khoản
↓
Giảng viên đăng nhập
↓
Trình chiếu bài giảng
↓
Phát tài liệu
↓
Sinh viên làm bài
↓
Thu bài
↓
Xem kết quả
Những gì KHÔNG nên có

❌ SQL

❌ Database

❌ API

❌ TCP

❌ UDP

❌ Heartbeat

❌ ACK

❌ FPS

❌ Mbps

❌ Packet Loss

❌ Transaction

❌ Validate dữ liệu

❌ "Kiểm tra MSSV tồn tại"

❌ "Insert vào DB"

Mức độ chi tiết

Chỉ nên ở cấp:

Plain Text
Thu bài

KHÔNG nên:

Plain Text
Thu bài
↓
Kiểm tra thư mục tồn tại
↓
Kiểm tra quyền ghi
↓
Tạo socket TCP
↓
Nhận file
↓
Lưu DB
Số lượng node lý tưởng

Khoảng:

Plain Text
10 → 25 node

Nếu hơn:

Plain Text
40 → 50 node
 

thì thường đã quá chi tiết.

2. Workflow Con (Activity Workflow)
Mục tiêu

Trả lời:

"Một chức năng hoạt động như thế nào?"

Ví dụ:

Plain Text
Workflow Phát tài liệu
 
Workflow Thu bài
 
Workflow Ghi hình
 
Workflow Khóa màn hình
``
Ví dụ
Workflow Thu bài
Plain Text
Giảng viên chọn Thu bài
↓
Hệ thống gửi yêu cầu
↓
Sinh viên nộp bài
↓
Hệ thống nhận bài
↓
Cập nhật trạng thái
↓
Giảng viên xem thống kê
Có thể xuất hiện

✅ Điều kiện

Plain Text
[Đã nộp?]

✅ Decision

Plain Text
Có
Không

✅ Luồng thay thế

✅ Luồng lỗi

Không nên có

Vẫn không nên đi quá sâu kỹ thuật.

Sai:

Plain Text
TCP Receive
Deserialize
Repository.Save()
 

Đúng:

Plain Text
Nhận bài
Cập nhật trạng thái
Thông báo kết quả
Mức độ chi tiết

Một workflow con thường:

Plain Text
10 → 20 bước

là đẹp.

3. Sequence Diagram
Mục tiêu

Trả lời:

"Hệ thống xử lý bên trong như thế nào?"

Đây mới là nơi mô tả kỹ thuật

Ví dụ:

Plain Text
Giảng viên
UI
Controller
Service
Repository
Database

Ví dụ chức năng Thu bài:

Plain Text
Teacher
↓
UI
↓
SubmitController
↓
SubmissionService
↓
FileStorage
↓
Database
 
Những thứ NÊN có

✅ Request

✅ Response

✅ Method

✅ API

✅ Service

✅ Repository

✅ Database

✅ Message

✅ Xử lý hệ thống

Ví dụ:

Plain Text
Teacher
→ Controller
 
collectSubmission()
 
Controller
→ Service
 
startCollect()
 
Service
→ Client
 
sendCollectRequest()
 
Client
→ Service
 
uploadFile()
 
Service
→ Repository
 
saveSubmission()
 
Repository
→ Database
 
INSERT
 
Những thứ KHÔNG nên có

❌ Mô tả nghiệp vụ dài dòng

Ví dụ:

Plain Text
Giảng viên vui vẻ kiểm tra bài
 

❌ Mô tả giao diện người dùng quá nhiều

Công thức nhớ siêu nhanh
Workflow Tổng Thể

Hỏi:

Người dùng làm gì?

Ví dụ:

Plain Text
Đăng nhập
↓
Dạy học
↓
Thu bài
Workflow Con

Hỏi:

Chức năng đó vận hành thế nào?

Ví dụ:

Plain Text
Thu bài
↓
Sinh viên nộp
↓
Cập nhật trạng thái
Sequence Diagram

Hỏi:

Phần mềm xử lý bên trong thế nào?

Ví dụ:

Plain Text
Controller
↓
Service
↓
Repository
↓
Database
 
Quy tắc vàng khi làm đồ án

Nếu thấy xuất hiện:

Plain Text
Database
API
TCP
UDP
Repository
Service
Controller
 

➡️ Hầu như chắc chắn không phải Workflow Tổng Thể.

Nếu thấy xuất hiện:

Plain Text
Actor
Nghiệp vụ
Phát tài liệu
Làm bài
Thu bài

➡️ Đó là Workflow Tổng Thể hoặc Workflow Con.

Nếu thấy xuất hiện:

Plain Text
Teacher
UI
Controller
Service
Database

➡️ Đó là Sequence Diagram.