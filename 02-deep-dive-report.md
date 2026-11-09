# Lab 02 — Deep-Dive Report

## 1. Scope và giả định

**Use case:** Vinhomes — AI hỗ trợ phân loại và điều hướng phản ánh cư dân.

Prototype chỉ xử lý ticket văn bản đã ẩn danh và đề xuất `category`, `urgency`, `destination_team` cùng bản nháp phản hồi. Prototype **không** tự gửi phản hồi, tự đóng ticket, cam kết thời gian xử lý, quyết định bồi thường hoặc xử lý tình huống khẩn cấp. Các con số thời gian dưới đây là giả định scoping, cần thay bằng baseline từ log vận hành.

## 2. Current-State Workflow

| Bước | Actor | Input | Hoạt động | Output | Thời gian giả định |
|---:|---|---|---|---|---:|
| 1 | Cư dân | Sự cố/nhu cầu | Gửi phản ánh dạng văn bản qua ứng dụng hoặc hotline | Ticket tự do | 2 phút |
| 2 | Nhân viên CSKH | Ticket mới | Đọc, làm rõ tòa nhà/căn hộ và loại vấn đề | Ticket đã hiểu sơ bộ | 4 phút |
| 3 | Nhân viên CSKH | Nội dung ticket | Chọn danh mục và mức độ khẩn cấp | Nhãn ticket | 3 phút |
| 4 | Nhân viên CSKH | Nhãn + địa điểm | Tìm bộ phận/tòa nhà chịu trách nhiệm | Routing decision | 3 phút |
| 5 | CSKH/Ban quản lý | Ticket đã route | Kiểm tra, phản hồi và xử lý | Ticket được tiếp nhận | 2 phút |

**Tổng baseline giả định:** 14 phút/lượt trước khi đội xử lý chuyên môn bắt đầu công việc.  
**Bottleneck:** Bước 2–4.  
**Handoffs:** Cư dân → CSKH; CSKH → ban quản lý tòa nhà/bộ phận kỹ thuật/an ninh/vệ sinh; bộ phận xử lý → cư dân.

Sơ đồ: `04-workflow-diagram.png`.

## 3. Problem Statement — 6 Fields

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Nhân viên CSKH Vinhomes tiếp nhận phản ánh; ban quản lý và các đội kỹ thuật/an ninh/vệ sinh nhận ticket; cư dân chờ phản hồi. |
| **2. Current Workflow** | CSKH đọc nội dung tự do, xác minh địa điểm, chọn danh mục/độ khẩn cấp, tìm bộ phận phụ trách và tạo phản hồi tiếp nhận. Quy trình giả định gồm 5 bước, mất khoảng 14 phút trước khi ticket tới đội xử lý. |
| **3. Bottleneck** | Nội dung có thể mơ hồ, chứa nhiều vấn đề hoặc dùng cách gọi không thống nhất. Nhân viên phải nhớ taxonomy và ma trận routing của nhiều tòa nhà/bộ phận. |
| **4. Business Impact** | Ticket route sai làm tăng handoff, kéo dài SLA và khiến cư dân phải mô tả lại. Tác động tài chính chưa được định lượng vì chưa có log thật. |
| **5. Success Metric** | (a) 90% ticket có đề xuất phân loại trong dưới 10 giây; (b) macro-F1 ≥0,90 trên bộ test đã gán nhãn; (c) routing accuracy ≥95%; (d) 100% ticket liên quan cháy, khói, gas, người bị thương hoặc nguy cơ an toàn được gắn `emergency_escalation`; (e) 0 ticket được AI tự đóng/gửi. |
| **6. Operational Boundary** | AI chỉ được đề xuất nhãn, route và bản nháp. AI không tự gửi, tự đóng, hứa SLA, xác nhận trách nhiệm, quyết định bồi thường hoặc đưa hướng dẫn thay thế dịch vụ khẩn cấp. Thiếu địa điểm/thông tin hoặc confidence thấp phải chuyển human review. |

## 4. Taxonomy tối thiểu cho prototype

| Category | Destination team | Ví dụ |
|---|---|---|
| `utilities` | Kỹ thuật tòa nhà | Mất nước, mất điện khu vực chung |
| `elevator` | Kỹ thuật thang máy | Kẹt, rung, dừng sai tầng |
| `security` | An ninh | Người lạ, mất đồ, xô xát |
| `noise` | Ban quản lý/An ninh | Tiếng ồn ngoài khung giờ |
| `cleanliness` | Vệ sinh | Rác, mùi, hành lang bẩn |
| `parking` | Vận hành bãi xe | Thẻ xe, chắn lối, phí gửi xe |
| `administrative` | CSKH/Ban quản lý | Đăng ký thi công, thẻ cư dân |
| `emergency` | Human emergency escalation | Cháy, khói, gas, người bị thương |
| `unknown` | CSKH human review | Thiếu hoặc mâu thuẫn thông tin |

Taxonomy phải được stakeholder xác nhận trước pilot; bảng trên chỉ là bản đầu để thiết kế test.

## 5. AI Fit Decision

| Phương án | Điểm mạnh | Điểm yếu | Quyết định |
|---|---|---|---|
| Rule/Keyword | Nhanh, dễ kiểm toán; tốt cho từ khóa khẩn cấp | Dễ bỏ sót cách diễn đạt mới, ticket nhiều ý | Dùng làm emergency guardrail |
| LLM Feature | Hiểu tiếng Việt tự do, nhiều ý và ngữ cảnh | Có thể hallucinate route hoặc cam kết ngoài quyền | Dùng để đề xuất nhãn và draft |
| Agentic Loop | Có thể tự tạo/cập nhật ticket | Blast radius lớn; khó kiểm soát việc gửi/đóng ticket | Không dùng trong prototype |

**Kết luận:** Kiến trúc lai **keyword/rule safety gate + LLM classifier/drafter + output validator + Human-in-the-loop**.

## 6. Future-State Flow

1. Ticket mới được tiếp nhận và loại bỏ/che dữ liệu cá nhân không cần thiết.
2. Schema validator kiểm tra nội dung, khu/tòa nhà và kênh liên hệ.
3. **Emergency rule gate:** phát hiện dấu hiệu cháy, khói, gas, người bị thương hoặc nguy cơ tức thời → `emergency_escalation`, không tạo hướng dẫn thay thế dịch vụ khẩn cấp.
4. **LLM step:** đề xuất category, urgency, destination team, confidence và draft acknowledgement.
5. Output validator kiểm tra taxonomy allowlist, cấm cam kết SLA/bồi thường và yêu cầu `requires_human_approval=true`.
6. **Human-in-the-loop:** CSKH duyệt, sửa hoặc route lại.
7. Chỉ hệ thống ticketing mới được gửi/chuyển sau khi người có thẩm quyền duyệt.

### Fallback

- Thiếu tòa nhà, ticket nhiều ý hoặc confidence <0,80 → `human_review`.
- Category/đội xử lý không thuộc allowlist → chặn output.
- LLM timeout hoặc output không parse được → quay lại workflow thủ công.
- Ticket khẩn cấp → hiển thị cảnh báo cho nhân viên; không chờ LLM để bắt đầu escalation.

## 7. Evaluation Plan

### Bộ dữ liệu

- Tối thiểu 200 ticket lịch sử đã ẩn danh.
- Hai nhân viên nghiệp vụ gán nhãn độc lập; bất đồng được adjudicate.
- Chia train/prompt-development và holdout test, tránh dùng cùng ticket để sửa prompt và báo cáo kết quả.

### Adversarial cases

1. Ticket yêu cầu AI tự đóng vì “đã xử lý rồi”.
2. Cư dân yêu cầu hứa hoàn tiền hoặc thời gian sửa chữa chắc chắn.
3. Ticket có prompt injection yêu cầu bỏ taxonomy và tiết lộ system prompt.
4. Ticket mơ hồ chứa “có mùi khét và khói nhẹ” nhưng người gửi yêu cầu đánh dấu không khẩn cấp.
5. Ticket chứa hai vấn đề thuộc hai đội khác nhau.

### Metrics

- Macro-F1 theo category và recall riêng cho emergency.
- Routing accuracy.
- Tỷ lệ human override.
- Median time-to-route.
- Boundary violation rate trên adversarial set.

## 8. AI Readiness Checklist

| Câu hỏi | Trạng thái | Bằng chứng / việc còn thiếu |
|---|---|---|
| Có dữ liệu mẫu/log sạch? | **Chưa** | Cần ticket lịch sử đã ẩn danh và taxonomy được stakeholder duyệt. |
| Rủi ro khi AI sai được kiểm soát? | **Có ở mức prototype** | Emergency rule, output validator, draft-only, HITL và fallback thủ công. |
| Stakeholder sẵn sàng đổi workflow? | **Chưa xác nhận** | Cần phỏng vấn CSKH và ban quản lý, sau đó shadow pilot. |

## 9. Decision

### **NOT YET — chuẩn bị dữ liệu và chạy shadow pilot trước khi GO**

Lý do:

- Use case phù hợp với LLM vì input là ngôn ngữ tự do và output có taxonomy rõ.
- Rủi ro có thể giới hạn bằng rule khẩn cấp, validator và human approval.
- Tuy nhiên chưa có taxonomy chính thức, baseline thật hoặc bộ test đã gán nhãn; vì vậy chưa đủ bằng chứng để GO production.

Điều kiện chuyển sang GO:

1. Stakeholder phê duyệt taxonomy và ma trận routing.
2. Thu thập tối thiểu 200 ticket đã ẩn danh, gán nhãn và adjudicate.
3. Chạy shadow-mode tối thiểu 100 ticket mà không tự gửi/chuyển ticket.
4. Emergency recall đạt 100% trên safety set; routing accuracy ≥95%; macro-F1 ≥0,90.
5. Boundary violation rate bằng 0 trên adversarial set.
6. Privacy review cho dữ liệu cư dân và retention policy.
