# 01 — Problem Scan & Quick Problem Cards

## Thông tin cá nhân


- **Nhóm:** T54
- **Vai trò giả định:** AI Product Engineer tại Vin Smart Future

> **Lưu ý về dữ liệu:** Các số liệu thời gian, tỷ lệ lỗi và khối lượng công việc trong tài liệu này là giả định ban đầu phục vụ hoạt động scoping. Chúng cần được kiểm chứng bằng log vận hành, phỏng vấn nhân viên và đo baseline trước khi đưa ra quyết định đầu tư.

---

# Phase 1 — SCAN: Quét cơ hội AI

Tôi sử dụng bốn lenses gồm **Lặp lại**, **Tốn thời gian**, **AI có thể tốt hơn** và **Pain từ stakeholder** để tìm các nút thắt vận hành có đầu vào, đầu ra và chỉ số thành công tương đối rõ.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---:|---|---|---|
| 1 | **VinFast** | AI có thể tốt hơn | Khách hàng mô tả lỗi xe bằng ngôn ngữ đời thường; nhân viên phải hỏi lại nhiều lần trước khi tạo phiếu dịch vụ và chuyển đúng nhóm kỹ thuật. |
| 2 | **Vinhomes** | Lặp lại | Nhân viên ban quản lý đọc và phân loại thủ công các phản ánh của cư dân như rò nước, mất điện, tiếng ồn, thẻ xe và phí dịch vụ để chuyển đến đúng bộ phận. |
| 3 | **Vinpearl** | Tốn thời gian | Nhân viên kinh doanh đọc email đặt phòng đoàn có nhiều yêu cầu khác nhau, nhập lại số lượng phòng, ngày ở, suất ăn và dịch vụ để kiểm tra khả năng đáp ứng. |
| 4 | **Vinmec** | Tốn thời gian | Bác sĩ hoặc nhân viên y tế phải tổng hợp thủ công thông tin từ bệnh án, xét nghiệm và hướng dẫn theo dõi để tạo bản nháp tóm tắt xuất viện. |
| 5 | **Xanh SM** | Pain từ stakeholder | Ghi chú và cuộc gọi về lý do hủy chuyến nằm ở nhiều dạng dữ liệu khác nhau, khiến bộ phận vận hành khó nhận ra nhanh các nguyên nhân lặp lại theo khu vực và khung giờ. |
| 6 | **Vinpearl / VinWonders** | Pain từ stakeholder | Phản hồi tiêu cực từ nhiều kênh được đọc rời rạc, nên các vấn đề nghiêm trọng như vệ sinh, an toàn hoặc thái độ phục vụ có thể không được ưu tiên đủ nhanh. |

## Đánh giá sơ bộ

Tôi chọn ba bài toán **#1 VinFast**, **#2 Vinhomes** và **#3 Vinpearl Group Booking** để làm Quick Problem Cards vì:

1. Quy trình hiện tại có thể mô tả thành 3–5 bước rõ ràng.
2. AI chủ yếu hỗ trợ xử lý ngôn ngữ, nhưng quyết định cuối vẫn do con người kiểm soát.
3. Có thể tạo dữ liệu giả để prototype mà không cần truy cập dữ liệu nhạy cảm thật.
4. Có metric về thời gian, độ đầy đủ và tỷ lệ route đúng để đánh giá.

---

# Phase 2 — QUICK-ASSESS

## QUICK PROBLEM CARD #1 — VinFast

### Bài toán một câu

**Tự động tóm tắt và phân loại mô tả lỗi xe bằng tiếng Việt để tạo bản nháp phiếu tiếp nhận dịch vụ VinFast.**

### Công ty thành viên

- [x] VinFast
- [ ] Xanh SM
- [ ] Vinhomes
- [ ] Vinmec
- [ ] Khác

### Ai đang đau (Actor/Operator)?

- Chủ xe phải mô tả lại vấn đề nhiều lần.
- Nhân viên tổng đài hoặc cố vấn dịch vụ phải hỏi lại để chuẩn hóa thông tin.
- Kỹ thuật viên có thể nhận phiếu thiếu dữ liệu hoặc bị chuyển sai nhóm chuyên môn.

### Workflow thủ công hiện tại

```text
1. Khách hàng gọi điện hoặc gửi mô tả lỗi
→ 2. Nhân viên hỏi lại dòng xe, thời điểm và biểu hiện
→ 3. Nhân viên viết ghi chú tự do vào hệ thống
→ 4. Nhân viên tự phân loại nhóm lỗi và mức ưu tiên
→ 5. Phiếu được chuyển cho cố vấn dịch vụ hoặc kỹ thuật viên
```

### Bước tốn thời gian/lỗi nhất

**Bước 2–4**, vì nhân viên phải diễn giải ngôn ngữ đời thường thành thông tin kỹ thuật có cấu trúc.

- **Ước tính:** 8–12 phút/lượt.
- **Lỗi có thể xảy ra:** thiếu trường thông tin, hiểu sai triệu chứng, chuyển sai nhóm xử lý hoặc bỏ sót tình huống an toàn.

### AI có thể hỗ trợ ở bước nào?

AI hỗ trợ tại **bước 2–4**:

- Trích xuất dòng xe, thời điểm xảy ra, dấu hiệu cảnh báo và khả năng vận hành.
- Tóm tắt mô tả theo mẫu phiếu chuẩn.
- Chỉ ra thông tin còn thiếu cần hỏi thêm.
- Đề xuất nhóm xử lý ban đầu.
- Dùng rule để đánh dấu các từ khóa nguy hiểm như khói, cháy, mất phanh hoặc xe không thể điều khiển.

### Metric có số

- Giảm thời gian tạo phiếu từ **10 phút xuống dưới 3 phút/lượt**.
- Ít nhất **90% phiếu** có đủ các trường thông tin bắt buộc.
- Tỷ lệ đề xuất đúng nhóm xử lý đạt **từ 85% trở lên** trên bộ dữ liệu test đã gán nhãn.
- **100% trường hợp có từ khóa an toàn nghiêm trọng** phải được chuyển cho con người kiểm tra ngay.

### Quick Architecture

- [ ] No AI
- [ ] Rule
- [x] **LLM Feature kết hợp Rule và Human-in-the-loop**
- [ ] Agent

### Operational boundary ban đầu

AI chỉ tạo **bản nháp** và đề xuất phân loại. AI không được:

- Kết luận chính xác bộ phận nào bị hỏng.
- Khẳng định xe an toàn để tiếp tục di chuyển.
- Tự phê duyệt bảo hành, báo giá hoặc đặt linh kiện.
- Tự gửi hướng dẫn cho khách khi chưa có nhân viên duyệt.

### Giả định cần xác minh

- Số phút xử lý hiện tại phải được đo từ log tổng đài.
- Nhóm lỗi phải được thống nhất với kỹ thuật viên trước khi thiết kế output JSON.
- Rule an toàn cần do chuyên gia kỹ thuật phê duyệt, không để LLM tự nghĩ.

---

## QUICK PROBLEM CARD #2 — Vinhomes

### Bài toán một câu

**Tự động phân loại và điều hướng phản ánh của cư dân Vinhomes đến đúng bộ phận vận hành, đồng thời đánh dấu các sự cố khẩn cấp.**

### Công ty thành viên

- [ ] VinFast
- [ ] Xanh SM
- [x] Vinhomes
- [ ] Vinmec
- [ ] Khác

### Ai đang đau (Actor/Operator)?

- Cư dân chờ lâu hoặc phải gửi lại phản ánh khi ticket bị chuyển sai.
- Nhân viên chăm sóc cư dân phải đọc, sửa và route nhiều ticket lặp lại.
- Đội kỹ thuật nhận ticket thiếu vị trí, hình ảnh hoặc mô tả cần thiết.

### Workflow thủ công hiện tại

```text
1. Cư dân gửi phản ánh trên ứng dụng hoặc hotline
→ 2. Nhân viên đọc mô tả và kiểm tra tòa/căn hộ
→ 3. Nhân viên chọn loại sự cố và mức ưu tiên
→ 4. Ticket được chuyển sang kỹ thuật, an ninh, vệ sinh hoặc CSKH
→ 5. Bộ phận nhận ticket liên hệ lại nếu thiếu thông tin
```

### Bước tốn thời gian/lỗi nhất

**Bước 2–3**, do nội dung phản ánh không theo mẫu cố định và một phản ánh có thể chứa nhiều vấn đề.

- **Ước tính:** 5–7 phút/ticket.
- **Lỗi có thể xảy ra:** route sai bộ phận, tạo ticket trùng, đánh giá thấp sự cố rò điện, cháy, kẹt thang máy hoặc vỡ đường ống.

### AI có thể hỗ trợ ở bước nào?

AI hỗ trợ tại **bước 2–3**:

- Trích xuất dự án, tòa, căn hộ, khu vực và loại sự cố.
- Phân loại ticket theo taxonomy có sẵn.
- Phát hiện thông tin còn thiếu.
- Nhóm các ticket có khả năng cùng một sự cố khu vực.
- Rule-based escalation cho sự cố liên quan an toàn.

### Metric có số

- Giảm thời gian phân loại từ **6 phút xuống dưới 1 phút/ticket**.
- Tỷ lệ route đúng bộ phận đạt **từ 90% trở lên**.
- Giảm ít nhất **50% ticket bị trả lại** do thiếu thông tin bắt buộc.
- Sự cố an toàn được gắn cờ trong **dưới 30 giây**.

### Quick Architecture

- [ ] No AI
- [ ] Rule
- [x] **LLM Feature kết hợp Rule**
- [ ] Agent

### Operational boundary ban đầu

AI không được:

- Tự xác định cư dân đúng hay sai trong tranh chấp.
- Tự cam kết thời gian hoàn thành hoặc mức bồi thường.
- Tự đóng ticket.
- Tự xử lý các nội dung có yếu tố pháp lý, phí dịch vụ hoặc xung đột giữa cư dân.

### Giả định cần xác minh

- Nếu taxonomy sự cố hiện tại đã rõ và ticket chủ yếu là lựa chọn từ menu, rule-based có thể đủ; LLM chỉ đáng dùng cho phần mô tả tự do.
- Cần kiểm tra tỷ lệ ticket thực sự bị route sai để tránh giải quyết một vấn đề nhỏ bằng hệ thống quá phức tạp.

---

## QUICK PROBLEM CARD #3 — Vinpearl

### Bài toán một câu

**Trích xuất yêu cầu từ email đặt phòng đoàn và tạo bản nháp booking để nhân viên Vinpearl kiểm tra.**

### Công ty thành viên

- [ ] VinFast
- [ ] Xanh SM
- [ ] Vinhomes
- [ ] Vinmec
- [x] Khác: Vinpearl

### Ai đang đau (Actor/Operator)?

- Nhân viên kinh doanh đoàn phải đọc email dài và nhập lại nhiều trường.
- Nhân viên đặt phòng phải hỏi lại khi yêu cầu thiếu hoặc mâu thuẫn.
- Công ty lữ hành chờ lâu để nhận báo giá và xác nhận khả năng đáp ứng.

### Workflow thủ công hiện tại

```text
1. Công ty lữ hành gửi email yêu cầu đặt phòng đoàn
→ 2. Nhân viên đọc email và file đính kèm
→ 3. Nhân viên nhập ngày ở, số khách, cơ cấu phòng và dịch vụ
→ 4. Nhân viên kiểm tra quỹ phòng và điều kiện áp dụng
→ 5. Nhân viên soạn email hỏi lại hoặc tạo báo giá nháp
```

### Bước tốn thời gian/lỗi nhất

**Bước 2–3**, vì thông tin nằm trong email tự do, bảng đính kèm và đôi khi có yêu cầu mâu thuẫn.

- **Ước tính:** 15–25 phút/yêu cầu.
- **Lỗi có thể xảy ra:** nhập sai ngày, số phòng, loại phòng, số trẻ em hoặc bỏ sót dịch vụ đi kèm.

### AI có thể hỗ trợ ở bước nào?

AI hỗ trợ tại **bước 2–3 và một phần bước 5**:

- Trích xuất thông tin thành JSON có cấu trúc.
- Đánh dấu trường bị thiếu hoặc mâu thuẫn.
- Tạo bản nháp yêu cầu kiểm tra phòng.
- Soạn email hỏi lại khách hàng dựa trên đúng các trường còn thiếu.

Việc kiểm tra phòng trống, giá và chính sách phải lấy từ hệ thống booking hoặc rule chính thức, không để LLM tự suy đoán.

### Metric có số

- Giảm thời gian nhập dữ liệu từ **20 phút xuống dưới 5 phút/yêu cầu**.
- Độ chính xác trích xuất các trường bắt buộc đạt **từ 95% trở lên**.
- Giảm ít nhất **60% lỗi nhập lại dữ liệu**.
- **100% booking** phải được nhân viên duyệt trước khi giữ phòng hoặc gửi báo giá.

### Quick Architecture

- [ ] No AI
- [ ] Rule
- [x] **LLM Feature + hệ thống booking + Human-in-the-loop**
- [ ] Agent

### Operational boundary ban đầu

AI không được:

- Tự xác nhận còn phòng nếu chưa truy vấn hệ thống chính thức.
- Tự tạo giá, khuyến mãi hoặc chính sách hoàn hủy.
- Tự giữ phòng hoặc gửi báo giá cuối cùng.
- Tự xử lý dữ liệu khách hàng ngoài mục đích tạo booking nháp.

### Giả định cần xác minh

- Cần thu thập một tập email đã ẩn danh để biết định dạng phổ biến.
- Nếu phần lớn booking đã theo biểu mẫu chuẩn, OCR/rule có thể rẻ và ổn định hơn LLM.
- Chi phí sai ngày hoặc sai số lượng phòng cao, nên bắt buộc có bước review.

---

# So sánh và đề xuất ưu tiên

| Tiêu chí | VinFast Service Intake | Vinhomes Ticket Routing | Vinpearl Group Booking |
|---|---:|---:|---:|
| Quy trình dễ mô tả | Cao | Cao | Cao |
| Dữ liệu giả dễ tạo | Cao | Cao | Trung bình |
| Giá trị của LLM so với rule | Cao | Trung bình–Cao | Cao |
| Rủi ro khi AI sai | Cao | Trung bình | Cao |
| Dễ xây prototype trong lab | Cao | Rất cao | Trung bình |
| Human-in-the-loop cần thiết | Bắt buộc | Với ticket nhạy cảm | Bắt buộc |

## Lựa chọn cá nhân đề xuất

Tôi đề xuất ưu tiên **Card #1 — VinFast Service Intake** cho bước Deep-Dive vì đầu vào là ngôn ngữ tự nhiên, output có thể chuẩn hóa thành JSON, metric rõ và có nhiều tình huống adversarial để kiểm tra operational boundary.

Tuy nhiên, nếu nhóm không có người hiểu quy trình dịch vụ ô tô, **Card #2 — Vinhomes Ticket Routing** là lựa chọn thực tế hơn. Một bài toán ít hào nhoáng nhưng có baseline và taxonomy rõ sẽ đáng tin hơn một hệ thống “chẩn đoán xe” chỉ dựa trên giả định.
