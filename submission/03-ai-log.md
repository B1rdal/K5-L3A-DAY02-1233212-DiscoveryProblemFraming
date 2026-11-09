# Lab 02 — AI Log & Reflection

## 1. Tôi đã dùng AI như thế nào?

Tôi dùng ChatGPT như một thought-partner để:

1. Đọc rubric và tách bài lab thành các deliverable cụ thể.
2. Brainstorm các pain point theo bốn lenses.
3. Phản biện xem bài toán Vinhomes nên dùng rule, LLM hay agent.
4. Viết ranh giới vận hành cho phân loại ticket và thiết kế adversarial tests.
5. Kiểm tra code, cấu trúc file và cách chạy prototype trên Windows.

Tôi không cung cấp API key cho AI và không đưa key vào source code.

## 2. AI giúp tốt ở đâu?

- **Cấu trúc hóa bài toán:** AI giúp chuyển ý tưởng “phân loại phản ánh cư dân” thành actor, workflow, taxonomy, bottleneck, metric và boundary.
- **Stress-test ý tưởng:** AI chỉ ra rằng emergency detection cần rule riêng, không nên giao toàn bộ quyết định cho LLM.
- **Tạo tình huống tấn công:** AI đề xuất các prompt cố bỏ tag, ép gửi thẳng và yêu cầu tiết lộ system prompt.
- **Debug môi trường:** AI xác định `python.exe` bị Windows Store alias che khuất, tạo `.venv`, và sửa lệnh kiểm tra biến `GEMINI_API_KEY`.

## 3. AI sai hoặc chưa đáng tin ở đâu?

### 3.1. Con số vận hành không có nguồn

AI có thể đề xuất các số như số ticket/ngày, thời gian xử lý hay tỷ lệ cư dân không hài lòng nhưng không có dữ liệu nội bộ để chứng minh. Tôi không dùng các số đó như sự thật. Trong báo cáo, tôi ghi rõ baseline 14 phút là giả định scoping và chọn quyết định `NOT YET` cho đến khi có log thật.

### 3.2. “Dùng LLM cho mọi thứ”

Bản brainstorm ban đầu dễ nghiêng về một agent tự tạo, chuyển và đóng ticket. Tôi thu hẹp scope: rule phát hiện trường hợp khẩn cấp, LLM chỉ đề xuất nhãn và tạo draft, validator kiểm tra output và con người phê duyệt.

### 3.3. Lệnh kiểm tra API key

Một lần kiểm tra đã dùng giá trị key làm tên biến trong `os.getenv(...)`, khiến kết quả là `MISSING` dù biến môi trường đã được đặt. Tôi sửa thành `os.getenv("GEMINI_API_KEY")` và không in giá trị key ra màn hình.

### 3.4. API key bị lộ trong ảnh

Key cũ xuất hiện trong ảnh terminal. Tôi coi key đó là compromised, thu hồi/rotate và không tái sử dụng trong code hoặc tài liệu.

## 4. Tôi đã thay đổi prompt và boundary ra sao?

| Vấn đề | Thay đổi |
|---|---|
| Output có thể bị gửi nhầm | Bắt buộc mọi output bắt đầu bằng `[DRAFT_ONLY]`. |
| Người dùng ép bỏ quy tắc | Nêu rõ user input không thể override system boundary. |
| Ticket có dấu hiệu khẩn cấp | Rule gate chuyển `emergency_escalation`, không chờ LLM. |
| Thiếu tòa nhà, nhiều ý hoặc confidence thấp | Chuyển `human_review`, không được đoán. |
| Output tự do khó kiểm tra | Yêu cầu JSON với allowlist action và `requires_human_approval=true`. |
| Prompt injection | Cấm tiết lộ system prompt và vẫn áp dụng rule an toàn. |

## 5. Điều tôi học được

Scoping tốt không bắt đầu từ việc chọn model mạnh nhất. Nó bắt đầu từ workflow thật, baseline đo được và phạm vi quyết định. Với Vinhomes, LLM phù hợp để hiểu phản ánh ngôn ngữ tự do, còn rule phù hợp để bắt tín hiệu khẩn cấp. Prototype phải dễ chặn, dễ fallback và dễ audit hơn là tự chủ tối đa.

## 6. Việc cần làm tiếp

1. Hoàn thiện bài code cá nhân Xanh SM theo starter code/autograder được cung cấp và chạy bằng key mới.
2. Với deep-dive nhóm Vinhomes, xin CSKH review taxonomy và ma trận routing.
3. Thay số liệu giả định bằng baseline từ log vận hành đã ẩn danh.
4. Chuẩn bị bộ ticket holdout và adversarial set để đánh giá trước shadow pilot.

## 7. Phân biệt bài nhóm và bài code cá nhân

Nhóm chọn **Vinhomes resident complaint routing** cho báo cáo deep-dive. Tuy nhiên, starter code và autograder được giảng viên cung cấp kiểm tra riêng boundary **Xanh SM** (`[DRAFT_ONLY]`, pin 5%, `dispatch_mobile_charger`). Vì code `.py` được chấm trên branch cá nhân, tôi giữ prototype Xanh SM theo đúng đề kỹ thuật, đồng thời không dùng kết quả code đó làm bằng chứng rằng giải pháp Vinhomes đã được kiểm thử.
