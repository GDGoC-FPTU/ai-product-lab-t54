Học viên: Nguyễn Đức Sơn
MSSV: 2A202601485
Lớp/Nhóm: C-401
Lab: Lab 02 — AI Product Scoping

Ghi chú: Các mốc thời gian và chỉ số dưới đây là giả định ban đầu phục vụ bước scoping. Khi triển khai thực tế, nhóm cần xác minh lại bằng dữ liệu vận hành và phỏng vấn stakeholder.

PHASE 1 — SCAN

1. Bảng quét cơ hội AI

STT

Công ty/đơn vị

Bài toán thực tế

Actor/Operator chính

Thấu kính phát hiện cơ hội

Pain point hiện tại

Cơ hội ứng dụng AI

Giá trị kỳ vọng

1

VinFast

Phân loại yêu cầu bảo dưỡng/sửa chữa từ mô tả, ảnh và lịch sử xe trước khi khách đến xưởng

Cố vấn dịch vụ, tổng đài viên, kỹ thuật viên

Tốn thời gian + AI-upgrade + Stakeholder Pain

Nhân viên phải đọc mô tả không đồng nhất, hỏi lại nhiều lần và chuyển sai nhóm kỹ thuật

AI trích xuất triệu chứng, phân loại hạng mục, đánh giá mức khẩn cấp và gợi ý checklist tiếp nhận

Giảm thời gian tiếp nhận, giảm chuyển nhầm bộ phận, tăng tỷ lệ xử lý đúng ngay lần đầu

2

Vinmec

Tóm tắt hồ sơ khám trước buổi hẹn và phát hiện thông tin còn thiếu

Nhân viên điều phối khám, bác sĩ

Lặp lại + Tốn thời gian + Stakeholder Pain

Hồ sơ dài, dữ liệu nằm ở nhiều biểu mẫu; bác sĩ phải đọc lại nhiều thông tin trước khi khám

LLM tóm tắt có cấu trúc, nêu tiền sử, thuốc đang dùng, xét nghiệm gần nhất và cảnh báo trường dữ liệu thiếu

Giảm thời gian chuẩn bị hồ sơ; bác sĩ tập trung hơn vào thăm khám. Mọi kết luận y khoa vẫn do bác sĩ phê duyệt

3

Vinhomes

Phân loại và điều phối yêu cầu dịch vụ của cư dân

Nhân viên chăm sóc cư dân, ban quản lý, nhà thầu

Lặp lại + Tốn thời gian + Stakeholder Pain

Yêu cầu đến từ nhiều kênh, nội dung tự do, thiếu thông tin; dễ chuyển sai đơn vị và chậm SLA

AI chuẩn hóa nội dung, phân loại sự cố, hỏi bổ sung, gán mức ưu tiên và đề xuất đơn vị xử lý

Rút ngắn thời gian tạo phiếu, giảm backlog, tăng tỷ lệ xử lý đúng SLA

4

Vinpearl

Tiếp nhận và điều phối yêu cầu đa ngôn ngữ của khách lưu trú

Lễ tân, tổng đài, housekeeping, kỹ thuật

Lặp lại + AI-upgrade + Stakeholder Pain

Khách dùng nhiều ngôn ngữ; yêu cầu dễ bị hiểu thiếu hoặc chuyển chậm giữa các bộ phận

AI dịch, tóm tắt, phân loại yêu cầu, nhận diện mức khẩn cấp và tạo ticket thống nhất

Phản hồi nhanh hơn, giảm hiểu sai, nâng điểm hài lòng của khách

5

VinWonders

Dự báo tải khách theo khung giờ để bố trí nhân sự và hướng dẫn phân luồng

Điều hành công viên, quản lý vận hành

Tốn thời gian + AI-upgrade

Điều phối dựa nhiều vào kinh nghiệm; khi lượng khách biến động dễ xảy ra hàng đợi dài hoặc thừa/thiếu nhân sự

Mô hình dự báo kết hợp dữ liệu vé, lịch sự kiện, thời tiết và lịch sử hàng đợi để đề xuất phân bổ nhân sự

Giảm thời gian chờ, sử dụng nhân lực hiệu quả hơn, cải thiện trải nghiệm khách

6

VinBus

Tổng hợp và phân loại phản ánh của hành khách theo tuyến, thời gian và mức độ nghiêm trọng

Trung tâm vận hành, chăm sóc khách hàng

Lặp lại + Tốn thời gian + Stakeholder Pain

Phản ánh ở dạng văn bản tự do, trùng lặp và khó nhìn ra sự cố theo cụm

AI gom nhóm phản ánh tương tự, trích xuất tuyến/điểm dừng/thời gian và cảnh báo xu hướng bất thường

Phát hiện vấn đề sớm, ưu tiên xử lý đúng sự cố, giảm thời gian đọc thủ công

2. Sàng lọc nhanh

Thang điểm: 1 = thấp, 5 = cao.

Bài toán

Mức độ đau

Tần suất

Dữ liệu sẵn có

Khả năng đo lường

Rủi ro triển khai

Tổng tiềm năng

VinFast — Tiếp nhận yêu cầu dịch vụ

5

5

4

5

3

22/25

Vinmec — Tóm tắt hồ sơ khám

5

4

4

4

2

19/25

Vinhomes — Điều phối yêu cầu cư dân

5

5

4

5

4

23/25

Vinpearl — Yêu cầu đa ngôn ngữ

4

5

4

5

4

22/25

VinWonders — Dự báo tải khách

4

4

3

4

3

18/25

VinBus — Phân loại phản ánh

4

4

4

4

4

20/25

Ba bài toán được chọn để Quick-Assess:

Vinhomes — Phân loại và điều phối yêu cầu dịch vụ cư dân.

VinFast — Phân loại yêu cầu bảo dưỡng/sửa chữa trước khi khách đến xưởng.

Vinpearl — Tiếp nhận và điều phối yêu cầu đa ngôn ngữ của khách lưu trú.

Lý do lựa chọn: cả ba bài toán đều có tần suất cao, quy trình hiện tại chứa nhiều thao tác đọc–phân loại–chuyển giao lặp lại, có metric vận hành rõ và phù hợp với kiến trúc kết hợp Rule + LLM + Human-in-the-loop.

PHASE 2 — QUICK-ASSESS

QUICK PROBLEM CARD 1

1. Tên bài toán

AI hỗ trợ phân loại và điều phối yêu cầu dịch vụ cư dân tại Vinhomes

2. Actor/Operator

Cư dân gửi yêu cầu.

Nhân viên chăm sóc cư dân tiếp nhận và tạo phiếu.

Ban quản lý phân công.

Đội kỹ thuật, an ninh, vệ sinh hoặc nhà thầu xử lý.

3. Current-State Workflow

Cư dân gửi yêu cầu qua ứng dụng/điện thoại/quầy
        ↓
Nhân viên đọc nội dung và kiểm tra thông tin
        ↓
Nếu thiếu dữ liệu → liên hệ hỏi lại cư dân
        ↓
Phân loại thủ công: kỹ thuật / vệ sinh / an ninh / tiện ích / khác
        ↓
Ước lượng mức ưu tiên
        ↓
Tạo ticket và chuyển cho đơn vị phụ trách
        ↓
Đơn vị tiếp nhận kiểm tra lại
        ↓
Nếu chuyển sai → trả ticket/chuyển tiếp
        ↓
Xử lý và cập nhật kết quả cho cư dân

4. Bước tốn thời gian/gây lỗi nhiều nhất

Bước đọc nội dung, hỏi bổ sung và phân loại ticket.

Thời gian ước tính hiện tại: 5–8 phút/ticket.

Trường hợp nội dung thiếu hoặc mơ hồ có thể mất 10–15 phút do phải liên hệ lại.

Lỗi phổ biến: chọn sai loại yêu cầu, thiếu tòa/căn hộ/vị trí, gán sai mức khẩn cấp hoặc chuyển sai đội xử lý.

5. AI có thể tham gia ở đâu?

Trích xuất dữ liệu: tòa, căn hộ, khu vực, loại sự cố, thời gian phát sinh.

Phân loại yêu cầu vào taxonomy chuẩn.

Nhận diện từ khóa khẩn cấp như cháy, rò điện, mất nước diện rộng, kẹt thang máy.

Tạo câu hỏi bổ sung khi thiếu thông tin.

Đề xuất đội xử lý và SLA.

Sinh bản tóm tắt ticket ngắn gọn cho nhân viên phê duyệt.

6. Success Metrics

Giảm thời gian tạo ticket trung bình từ 6 phút xuống dưới 2 phút.

Tỷ lệ phân loại đúng ngay lần đầu đạt ≥ 90%.

Giảm tỷ lệ ticket bị chuyển lại/chuyển sai ít nhất 40%.

Tăng tỷ lệ yêu cầu được tiếp nhận trong SLA lên ≥ 95%.

100% ticket mức nguy hiểm cao phải được nhân viên xác nhận trước khi điều phối.

7. Kiến trúc sơ bộ

Hybrid: Rule + LLM Feature + Human-in-the-loop

Input đa kênh
   ↓
Rule kiểm tra trường bắt buộc và từ khóa khẩn cấp
   ↓
LLM trích xuất + phân loại + tóm tắt
   ↓
Confidence Gate
   ├── Tin cậy cao → đề xuất ticket
   └── Tin cậy thấp/rủi ro cao → chuyển nhân viên kiểm tra
   ↓
Nhân viên phê duyệt
   ↓
Hệ thống tạo và điều phối ticket

Không dùng Agent tự chủ hoàn toàn ở giai đoạn đầu.

Fallback: khi LLM lỗi hoặc confidence thấp, giao diện quay về quy trình tạo ticket thủ công.

Không gửi dữ liệu định danh nhạy cảm sang mô hình không được doanh nghiệp phê duyệt.

8. Nhận định nhanh

Khuyến nghị: GO cho MVP giới hạn.Phạm vi MVP nên bắt đầu với 5–7 loại yêu cầu có dữ liệu lịch sử rõ, chưa tự động xử lý các sự cố an toàn cao.

QUICK PROBLEM CARD 2

1. Tên bài toán

AI hỗ trợ tiếp nhận yêu cầu bảo dưỡng/sửa chữa xe tại VinFast

2. Actor/Operator

Chủ xe.

Tổng đài viên/cố vấn dịch vụ.

Điều phối xưởng.

Kỹ thuật viên chẩn đoán và sửa chữa.

3. Current-State Workflow

Khách mô tả triệu chứng qua điện thoại/form/chat
        ↓
Cố vấn dịch vụ hỏi thêm thông tin
        ↓
Đọc lịch sử bảo dưỡng và thông tin xe
        ↓
Phân loại sơ bộ hệ thống có vấn đề
        ↓
Đánh giá mức độ có thể tiếp tục vận hành hay cần hỗ trợ khẩn cấp
        ↓
Đặt lịch và phân bổ kỹ thuật viên
        ↓
Khách đưa xe đến xưởng
        ↓
Kỹ thuật viên hỏi/chẩn đoán lại từ đầu nếu thông tin chưa đầy đủ

4. Bước tốn thời gian/gây lỗi nhiều nhất

Bước thu thập triệu chứng và chuẩn hóa mô tả của khách.

Thời gian ước tính: 10–15 phút/yêu cầu.

Nếu khách mô tả không rõ, cố vấn có thể phải gọi lại hoặc kỹ thuật viên phải khai thác lại khi xe đến.

Lỗi phổ biến: thiếu điều kiện xảy ra lỗi, nhầm nhóm hạng mục, không nhận diện sớm dấu hiệu cần hỗ trợ khẩn cấp.

5. AI có thể tham gia ở đâu?

Chuyển hội thoại tự do thành checklist triệu chứng có cấu trúc.

Gợi ý câu hỏi tiếp theo theo loại triệu chứng.

Đọc mã lỗi hoặc nội dung cảnh báo do khách cung cấp.

Kết hợp lịch sử bảo dưỡng để tóm tắt thông tin liên quan.

Gợi ý nhóm kỹ thuật và thời lượng lịch hẹn.

Cảnh báo các trường hợp cần nhân viên đánh giá ngay; AI không tự đưa ra kết luận an toàn cuối cùng.

6. Success Metrics

Giảm thời gian tiếp nhận từ 12 phút xuống dưới 5 phút.

Tỷ lệ phiếu có đủ trường thông tin trước khi xe đến đạt ≥ 95%.

Giảm tỷ lệ kỹ thuật viên phải hỏi lại toàn bộ triệu chứng ít nhất 50%.

Tỷ lệ điều phối đúng nhóm kỹ thuật đạt ≥ 90%.

Không tự động khuyến nghị tiếp tục vận hành đối với trường hợp an toàn chưa được con người xác nhận.

7. Kiến trúc sơ bộ

Rule + LLM + Retrieval, chưa dùng Agent tự chủ

Mô tả/ảnh/mã cảnh báo của khách
        ↓
Rule nhận diện từ khóa nguy hiểm
        ↓
LLM trích xuất triệu chứng và sinh câu hỏi bổ sung
        ↓
Retrieval lịch sử xe + tài liệu hướng dẫn đã phê duyệt
        ↓
Tạo bản tóm tắt tiếp nhận
        ↓
Cố vấn dịch vụ xác nhận
        ↓
Đặt lịch và chuyển xưởng

Rule chịu trách nhiệm với các cờ an toàn bắt buộc.

LLM chỉ hỗ trợ cấu trúc hóa và gợi ý, không thay thế chẩn đoán kỹ thuật.

Fallback: biểu mẫu tiếp nhận chuẩn khi mô hình không khả dụng.

8. Nhận định nhanh

Khuyến nghị: GO có điều kiện.Cần ưu tiên dữ liệu chất lượng, taxonomy triệu chứng thống nhất và ranh giới rõ giữa “gợi ý tiếp nhận” với “chẩn đoán an toàn”.

QUICK PROBLEM CARD 3

1. Tên bài toán

AI hỗ trợ tiếp nhận và điều phối yêu cầu đa ngôn ngữ của khách tại Vinpearl

2. Actor/Operator

Khách lưu trú.

Nhân viên lễ tân/tổng đài.

Housekeeping, kỹ thuật, ẩm thực, an ninh.

Quản lý ca.

3. Current-State Workflow

Khách gửi yêu cầu bằng cuộc gọi/chat/trực tiếp
        ↓
Nhân viên nghe/đọc và dịch nếu cần
        ↓
Xác định phòng, nội dung, mức độ khẩn cấp
        ↓
Ghi chú hoặc tạo ticket
        ↓
Chuyển cho bộ phận liên quan
        ↓
Bộ phận xử lý xác nhận lại thông tin
        ↓
Cập nhật trạng thái cho lễ tân
        ↓
Lễ tân phản hồi khách

4. Bước tốn thời gian/gây lỗi nhiều nhất

Bước dịch, hiểu ý và chuyển giao yêu cầu giữa các bộ phận.

Thời gian ước tính hiện tại: 4–7 phút/yêu cầu.

Có thể lâu hơn với ngôn ngữ ít phổ biến hoặc khi yêu cầu chứa nhiều ý.

Lỗi phổ biến: dịch thiếu chi tiết, nhầm số phòng/thời gian, chuyển sai bộ phận, phản hồi khách không nhất quán.

5. AI có thể tham gia ở đâu?

Dịch hai chiều theo ngữ cảnh dịch vụ khách sạn.

Tóm tắt yêu cầu theo mẫu: phòng, nội dung, số lượng, thời điểm, mức ưu tiên.

Phân loại bộ phận xử lý.

Phát hiện yêu cầu liên quan an toàn, y tế hoặc khiếu nại nghiêm trọng.

Soạn phản hồi đa ngôn ngữ để nhân viên duyệt.

Nhắc SLA và phát hiện ticket chưa được tiếp nhận.

6. Success Metrics

Giảm thời gian tạo và chuyển ticket từ 5 phút xuống dưới 90 giây.

Tỷ lệ đúng bộ phận ngay lần đầu đạt ≥ 92%.

Giảm khiếu nại do hiểu sai yêu cầu ít nhất 30%.

Tỷ lệ phản hồi ban đầu trong vòng 3 phút đạt ≥ 95%.

100% yêu cầu y tế/an toàn/khiếu nại nghiêm trọng phải chuyển cho quản lý ca xác nhận.

7. Kiến trúc sơ bộ

LLM Feature + Rule + Workflow Automation

Chat/voice transcript
        ↓
Language Detection + Translation
        ↓
LLM trích xuất và phân loại yêu cầu
        ↓
Rule kiểm tra phòng, trường bắt buộc và mức khẩn cấp
        ↓
Nhân viên xác nhận
        ↓
Workflow tạo ticket + gửi bộ phận phụ trách
        ↓
LLM soạn phản hồi theo trạng thái để nhân viên duyệt

Có thể bổ sung Agentic Loop ở giai đoạn sau để theo dõi ticket quá SLA, nhưng không tự xử lý khiếu nại hoặc yêu cầu an toàn.

Fallback: chuyển nguyên văn và bản dịch máy đến nhân viên.

Lưu log bản dịch, bản chỉnh sửa và người phê duyệt để phục vụ kiểm tra chất lượng.

8. Nhận định nhanh

Khuyến nghị: GO cho pilot tại một cơ sở.Đây là bài toán có phạm vi rõ, metric trực tiếp và rủi ro có thể kiểm soát bằng phê duyệt của nhân viên.

KẾT LUẬN CÁ NHÂN

Trong ba bài toán, tôi ưu tiên AI hỗ trợ phân loại và điều phối yêu cầu cư dân tại Vinhomes để thực hiện Deep-Dive. Bài toán có tần suất cao, nhiều thao tác lặp lại, dữ liệu đầu vào dạng ngôn ngữ tự nhiên phù hợp với LLM và có các chỉ số vận hành dễ đo như thời gian tạo ticket, độ chính xác phân loại, tỷ lệ chuyển sai và tỷ lệ đáp ứng SLA.

Giải pháp phù hợp nhất trong giai đoạn đầu không phải là một agent tự động hoàn toàn, mà là kiến trúc Rule + LLM + Human-in-the-loop. Rule bảo vệ các trường hợp khẩn cấp và kiểm tra dữ liệu bắt buộc; LLM hỗ trợ hiểu ngôn ngữ, trích xuất và tóm tắt; nhân viên chịu trách nhiệm phê duyệt trước khi ticket được điều phối.