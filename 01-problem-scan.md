# 01 — Problem Scan & Quick Assessments (Vin Smart Future)

> **Tài liệu nộp bài Lab 02:** Quét tìm kiếm cơ hội tối ưu hóa bằng AI (Phase 1: SCAN), đánh giá nhanh 3 bài toán tiềm năng (Phase 2: QUICK-ASSESS), khung đánh giá lợi ích định lượng kinh tế — thời gian và quyết định lựa chọn đề tài phân tích sâu thuộc hệ sinh thái Vingroup.

---

## 🔍 Phase 1 — SCAN: Quét cơ hội vận hành trong hệ sinh thái Vingroup

Áp dụng **4 Lenses** (Lặp lại, Tốn thời gian, AI-upgrade, Pain từ người khác) để khảo sát hoạt động vận hành tại 5 công ty thành viên Vingroup. Mọi bài toán đều được lượng hóa thời gian lãng phí và ước tính thiệt hại kinh tế.

| # | Đơn vị thành viên (Subsidiary) | Lăng kính (Lens) | Mô tả bài toán / Điểm nghẽn vận hành | Định lượng thời gian & Chi phí lãng phí (Ước tính) |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **Vinhomes** | AI-upgrade | Phân loại và định tuyến tự động phản ánh của cư dân trên App Vinhomes Resident (thay thế xử lý thủ công tốn 10–12 phút/ticket, SLA phản hồi chậm 4–12 giờ). | Lãng phí **~92 đến 300 giờ làm việc/ngày** trên toàn hệ thống (tùy kịch bản 550 – 1.800 phản ánh/ngày trên 110.000 căn hộ); chi phí nhân sự cơ học tiêu tốn **~2,06 đến 6,75 tỷ VNĐ/năm**. |
| 2 | **Xanh SM** | Tốn thời gian | Điều phối viên xử lý thủ công sự cố xe điện cạn pin giữa đường: đối chiếu vị trí GPS, tìm trạm sạc còn trụ trống, gọi xe cứu hộ sạc di động (12–15 phút/lượt). | Lãng phí **~20 giờ làm việc/ngày** của team điều phối (~80 sự cố pin/ngày tại Hà Nội theo kịch bản chuẩn của đề bài); rò rỉ doanh thu cuốc xe nằm chờ sạc **~1,82 tỷ VNĐ/năm**. |
| 3 | **VinFast** | Lặp lại | Đối soát dữ liệu phiên sạc định kỳ hằng tuần từ hàng nghìn trụ sạc đối tác công cộng ngoài hệ thống với bảng kê tài chính chi trả điện năng. | Lãng phí **~60 giờ/tuần** của chuyên viên kế toán vận hành; rủi ro thất thoát số liệu đối soát sai lệch ước tính **~500 triệu VNĐ/quý**. |
| 4 | **Vinmec** | Pain từ người khác | Bác sĩ lâm sàng chịu áp lực hành chính lớn khi mất 20–30 phút/bệnh nhân để tổng hợp bệnh án điện tử (EMR) thành bản tóm tắt xuất viện (Discharge Summary). | Lãng phí **~38 đến 108 giờ/ngày** của đội ngũ bác sĩ nội trú (tùy kịch bản 120 – 340 ca xuất viện/ngày); lãng phí giá trị chuyên môn tương đương **~3,41 đến 9,67 tỷ VNĐ/năm**. |
| 5 | **Vinpearl** | Tốn thời gian | Xử lý email đặt phòng khách đoàn (Group Booking) phức tạp từ công ty lữ hành: đọc văn bản không cấu trúc, kiểm tra quỹ phòng trống theo từng hạng phòng và soạn bản thảo báo giá. | Mất **25–40 phút/booking đoàn**; tỷ lệ trễ hạn báo giá 18% làm mất cơ hội chuyển đổi đơn hàng đoàn (ước tính rò rỉ doanh thu **~3 tỷ VNĐ/năm**). |

---

## 🃏 Phase 2 — QUICK-ASSESS: 3 Thẻ bài toán đánh giá nhanh

### 📌 Quick Problem Card #1: Vinhomes — Phân Loại & Định Tuyến Tự Động Phản Ánh Cư Dân

- **Tên bài toán (1 câu):** Phân loại đa nhãn và định tuyến tự động phản ánh, khiếu nại của cư dân trên ứng dụng Vinhomes Resident đến đúng ban quản lý chuyên trách.
- **Công ty thành viên:** Vinhomes.
- **Đối tượng trực tiếp chịu tác động (Actor):** Nhân viên Chăm sóc khách hàng (CSKH) tổng đài trung tâm và Ban Quản lý (BQL) các khu đô thị Vinhomes.
- **Quy trình thủ công hiện tại (4 bước):**
  1. Cư dân gửi phản ánh dạng văn bản tự do kèm hình ảnh qua ứng dụng Vinhomes Resident (vấn đề điện nước, vệ sinh, trật tự, kế toán phí, kỹ thuật thang máy).
  2. Nhân viên CSKH đọc nội dung phản ánh, tra cứu mã căn hộ và tòa nhà trên cơ sở dữ liệu cư dân.
  3. Đọc hiểu ngữ cảnh để phân loại sự vụ vào 1 trong hơn 30 danh mục phòng ban nghiệp vụ.
  4. Tạo phiếu yêu cầu (ticket) trên phần mềm quản lý và chuyển tiếp thủ công đến hòm thư BQL tòa nhà phụ trách.
- **Bước tốn nhiều thời gian / dễ phát sinh lỗi nhất:** Bước 2 & Bước 3 (⏱ Ước tính: 8–15 phút/ticket do mô tả cư dân dài dòng, dễ phân loại nhầm phòng ban dẫn đến chuyển tiếp lòng vòng).
- **Điểm AI có thể can thiệp hỗ trợ:** LLM tiếp nhận văn bản phản ánh, trích xuất thực thể (vị trí căn hộ, loại khiếu nại, mức độ khẩn cấp), gán nhãn danh mục và tạo bản thảo ticket định tuyến tự động đến đúng BQL tòa nhà.
- **Thước đo thành công định lượng (Metric có số cụ thể):**
  1. Giảm thời gian phân loại và tạo ticket từ 12 phút xuống dưới 1 phút/ticket (tiết kiệm từ 92 đến 300 giờ làm việc/ngày).
  2. Cắt giảm chi phí nhân sự vận hành tương đương 2,06 đến 6,75 tỷ VNĐ/năm (giải phóng 11,5 đến 37,5 FTE).
  3. Tỷ lệ định tuyến chính xác đến đúng bộ phận phụ trách đạt tối thiểu 92% ngay lần phân loại đầu tiên.
- **Kiến trúc giải pháp sơ bộ (Quick Architecture):** LLM Feature kết hợp Rule-based Router (LLM trích xuất intent/entity, rule định tuyến theo ma trận phân quyền BQL).

---

### 📌 Quick Problem Card #2: Xanh SM — Điều Phối Xử Lý Sự Cố Pin Thực Địa & Xe Sạc Di Động

- **Tên bài toán (1 câu):** Điều phối xử lý khẩn cấp sự cố pin EV thực địa và kích hoạt xe sạc di động khi pin dưới ngưỡng an toàn.
- **Công ty thành viên:** Xanh SM (GSM).
- **Đối tượng trực tiếp chịu tác động (Actor):** Điều phối viên (Dispatcher) tại Trung tâm Điều vận Xanh SM và Tài xế taxi điện Xanh SM.
- **Quy trình thủ công hiện tại (5 bước):**
  1. Tài xế gọi tổng đài điều vận thông báo tình trạng pin cạn kiệt hoặc trạm sạc chỉ định gặp sự cố.
  2. Điều phối viên tra cứu thủ công tọa độ GPS của xe trên cổng giám sát hành trình.
  3. Mở bản đồ trạm sạc VinFast, rà soát bán kính xung quanh để tìm trụ sạc tương thích cổng sạc (CCS2) còn chỗ trống.
  4. Soạn thảo văn bản tin nhắn chỉ dẫn lộ trình gửi qua ứng dụng tài xế.
  5. Liên hệ đội xe sạc pin di động (Mobile Charging Vehicle) qua điện thoại nếu pin xe dưới 5% hoặc trạm sạc ở quá xa.
- **Bước tốn nhiều thời gian / dễ phát sinh lỗi nhất:** Bước 3 & Bước 4 (⏱ Ước tính: 10–12 phút/lượt do thao tác đối chiếu đa màn hình và nhập liệu văn bản chỉ dẫn thủ công).
- **Điểm AI có thể can thiệp hỗ trợ:** Tiếp nhận thông số telemetry (vị trí GPS, tỷ lệ pin SOC, model xe), tự động truy vấn trạm sạc trống phù hợp, kiểm tra ngưỡng pin an toàn (< 5%) và sinh bản thảo tin nhắn điều phối kèm thẻ `[DRAFT_ONLY]` để điều phối viên bấm duyệt; tự động phát lệnh điều xe sạc di động khi pin chạm ngưỡng nguy cấp.
- **Thước đo thành công định lượng (Metric có số cụ thể):**
  1. Giảm tổng thời gian xử lý sự cố từ 15 phút/lượt xuống dưới 3 phút/lượt (giảm 80% thời gian xử lý).
  2. Tiết kiệm ~1,82 tỷ VNĐ/năm chi phí rò rỉ cuốc xe do giảm thời gian xe chờ sạc và ~538 triệu VNĐ/năm giờ công điều phối viên.
  3. Tỷ lệ đề xuất trạm sạc đúng cổng sạc và khoảng cách an toàn đạt trên 98%.
- **Kiến trúc giải pháp sơ bộ (Quick Architecture):** LLM Feature (Human-in-the-loop phê duyệt trước khi gửi tin; tích hợp ranh giới cấm vượt cấp).

---

### 📌 Quick Problem Card #3: Vinmec — Tự Động Hóa Soạn Thảo Tóm Tắt Hồ Sơ Xuất Viện (Discharge Summary)

- **Tên bài toán (1 câu):** Trích xuất dữ liệu lâm sàng từ Bệnh án Điện tử (EMR) để tự động soạn thảo bản tóm tắt hồ sơ xuất viện hỗ trợ bác sĩ lâm sàng.
- **Công ty thành viên:** Vinmec.
- **Đối tượng trực tiếp chịu tác động (Actor):** Bác sĩ lâm sàng điều trị nội trú và Bệnh nhân/Thân nhân người bệnh chờ thủ tục xuất viện.
- **Quy trình thủ công hiện tại (5 bước):**
  1. Bác sĩ tra cứu và thu thập diễn tiến điều trị của bệnh nhân trên hệ thống EMR (chẩn đoán vào viện, kết quả cận lâm sàng, thuốc đã dùng, thủ thuật can thiệp).
  2. Tổng hợp các mã bệnh ICD-10 và tóm tắt quá trình điều trị nội trú vào biểu mẫu xuất viện.
  3. Soạn thảo văn bản dặn dò tái khám, chế độ vận động/dinh dưỡng và đơn thuốc xuất viện bằng ngôn ngữ thông thường cho bệnh nhân.
  4. Rà soát chéo các chỉ số xét nghiệm và đơn thuốc để tránh sai lệch thông tin lâm sàng.
  5. Ký duyệt hồ sơ điện tử và gửi sang bộ phận hành chính in ấn bàn giao.
- **Bước tốn nhiều thời gian / dễ phát sinh lỗi nhất:** Bước 1 & Bước 3 (⏱ Ước tính: 20–30 phút/hồ sơ do dữ liệu điều trị phân tán ở nhiều phân hệ EMR khác nhau).
- **Điểm AI có thể can thiệp hỗ trợ:** LLM tiếp nhận các trường dữ liệu có cấu trúc và ghi chú lâm sàng từ EMR, tổng hợp các mốc điều trị và tạo bản thảo (draft) văn bản Discharge Summary theo quy chuẩn y khoa, đưa lên giao diện để bác sĩ xem xét và ký duyệt.
- **Thước đo thành công định lượng (Metric có số cụ thể):**
  1. Giảm thời gian soạn thảo hồ sơ xuất viện từ 25 phút xuống dưới 6 phút/bệnh nhân (tiết kiệm từ 38 đến 108 giờ làm việc/ngày của đội ngũ bác sĩ).
  2. Giá trị thời gian chuyên môn của bác sĩ được giải phóng để khám chữa bệnh ước tính từ 3,41 đến 9,67 tỷ VNĐ/năm.
  3. Tỷ lệ bác sĩ chấp thuận bản thảo sau hiệu chỉnh nhỏ đạt tối thiểu 90%.
- **Kiến trúc giải pháp sơ bộ (Quick Architecture):** LLM Feature có Human-in-the-loop (Bác sĩ bắt buộc phải ký số xác nhận, AI tuyệt đối không tự phát hành tài liệu y khoa).

---

## 📊 Khung Đánh Giá Lợi Ích Định Lượng So Sánh 3 Quick Problem Cards (Thời Gian, Chi Phí & Bằng Chứng Thực Tế)

Nhằm bảo đảm tính khách quan khi lựa chọn đề tài đi tiếp vào Phase 3 (Deep-Dive), dưới đây là khung đánh giá lợi ích định lượng chi tiết cho cả 3 bài toán, dựa trên số liệu thực tế công khai từ báo cáo thường niên doanh nghiệp và báo cáo thị trường lao động.

### 1. Bóc Tách Nguồn Gốc Dữ Liệu Thực Tế từ Internet & Tài Liệu Đề Bài

| Đơn vị thành viên | Bằng chứng thực tế công khai (`[PROVEN]`) | Cơ sở kịch bản đánh giá lợi ích (`[EXTRAPOLATED]`) |
| :--- | :--- | :--- |
| **Vinhomes** | • Quản lý vận hành **hơn 110.000 căn hộ, biệt thự** và **gần 493.000 cư dân** *(Báo cáo thường niên Vinhomes 2023–2024)*.<br>• Mức lương nhân viên CSKH/Helpdesk tại Hà Nội/TP.HCM: 9,5 – 12 triệu VNĐ/tháng, chi phí thực tế doanh nghiệp ~15 triệu VNĐ/tháng $\approx$ **85.200 VNĐ/giờ** *(Báo cáo tuyển dụng JobsGO, CareerLink 2024)*. | • **Tần suất gửi phản ánh hàng ngày**: Vinhomes không công bố số liệu ticket nội bộ. Nhóm xây dựng các kịch bản đánh giá lợi ích với tỷ lệ dao động từ 0,5% đến 1,6% số căn hộ/ngày. |
| **Xanh SM** | • Vận hành **hơn 288.000 phương tiện chạy điện**, chiếm **70,9% thị phần taxi điện toàn quốc** *(Báo cáo Bộ Xây dựng, Mordor Intelligence 2024)*.<br>• Lương điều phối viên: 12 – 15 triệu/tháng *(JobsGO)* $\to$ Chi phí: ~102.000 VNĐ/giờ.<br>• **Số ca cạn pin (~80 ca/ngày tại Hà Nội)**: **Trích dẫn trực tiếp từ file ví dụ chuẩn của đề bài tại `02-deliverable-example.md` (Dòng 114)**. | Giữ nguyên các giả định chuẩn do giảng viên cung cấp trong tài liệu bài lab. |
| **Vinmec** | • Chuỗi 7 Bệnh viện Đa khoa Quốc tế (Times City: 300 giường, Central Park: 178 giường, Cần Thơ: 155 giường...), tổng quy mô toàn hệ thống ước đạt 1.200 – 1.400 giường bệnh; doanh thu y tế đạt >5.300 tỷ VNĐ *(Báo cáo thường niên Vingroup 2024)*.<br>• Chi phí giờ công bác sĩ CKI/nội trú Vinmec: ~60 triệu VNĐ/tháng $\approx$ **340.000 VNĐ/giờ** *(Medpro, CareerLink 2024)*. | • **Số ca xuất viện hàng ngày**: Vinmec không công bố thống kê hồ sơ xuất viện. Nhóm xây dựng kịch bản đánh giá lợi ích dựa trên vòng quay giường bệnh với thời gian lưu viện trung bình (ALOS 3,5 – 5 ngày). |

---

### 2. Đánh Giá Lợi Ích Vận Hành & Tài Chính Cụ Thể Cho Cả 3 Đề Tài

#### a. Đánh giá lợi ích Đề tài 1: Vinhomes (110.000 căn hộ — Tiết kiệm 10 phút/ticket — Chi phí 85.200 VNĐ/giờ)
Do khối lượng ticket thực tế biến động theo mùa và sự kiện đô thị, nhóm xây dựng 3 kịch bản lợi ích:

| Kịch bản đánh giá lợi ích | Tỷ lệ căn hộ phản ánh / ngày | Khối lượng ticket / ngày | Thời gian tiết kiệm / ngày | Nhân sự giải phóng (FTE) | Chi phí tiết kiệm hàng năm (VNĐ) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Kịch bản Thấp (Bảo thủ)** | **0,5%** số căn | 550 tickets | 91,7 giờ/ngày | 11,5 nhân sự | **~2,06 tỷ VNĐ / năm** |
| **Kịch bản Cơ sở (Trung bình)** | **1,0%** số căn | 1.100 tickets | 183,3 giờ/ngày | 22,9 nhân sự | **~4,12 tỷ VNĐ / năm** |
| **Kịch bản Cao (Giờ cao điểm/Lễ)** | **1,6%** số căn | 1.800 tickets | 300,0 giờ/ngày | 37,5 nhân sự | **~6,75 tỷ VNĐ / năm** |

> *Ý nghĩa lợi ích:* Ngay tại kịch bản bảo thủ nhất (0,5%), giải pháp vẫn giúp tiết kiệm hơn **2 tỷ VNĐ/năm** và giải phóng hơn **11 nhân sự**.

#### b. Đánh giá lợi ích Đề tài 3: Vinmec (1.200–1.400 giường — Tiết kiệm 19 phút/ca — Chi phí bác sĩ 340.000 VNĐ/giờ)
Số ca xuất viện hàng ngày được ước tính theo công thức: $\text{Số ca/ngày} = \frac{\text{Số giường vận hành} \times \text{Công suất sử dụng giường (Occupancy)}}{\text{Ngày nằm viện trung bình (ALOS)}}$.

| Kịch bản đánh giá lợi ích | Tham số giường & Thời gian lưu viện | Số ca xuất viện / ngày | Thời gian bác sĩ tiết kiệm / ngày | Nhân sự bác sĩ tương đương | Giá trị chuyên môn giải phóng / năm |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **Kịch bản Thấp (Bảo thủ)** | 1.200 giường, 50% công suất, ALOS 5 ngày | 120 ca/ngày | 38,0 giờ/ngày | 4,7 bác sĩ | **~3,41 tỷ VNĐ / năm** |
| **Kịch bản Cơ sở (Trung bình)** | 1.300 giường, 70% công suất, ALOS 4 ngày | 228 ca/ngày | 72,2 giờ/ngày | 9,0 bác sĩ | **~6,48 tỷ VNĐ / năm** |
| **Kịch bản Cao (Tối đa)** | 1.400 giường, 85% công suất, ALOS 3,5 ngày | 340 ca/ngày | 107,7 giờ/ngày | 13,5 bác sĩ | **~9,67 tỷ VNĐ / năm** |

> *Ý nghĩa lợi ích:* Giá trị quy đổi giờ công bác sĩ rất cao (3,41 – 9,67 tỷ/năm), tuy nhiên đây là giá trị năng suất chuyên môn nội bộ, không tạo ra dòng tiền tiết kiệm trực tiếp từ việc giảm chi phí tuyển dụng như ở CSKH.

#### c. Đánh giá lợi ích Đề tài 2: Xanh SM (Số liệu đề bài tại `02-deliverable-example.md`)
- Khối lượng: **80 sự cố pin/ngày** tại địa bàn Hà Nội.
- Thời gian tiết kiệm: 12 phút/lượt $\to$ **20 giờ làm việc/ngày** của team điều phối (tiết kiệm ~538 triệu VNĐ/năm).
- Thiệt hại cuốc xe mất đi khi xe nằm đường chờ sạc: ~250.000 VNĐ/sự cố $\to$ Bảo toàn **~1,82 tỷ VNĐ/năm** doanh thu vận hành.
- Tổng giá trị kinh tế mang lại: **~2,36 tỷ VNĐ/năm**.

---

### 3. Bảng Tổng Hợp Đối Chiếu Lợi Ích Toàn Diện (Tại Kịch Bản Cơ Sở / Trung Bình)

| Tiêu chí định lượng lợi ích | Đề tài 1: Vinhomes (Kịch bản Cơ sở) | Đề tài 2: Xanh SM (Kịch bản Đề bài) | Đề tài 3: Vinmec (Kịch bản Cơ sở) |
| :--- | :--- | :--- | :--- |
| **Khối lượng xử lý hàng ngày** | **1.100 tickets / ngày** | **80 sự cố / ngày** | **228 ca / ngày** |
| **Thời gian tiết kiệm trên mỗi lượt** | **10 phút / ticket** (giảm 90%) | **12 phút / lượt** (giảm 80%) | **19 phút / ca** (giảm 76%) |
| **Tổng thời gian tiết kiệm mỗi ngày** | **183,3 giờ làm việc / ngày** | **20,0 giờ làm việc / ngày** | **72,2 giờ làm việc / ngày** |
| **Tổng thời gian tiết kiệm mỗi năm** | **48.391 giờ / năm** (264 ngày) | **5.280 giờ / năm** (264 ngày) | **19.061 giờ / năm** (264 ngày) |
| **Định biên nhân sự giải phóng** | **22,9 nhân sự CSKH (FTE)** | **2,5 điều phối viên (FTE)** | **9,0 bác sĩ tương đương** |
| **Giá trị tài chính trực tiếp / năm** | **~4,12 tỷ VNĐ / năm** (tiết kiệm lương) | **~538 triệu VNĐ / năm** (giờ điều phối) | **~6,48 tỷ VNĐ / năm** (giờ công bác sĩ) |
| **Giá trị tài chính gián tiếp / năm** | Nâng cao CSAT, giảm khiếu nại | **~1,82 tỷ VNĐ / năm** (bảo toàn cuốc) | Giảm ùn ứ thủ tục hành chính |
| **Tổng giá trị kinh tế mang lại** | **~4,12 tỷ VNĐ / năm** | **~2,36 tỷ VNĐ / năm** | **~6,48 tỷ VNĐ / năm** |

---

### 4. Ma Trận Đánh Giá Đa Tiêu Chí Có Trọng Số

| Tiêu chí đánh giá trọng số | Trọng số | Đề tài 1: Vinhomes | Đề tài 2: Xanh SM | Đề tài 3: Vinmec |
| :--- | :---: | :--- | :--- | :--- |
| **1. Giá trị kinh tế & Tiết kiệm thời gian** | 30% | **Điểm: 9/10** (Tiết kiệm 4,12 - 6,75 tỷ VNĐ/năm chi phí tiền mặt thực tế). | **Điểm: 6/10** (2,36 tỷ VNĐ/năm, quy mô giới hạn ở đội xe Hà Nội). | **Điểm: 9/10** (6,48 - 9,67 tỷ VNĐ/năm giá trị chuyên môn bác sĩ). |
| **2. Kiểm soát rủi ro an toàn & pháp lý** | 30% | **Điểm: 9/10** (Quy trình nội bộ, không đe dọa tính mạng; có HITL duyệt). | **Điểm: 7/10** (Sự cố pin vật lý giữa đường; rủi ro xe cạn pin). | **Điểm: 3/10** (Rủi ro y tế và pháp lý cực kỳ cao; ảo giác gây nguy hiểm). |
| **3. Tính sẵn sàng của dữ liệu (Data Readiness)** | 25% | **Điểm: 9/10** (Hàng triệu logs ticket lịch sử có sẵn trên CRM Vinhomes). | **Điểm: 6/10** (Cần tích hợp dòng IoT telemetry xe và trạng thái trụ sạc). | **Điểm: 2/10** (Dữ liệu EMR bảo mật nghiêm ngặt; không thể tiếp cận). |
| **4. Độ phù hợp kiến trúc AI (AI Fit)** | 15% | **Điểm: 9/10** (LLM Feature + Rule Router rất phù hợp và khả thi). | **Điểm: 6/10** (Ngưỡng an toàn vật lý pin < 5% phù hợp Hard Rules hơn). | **Điểm: 5/10** (Đòi hỏi hội đồng chuyên môn y tế thẩm định phức tạp). |
| **TỔNG ĐIỂM CÓ TRỌNG SỐ** | **100%** | **8,95 / 10 (HẠNG NHẤT)** | **6,35 / 10 (HẠNG BA)** | **4,80 / 10 (HẠNG TƯ - LOẠI)** |

---

## 🗳️ Quyết Định Lựa Chọn Của Nhóm Cho Bài Phân Tích Sâu (Phase 3)

### 1. Đề tài được nhóm thống nhất chọn
**Vinhomes — Phân loại & Định tuyến tự động phản ánh/khiếu nại của cư dân trên App Vinhomes Resident (Quick Problem Card #1)**.

### 2. Luận cứ bảo vệ quyết định lựa chọn dựa trên đánh giá lợi ích
1. **Dòng tiền tiết kiệm thực tế bền vững và minh bạch:**
   - Dù ở kịch bản bảo thủ nhất (0,5% số căn hộ gửi ticket $\approx$ 550 tickets/ngày), hệ thống vẫn giúp Vinhomes tiết kiệm **hơn 2,06 tỷ VNĐ/năm** và giải phóng **11,5 nhân sự CSKH**. Ở kịch bản cơ sở, con số này đạt **4,12 tỷ VNĐ/năm** (giải phóng 22,9 nhân sự). Đây là khoản cắt giảm chi phí tiền mặt trực tiếp cho khối vận hành.
2. **Chỉ số an toàn vận hành vượt trội so với Vinmec:**
   - Điểm kiểm soát rủi ro của Vinhomes đạt **9/10** so với **3/10** của Vinmec. Việc phân loại nhầm danh mục phản ánh tại Vinhomes có thể hiệu chỉnh tức thì qua giao diện của nhân viên CSKH mà không gây nguy cơ đe dọa tính mạng con người như sai lệch thông tin lâm sàng tại Vinmec.
3. **Tính sẵn sàng của dữ liệu vượt trội so với Xanh SM và Vinmec:**
   - Vinhomes có dữ liệu text ticket lịch sử phong phú, không đòi hỏi kết nối phần cứng viễn thông IoT phức tạp như Xanh SM và không vướng rào cản bảo mật nghiêm ngặt của Luật Khám bệnh, chữa bệnh như Vinmec.

### 3. Lý do không chọn các bài toán còn lại

- **Lý do không chọn Xanh SM (Quick Problem Card #2 — Sự cố sạc pin thực địa):**
  - *Quy mô tác động tài chính hạn chế hơn*: Tổng giá trị kinh tế của Xanh SM đạt khoảng 2,36 tỷ VNĐ/năm, thấp hơn đáng kể so với tiềm năng tiết kiệm của Vinhomes (từ 4,12 đến 6,75 tỷ VNĐ/năm).
  - *Logic ranh giới an toàn thực chất là Hard Rules*: Ngưỡng pin $< 5\%$ cấm điều xe đi xa là quy tắc logic vật lý cố định, giải quyết bằng các câu lệnh điều kiện `if-else` thông thường mang lại độ tin cậy cơ học cao hơn là dùng mô hình ngôn ngữ lớn (LLM).

- **Lý do không chọn Vinmec (Quick Problem Card #3 — Tóm tắt hồ sơ xuất viện):**
  - *Rủi ro pháp lý và an toàn sức khỏe quá cao (Điểm rủi ro: 3/10)*: Dù giá trị thời gian chuyên môn của bác sĩ được giải phóng rất lớn (~6,48 tỷ VNĐ/năm), rủi ro ảo giác (hallucination) trong trích xuất đơn thuốc hoặc diễn tiến phẫu thuật có thể dẫn đến hậu quả pháp lý nghiêm trọng.
  - *Không thể tiếp cận dữ liệu thực tế (Điểm dữ liệu: 2/10)*: Thiếu dữ liệu EMR thực tế để kiểm chứng và đánh giá ranh giới an toàn trong khuôn khổ thời gian của bài lab.
