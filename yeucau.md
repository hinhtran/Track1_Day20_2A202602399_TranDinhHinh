# Đề bài & Hướng dẫn: Thiết kế Hệ thống Product Metrics (Day 20)

> **Thời gian:** 90 phút · **Hình thức:** Bài làm cá nhân · **Trọng tâm:** Phase 1 – 3 (Phase 4 ghi nhanh ý chính)  
> **Áp dụng:** Trực tiếp trên dự án bạn đang build  

---

## I. Đọc trước khi làm (3 phút)

### 1. Về bài lab này
Mỗi học viên áp dụng framework product metrics của buổi giảng lên chính dự án mình đang build:
* Chọn core action, xây bộ metric tối ưu core action.
* Định nghĩa retention theo nhịp tự nhiên (nature).
* Phác thảo product loop và đặt yêu cầu tracking.

### 2. Bạn làm được gì sau bài này?
* **Core Action:** Chọn được một core action gắn chặt với core value; phân biệt rạch ròi core action với thao tác giao diện (UI) và output hệ thống.
* **Natural Cadence:** Xác định nhịp tự nhiên của core action từ bản chất hành vi người dùng thay vì chọn daily/weekly theo thói quen dashboard.
* **Metric System:** Xây dựng bộ metric tối ưu core action: *Activation, Engagement, North Star Metric, Leading Indicators, Counter-metric*.
* **Retention 6 thành phần:** Định nghĩa retention đầy đủ 6 thành phần (*Unit, Cohort entry, Return event, Window, Threshold, Segment*) khớp với nhịp tự nhiên.
* **Product Loop & Tracking:** Thiết kế product loop như một giả thuyết có *metric hypothesis*, và đặt yêu cầu tracking tối thiểu cho bộ metric.

### 3. Cần chuẩn bị
1. Đã tham gia bài giảng Day 20 (*North Star Metric, Retention & Engagement, Nature vs Nurture, Habit Loop*).
2. Có một dự án đang build (dự án nhóm của khoá học hoặc dự án cá nhân đều được).
3. Một tệp trình bày trực quan của riêng bạn (Markdown / Notion / FigJam / Slide...).
4. Deck bài giảng Day 20 để tra cứu framework.
5. Đồng hồ bấm giờ.

### 4. Lỗi thường gặp (Cần tránh tuyệt đối)
* ❌ Chọn core action vì dễ tracking hoặc chọn output của hệ thống thay cho hành vi tạo value.
* ❌ Xem hoàn thành onboarding hay đăng nhập là activation.
* ❌ Ép frequency cao hơn nhu cầu thật — ép daily cho sản phẩm vốn theo tháng/dự án.
* ❌ Dùng notification làm reason to return của loop.
* ❌ Dùng một metric cho mọi cadence — ví dụ dùng D7 cho action xảy ra theo tháng.
* ❌ Viết "D7 retention" mà thiếu cohort, return event, window.
* ❌ Track mọi click — event không map về metric hay câu hỏi sản phẩm nào.
* ❌ Có metric nhưng không có event, trigger, identity để tính nó.
* ❌ Viết core action mơ hồ kiểu "engage", "sử dụng sản phẩm".

---

## II. Tổng quan & Phương pháp thực hiện

### 1. Bài này làm gì?
Bạn đóng vai PM của chính dự án mình đang build và đi qua một chuỗi quyết định logic:
$$\text{Core Action} \longrightarrow \text{Nhịp tự nhiên (Nature)} \longrightarrow \text{Bộ Metric + Retention} \longrightarrow \text{Product Loop} \longrightarrow \text{Tracking}$$

### 2. Bảng thuật ngữ cốt lõi

| Thuật ngữ | Định nghĩa đơn giản |
| :--- | :--- |
| **Core Action** | Hành vi quan trọng nhất user thực hiện để nhận giá trị cốt lõi (không phải mở app hay đăng nhập). |
| **Core Value Event** | Sự kiện chứng minh giá trị đã thực sự xảy ra (ví dụ: `task_completed`). |
| **Nature / Natural Cadence** | Nhịp nhu cầu tự nhiên của user — trước khi có notification hay gamification can thiệp. |
| **Nurture** | Những gì team chủ động làm để nuôi dưỡng và khuếch đại nhịp đó (notification, email, onboarding...). |
| **Activation** | Thời điểm user lần đầu tiên thực sự nhận được giá trị cốt lõi. |
| **Retention (6 thành phần)** | *Unit · Cohort entry · Return event · Window · Threshold · Segment*. |
| **North Star Metric** | Chỉ số cốt lõi = Unit of Value + Quality Threshold + Frequency. |
| **Counter-metric** | Chỉ số kiểm soát: phát hiện "metric chính tăng nhưng trải nghiệm/chất lượng xấu đi". |
| **Metric Hypothesis** | Giả thuyết: *"Nếu loop này đúng thì metric X sẽ thay đổi theo hướng Y trong khung thời gian Z"*. |

### 3. Lộ trình 5 Phase & Thời gian

| Phase | Thời gian | Câu hỏi trung tâm | Đầu ra bắt buộc |
| :---: | :---: | :--- | :--- |
| **Phase 0** | 10 phút | Dự án nào, persona nào, core job nào? | Phạm vi bài làm (Mục 00) |
| **Phase 1** | 15 phút | Hành vi nào gần core value nhất? | Core Action Card (Mục 01) |
| **Phase 2** | 15 phút | Nhu cầu tự nhiên xuất hiện bao lâu một lần? | Action Nature Card + Kết luận Cadence (Mục 02) |
| **Phase 3** | 25 phút | Đo core action bằng gì, quay lại tính thế nào? | Metric System + Retention Definition (Mục 03, 04) |
| **Phase 4** | 15 phút | Loop nào di chuyển metric đó, đo bằng event gì? | Loop 2 chu kỳ + 4–8 Events tracking (Mục 05, 06) |
| **Phase 5** | 10 phút | Bài có mắc lỗi kinh điển nào không? | Bản hoàn chỉnh + Reflection |

> [!NOTE]
> Cứ xong 1 Phase sẽ có 1 **"Gate"** tự kiểm tra. Đạt Gate thì mới đi tiếp.

### 4. 5 Luật bất biến của bài Lab
1. **Metric đi từ use case lên:** Không bắt chước "app kia dùng DAU mình cũng dùng DAU", không chọn "MAU số to để làm đẹp báo cáo".
2. **Nurture chỉ khuếch đại Nature:** Không dùng notification để bịa ra một nhịp quay lại không tồn tại trong đời thực.
3. **Không ép daily habit:** Tần suất phải phản ánh đúng bản chất hành vi — sản phẩm theo tháng/dự án không cần DAU.
4. **Mọi event phải map về một metric:** Event nào không tính được chỉ số nào thì loại bỏ.
5. **Loop là giả thuyết, Metric là phép thử:** Mọi loop thiết kế ra đều phải có metric hypothesis đi kèm.

---

## III. Chi tiết từng Phase

### Phase 0 — Chốt phạm vi (10 phút)
Ghi rõ 3 mục lên đầu bài làm:
1. **Dự án:** Tên và giải pháp sản phẩm bạn đang build là gì?
2. **Persona:** Ai là người dùng chính của use case này? (Chỉ chọn **duy nhất 1** persona đại diện).
3. **Core Job:** Họ đang cố hoàn thành việc gì? (Viết bằng ngôn ngữ của user, không mô tả tính năng).
   * *Ví dụ sai:* "Cần một AI assistant thông minh" (tính năng).
   * *Ví dụ đúng:* "Tôi mất quá nhiều thời gian gom thông tin môn học và vẫn bỏ lỡ deadline."

---

### Phase 1 — Core Action (15 phút)

#### 1. Phân biệt 4 khái niệm
Điền nhanh bảng sau trước khi làm Core Action Card:

| Khái niệm | Câu hỏi then chốt | Ví dụ (Trợ lý học tập) |
| :--- | :--- | :--- |
| **Core Job** | User đang cố hoàn thành việc gì? | Không bỏ lỡ nhiệm vụ học tập quan trọng |
| **Core Action** | User làm gì trong sản phẩm để tiến tới giá trị? | Thêm và hoàn thành một nhiệm vụ |
| **Core Value** | User nhận được lợi ích gì? | Biết rõ việc cần làm, hoàn thành đúng hạn |
| **Core Value Event** | Sự kiện nào chứng minh value đã xảy ra? | `task_completed` |

#### 2. Core Action Card Template
Copy bảng sau và điền cho dự án của bạn:

| Thành phần | Câu hỏi / Hướng dẫn |
| :--- | :--- |
| **Target user** | Ai thực hiện hành vi? |
| **Core job** | Họ đang cố hoàn thành việc gì? |
| **Core action** | Hành vi được chọn là gì? |
| **Object** | Hành vi tác động lên đối tượng nào? |
| **Preconditions** | Điều gì phải có trước khi hành vi xảy ra? |
| **Completion rule** | Khi nào action được xem là hoàn tất? |
| **Core value** | Người dùng nhận được lợi ích gì? |
| **Evidence of value** | Dấu hiệu nào chứng minh value đã thực sự xảy ra? |
| **Candidate event** | Event nào có thể dùng để tracking trong telemetry? |

#### 3. Tự kiểm 5 tiêu chí Core Action
Chấm điểm hành động vừa chọn; nếu trượt $\ge 2$ tiêu chí thì bắt buộc phải chọn lại:
1. **Gần core value:** Hành vi xảy ra là user đã tiến gần rõ rệt tới value chưa?
2. **Có thể lặp lại:** Hành vi có xuất hiện lại khi nhu cầu quay lại không?
3. **Có thể quan sát:** Bạn có biết chính xác khi nào nó hoàn tất không?
4. **Có ý nghĩa:** Hành vi này tăng có thực sự chứng tỏ sản phẩm tốt hơn không?
5. **Có thể tác động:** Team phát triển có thể cải thiện khả năng nó xảy ra không?

> [!IMPORTANT]
> **GATE 1 — Core action đứng vững:** Có actor, object, completion rule; đạt ít nhất 4/5 tiêu chí tự kiểm; và giải thích được vì sao nó không phải là "mở app", "đăng nhập" hay "hỏi AI".

---

### Phase 2 — Nature & Cadence (15 phút)

#### 1. Action Nature Card (8 thuộc tính)

| Thuộc tính | Câu hỏi phân tích |
| :--- | :--- |
| **Actor** | User, account, team hay object nào thực hiện? |
| **Intent** | Hành vi bắt đầu từ nhu cầu/mục đích gì? |
| **Trigger** | Do user chủ động, sự kiện bên ngoài, người khác hay hệ thống kích hoạt? |
| **Effort** | Mất bao nhiêu thời gian, nhận thức suy nghĩ, chuẩn bị dữ liệu? |
| **Value timing** | Value xuất hiện ngay, trễ, tích lũy, hay phụ thuộc người khác? |
| **State** | Sau action, dữ liệu/trạng thái nào được hệ thống lưu trữ lại? |
| **Dependency** | Có phụ thuộc nguồn cung, thành viên khác, approval, thời điểm không? |
| **Repeat condition** | Điều kiện nào khiến action có lý do xuất hiện lại trong thực tế? |

#### 2. Kết luận Cadence
1. Chọn một dạng hành vi: *Thói quen thường xuyên · Tiến trình tích lũy · Theo dự án · Giao dịch · Workflow của team · Phản ứng theo sự kiện · Theo chu kỳ*.
2. Viết kết luận bắt buộc theo template:
> *"Đối với **[đối tượng]**, core action **[tên core action]** thường xuất hiện **[tần suất tự nhiên]** vì **[lý do bản chất nhu cầu]**. Do đó, nhịp đo phù hợp là **[nhịp đo]** ở cấp **[user / team / account]**."*

> [!IMPORTANT]
> **GATE 2 — Cadence từ nature, không từ dashboard:** Kết luận đúng template, có lý do "vì" hợp lý, và nhịp đo không mâu thuẫn với dạng hành vi đã chọn.

---

### Phase 3 — Metric System & Retention (25 phút)

#### 1. Activation Metric (3 thành phần)
* **Start event:** Khi nào user bắt đầu hành trình (bước đầu tiên)?
* **Activation event:** Event nào xác nhận core action đầu tiên / first value đạt chuẩn?
* **Time window:** Core action cần xảy ra trong bao lâu kể từ start event?

#### 2. Engagement Metric
Chọn tối đa 2 góc đo phù hợp:
* **Frequency:** Core action xảy ra bao nhiêu lần trong cadence tự nhiên?
* **Depth:** Mỗi lần action tạo ra bao nhiêu giá trị / xử lý bao nhiêu dung lượng?
* **Breadth:** Có bao nhiêu workflow / tính năng cốt lõi được sử dụng đồng thời?

#### 3. Retention Definition (Đủ 6 thành phần)

| Thành phần | Câu hỏi định nghĩa |
| :--- | :--- |
| **1. Unit** | Đo trên User, Account, Team hay Organization? |
| **2. Cohort entry** | Event nào chính thức đưa unit vào cohort theo dõi? |
| **3. Return event** | Core action / Value event nào bắt buộc phải lặp lại? |
| **4. Window** | Khung thời gian theo dõi (Daily, Weekly, Monthly, Bracket... khớp với Phase 2)? |
| **5. Threshold** | Bao nhiêu lần thực hiện hành vi trong window thì được coi là retained? |
| **6. Segment** | Retention này áp dụng cho nhóm đối tượng nào? |

#### 4. North Star Metric, Leading Indicators & Counter-metric
1. **North Star Metric (NSM):** Đúng công thức 3 thành phần:
   $$\text{NSM} = \text{Unit of Value} + \text{Quality Threshold} + \text{Frequency}$$
2. **Leading Indicators:** Tối đa 3 chỉ số, mỗi chỉ số kèm một câu giải thích: *"Vì sao tin rằng chỉ số này dự báo trước được core action lặp lại"*.
3. **Counter-metric:** Ít nhất 1 chỉ số kiểm soát: Khi core action tăng mạnh, chỉ số nào không được phép xấu đi? (Chất lượng kết quả, chi phí vận hành, tỉ lệ rollback, tỉ lệ phàn nàn...).

> [!IMPORTANT]
> **GATE 3 — Metric tính được, retention đủ nghĩa:** Activation có đủ start/activation event + time window; Retention đủ 6 thành phần và khớp cadence; NSM đúng công thức 3 thành phần; có ít nhất 1 counter-metric bảo vệ.

---

### Phase 4 — Ghi nhanh: Product Loop & Tracking (15 phút)

#### 1. Product Loop
* **Vẽ nhanh loop tối thiểu 2 chu kỳ:**
  $$\text{Natural trigger} \longrightarrow \text{Core action} \longrightarrow \text{Immediate value} \longrightarrow \text{Saved state / Investment}$$
  $$\longrightarrow \text{Next natural trigger} \longrightarrow \text{Next core action} \longrightarrow \text{Repeat value}$$
* **Chọn loại loop:** *Habit · Progress · Project · Workflow · Transaction · Event-response · Account-level*.
* **Metric Hypothesis (Bắt buộc 1 câu):**
  > *"Nếu loop này hoạt động, metric **[tên metric]** sẽ thay đổi theo hướng **[tăng/giảm]** trong **[khung thời gian]**, vì **[cơ chế tác động]**."*

#### 2. Tracking nhanh (4 – 8 Events cốt lõi)
Liệt kê các sự kiện bắt buộc theo bảng:

| Tên Event (`object_action`) | Ý nghĩa nghiệp vụ | Thời điểm ghi nhận | Metric sử dụng ở Phase 3 |
| :--- | :--- | :--- | :--- |
| `candidate_pair_resolved` | Quyết định xử lý được lưu thành công | Khi API backend trả về 200 OK | Activation, Engagement, NSM |
| ... | ... | ... | ... |

* **2 Tiêu chí nghiệm thu (Acceptance Criteria):**
  1. Event chỉ phát sinh khi hành vi thực sự hoàn tất (không bắn khi mới bấm nút hoặc mở modal).
  2. Reload trang / Retry / Network failure / Autosave không được tạo bản ghi event trùng lặp (Idempotency).

> [!IMPORTANT]
> **GATE 4 — Loop nối metric, event nối loop:** Loop $\ge 2$ chu kỳ có kèm hypothesis; mọi event trong bảng telemetry đều map trực tiếp về ít nhất 1 metric đã khai báo.

---

### Phase 5 — Tự soi lỗi & Nộp bài (10 phút)

#### Bảng tự kiểm tra (Checklist 7 câu hỏi vàng)
* [ ] Core action không phải là thao tác giao diện (click, scroll) hay output đơn thuần của hệ thống?
* [ ] Activation không phải là "xem hết onboarding" hay "đăng nhập"?
* [ ] Tần suất đo lường (cadence) không bị ép cao hơn nhu cầu tự nhiên của người dùng?
* [ ] Product loop có lý do quay lại (reason to return) tự nhiên kể cả khi tắt hết notification?
* [ ] Retention không dùng chung một mốc cứng (như D7) cho mọi loại chu kỳ hành vi?
* [ ] Tất cả các event đều map về tính toán ít nhất một metric?
* [ ] Mọi metric trong hệ thống đều có event tương ứng để đo đếm?

> [!IMPORTANT]
> **GATE 5 — Bài sạch lỗi kinh điển:** Vượt qua toàn bộ 7 câu hỏi tự soi lỗi; nếu có quyết định nào "phá lệ" so với quy chuẩn thông thường, phải giải thích rõ ràng lý do trong phần Rationale.

---

## IV. Quy định sử dụng AI & AI Support Log

### 1. Phạm vi cho phép & Nghiêm cấm

**Được dùng AI để:**
* Brainstorm danh sách các ứng viên Core Action và câu hỏi phản biện để tự tranh luận.
* Gợi ý cấu trúc tên event chuẩn `object_action` và tiêu chí nghiệm thu mẫu.
* Đóng vai "khách hàng khó tính" hoặc "Data Leader khó tính" để phản biện lại Core Job và Cadence.

**Tuyệt đối KHÔNG dùng AI để:**
* Chọn thay Core Action, viết thay kết luận Cadence hay Metric Hypothesis (quyết định nghiệp vụ cốt lõi phải do chính bạn đưa ra).
* Bịa số liệu benchmark hoặc tỉ lệ retention không có cơ sở thực tế.
* Viết thay toàn bộ phần Rationale và Reflection.

### 2. Mẫu AI Support Log (Kèm trong repo)
```markdown
# AI Support Log

## 1. AI đã giúp tôi ở đâu?
(Ghi rõ prompt và phần AI hỗ trợ cấu trúc, brainstorm)

## 2. AI sai, hời hợt hoặc đề xuất metric sai nature ở đâu?
(Ghi lại những điểm AI gợi ý sai lệch, rập khuôn kiểu DAU/MAU)

## 3. Tôi đã tự sửa hoặc quyết định lại điều gì?
(Những quyết định độc lập của bạn dựa trên hiểu biết sâu sắc về nghiệp vụ)
```

---

## V. Cấu trúc Nộp bài chuẩn

Mỗi học viên nộp một repository GitHub cá nhân theo định dạng:
`Track1_Day20_MHV_HoVaTen/`

```text
Track1_Day20_MHV_HoVaTen/
├── README.md               # Họ tên, MHV, Dự án, Link tệp Metrics Pack, Đúc kết áp dụng
├── metrics-pack.md         # Toàn bộ nội dung phân tích chi tiết từ Mục 00 đến Mục 06
├── ai-support-log.md       # Báo cáo nhật ký sử dụng AI minh bạch
└── yeucau.md               # Tài liệu đề bài và hướng dẫn chuẩn hóa
```

### Cấu trúc tệp `metrics-pack.md`:
* **00 — Dự án, persona, core job**
* **01 — Core Action Card (+ kết quả tự kiểm 5 tiêu chí)**
* **02 — Action Nature Card + kết luận cadence**
* **03 — Metric System (activation / engagement / NSM / leading / counter)**
* **04 — Retention Definition (6 thành phần)**
* **05 — Product Loop (2 chu kỳ + metric hypothesis)**
* **06 — Tracking nhanh (4–8 events + 2 acceptance criteria)**

---

## VI. 5 Gate đánh giá tổng kết của Giảng viên / Coach

| Gate | Tiêu chuẩn ĐẠT | Dấu hiệu KHÔNG ĐẠT |
| :--- | :--- | :--- |
| **1. Core Action** | Có actor / object / completion rule rõ ràng; vượt qua 5 tiêu chí tự kiểm. | Chọn "mở app", "hỏi AI", "đăng nhập", "engage". |
| **2. Cadence** | Kết luận chuẩn template, xuất phát từ nhịp tự nhiên của bài toán. | Chọn Daily/Weekly theo quán tính dashboard, thiếu chữ "vì". |
| **3. Metric & Retention** | Retention đủ 6 thành phần; NSM đủ 3 thành phần; có Counter-metric bảo vệ. | "D7 retention" trơ trọi; NSM chỉ đếm số lượng truy vấn AI. |
| **4. Loop** | Loop $\ge 2$ chu kỳ; có Metric Hypothesis trỏ về metric cụ thể. | Dùng notification/streak làm động lực chính để kéo user về. |
| **5. Tracking** | 4–8 events chuẩn cú pháp; map 1-1 với metric; có $\ge 2$ tiêu chí nghiệm thu. | Track click vụn vặt; bắn event khi action chưa hoàn tất. |
