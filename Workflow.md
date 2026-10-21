**I. Thành phần cốt lõi của một Workflow**

**1. Tác nhân và Phân làn (Actors / Pools & Swimlanes)**: Xác định rõ "Ai làm bước này?". Trong sơ đồ, chúng được chia thành các bể (Pool) và các làn bơi (Lane) riêng biệt cho từng đối tượng: Khách hàng (User), Quản trị viên (Admin), Hệ thống nội bộ (System/Backend), hoặc Hệ thống bên thứ ba (Cổng thanh toán, Đơn vị vận chuyển).
**2. Sự kiện (Events / Triggers):**
  - Điểm bắt đầu (Start Event): Sự kiện kích hoạt luồng chạy (ví dụ: Khách hàng nhấn nút "Thanh toán", hoặc Hệ thống đến 00:00 tự động quét đối soát).
  - Sự kiện trung gian (Intermediate Event): Các điểm chờ hoặc nhận tín hiệu (ví dụ: Chờ khách nhập OTP trong 60 giây).
  - Điểm kết thúc (End Event): Trạng thái khép lại quy trình (Đặt hàng thành công, hoặc Hủy đơn).
**3. Hoạt động / Tác vụ (Activities / Tasks):** Các bước xử lý cụ thể. Nguyên tắc vàng của BA khi đặt tên Task là dùng cụm Động từ + Danh từ rõ nghĩa (ví dụ: "Kiểm tra tồn kho", "Khấu trừ hạn mức", tuyệt đối tránh viết chung chung kiểu "Xử lý đơn").
**4. Điểm rẽ nhánh / Điều kiện (Gateways / Decisions):** Thường biểu diễn bằng hình thoi để kiểm tra logic và điều hướng luồng đi:
  - Rẽ nhánh loại trừ (Exclusive / XOR): Chỉ đi theo 1 nhánh duy nhất dựa trên điều kiện Đúng/Sai (ví dụ: Tồn kho đủ → Tạo đơn; Tồn kho thiếu → Báo lỗi).
  - Rẽ nhánh song song (Parallel / AND - ký hiệu dấu +): Tách luồng để thực hiện nhiều việc cùng lúc mà không cần chờ nhau (ví dụ: Vừa Gửi email xác nhận, vừa Bắn thông báo cho kho đóng gói).
  - Rẽ nhánh bao hàm (Inclusive / OR): Có thể đi vào 1 hoặc nhiều nhánh cùng lúc tùy điều kiện thỏa mãn.
**5. Luồng kết nối (Sequence Flows & Message Flows):** Các đường mũi tên chỉ thứ tự thực hiện từ bước này sang bước khác, hoặc luồng truyền dữ liệu/thông báo giữa các hệ thống khác nhau.
**6. Quy tắc nghiệp vụ & Dữ liệu đi kèm (Business Rules & Artifacts):** Các điều kiện ràng buộc hoặc tài liệu/dữ liệu sinh ra tại bước đó (ví dụ: Hóa đơn VAT, Bản ghi lịch sử giao dịch).

**Sơ đồ BPMN mẫu**
<img width="825" height="344" alt="image" src="https://github.com/user-attachments/assets/593267ca-4cc3-449d-a8de-03233234d08d" />
Trong hình trên, toàn bộ quy trình nằm trong Pool One và được chia thành 3 làn (Lane One, Lane Two, Lane Three) tương ứng với 3 vai trò khác nhau. Luồng bắt đầu từ vòng tròn Start Event, đi qua tác vụ Activity A rồi gặp hình thoi Gateway One để xét điều kiện: nếu thỏa mãn Condition One thì đi thẳng sang Activity B và Activity C tới End Event One; nếu rơi vào Condition Two thì luồng chuyển xuống làn thứ hai (Lane Two) để chạy Activity D. Tại Gateway Two (có dấu + biểu thị chạy song song), luồng tách làm hai nhánh chạy đồng thời xuống Activity E ở làn 2 và Activity F ở làn 3 trước khi kết thúc tại End Event Two và End Event Three.

**II. Cách vẽ một Workflow (Quy trình 5 bước)**

**1. Chốt biên quy trình (Xác định Start & End):** Đặt câu hỏi "Quy trình này bắt đầu từ khoảnh khắc nào và khi nào thì coi là xong?". Nếu không khóa chặt điểm đầu và điểm cuối, bạn sẽ vẽ lan man từ luồng "Đặt hàng" sang tận luồng "Kế toán hoàn thuế".
**2. Xác định Actors để kẻ Swimlane:** Liệt kê tất cả các bên tham gia (Người dùng, Hệ thống, Admin, Bên thứ 3) và kẻ sẵn các làn. Hành động của ai thì đặt đúng vào làn của người đó.
**3. Vẽ "Happy Path" trước (Luồng màu hồng):** Giả định mọi thứ diễn ra thuận lợi 100% (khách có đủ tiền, kho còn hàng, mạng không rớt) để nối một mạch từ Start Event đến End Event. Bước này giúp bạn dựng được bộ khung chính cực nhanh.
**4. Đặt câu hỏi "What-if" để tìm Alternate & Exception Flows:** Đây là bước ăn tiền nhất của một BA. Đi rà lại từng hình chữ nhật trên Happy Path và tự hỏi: Nếu bước này thất bại hoặc rẽ hướng khác thì sao? (Ví dụ: Khách thanh toán thất bại 3 lần thì khóa giao dịch hay cho chọn phương thức khác? Kho hết hàng ngay lúc vừa bấm thanh toán thì hoàn tiền tự động hay tạo phiếu chờ?).
**5. Kiểm tra điểm mù (Dry-run & Validate):** Đọc nhẩm theo từng mũi tên từ đầu đến cuối. Kiểm tra xem có hình chữ nhật nào "vào mà không có ra" (Dead-end), hoặc hình thoi Gateway nào mới chỉ có nhánh Yes mà quên vẽ nhánh No hay không.
