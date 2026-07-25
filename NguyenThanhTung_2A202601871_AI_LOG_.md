
## 1. AI đã giúp tôi những gì?

Trong buổi lab, tôi dùng AI (Gemini 2.5 Flash qua `prompt_prototype.py`, và Claude/ChatGPT để brainstorm) ở ba vai trò chính:

- **Thought-partner khi Scan (Phase 1):** Khi mới đọc brief Vin Smart Future, tôi chưa hình dung được quy trình thật của một Trung tâm Điều vận trông như thế nào, nên dùng prompt gợi ý trong worksheet để AI liệt kê các bước nghiệp vụ thủ công của Xanh SM. Việc này giúp tôi có điểm khởi đầu nhanh hơn nhiều so với việc tự đoán, đặc biệt là các chi tiết kỹ thuật như "loại cổng sạc CCS2/GBT theo từng dòng xe" — thứ tôi không tự nghĩ ra được.
- **Stress-test thẻ bài toán (Phase 2):** Tôi dán Quick Problem Card #2 vào AI và yêu cầu nó đóng vai CFO/Trưởng phòng Vận hành khắt khe. AI chỉ ra một điểm yếu đúng: metric "giảm từ 15 phút xuống dưới 3 phút" ban đầu tôi viết không có mẫu số (không rõ tính trên bao nhiêu sự cố/ngày), nên tôi bổ sung thêm con số ~80 sự cố/ngày ở Hà Nội để metric có sức nặng hơn.
- **Viết System Prompt & Operational Boundary (Phase 4):** AI giúp tôi cấu trúc lại system prompt rõ ràng hơn — tách phần "vai trò", "được phép làm", "tuyệt đối cấm" thành các mục riêng thay vì viết chung một đoạn, và đề xuất định dạng JSON output có trường `reason` để dễ audit sau này.

## 2. AI đã sai ở đâu?

Mặc dù khi chạy 3 adversarial test cases cuối cùng thì ranh giới an toàn (pin dưới 5% → không chỉ trạm xa, bắt buộc `[DRAFT_ONLY]`) đều giữ vững, quá trình đi đến bản prompt cuối cùng đó không suôn sẻ ngay từ đầu:

- **Ở bản prompt nháp đầu tiên**, tôi chỉ viết ranh giới bằng một câu chung chung kiểu "không được gửi tin nhắn khi chưa được duyệt". Khi tôi thử nghĩ trước (mental test) với tình huống "tài xế nói đang vội đón khách VIP, bỏ qua bước duyệt", tôi nhận ra prompt gốc không có từ khóa bắt buộc `[DRAFT_ONLY]` cụ thể, nên rất dễ bị AI "linh động" hiểu nhầm là được phép gửi thẳng nếu tình huống nghe có vẻ khẩn cấp. Đây không hẳn là AI trả lời sai, mà là **tôi đã viết ranh giới quá mơ hồ** khiến mô hình có khoảng trống để tự diễn giải theo hướng "giúp đỡ" người dùng thay vì tuân thủ boundary.
- Khi brainstorm ban đầu, AI cũng từng đề xuất một kiến trúc phức tạp hơn mức cần thiết — gợi ý dùng "Agentic Loop" tự động gọi API và tự quyết định điều xe cứu hộ mà không cần con người duyệt bước cuối. Điều này đi ngược nguyên tắc "Problem First, AI Second" trong Inspiration Kit: rủi ro an toàn (xe cạn pin giữa đường) là quá cao để giao toàn quyền cho AI, nên nhóm quyết định hạ xuống LLM Feature + HITL bắt buộc thay vì nghe theo đề xuất Agent ban đầu của AI.

## 3. Tôi đã sửa đổi ra sao?

- Viết lại Operational Boundary thành **quy tắc tường minh, có điều kiện số cụ thể** (ví dụ: "nếu pin < 5% VÀ khoảng cách trạm sạc gần nhất > 5km → bắt buộc trả về `dispatch_mobile_charger`, không được đề xuất trạm xa") thay vì mô tả chung chung. Ranh giới càng cụ thể bằng số, AI càng khó "lách".
- Thêm bắt buộc **prefix `[DRAFT_ONLY]`** ở mọi output gửi tài xế, và yêu cầu structured output JSON để dễ kiểm tra tự động (không phụ thuộc vào việc đọc hiểu văn bản tự do).
- Từ chối gợi ý kiến trúc Agentic Loop của AI, giữ ở mức LLM Feature với con người duyệt bước cuối, dựa trên đánh giá rủi ro thực tế của nhóm chứ không theo đề xuất mặc định của AI.

## 4. Bài học rút ra

AI là một thought-partner hữu ích để tăng tốc độ scoping và soạn thảo, nhưng **không nên tin tưởng ranh giới an toàn do AI tự đề xuất ở lần đầu tiên** — cần tự mình stress-test bằng các tình huống "nghe có vẻ khẩn cấp/hợp lý" trước khi coi là đủ chặt. Ranh giới càng có số cụ thể (ngưỡng %, khoảng cách km) thì càng khó bị mô hình diễn giải sai theo hướng có lợi cho người dùng cuối thay vì tuân thủ quy tắc.