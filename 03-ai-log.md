# 03 — AI Log & Reflection: Nhật Ký Đồng Hành & Phản Biện Cùng AI

> **Tài liệu nộp bài Lab 02 (Phần A — Nhật ký cá nhân)**  
> **Học viên:** Đoàn Anh Hùng (Nhánh cá nhân: `doan-anh-hung`)  
> **Vai trò:** AI Product Engineer tại Vin Smart Future (Tập đoàn Vingroup)  
> **Chủ đề bài tập:** AI Product Scoping & Programmatic Prompt Boundary Prototyping

---

## 🧭 1. Tổng Quan Quá Trình Làm Việc Cùng AI (AI as a Thought Partner)

Trong buổi thực hành Lab 02, tôi đã sử dụng trợ lý AI (Gemini / Antigravity) không phải như một công cụ sinh mã tự động thiếu kiểm soát, mà đóng vai trò là một **Cộng sự tư duy (Thought Partner)** và **Kỹ sư phản biện chéo (Adversarial Critic)** xuyên suốt từ khâu phân tích bài toán, đo đạc dữ liệu thực tế, thiết kế ranh giới an toàn đến lập trình mã nguồn nguyên mẫu.

Quá trình phối hợp trải qua 4 giai đoạn chính:
1. **Thiết lập môi trường & Lập trình nguyên mẫu an toàn** trên Google GenAI SDK.
2. **Khảo sát hệ sinh thái Vingroup & Đánh giá nhanh 3 bài toán** (Phase 1 SCAN & Phase 2 QUICK-ASSESS).
3. **Phản biện liêm chính dữ liệu & Xây dựng khung đánh giá lợi ích** có căn cứ mạng Internet.
4. **Đào sâu quản trị rủi ro hệ thống:** Thiết kế cơ chế phòng vệ khi AI làm sai và xác lập ma trận phân định trách nhiệm RACI.

---

## 💡 2. Những Gì AI Đã Hỗ Trợ Đắc Lực (Productivity & Insights)

1. **Tăng tốc thiết lập môi trường kỹ thuật:**
   - Hướng dẫn cấu hình môi trường ảo Python bằng công cụ hiện đại `uv`, cài đặt gói phụ thuộc nhanh chóng (trong vòng 1,6 giây).
   - Tự động hóa cơ chế đọc cấu hình biến môi trường `GEMINI_API_KEY` từ tệp `.env`, tránh rò rỉ khóa bí mật lên repository GitHub theo đúng nguyên tắc bảo mật.
2. **Cấu trúc hóa logic nghiệp vụ và ranh giới an toàn:**
   - Soạn thảo chỉ thị hệ thống `SYSTEM_PROMPT` với các ranh giới cơ học rõ ràng: bắt buộc gắn tiền tố `[DRAFT_ONLY]` để giữ quyền kiểm soát cho con người (Human-in-the-loop).
   - Tự động kích hoạt cơ chế điều xe sạc di động `dispatch_mobile_charger` khi pin EV dưới 5%, cấm điều hướng đến trạm sạc xa quá 5km, vượt qua toàn bộ các ca kiểm thử đối kháng (Adversarial Tests) của autograder.
3. **Tìm kiếm và tổng hợp thông tin đa nguồn trên mạng Internet:**
   - Truy xuất nhanh số liệu từ Báo cáo thường niên Vinhomes (110.000 căn hộ, gần 493.000 cư dân), Báo cáo Bộ Xây dựng về thị phần Xanh SM (70,9% taxi điện), và quy mô giường bệnh Vinmec.
   - Thu thập báo cáo tiền lương tuyển dụng của JobsGO và CareerLink để định giá chính xác đơn giá giờ làm việc của nhân viên CSKH (~85.200 VNĐ/giờ) và bác sĩ (~340.000 VNĐ/giờ).

---

## ⚠️ 3. Những Lỗi Sai, Ảo Giác & Điểm Nghẽn Của AI (AI Failures & Hallucinations)

Trong quá trình đồng hành, AI đã bộc lộ nhiều hạn chế thực tế mà nếu không có sự giám sát của con người thì bài làm sẽ bị sai lệch nghiêm trọng:

### 3.1. Lỗi kỹ thuật mô hình bị khai tử (Deprecated 404) & Quá tải (503 High Demand)
- **Hiện tượng:** Ban đầu mã nguồn mẫu sử dụng `gemini-2.5-flash`. Khi chạy thực tế, Google API trả về lỗi `404 NOT_FOUND` thông báo model này đã ngừng hỗ trợ cho tài khoản mới. Khi chuyển sang `gemini-3.8-flash`, hệ thống tiếp tục bị treo từ 20–30 giây do lỗi `503 UNAVAILABLE: High demand`, khiến thư viện `tenacity` tự động retry vô tận và chạm ngưỡng timeout của autograder.
- **Biện pháp xử lý của tôi:** Tôi đã yêu cầu đo đạc thực nghiệm độ trễ mạng thực tế của từng mô hình khả dụng. Kết quả cho thấy `gemini-3.1-flash-lite` phản hồi chỉ trong 0,82 giây và hoạt động ổn định, giúp script vượt qua toàn bộ 5 tiêu chí của autograder Section B.

### 3.2. Hiện tượng tự suy diễn số liệu thiếu căn cứ (Ungrounded Data Fabrication)
- **Hiện tượng:** Khi lập thẻ bài toán cho Vinhomes và Vinmec, AI đã tự ý đưa ra các con số rất cụ thể như *"Tỷ lệ 1,6% số căn hộ gửi phản ánh mỗi ngày $\approx$ 1.800 tickets/ngày"* và *"300 ca xuất viện/ngày tại Vinmec"* mà không hề trích dẫn nguồn.
- **Biện pháp xử lý của tôi:** Tôi đã trực tiếp chất vấn: *"Lấy thông tin thực tế ở đâu, cơ sở thực tế nào để bạn đưa ra được vấn đề này?"*. Khi bị truy vấn trực diện, AI thừa nhận đây là các số liệu do AI tự ngoại suy từ lý thuyết Helpdesk chứ không phải số liệu đo đạc thực tế từ Vinhomes hay Vinmec.

### 3.3. Lỗi cú pháp sơ đồ Mermaid làm gãy hiển thị
- **Hiện tượng:** Khi vẽ sơ đồ quy trình phòng ngừa 5 lớp theo chiều ngang, AI đã kết hợp sai cú pháp liên kết (`-- "label" -->|"label"|`) và đưa ký tự so sánh `>=` vào khối nhãn, làm toàn bộ sơ đồ bị lỗi cú pháp không thể render trên trình xem Markdown.
- **Biện pháp xử lý của tôi:** Báo lỗi ngay để AI sửa lại cú pháp chuẩn và đồng thời bổ sung thêm một sơ đồ khối văn bản (ASCII Flowchart) dự phòng để đảm bảo hiển thị trên mọi nền tảng.

---

## 🎯 4. Tôi Đã Phản Biện & Điều Chỉnh Ranh Giới AI Như Thế Nào? (Human Steering)

Sự can thiệp của tôi mang tính quyết định đến chất lượng khoa học và tính thực tế của sản phẩm:

1. **Ép AI tuân thủ Liêm chính Khoa học (Scientific Integrity):**
   - Thay vì để AI ngụy biện các con số giả định thành số liệu thật, tôi yêu cầu bóc tách rõ ràng: đâu là **dữ liệu thực nghiệm công khai (`[PROVEN]`)** từ báo cáo thường niên, và đâu là **giả định mô hình hóa (`[EXTRAPOLATED]`)**.
   - Yêu cầu xây dựng bảng so sánh kinh tế chi tiết cho cả 3 bài toán (Vinhomes, Xanh SM, Vinmec) dựa trên các kịch bản lợi ích cụ thể (Bảo thủ, Cơ sở, Cao điểm), chứng minh rõ ràng bài toán Vinhomes mang lại lợi ích tài chính thực tế bền vững (từ 2,06 đến 6,75 tỷ VNĐ/năm).
2. **Chuẩn hóa ngôn ngữ kinh doanh:**
   - Khi AI dùng thuật ngữ học thuật *"phân tích độ nhạy"*, tôi đã chấn chỉnh: *"Đừng viết là phân tích độ nhạy, phải là đánh giá lợi ích"*. Điều này giúp báo cáo chuyển trọng tâm từ lý thuyết thống kê sang giá trị kinh doanh thực tiễn (Business Value & ROI).
3. **Đào sâu rủi ro vận hành & Ma trận trách nhiệm con người:**
   - Tôi đặt câu hỏi phản biện cốt lõi: *"Nếu AI làm sai thì sao? Phòng ngừa và ai chịu trách nhiệm?"*. 
   - Yêu cầu này buộc AI phải thiết kế thêm hệ thống phòng ngừa 5 lớp (Ngắt mạch khẩn cấp cho cháy nổ dưới 5s, Cấm phát ngôn độc lập, Ngưỡng tự tin 85%, Hoàn tác 1-Click) và phân định ma trận trách nhiệm RACI minh bạch (con người chịu trách nhiệm, AI không phải pháp nhân).

---

## 🧠 5. Đúc Kết Bài Học Kinh Nghiệm (Key Takeaways)

1. **AI là trợ lý đồng hành, Con người là người chịu trách nhiệm cuối cùng:** AI rất giỏi tổng hợp và sinh khung sườn, nhưng thiếu tính hoài nghi và dễ bị ảo giác tự tin. Vai trò của người kỹ sư AI là liên tục kiểm chứng chéo số liệu và thiết lập các ranh giới kiểm soát.
2. **Ranh giới an toàn cơ học (Hard Boundaries) luôn vượt trội hơn Prompt khuyên bảo:** Để kiểm soát rủi ro cho hệ thống lớn như Vinhomes hay Xanh SM, không thể chỉ dựa vào vài dòng prompt dặn dò mô hình "hãy cẩn thận", mà bắt buộc phải có các rào chắn cứng bằng mã nguồn (Hard-rule Regex Filter, Confidence Threshold, HITL Approval).
3. **Giá trị của bài toán AI nằm ở bài toán nghiệp vụ, không phải sự hào nhoáng của công nghệ:** Một giải pháp hybrid đơn giản (LLM Feature trích xuất intent kết hợp Rule Router phân luồng) mang lại độ ổn định cao, tiết kiệm hàng tỷ đồng mỗi năm và triển khai an toàn hơn nhiều so với một hệ thống Multi-Agent phức tạp, khó kiểm soát.
