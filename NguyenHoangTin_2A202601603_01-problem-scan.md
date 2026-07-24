# Lab 02 — Problem Scan & Quick Problem Cards

> **Quy ước về số liệu:** Các số liệu thời gian, tần suất và tỷ lệ trong tài liệu này là giả định scoping của cá nhân tôi để so sánh cơ hội. Chúng không được xem là số liệu vận hành chính thức của Vingroup. Trước pilot, các giả định phải được xác minh bằng ticket, log hệ thống, time study và phỏng vấn stakeholder.

## 1. Mục tiêu và phương pháp SCAN

Trong vai trò AI Product Engineer tại Vin Smart Future, tôi rà soát các điểm nghẽn vận hành tại các công ty thành viên Vingroup dựa trên 4 thấu kính (Lenses):

Repetitive (Lặp lại): Các tác vụ xử lý theo quy trình cố định với mẫu dữ liệu tương tự.

Time-consuming (Tốn thời gian): Các khâu thủ công kéo dài thời gian xử lý của nhân sự.

AI-upgrade (Nâng cấp bằng AI): Tác vụ hiện có nhưng sẽ tăng vượt trội về tốc độ/chất lượng nếu ứng dụng xử lý ngôn ngữ hoặc thị giác máy tính.

Stakeholder Pain (Điểm nghẽn trải nghiệm): Nơi phát sinh chờ đợi, khiếu nại hoặc áp lực cho khách hàng/nhân viên.

## 2. Danh sách cơ hội

| # | Công ty | Lens chính | Actor gặp pain | Bài toán vận hành | Baseline cần xác minh | Hướng giải pháp ban đầu |
|---:|---|---|---|---|---|---|
| 1 | Xanh SM | Repetitive | Điều phối viên | Phân bổ lại cuốc xe khi khách đổi điểm đến hoặc tài xế không thể tiếp tục chuyến | 5–8 phút/lượt | Rule/optimization |
| 2 | Xanh SM | Time-consuming, Stakeholder Pain | Tài xế, điều phối viên | Xử lý sự cố xe sắp hết pin: xác minh xe, tìm trạm, soạn hướng dẫn hoặc gọi hỗ trợ | Khoảng 15 phút/lượt | Rule + LLM + HITL |
| 3 | VinFast | Repetitive | Nhân viên tài chính vận hành | Đối soát hóa đơn sạc với log giao dịch và xử lý dòng lệch | Khoảng 4 giờ/batch tuần | Rule-based matching |
| 4 | Vinhomes | AI-upgrade, Stakeholder Pain | Cư dân, CSKH | Đọc, phân loại, ưu tiên và chuyển tuyến phản ánh cư dân | Khoảng 8 phút/ticket | LLM classifier + HITL |
| 5 | Vinmec | Time-consuming | Bác sĩ | Tổng hợp hồ sơ và soạn bản tóm tắt xuất viện | 20–30 phút/bệnh nhân | LLM draft, bác sĩ duyệt |
| 6 | Vinpearl | AI-upgrade | Guest Relations | Tổng hợp phản hồi đa ngôn ngữ từ nhiều kênh | 1–2 ngày/báo cáo | LLM summarize/classify |
| 7 | VinFast | Stakeholder Pain | Kỹ thuật viên dịch vụ | Tìm kiếm hướng dẫn sửa chữa phù hợp từ tài liệu kỹ thuật dài | 10–20 phút/ca | Retrieval + LLM, kỹ sư duyệt |
| 8 | Xanh SM | Time-consuming | Phân tích vận hành | Tóm tắt lý do hủy chuyến từ ghi chú và transcript để phát hiện pattern | 1 ngày/báo cáo | Offline LLM analytics |

## 3. Ma trận sàng lọc

Thang điểm 1–5; điểm cao là thuận lợi. Với **Safety controllability**, 5 nghĩa là rủi ro dễ giới hạn bằng rule/HITL. Đây là đánh giá ban đầu, không thay thế discovery thực địa.

| Cơ hội | Giá trị vận hành | Dữ liệu sẵn có | AI cần thiết | Safety controllability | Khả năng đo lường | Tổng /25 |
|---|---:|---:|---:|---:|---:|---:|
| Xanh SM — sự cố pin | 5 | 4 | 4 | 4 | 5 | **22** |
| Vinhomes — phản ánh cư dân | 4 | 4 | 4 | 3 | 4 | **19** |
| VinFast — đối soát sạc | 4 | 5 | 2 | 5 | 5 | **21** |
| Vinmec — tóm tắt xuất viện | 4 | 3 | 4 | 2 | 4 | **17** |
| Vinpearl — phản hồi đa ngôn ngữ | 3 | 4 | 4 | 4 | 3 | **18** |

VinFast đối soát có điểm tổng cao nhưng **AI cần thiết chỉ đạt 2/5**; rule-based matching phù hợp hơn. Vì vậy tôi đưa Xanh SM, Vinhomes và VinFast vào Quick Problem Cards để thể hiện rõ sự khác nhau giữa LLM-fit và rule-fit.

## 4. Quick Problem Card 1

### Xanh SM — Hỗ trợ xử lý sự cố pin thực địa

| Thuộc tính | Nội dung |
|---|---|
| **Bài toán một câu** | Giảm thời gian điều phối khi tài xế Xanh SM báo xe sắp hết pin, đồng thời không đánh đổi an toàn. |
| **Actor** | Điều phối viên Trung tâm Điều vận; stakeholder chịu tác động là tài xế và hành khách kế tiếp. |
| **Trigger** | Tài xế gọi/app báo pin thấp hoặc không chắc có thể tới trạm sạc. |
| **Input** | Biển số/vehicle ID, mức pin, GPS, loại xe/cổng sạc, khoảng cách, trạng thái trụ. |
| **Output** | Bản nháp hướng dẫn tới trạm phù hợp hoặc bản nháp lệnh `dispatch_mobile_charger`. |

#### Current workflow

```text
1. Tài xế gọi báo sự cố
→ 2. Dispatcher xác minh xe, pin và vị trí GPS
→ 3. Dispatcher tra trạm, khoảng cách, cổng sạc và trụ trống
→ 4. Dispatcher soạn hướng dẫn
→ 5. Dispatcher gửi tin hoặc gọi đội hỗ trợ lưu động
```

- **Bottleneck:** Bước 3–4, giả định 10 phút trong tổng 15 phút/lượt.
- **Root cause giả định:** chuyển đổi giữa nhiều màn hình; dữ liệu ở dạng cấu trúc nhưng hướng dẫn đầu ra là ngôn ngữ tự nhiên; áp lực thời gian làm tăng nguy cơ bỏ sót điều kiện.
- **AI step:** LLM chỉ soạn bản nháp từ dữ liệu đã được rule/API xác minh.
- **Phần không giao cho AI:** xác thực dữ liệu, áp dụng ngưỡng an toàn, gửi tin, điều xe và phê duyệt.
- **Success metrics:**
  - Median handling time: 15 phút → dưới 3 phút.
  - ≥98% output dùng đúng dữ liệu trạm/cổng đã cung cấp.
  - 100% output dành cho tài xế bắt đầu bằng `[DRAFT_ONLY]`.
  - 100% ca pin dưới 5% có trạm yêu cầu xa hơn 5 km được chuyển sang `dispatch_mobile_charger`.
  - 0 hành động được gửi/thực thi khi chưa có phê duyệt của dispatcher.
- **Quick Architecture:** **Rule-based safety gate + LLM Feature + HITL**.
- **Rủi ro chính:** dữ liệu trạm cũ, hallucination, prompt injection, automation bias.

## 5. Quick Problem Card 2

### Vinhomes — Phân loại và chuyển tuyến phản ánh cư dân

| Thuộc tính | Nội dung |
|---|---|
| **Bài toán một câu** | Giảm thời gian đọc và chuyển tuyến phản ánh cư dân mà không để AI tự quyết định các vấn đề pháp lý hoặc an toàn. |
| **Actor** | Nhân viên CSKH, Ban quản lý tòa nhà và cư dân. |
| **Trigger** | Cư dân gửi phản ánh bằng văn bản/ảnh trên ứng dụng. |
| **Input** | Nội dung phản ánh, tòa/căn hộ, thời gian, lịch sử ticket và taxonomy bộ phận. |
| **Output** | Nhãn vấn đề, mức ưu tiên, bộ phận đề xuất và bản nháp phản hồi tiếp nhận. |

#### Current workflow

```text
1. Nhận phản ánh
→ 2. Đọc nội dung và ảnh
→ 3. Phân loại/mức ưu tiên
→ 4. Xác định bộ phận phụ trách
→ 5. Nhập ticket và phản hồi ban đầu
```

- **Bottleneck:** Bước 2–4, giả định khoảng 8 phút/ticket.
- **AI step:** gợi ý taxonomy, priority, owner và draft acknowledgement.
- **Success metrics:**
  - ≥90% ticket được gợi ý đúng tuyến trong 30 giây.
  - Thời gian thao tác của agent: 8 phút → dưới 2 phút.
  - 100% ticket liên quan an toàn, pháp lý, phí hoặc tranh chấp được bắt buộc human review.
- **Quick Architecture:** **LLM Feature + confidence threshold + HITL**.
- **Rủi ro chính:** bỏ sót tình huống khẩn cấp, vi phạm riêng tư, phản hồi sai về phí/quy định.

## 6. Quick Problem Card 3

### VinFast — Đối soát giao dịch sạc

| Thuộc tính | Nội dung |
|---|---|
| **Bài toán một câu** | Rút ngắn thời gian đối soát hóa đơn với log trạm sạc và tập trung con người vào ngoại lệ thật sự. |
| **Actor** | Nhân viên tài chính vận hành trạm sạc. |
| **Trigger** | Batch đối soát theo ngày/tuần. |
| **Input** | Transaction ID, station ID, timestamp, kWh, đơn giá, thuế, tổng tiền và invoice ID. |
| **Output** | Các dòng matched, unmatched, duplicate và reason code. |

#### Current workflow

```text
1. Xuất log giao dịch
→ 2. Nhận dữ liệu hóa đơn
→ 3. Chuẩn hóa mã/thời gian
→ 4. So khớp
→ 5. Kiểm tra ngoại lệ và lập biên bản
```

- **Bottleneck:** chuẩn hóa và kiểm tra ngoại lệ, giả định 4 giờ/batch.
- **AI step phù hợp:** LLM chỉ giải thích ghi chú tự do hoặc draft biên bản ngoại lệ.
- **Success metrics:**
  - 4 giờ → dưới 1 giờ/batch.
  - ≥99,5% dòng được phân loại đúng.
  - 100% bút toán vẫn tuân theo kiểm soát tài chính hiện hành.
- **Quick Architecture:** **Rule-based**, không dùng LLM cho phép tính/so khớp cốt lõi.
- **Rủi ro chính:** sai số tài chính nếu dùng LLM cho tính toán; dữ liệu trùng hoặc timezone không đồng nhất.

## 7. Quyết định chọn bài toán

Tôi đề xuất **Card 1 — Xanh SM hỗ trợ xử lý sự cố pin thực địa** để đưa vào thảo luận và lựa chọn bài toán nhóm vì:

1. Pain trực tiếp, có áp lực thời gian và stakeholder rõ.
2. Workflow 5 bước có thể quan sát và đo.
3. Có phần rule-based rõ ràng và một phần ngôn ngữ tự nhiên phù hợp LLM.
4. Có thể khóa rủi ro bằng ngưỡng cứng, output draft và Human-in-the-loop.
5. Có thể pilot ở shadow mode mà chưa tác động đến tài xế.

### Vì sao chưa chọn các card khác?

- **Vinhomes:** đáng thử nhưng taxonomy, SLA và escalation policy cần discovery sâu; sai sót có thể dẫn tới khiếu nại pháp lý.
- **VinFast đối soát:** có giá trị nhưng bài toán cốt lõi là deterministic matching; dùng LLM làm kiến trúc chính sẽ tăng rủi ro mà không tăng giá trị tương ứng.

## 8. Kế hoạch xác minh giả định

Giả địnhCách kiểm chứngNgười cần phỏng vấn / Dữ liệuTiêu chí tiếp tụcWorkflow mất khoảng 15 phútTime study tối thiểu 50 caDispatcher, ticket logMedian $\ge 10$ phútBước 3–4 là bottleneckĐo thời gian theo từng bướcScreen recording/log thao tác đã được phépChiếm $\ge 50\%$ tổng thời gianAPI có đủ GPS/trạm/cổngData audit và API spikeĐội Fleet/Charging Platform$\ge 95\%$ field bắt buộc đầy đủHITL không tạo thêm chậm trễShadow pilotDispatcherReview median $\le 30$ giâyRule pin dưới 5% phù hợpSafety reviewFleet Safety/OperationsĐược phê duyệt bằng văn bản
