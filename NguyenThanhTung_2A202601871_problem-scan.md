

# Phase 1 — SCAN

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Xanh SM** | Tốn thời gian | Điều phối viên xử lý thủ công sự cố tài xế báo hết pin/xin cứu hộ giữa đường: tự tra vị trí GPS, tự tra trạm sạc VinFast còn trụ trống, tự soạn tin nhắn hướng dẫn (mất ~15 phút/lượt, ~80 lượt/ngày tại Hà Nội). |
| 2 | **Xanh SM** | Lặp lại | Re-route và phân bổ lại cuốc xe khi khách đổi điểm đến giữa chừng — điều phối viên phải thao tác lại thủ công trên hệ thống thay vì tự động cập nhật. |
| 3 | **VinFast** | Lặp lại | Đối chiếu hóa đơn sạc điện hằng tuần từ hàng nghìn trụ sạc đối tác bên ngoài với dữ liệu tài chính nội bộ — hiện làm thủ công bằng Excel, dễ sai lệch số liệu. |
| 4 | **Vinhomes** | AI-upgrade | Phân loại và định tuyến phản ánh của cư dân trên App Vinhomes Resident (mất nước, hỏng đèn, tiếng ồn...) đến đúng ban quản lý tòa nhà — hiện CSKH trả lời rập khuôn, chậm tới 12 tiếng. |
| 5 | **Vinmec** | Pain từ người khác | Bác sĩ mất 20–30 phút/bệnh nhân để soạn tóm tắt hồ sơ xuất viện từ bệnh án điện tử và ghi chú lâm sàng, gây quá tải và phàn nàn từ đội ngũ y bác sĩ. |

---

# Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Top 3 chọn từ SCAN: **#1 (Xanh SM sự cố sạc pin), #4 (Vinhomes phân loại phản ánh), #5 (Vinmec tóm tắt xuất viện).**

## Quick Problem Card #1 — Xanh SM: Xử lý sự cố sạc pin thực địa

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                        │
│                                                                │
│ Bài toán: Tài xế Xanh SM báo hết pin/sạc dở giữa đường,      │
│ cần điều phối cứu hộ hoặc trạm sạc gần nhất.                 │
│ Công ty thành viên: [x] Xanh SM                               │
│                                                                │
│ Ai đang đau? Tài xế (chờ đợi giữa đường), Điều phối viên      │
│ (quá tải giờ cao điểm)                                        │
│                                                                │
│ Workflow thủ công hiện tại (5 bước):                          │
│   1. Tài xế gọi báo sự cố ──> 2. Tra vị trí GPS xe            │
│   ──> 3. Tra trạm sạc trống phù hợp loại cổng sạc              │
│   ──> 4. Soạn tin nhắn hướng dẫn ──> 5. Gọi cứu hộ (nếu cần)  │
│                                                                │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3–4 (⏱ 10 phút/lượt)    │
│ AI có thể hỗ trợ ở bước nào? Bước 3–4 (tự động lấy vị trí,    │
│ tra trạm sạc trống, draft tin nhắn hướng dẫn)                 │
│                                                                │
│ Đo thành công bằng gì (Metric có số)?                          │
│ Giảm thời gian xử lý sự cố từ 15 phút ──> dưới 3 phút.        │
│                                                                │
│ Quick Architecture: [x] LLM Feature  [ ] Rule [ ] Agent       │
└─────────────────────────────────────────────────────────────┘
```

## Quick Problem Card #2 — Vinhomes: Phân loại & điều hướng phản ánh cư dân

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                        │
│                                                                │
│ Bài toán: Phản ánh của cư dân (mất nước, hỏng đèn, ồn ào...)  │
│ gửi qua App bị phản hồi chậm và rập khuôn.                    │
│ Công ty thành viên: [x] Vinhomes                              │
│                                                                │
│ Ai đang đau? Cư dân (chờ phản hồi), CSKH (xử lý thủ công       │
│ khối lượng lớn ticket)                                        │
│                                                                │
│ Workflow thủ công hiện tại (4 bước):                          │
│   1. Cư dân gửi phản ánh ──> 2. CSKH đọc & phân loại thủ công │
│   ──> 3. Chuyển ticket đến đúng ban quản lý tòa               │
│   ──> 4. Ban quản lý xử lý & phản hồi cư dân                  │
│                                                                │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 (⏱ phân loại sai      │
│ khiến ticket bị chuyển nhầm ban, mất thêm 12 tiếng)           │
│ AI có thể hỗ trợ ở bước nào? Bước 2 (tự động phân loại &      │
│ gợi ý ban quản lý phù hợp, kèm draft phản hồi mẫu)            │
│                                                                │
│ Đo thành công bằng gì (Metric có số)?                          │
│ Giảm thời gian phân loại & định tuyến từ 12 tiếng ──> dưới    │
│ 1 tiếng; tỉ lệ chuyển đúng ban đạt ≥ 90%.                     │
│                                                                │
│ Quick Architecture: [ ] LLM Feature  [x] Rule (kết hợp LLM     │
│ để phân loại ngôn ngữ tự nhiên trước khi route)                │
└─────────────────────────────────────────────────────────────┘
```

## Quick Problem Card #3 — Vinmec: Soạn tóm tắt hồ sơ xuất viện

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                        │
│                                                                │
│ Bài toán: Bác sĩ mất nhiều thời gian soạn tóm tắt hồ sơ       │
│ xuất viện cho bệnh nhân từ bệnh án điện tử.                   │
│ Công ty thành viên: [x] Vinmec                                │
│                                                                │
│ Ai đang đau? Bác sĩ (quá tải cuối ca), Bệnh nhân (chờ hồ sơ    │
│ xuất viện lâu)                                                │
│                                                                │
│ Workflow thủ công hiện tại (4 bước):                          │
│   1. Bác sĩ tổng hợp bệnh án, xét nghiệm, ghi chú điều trị    │
│   ──> 2. Tự viết tóm tắt bằng ngôn ngữ dễ hiểu cho bệnh nhân  │
│   ──> 3. Rà soát lại thông tin thuốc/liều dùng                │
│   ──> 4. Ký duyệt & in hồ sơ xuất viện                        │
│                                                                │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 (⏱ 20–30 phút/       │
│ bệnh nhân, dễ sót thông tin quan trọng)                       │
│ AI có thể hỗ trợ ở bước nào? Bước 2 (draft bản tóm tắt từ dữ  │
│ liệu bệnh án, bác sĩ chỉ cần rà soát & chỉnh sửa)              │
│                                                                │
│ Đo thành công bằng gì (Metric có số)?                          │
│ Giảm thời gian soạn thảo từ 25 phút ──> dưới 8 phút/          │
│ bệnh nhân, độ chính xác thông tin thuốc phải đạt 100%.        │
│                                                                │
│ Quick Architecture: [x] LLM Feature (bắt buộc bác sĩ duyệt    │
│ trước khi phát hành — không tự động gửi cho bệnh nhân)         │
└─────────────────────────────────────────────────────────────┘
```

---
