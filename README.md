[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24262301&assignment_repo_type=AssignmentRepo)
# 📖 Hướng Dẫn Học Viên (Student Guide) — Lab 02: AI Product Scoping

Tài liệu này hướng dẫn chi tiết cách thiết lập môi trường lập trình Python, cấu hình API Key và chuẩn bị sản phẩm nộp bài cho **Lab 02: AI Product Scoping (Vin Smart Future)**.

---

## 🛠️ 1. Hướng dẫn thiết lập Môi trường ảo (`.venv`)

Môi trường ảo (virtual environment) giúp cô lập các thư viện của dự án này, tránh xung đột với các phiên bản thư viện khác cài trên máy của bạn.

### 💻 Bước 1: Tạo môi trường ảo
Mở terminal tại thư mục gốc của dự án (`VinUni_Day02-AI-Product-Lab`) và chạy lệnh tương ứng với hệ điều hành của bạn:

*   **Windows (PowerShell hoặc CMD):**
    ```powershell
    python -m venv .venv
    ```
*   **macOS / Linux:**
    ```bash
    python3 -m venv .venv
    ```

### 🔌 Bước 2: Kích hoạt (Activate) môi trường ảo
Bạn phải kích hoạt môi trường ảo mỗi khi mở terminal mới trước khi chạy code.

*   **Windows (PowerShell):**
    ```powershell
    .venv\Scripts\Activate.ps1
    ```
    *(Nếu gặp lỗi "Execution Policy", hãy chạy lệnh: `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process` rồi kích hoạt lại).*
*   **Windows (CMD):**
    ```cmd
    .venv\Scripts\activate.bat
    ```
*   **macOS / Linux:**
    ```bash
    source .venv/bin/activate
    ```
*   **Dấu hiệu kích hoạt thành công:** Ở đầu dòng lệnh của terminal xuất hiện ký hiệu `(.venv)`.

### 📥 Bước 3: Cài đặt thư viện cần thiết
Chạy lệnh sau để cài đặt SDK của Gemini và các thư viện hỗ trợ:
```bash
pip install google-genai google-generativeai pytest
```

---

## 🔑 2. Thiết lập biến môi trường `GEMINI_API_KEY`

Để code Python gọi được Gemini API, bạn cần khai báo khóa API của mình vào biến môi trường. **Lưu ý: Không được dán trực tiếp API Key vào code để tránh bị lộ khóa khi push lên GitHub.**

Hãy mở terminal đã kích hoạt `(.venv)` và chạy lệnh nạp khóa tương ứng:

### 🪟 Trên Windows:
*   **Nếu dùng PowerShell (Mặc định của VS Code / Cursor):**
    ```powershell
    $env:GEMINI_API_KEY="AIzaSyYourGeminiApiKeyHere"
    ```
*   **Nếu dùng Command Prompt (CMD):**
    ```cmd
    set GEMINI_API_KEY=AIzaSyYourGeminiApiKeyHere
    ```

### 🍎 Trên macOS / Linux:
*   **Dùng Terminal:**
    ```bash
    export GEMINI_API_KEY="AIzaSyYourGeminiApiKeyHere"
    ```

### 🧪 Kiểm tra xem API Key đã nhận diện chưa:
Chạy lệnh python nhanh này trong terminal để kiểm tra:
```bash
python -c "import os; print('API Key status: OK' if os.getenv('GEMINI_API_KEY') else 'API Key status: MISSING')"
```

---

## 👥 3. Hướng dẫn làm bài và Nộp bài Nhóm (Group Assignment)

Môn học này áp dụng cơ chế **Group Assignment** trên GitHub Classroom. Cả nhóm của bạn sẽ dùng chung **một repository duy nhất** để cộng tác và nhận một điểm số chung cuộc cho cả nhóm.

### 📂 Cơ cấu tổ chức thư mục của Repo nhóm:
Tất cả các thành viên clone chung một repo về máy. Sau khi hoàn tất bài lab, cấu trúc các file tại thư mục gốc (root) của repository nhóm phải đảm bảo đầy đủ như sau:

```text
ai-product-lab-groupname/
├── 01-problem-scan.md             ← Báo cáo Phase 1 & 2 (Scan & 3 Quick Cards)
├── 02-deep-dive-report.md          ← Báo cáo Phase 3 & 5 (Deep-Dive & Evaluation)
├── 03-ai-log.md                    ← Nhật ký chiêm nghiệm Phase 6 (Nhận xét của nhóm/thành viên)
├── 04-workflow-diagram.png/.pdf   ← Ảnh chụp sơ đồ workflow vẽ tay ở Phase 3.1
└── extras/
    └── prompt_prototype.py         ← File code Python hoàn chỉnh của nhóm (hoặc để tại starter-code/prompt_prototype.py)
```

### ⚠️ Lưu ý quan trọng cho làm việc nhóm:
*   **Khai báo thành viên:** Tại đầu file `02-deep-dive-report.md` (Báo cáo nhóm), bắt buộc phải điền đầy đủ và chính xác: **Tên nhóm**, **Họ và tên** kèm **Mã số sinh viên (MSSV)** của từng thành viên tham gia dự án.
*   **Cộng tác trực tiếp:** Cả nhóm cùng thảo luận và phân chia nhiệm vụ. Một thành viên có thể phụ trách viết code `prompt_prototype.py`, thành viên khác vẽ sơ đồ `04-workflow-diagram.png`, các bạn khác viết báo cáo. Hãy tận dụng Git Branch để tránh conflict và push trực tiếp lên repo chung này.
*   **Đồng bộ dữ liệu:** Hãy đảm bảo trước giờ nộp bài, các file cá nhân của các thành viên (như các ý tưởng trong `01-problem-scan.md` hay cảm nhận trong `03-ai-log.md`) đã được tổng hợp chung vào các file mẫu tương ứng tại thư mục gốc của repository nhóm.

---

## 📝 3.5. Hướng dẫn chi tiết cách hoàn thiện các file nộp bài

Dưới đây là nội dung và cách thức thực hiện chi tiết cho từng file để đảm bảo đạt điểm tối đa theo Rubric chấm:

### 📄 1. File `01-problem-scan.md` (Bài cá nhân - 15 điểm)
File này thể hiện tư duy tìm kiếm bài toán của cá nhân bạn trước khi thảo luận nhóm.
*   **Cách làm:** Copy và hoàn thiện nội dung của **Phase 1 (SCAN)** và **Phase 2 (QUICK-ASSESS)** từ file `01-worksheet.md`.
*   **Yêu cầu nội dung:**
    *   **Bảng quét cơ hội (SCAN):** Điền tối thiểu 5 bài toán thực tế thuộc các công ty thành viên Vingroup. Xác định đúng loại thấu kính áp dụng cho mỗi bài toán (Lặp lại, Tốn thời gian, AI-upgrade, Stakeholder Pain).
    *   **3 Quick Problem Cards:** Điền đầy đủ thông tin cho 3 bài toán tiềm năng nhất. Mỗi card phải mô tả rõ:
        *   Tên bài toán và công ty thành viên.
        *   Tác nhân đang gặp khó khăn (Actor/Operator).
        *   Sơ đồ quy trình thủ công hiện tại.
        *   Bước tốn thời gian/gây lỗi nhiều nhất (kèm thời gian xử lý ước tính).
        *   Bước mà AI có thể tham gia giải quyết.
        *   Metric đo thành công có con số cụ thể (Ví dụ: *"Giảm từ 10 phút xuống dưới 2 phút"*).
        *   Đề xuất kiến trúc sơ bộ (No AI, Rule, LLM, Agent).

### 📄 2. File `02-deep-dive-report.md` (Bài nhóm - 40 điểm)
Báo cáo phân tích sâu dự án AI mà cả nhóm đã chọn thống nhất.
*   **Cách làm:** Copy và hoàn thiện nội dung của **Phase 3 (DEEP-DIVE - trừ phần vẽ sơ đồ)** và **Phase 5 (EVALUATE)** từ file `01-worksheet.md`.
*   **Yêu cầu nội dung:**
    *   **Quyết định lựa chọn:** Ghi rõ tên bài toán được chọn để thực hiện Deep-Dive.
    *   **Problem Statement (6-field):** Điền đầy đủ 6 trường thông tin (Actor, Current Workflow, Bottleneck, Business Impact, Success Metric, Operational Boundary) cho bài toán đã chọn.
    *   **Future-State Flow & AI Fit:** Vẽ quy trình tương lai bằng text-diagram hoặc mô tả bước, phân loại mức độ ứng dụng AI (Rule, LLM Feature, Agentic Loop), xác lập rõ bước có sự phê duyệt của con người (Human-in-the-loop) và phương án dự phòng khi hệ thống AI gặp lỗi (Fallback).
    *   **Evaluate:** Đánh giá độ sẵn sàng qua bảng Checklist, đưa ra quyết định cuối cùng (GO / NOT YET / NO-GO) kèm theo luận điểm kỹ thuật và ước lượng chi phí chặt chẽ.

### 🖼️ 3. File `04-workflow-diagram.png` (hoặc `.pdf`) (Bài nhóm - 20 điểm)
Sơ đồ trực quan hóa quy trình vận hành hiện tại trước khi có AI.
*   **Cách làm:** Cả nhóm cùng vẽ sơ đồ quy trình hiện tại (Current-State Workflow) lên bảng trắng hoặc giấy A3 trong **Phase 3.1**.
*   **Yêu cầu nội dung:**
    *   Sơ đồ phải thể hiện rõ các bước tuần tự của quy trình thủ công.
    *   Đánh dấu rõ các điểm chuyển giao thông tin giữa người-người hoặc người-hệ thống (🔄 **Handoff**).
    *   Ghi rõ thời gian xử lý trung bình ở mỗi bước và tổng thời gian của cả quy trình.
    *   Đánh dấu rõ ràng các bước là nút thắt cổ chai bằng biểu tượng hoặc màu đỏ (🔴 **Bottleneck**).
    *   *Chụp ảnh sơ đồ rõ nét, không bị mờ/mất góc, lưu dưới định dạng `.png`, `.jpg` hoặc xuất `.pdf` rồi đặt vào repo.*

### 📄 4. File `03-ai-log.md` (Bài cá nhân - 15 điểm)
Nhật ký chiêm nghiệm về việc tương tác với AI (ChatGPT, Gemini, Claude...) trong suốt buổi học.
*   **Cách làm:** Viết bài tự luận ngắn phản ánh trung thực quá trình sử dụng AI làm trợ lý đồng hành (Thought-partner).
*   **Yêu cầu nội dung:**
    *   **AI giúp gì:** Bạn đã dùng AI để làm gì? (Brainstorm ý tưởng quy trình, viết Prompt, tìm cách tấn công prompt injection, hay hỗ trợ sửa lỗi code python...).
    *   **AI sai gì:** Chỉ ra ít nhất một điểm AI đưa ra câu trả lời sai lệch (hallucination), đề xuất giải pháp rule-based quá phức tạp, hoặc viết prompt bypass được ranh giới an toàn.
    *   **Sửa đổi ra sao:** Bạn đã điều chỉnh prompt hoặc bổ sung ranh giới như thế nào để ép AI trả về kết quả đúng?

---

## 🚀 4. Kiểm tra trước khi nộp bài (Self-Check)

Trước khi thực hiện lệnh push cuối cùng, hãy chạy thử script tự động kiểm tra xem bạn đã chuẩn bị đầy đủ 4 file bắt buộc hay chưa:
```bash
python autograder/autograder.py
```

Nếu kết quả hiển thị thông báo `[SUCCESS] Day du file nop bai. San sang push!`, hãy chạy các lệnh sau để nộp bài lên GitHub Classroom:
```bash
git add .
git commit -m "Submit Lab 02 Assignment"
git push origin main
```

