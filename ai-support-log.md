# NHẬT KÝ SỬ DỤNG AI (AI SUPPORT LOG)

> **Họ và tên:** Trần Đình Hinh  
> **Mã học viên:** 2A202602399  
> **Dự án:** P-149 (DATA-17) Multi-Agent Entity Resolution & Master Data Management  
> **Thời gian thực hiện:** Ngày 06/10/2026  

---

### 1. AI đã giúp tôi ở đâu?
* **Brainstorm và chuẩn hóa tên sự kiện:** AI gợi ý đặt tên các event theo đúng chuẩn cú pháp `object_action` (như `candidate_pair_resolved`, `golden_record_merged`, `cluster_unmerged`), giúp tracking plan mạch lạc và dễ tích hợp kỹ thuật.
* **Cấu trúc hóa công thức North Star Metric:** AI giúp tôi phân tách rõ ràng 3 thành phần trong NSM: `Unit of Value` (cặp hồ sơ xử lý), `Quality Threshold` (không bị unmerge sau 14 ngày), và `Frequency` (Weekly), tránh việc chỉ đo đếm số lượng thuần túy.
* **Xây dựng kịch bản Product Loop (Data Flywheel):** AI gợi ý luồng phản hồi Human-in-the-Loop (HITL) 2 chu kỳ: dữ liệu gắn nhãn của con người quay trở lại làm giàu tập dữ liệu huấn luyện cho AI Agent ở chu kỳ tiếp theo.

---

### 2. AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?
* **Đề xuất sai nhịp tự nhiên (Nature Cadence):** Ban đầu AI gợi ý đo theo **Daily (DAU, D1/D7 Retention)** giống như các ứng dụng B2C thông thường. Điều này **hoàn toàn sai lệch** với bản chất của hệ thống Master Data doanh nghiệp P-149 — nơi dữ liệu được đồng bộ và xử lý khử trùng theo các mẻ định kỳ hàng tuần (Weekly Batch) phục vụ đối soát.
* **Đề xuất vanity metric cho NSM:** AI từng đề xuất lấy *"Số lượt câu hỏi/truy vấn gửi đến AI Agent"* làm North Star Metric. Đây là một đề xuất hời hợt và dễ bị "game", vì số lượt hỏi nhiều không chứng minh được dữ liệu Master Data đã sạch hay chưa, thậm chí có thể do AI trả lời kém khiến người dùng phải hỏi đi hỏi lại nhiều lần.
* **Định nghĩa Activation chưa sát:** AI gợi ý sự kiện user xem xong màn hình onboarding là Activation, vi phạm lỗi kinh điển "xem giao diện là kích hoạt".

---

### 3. Tôi đã tự sửa hoặc quyết định lại điều gì?
* **Quyết định đưa Cadence về đúng nhịp Weekly:** Tôi bác bỏ nhịp Daily và chốt nhịp đo là **Weekly ở cấp User/Team**, phản ánh chính xác chu kỳ làm việc của Data Steward.
* **Xác định lại Core Action gắn chặt với Core Value:** Tôi chọn hành vi **Thẩm định và xác nhận quyết định xử lý cặp hồ sơ nghi trùng (Resolve Candidate Pair)**, phân biệt rõ với thao tác upload file hay xem báo cáo.
* **Bổ sung Counter-metric cốt lõi (Unmerge / Revert Rate):** Trong bài toán Entity Resolution, nguy cơ chết người nhất là **gộp nhầm khách hàng (False Merge)**. Tôi đã tự bổ sung chỉ số `Unmerge Rate` và đặt ngưỡng kiểm soát nghiêm ngặt ($\le 1.0\%$) làm Counter-metric bắt buộc để ngăn chặn tình trạng Data Steward duyệt ẩu để chạy chỉ tiêu số lượng.
* **Thiết lập 2 tiêu chí nghiệm thu chặt chẽ:** Tự quy định cơ chế khóa Idempotency Key để ngăn chặn tình trạng nhân bản event tracking khi Steward bấm nhanh nhiều lần hoặc F5 tải lại trang.
