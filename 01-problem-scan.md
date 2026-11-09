# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 |Vinpearl |Pain từ người khác |Quét qua các review trên Booking.com, Agoda, Google Map của Vinpearl để lọc ra các phàn nàn khẩn cấp (ví dụ: "phòng bẩn", "nhân viên thái độ tệ") gửi về Manager. |
| 2 | Xanh SM|Pain từ người khác |Tự động nghe ghi âm cuộc gọi hủy chuyến và ghi chú của tài xế để phân loại 10 lý do phổ biến nhất gây rò rỉ cuốc. |
| 3 | Vinhomes|Lặp lại | Phân loại tự động các khiếu nại (ví dụ: mất nước, hỏng đèn, ồn ào) gửi qua App Vinhomes Resident đến đúng ban quản lý từng tòa nhà.|
| 4 | Vinmec|Tốn thời gian | Ghi chép bệnh án và tóm tắt xuất viện: bác sĩ/điều dưỡng dành 1-1,5 giờ/ngày cho giấy tờ thay vì bệnh nhân.|
| 5 | VinFast| AI có thể tốt hơn|Tự động đề xuất lịch trình sạc tối ưu và trạm sạc trống phù hợp với loại cổng sạc (CCS2/GBT) của từng dòng xe điện (VF5, VF8, VF9). |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #___                                     │
│                                                             │
│ Bài toán (1 câu): ________________________________________  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? ______________________________________ │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. ___ ──> 2. ___ ──> 3. ___ ──> 4. ___                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? ___ (⏱ ___ phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? _____________________ │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? ______________________ │
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────
│ QUICK PROBLEM CARD #1
│
│ Bài toán (1 câu): Tự động gán loại sự cố, mức khẩn cấp và
│   ban quản lý đúng cho phản ánh cư dân gửi qua app.
│ Công ty thành viên: Vinhomes
│
│ Ai đang đau (Actor)?
│   - Cư dân: phản ánh bị chuyển nhầm, chờ lâu.
│   - Nhân viên CSKH/lễ tân BQL: đọc và gán tay mỗi ticket.
│
│ Workflow thủ công hiện tại:
│   1. Cư dân gửi phản ánh (text/ảnh) qua app
│   2. CSKH đọc, gán loại sự cố + tòa/khu
│   3. Chuyển cho BQL tòa hoặc đội kỹ thuật
│   4. Đội nhận thấy sai bộ phận ──> chuyển lại
│
│ Bước tốn thời gian/lỗi nhất? Bước 2 và 4
│   (~5-10 phút/ticket gán tay; ~10% chuyển nhầm, giả định)
│ AI có thể nhảy vào ở bước nào? Bước 2: gán nhãn tự động;
│   ca mơ hồ chuyển người duyệt.
│
│ Metric thành công:
│   - Thời gian từ lúc nhận đến lúc gán đúng bộ phận:
│     ~10 phút ──> dưới 1 phút
│   - Tỷ lệ chuyển nhầm: ~10% ──> dưới 3%
│   - Độ chính xác phân loại ≥ 90% trên tập ticket giữ lại
│
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent
│   (Rule cứng cho từ khóa khẩn cấp: cháy, rò điện, ngập;
│    LLM chỉ xử lý ca mơ hồ)
└──────────────────────────────────────────────────────────────

┌──────────────────────────────────────────────────────────────
│ QUICK PROBLEM CARD #2
│
│ Bài toán (1 câu): Tự sinh bản nháp tóm tắt xuất viện từ bệnh
│   án để bác sĩ chỉ cần duyệt và sửa.
│   (MVP chỉ làm tóm tắt xuất viện; ambient scribe để sau)
│ Công ty thành viên: Vinmec
│
│ Ai đang đau (Actor)?
│   - Bác sĩ điều trị/điều dưỡng: viết giấy tờ thay vì khám.
│   - Bệnh nhân: chờ giấy ra viện, nhận bản tóm tắt khó hiểu.
│
│ Workflow thủ công hiện tại:
│   1. Mở EMR, gom diễn tiến, xét nghiệm, thuốc
│   2. Viết lại thành bản tóm tắt
│   3. Rà số liệu, thuốc, liều, dặn dò tái khám
│   4. Ký duyệt, in/gửi bệnh nhân
│
│ Bước tốn thời gian/lỗi nhất? Bước 1-2
│   (~15-25 phút/ca, giả định)
│ AI có thể nhảy vào ở bước nào? Bước 1-2: sinh nháp có trích
│   dẫn nguồn từng mục. Bước 3 vẫn do bác sĩ, bắt buộc.
│
│ Metric thành công:
│   - Thời gian soạn: ~20 phút ──> dưới 7 phút/ca
│   - ≥ 70% bản nháp chỉ sửa nhẹ
│   - 0 lỗi nghiêm trọng chưa bị bắt (thuốc, liều, dị ứng)
│     trong đánh giá có bác sĩ chấm
│
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent
│   (LLM + người duyệt bắt buộc; chỉ dùng thông tin có trong
│    bệnh án)
└──────────────────────────────────────────────────────────────

┌──────────────────────────────────────────────────────────────
│ QUICK PROBLEM CARD #3
│
│ Bài toán (1 câu): Gợi ý trạm sạc phù hợp cổng sạc của xe và
│   cho biết pin còn lại khi đến nơi, tránh trụ báo trống
│   nhưng hỏng/bận.
│ Công ty thành viên: VinFast
│
│ Ai đang đau (Actor)?
│   - Chủ xe VF5/VF8/VF9: lo hết pin, mất thời gian tìm trụ.
│
│ Workflow thủ công hiện tại:
│   1. Mở app, tìm trạm gần hoặc dọc tuyến
│   2. Tự lọc loại cổng, xem trạng thái trụ
│   3. Tự ước tính pin khi đến nơi và cần sạc bao nhiêu
│   4. Đến nơi, trụ bận/hỏng ──> tìm trạm khác
│
│ Bước tốn thời gian/lỗi nhất? Bước 3 và 4
│   (~10-20 phút/lần gặp trụ không dùng được, giả định)
│ AI có thể nhảy vào ở bước nào? Bước 3: tính toán theo mức
│   tiêu thụ của từng dòng xe. Bước 2: dự đoán trụ thực sự
│   dùng được dựa trên lịch sử phiên sạc.
│
│ Metric thành công:
│   - Tỷ lệ đến trạm mà trụ không dùng được: baseline ──> -50%
│   - Thời gian từ lúc quyết định sạc đến lúc bắt đầu sạc
│     giảm ≥ 30%
│
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent
│   (Lọc + tính quãng đường là rule; dự đoán trụ dùng được là
│    ML nhẹ, không cần LLM)
└──────────────────────────────────────────────────────────────
```
# 🗳️ Quyết định lựa chọn của nhóm:
Nhóm quyết định chọn bài toán **"Card #1 — Vinhomes: Phân loại và điều hướng phản ánh cư dân"** để thực hiện Deep-Dive.

* **Dữ liệu có sẵn, đo được ngay:** Ticket phản ánh trên app Vinhomes Resident đã có lịch sử kèm nhãn và đội xử lý cuối cùng. Nhóm dựng được tập test và baseline trong 1-2 tuần mà không phụ thuộc hệ thống ngoài.
* **Rủi ro thấp, dễ kiểm soát:** Sai một ticket nhiều nhất là chuyển nhầm bộ phận, sửa được bằng cách chuyển lại. Rule cứng cho từ khóa khẩn cấp (cháy, rò điện, ngập) giữ an toàn cho ca nghiêm trọng, ca mơ hồ chuyển người duyệt.
* **Đúng nguyên tắc "đơn giản thắng":** Lộ trình rule-based baseline (dropdown + bảng tra danh mục × tòa → đội + keyword) rồi mới thêm LLM cho phần dư mơ hồ. Mỗi bước đều có số liệu chứng minh giá trị biên.
* **Có thể tính ROI bằng thước đo kết quả:** Time-to-resolution, tỷ lệ chuyển nhầm và reopen rate, không chỉ "gán nhanh hơn".
* **Mở rộng được:** Cùng pipeline phân loại dùng lại cho các tòa/dự án khác của Vinhomes.

## Lý do loại bỏ các thẻ khác:

* **Card #2 (Vinmec, tóm tắt xuất viện):**
  * *Rủi ro cao:* Một lỗi về liều thuốc hoặc dị ứng gây chi phí pháp lý và uy tín vượt mọi khoản tiết kiệm. Bác sĩ bận có thể ký lướt bản nháp (automation bias).
  * *Điều kiện chưa sẵn sàng:* Chưa rõ EMR có xuất dữ liệu cấu trúc không và chính sách đưa dữ liệu bệnh nhân vào mô hình (nội bộ hay cloud) cần hội đồng chuyên môn duyệt, kéo dài thời gian trước khi có PoC.
  * *Tiết kiệm khó thành tiền:* Thời gian bác sĩ tiết kiệm chỉ thành tiền khi khám thêm bệnh nhân hoặc giảm giờ làm thêm. Thời gian rà lại bản nháp có thể triệt tiêu phần lớn lợi ích.
  * *Hướng đi:* Hoãn. Làm template từ EMR trước (merge xác định, không bịa), chỉ xin LLM cho phần văn bản tự do khi có số liệu thời gian review thật.

* **Card #3 (VinFast, gợi ý trạm sạc):**
  * *Giá trị biên thấp:* Lọc cổng sạc, tính pin khi đến nơi và lập lộ trình là tính năng nền tảng, có khả năng app/xe đã có.
  * *Pain thật nằm ở hạ tầng:* "Trụ báo trống nhưng hỏng/bận" là vấn đề độ tin cậy dữ liệu trạng thái và bảo trì trụ. Đặt AI lên dữ liệu sai chỉ cho gợi ý sai một cách tự tin hơn.
  * *Không có baseline và dòng tiền rõ:* Chưa ai ghi nhận sự kiện "đến trạm mà trụ không dùng được", và chưa rõ tính năng tăng phiên sạc, giữ chân khách hay giảm chi phí hỗ trợ.
  * *Hướng đi:* Chưa duyệt. Đổi trọng tâm sang telemetry trụ (quy tắc heartbeat: báo trống nhưng 0 phiên trong N giờ thì gắn cờ nghi hỏng), thuộc đội hạ tầng nhiều hơn đội AI.

---