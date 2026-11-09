# Lab 02 — Problem Scan & Quick Problem Cards

> Người thực hiện: Duc Son  
> Branch cá nhân: `ducson`  
> Lưu ý dữ liệu: Các con số dưới đây là **giả định dùng để scoping prototype**, không phải số liệu vận hành đã được xác nhận của Vingroup. Trước khi triển khai thật, nhóm phải thay bằng baseline từ log và phỏng vấn stakeholder.

## 1. Opportunity Scan — 4 Lenses

| # | Công ty | Lens | Bài toán vận hành |
|---:|---|---|---|
| 1 | Xanh SM | Time-consuming | Điều phối viên phải tổng hợp vị trí xe, mức pin, loại cổng sạc và trạm còn chỗ khi tài xế báo pin yếu giữa chuyến. |
| 2 | Vinhomes | Repetitive | Nhân viên CSKH đọc và chuyển phản ánh cư dân như mất nước, tiếng ồn, hỏng thang máy đến đúng bộ phận/tòa nhà. |
| 3 | VinFast | Repetitive | Nhân viên tài chính đối chiếu phiên sạc với hóa đơn từ đối tác và xử lý các dòng chênh lệch. |
| 4 | Vinpearl | Stakeholder Pain | Quản lý phải đọc review từ nhiều kênh để phát hiện sớm sự cố vệ sinh, thái độ phục vụ hoặc an toàn. |
| 5 | Vinmec | Time-consuming | Bác sĩ mất thời gian tổng hợp ghi chú, kết quả xét nghiệm và hướng dẫn thành bản nháp tóm tắt xuất viện. |
| 6 | VinUni | AI-upgrade | Trợ giảng phải viết phản hồi lặp lại cho lỗi cú pháp/logic phổ biến sau khi autograder chấm code. |

## 2. Quick Problem Card 1 — Xanh SM: Hỗ trợ xử lý sự cố pin tới hạn

- **Bài toán:** Tạo bản nháp phương án an toàn khi xe điện báo pin yếu hoặc pin tới hạn trong lúc vận hành.
- **Actor:** Tài xế và điều phối viên Xanh SM.
- **Current workflow:**
  1. Tài xế gọi hoặc nhắn mô tả sự cố.
  2. Điều phối viên tra cứu vị trí và mức pin.
  3. Điều phối viên tra cứu trạm sạc phù hợp.
  4. Điều phối viên quyết định hướng dẫn đến trạm hay gọi cứu hộ.
  5. Điều phối viên soạn, duyệt và gửi hướng dẫn.
- **Bottleneck:** Bước 3–5; giả định mất 8–12 phút/lượt trong giờ cao điểm.
- **AI intervention:** Chuẩn hóa dữ liệu sự cố, áp dụng rào chắn an toàn và tạo bản nháp JSON để điều phối viên duyệt.
- **Success metrics:**
  - Giảm median handling time từ baseline giả định 12 phút xuống dưới 3 phút.
  - 100% trường hợp pin dưới 5% không được tự động hướng dẫn tới trạm cách quá 5 km.
  - 100% output giữ trạng thái `DRAFT_ONLY` và yêu cầu người duyệt.
- **Quick architecture:** **LLM Feature + deterministic safety rules + Human-in-the-loop**.

## 3. Quick Problem Card 2 — Vinhomes: Phân loại phản ánh cư dân

- **Bài toán:** Phân loại phản ánh cư dân và tạo bản nháp chuyển việc đến đúng bộ phận.
- **Actor:** Nhân viên CSKH, ban quản lý tòa nhà và cư dân.
- **Current workflow:**
  1. Cư dân gửi nội dung tự do qua ứng dụng.
  2. CSKH đọc và xác định loại sự cố.
  3. CSKH xác định tòa nhà/bộ phận phụ trách.
  4. Ticket được chuyển và nhân viên phản hồi.
- **Bottleneck:** Bước 2–3; dễ route sai khi nội dung mơ hồ.
- **AI intervention:** Trích xuất danh mục, mức khẩn cấp và đề xuất bộ phận; trường hợp không chắc chắn chuyển người kiểm tra.
- **Success metrics:**
  - 90% ticket được phân loại trong dưới 10 giây.
  - Macro-F1 tối thiểu 0,90 trên bộ test đã gán nhãn.
  - 100% ticket liên quan an toàn/cháy nổ được chuyển human review.
- **Quick architecture:** **LLM Feature**, không cho phép tự đóng ticket.

## 4. Quick Problem Card 3 — VinFast: Đối chiếu hóa đơn sạc

- **Bài toán:** Phát hiện các phiên sạc không khớp giữa log vận hành và hóa đơn đối tác.
- **Actor:** Nhân viên tài chính và vận hành trạm sạc.
- **Current workflow:**
  1. Xuất hai bộ dữ liệu.
  2. Chuẩn hóa mã trạm, thời gian và đơn vị điện.
  3. Ghép các giao dịch tương ứng.
  4. Điều tra các dòng lệch.
  5. Phê duyệt thanh toán.
- **Bottleneck:** Bước 2–4 khi dữ liệu khác định dạng hoặc thiếu mã tham chiếu.
- **AI intervention:** Chỉ dùng LLM để giải thích/nhóm lý do ngoại lệ; việc matching chính dùng rule và tolerance số học.
- **Success metrics:**
  - Tự động ghép ít nhất 95% dòng có khóa hợp lệ.
  - Không tự phê duyệt thanh toán.
  - Giảm 60% thời gian điều tra ngoại lệ sau khi có baseline.
- **Quick architecture:** **Rule-based first**, LLM chỉ hỗ trợ giải thích ngoại lệ.

## 5. Lựa chọn để Deep-Dive

Nhóm chọn **Card 2 — Vinhomes: Phân loại và điều hướng phản ánh cư dân**.

Lý do:

1. Phản ánh của cư dân là dữ liệu ngôn ngữ tự do, phù hợp để kiểm tra giá trị của LLM.
2. Workflow có actor, handoff và metric rõ: thời gian phân loại, độ chính xác route và tỷ lệ ticket phải chuyển người kiểm tra.
3. Có thể giới hạn prototype ở mức phân loại và tạo bản nháp; AI không tự đóng ticket hoặc đưa cam kết pháp lý/tài chính.
4. Có thể đánh giá offline bằng bộ ticket đã ẩn danh và gán nhãn trước khi kết nối hệ thống thật.

Không chọn Card 1 cho deep-dive nhóm vì rủi ro an toàn vận hành xe cao hơn và cần dữ liệu trạm theo thời gian thực. Card 1 vẫn được dùng cho **bài code cá nhân** vì starter code và autograder của môn học yêu cầu các boundary Xanh SM. Không chọn Card 3 vì phần cốt lõi phù hợp với rule-based matching hơn LLM.
