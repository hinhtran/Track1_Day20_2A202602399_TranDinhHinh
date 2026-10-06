# BÀI THỰC HÀNH DAY 20: PRODUCT METRICS, RETENTION & TRACKING PLAN

* **Học viên:** Trần Đình Hinh
* **Mã học viên:** 2A202602399
* **Dự án thực hiện:** [P-149 (DATA-17) Multi-Agent Entity Resolution & Master Data Management] (metrics-pack.md)
* **Kho lưu trữ:** `Track1_Day20_2A202602399_TranDinhHinh`

---

## 1. Liên kết hồ sơ bài làm (Metrics Pack)

Toàn bộ nội dung thiết kế chi tiết 7 phần (từ mục 00 đến mục 06) đã được chuẩn hóa và lưu trữ trực tiếp tại:
- **[Tệp Metrics Pack Hoàn Chỉnh (metrics-pack.md)]**

Nhật ký tương tác và phản biện với AI được ghi chép tại:
- **[Nhật ký sử dụng AI (ai-support-log.md)]**

---

## 2. Tóm tắt chuỗi logic 5 mắt xích (Logic Chain Summary)

1. **Phạm vi & Persona:** Data Steward khối VSF cần xử lý hồ sơ khách hàng nghi trùng lặp ở vùng xám ($0.55 \le \text{Score} < 0.85$) để kiến tạo Golden Record chuẩn xác.
2. **Core Action:** Thẩm định và xác nhận quyết định xử lý cặp hồ sơ nghi trùng (`candidate_pair_resolved`: Approve Merge hoặc Confirm Reject).
3. **Nature & Cadence:** Xuất phát từ chu kỳ đồng bộ dữ liệu theo mẻ để phục vụ đối soát, cadence tự nhiên là **Weekly** ở cấp **User / Team Data Quality**.
4. **North Star Metric (NSM):** Số lượng cặp hồ sơ nghi trùng được giải quyết dứt điểm **không bị Unmerge/Hoàn tác trong vòng 14 ngày**, tính theo tuần (**Weekly Confirmed Clean Resolves**).
   * *Counter-metric bảo vệ:* **Unmerge Rate** ($\le 1.0\%$) chống rủi ro gộp nhầm (False Merge).
5. **Product Loop:** Vòng lặp **HITL Data Flywheel** (Quyết định của Steward tuần này trở thành nhãn dữ liệu chuẩn giúp AI Agent ở tuần sau thông minh hơn, giảm 40% thời gian duyệt).
6. **Tracking Plan:** 5 Core events chuẩn `object_action` với 2 tiêu chí nghiệm thu chặt chẽ (chỉ bắn khi backend commit DB và chống trùng lặp qua Idempotency Key).

---

## 3. Điều tôi mang về áp dụng cho dự án thật (Takeaways for P-149)

1. **Chấm dứt tư duy "ép chỉ số vào dashboard":**
   * Trước đây, tôi thường có thói quen theo dõi DAU/MAU theo quán tính của các dashboard có sẵn. Sau bài lab này, tôi nhận thức rõ rằng P-149 là một hệ thống B2B Enterprise Data Management vận hành theo mẻ dữ liệu đối soát. Nhịp đo bắt buộc phải là **Weekly**, nếu ép theo Daily sẽ chỉ tạo ra các số liệu ảo hoặc ép người dùng làm việc trái với quy trình thực tế.

2. **Sức mạnh của Quality Threshold trong North Star Metric:**
   * Trong bài toán AI & Machine Learning, tối ưu hóa số lượng đơn thuần là "con dao hai lưỡi". Nếu chỉ đếm số ca gộp được duyệt, Data Steward có thể bấm bừa để đạt KPI, dẫn tới thảm họa **False Merge** (gộp nhầm tài khoản ngân hàng hoặc lịch sử mua hàng của hai người khác nhau). Việc bổ sung điều kiện ràng buộc *"Không bị Unmerge/Hoàn tác trong 14 ngày"* và Counter-metric `Unmerge Rate` giúp toàn bộ hệ thống giữ vững chất lượng dữ liệu cốt lõi.

3. **Product Loop phải có Reason to Return tự nhiên, không lệ thuộc vào Notification:**
   * Một sản phẩm tốt phải khiến người dùng quay lại vì **giá trị tích lũy (Investment)** và **nhu cầu công việc tự nhiên**, thay vì bắn notification quấy rầy. Trong P-149, sự tích lũy nhãn dữ liệu giúp AI Agent thông minh hơn theo từng tuần chính là động lực lớn nhất để Data Steward gắn bó và làm việc nhẹ nhàng hơn.

4. **Tracking Plan kỷ luật: Không track mọi click, chỉ track trạng thái hoàn tất:**
   * Tôi sẽ áp dụng ngay 2 tiêu chí nghiệm thu vào mã nguồn backend của P-149: Chỉ bắn sự kiện khi database commit thành công (HTTP 200) và dùng Idempotency Key cho từng cặp hồ sơ để hệ thống analytics luôn phản ánh dữ liệu sạch 100%.

---

## 4. Bảng tự rà soát 5 Gates đánh giá

| Gate | Tiêu chuẩn đạt | Kết quả trong bài làm | Tình trạng |
| :--- | :--- | :--- | :---: |
| **Gate 1: Core Action** | Có actor, object, completion rule; đạt $\ge 4/5$ tiêu chí; phân biệt rõ với thao tác UI. | Xác định hành vi `candidate_pair_resolved`, đạt 5/5 tiêu chí tự kiểm. | **ĐẠT** |
| **Gate 2: Cadence** | Kết luận theo template, nhịp đo từ nature, có lý do "vì" thuyết phục. | Kết luận nhịp **Weekly** theo mẻ dữ liệu đối soát doanh nghiệp. | **ĐẠT** |
| **Gate 3: Metric System** | Retention đủ 6 thành phần; NSM đủ 3 yếu tố; có Counter-metric. | NSM có Quality Threshold, Counter-metric là Unmerge Rate. | **ĐẠT** |
| **Gate 4: Product Loop** | Loop $\ge 2$ chu kỳ, có Metric Hypothesis định lượng nối thẳng về NSM. | Loop HITL Flywheel 2 chu kỳ; giả thuyết tăng 30% NSM và giảm 40% thời gian duyệt. | **ĐẠT** |
| **Gate 5: Tracking** | 4–8 events map metric; $\ge 2$ tiêu chí nghiệm thu rõ ràng. | 5 events chuẩn `object_action`; 2 acceptance criteria chống duplicate & pending click. | **ĐẠT** |
