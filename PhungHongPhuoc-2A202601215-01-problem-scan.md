# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
|1|Xanh SM|Stakeholder Pain / Lặp lại|Route lại chuyến & Xử lý sự cố pin xe: Điều phối viên phải xác minh thủ công mức pin, vị trí xe dừng/hỏng và tìm xe cứu hộ/trạm sạc phù hợp khi tài xế gặp sự cố hết pin hoặc hỏng hóc giữa đường.|
|2|VinFast|Lặp lại / Tốn thời gian|So khớp & Xác minh hóa đơn/Giao dịch sạc điện: Nhân viên tài chính/CSKH phải đối soát thủ công hàng ngàn giao dịch sạc lỗi (lỗi kết nối cổng sạc, trừ tiền trùng, sai lệch dung lượng KWh) giữa ứng dụng VinFast và hệ thống trạm sạc.|
|3|Vinhomes|Tốn thời gian / Stakeholder Pain|Xử lý phản ánh & Đánh giá tiêu cực (1–3 stars) từ Cư dân: Ban quản lý tòa nhà tốn thời gian đọc, phân loại phản ánh (tiếng ồn, vệ sinh, sự cố kỹ thuật) và soạn thảo phản hồi riêng biệt, chính xác theo quy chuẩn cho từng căn hộ.|
|4|Vinpearl|AI-upgrade|Tư vấn & Lên lịch trình nghỉ dưỡng cá nhân hóa: Khách hàng mất nhiều thời gian chờ tư vấn viên hoặc nhận câu trả lời rập khuôn khi muốn phối hợp lịch trình (combo phòng + vé VinWonders + bữa ăn) theo sở thích gia đình/trẻ nhỏ.|
|5|Vinmec|Tốn thời gian / Lặp lại|Sắp xếp lịch trực & Bố trí ca khám tối ưu theo lưu lượng bệnh nhân: Bộ phận điều hành phải xếp lịch làm việc thủ công cho bác sĩ/điều dưỡng dựa trên dự báo lượng bệnh nhân đến khám theo mùa và các khung giờ cao điểm.|


# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #02                                                                  │
│                                                                                         │
│ Bài toán (1 câu): So khớp và tự động xử lý khiếu nại giao dịch sạc điện bị lỗi.        │
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác        │
│                                                                                         │
│ Ai đang đau (Actor)? Nhân viên Đối soát Tài chính & Chuyên viên CSKH VinFast            │
│                                                                                         │
│ Workflow thủ công hiện tại (3-5 bước):                                                 │
│   1. Tiếp nhận khiếu nại (bị trừ tiền không sạc được) ──> 2. Mở log trụ sạc & log App   │
│   ──> 3. Tự so khớp dữ liệu dòng tiền ──> 4. Tạo lệnh hoàn tiền trên hệ thống ERP       │
│                                                                                         │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3: Đọc và đối soát log dữ liệu bị lệch        │
│ (⏱ 15 - 20 phút/lượt)                                                                   │
│                                                                                         │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3: Tự động gom log, phát hiện bất thường │
│ (Anomaly Detection) và phân loại nguyên nhân lỗi.                                       │
│                                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                                   │
│ "Giảm thời gian xử lý khiếu nại sạc lỗi từ 24 giờ ──> under 15 phút; Tự động hóa 80%    │
│ các ca lỗi cơ bản."                                                                     │
│                                                                                         │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent                             │
└─────────────────────────────────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #01                                                                  │
│                                                                                         │
│ Bài toán (1 câu): Tự động hóa điều hướng trạm sạc khẩn cấp hoặc cứu hộ pin cho xe Taxi. │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác        │
│                                                                                         │
│ Ai đang đau (Actor)? Tài xế Xanh SM (khi pin dưới 10%) & Điều phối viên tổng đài        │
│                                                                                         │
│ Workflow thủ công hiện tại (3-5 bước):                                                 │
│   1. Tài xế báo nguy cơ cạn pin ──> 2. Điều phối viên gọi hỏi tọa độ & dung lượng pin   │
│   ──> 3. Tra cứu trạm sạc/xe sạc lưu động thủ công ──> 4. Gợi ý tuyến đường qua điện thoại  │
│                                                                                         │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3: Tra cứu & tính toán khoảng cách an toàn        │
│ (⏱ 8 - 12 phút/lượt)                                                                    │
│                                                                                         │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3 & 4: Tự động phân tích telemetry của xe    │
│ (pin, vị trí), tra cứu bán kính khả thi và xuất lệnh cứu hộ/dẫn đường.                  │
│                                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                                   │
│ "Giảm thời gian ra quyết định điều hướng từ 10 min ──> under 1 min; 0% sự cố xe cạn pin  │
│ giữa đường."                                                                            │
│                                                                                         │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent                             │
└─────────────────────────────────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #03                                                                  │
│                                                                                         │
│ Bài toán (1 câu): Phân loại phản ánh cư dân và tạo bản thảo phản hồi chuẩn mực.        │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  [ ] Vinmec  [ ] Khác        │
│                                                                                         │
│ Ai đang đau (Actor)? Ban Quản lý Tòa nhà (BQL) Vinhomes                                 │
│                                                                                         │
│ Workflow thủ công hiện tại (3-5 bước):                                                 │
│   1. Tiếp nhận ý kiến trên Resident App ──> 2. Đọc & phân loại mức độ khẩn cấp         │
│   ──> 3. Tra cứu Sổ tay Cư dân/Nội quy ──> 4. Viết email/tin nhắn phản hồi cho cư dân   │
│                                                                                         │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4: Tra cứu quy định và soạn thảo câu trả lời  │
│ (⏱ 10 - 15 phút/lượt)                                                                   │
│                                                                                         │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3 & 4: Gán nhãn độ khẩn, trích xuất quy   │
│ định liên quan bằng RAG và đề xuất sẵn bản thảo phản hồi cho Trưởng BQL duyệt.          │
│                                                                                         │
│ Đo thành công bằng gì (Metric có số)?                                                   │
│ "Giảm thời gian tạo phản hồi phản ánh từ 12 min ──> under 2 min; Tăng tỷ lệ hài lòng    │
│ (CSAT) lên 95%."                                                                        │
│                                                                                         │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent                             │
└─────────────────────────────────────────────────────────────────────────────────────────┘
```