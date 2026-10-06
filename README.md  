# Track 1 — Day 20: Product Metrics Lab

**Họ tên:** Nguyễn Anh Dũng 

**MHV:** 2A202602554

**Dự án:** FIN-13 — AI Agent cá nhân hóa ưu đãi & tối ưu ngân sách  

**Metrics Pack:** Nội dung được trình bày trực tiếp trong README này.  

---

## Điều tôi mang về áp dụng cho dự án thật

Sau bài lab này, tôi xác định rõ metric của FIN-13 phải đi từ **giá trị thực mà Marketing/CRM Manager nhận được**, thay vì chỉ đo số lần đăng nhập, số prompt hỏi AI hay số chiến dịch được tạo. Core action cần phản ánh việc người dùng thực sự đưa một chiến dịch ưu đãi đã được tối ưu đến trạng thái có thể triển khai.

Điểm quan trọng nhất tôi rút ra là:

- Không ép FIN-13 thành sản phẩm có daily habit vì nhu cầu chạy campaign vốn mang tính **chu kỳ / workflow**.
- North Star phải gắn với **chiến dịch đủ chất lượng và thực sự được phê duyệt/triển khai**, không phải số output AI sinh ra.
- Retention phải đo theo chu kỳ chiến dịch của doanh nghiệp thay vì dùng D7 một cách máy móc.
- Product loop phải có lý do quay lại tự nhiên: **campaign mới, dữ liệu hiệu quả campaign cũ và ngân sách mới**, không phụ thuộc notification.
- Tracking chỉ giữ các event trực tiếp phục vụ metric; tránh track mọi click.

---

# 00 — Phạm vi

### 1. Dự án

**FIN-13 — AI Agent cá nhân hóa ưu đãi & hoàn tiền**, hỗ trợ doanh nghiệp lựa chọn đúng nhóm khách hàng, loại ưu đãi và phân bổ ngân sách tốt hơn dựa trên dữ liệu lịch sử, uplift/recommendation và các business constraints.

### 2. Persona

**Marketing/CRM Manager** tại doanh nghiệp có chương trình voucher/cashback và chịu trách nhiệm lập, duyệt hoặc vận hành campaign.

### 3. Core job

> “Tôi cần xác định nên ưu đãi cho nhóm khách hàng nào, mức ưu đãi bao nhiêu và phân bổ ngân sách thế nào để chiến dịch đạt mục tiêu mà không vượt ngân sách hoặc gửi voucher lãng phí.”

### Use case được chọn để phân tích sâu

**Tạo và phê duyệt một phương án campaign đã được tối ưu ngân sách để sẵn sàng triển khai.**

---

# 01 — Core Action

## 01.1 Phân biệt Core job, Core action, Core value và Core value event

| Khái niệm | Câu trả lời |
|---|---|
| **Core job** | Xây một phương án ưu đãi cho đúng nhóm khách hàng, phù hợp mục tiêu và giới hạn ngân sách |
| **Core action** | Marketing/CRM Manager **phê duyệt một campaign plan đã được hệ thống tối ưu** |
| **Core value** | Có một phương án campaign khả thi, đúng constraints và đủ cơ sở để triển khai thay vì chọn audience/voucher thủ công |
| **Core value event** | `campaign_plan_approved` |

### Vì sao không chọn “hỏi AI” hoặc “generate campaign”?

- `ask_ai` chỉ là thao tác giao diện, chưa chứng minh user nhận được value.
- `campaign_generated` là output của hệ thống, nhưng user có thể bỏ qua toàn bộ.
- `campaign_plan_approved` thể hiện người dùng đã xem xét và chấp nhận phương án đủ tốt để đi tiếp trong workflow thực tế.

---

## 01.2 Core Action Card

| Thành phần | Câu trả lời |
|---|---|
| **Target user** | Marketing/CRM Manager |
| **Core job** | Chọn audience, incentive và ngân sách phù hợp cho một campaign |
| **Core action** | Phê duyệt một campaign plan đã được tối ưu |
| **Object** | `campaign_plan` |
| **Preconditions** | Có mục tiêu campaign, budget, audience/data đầu vào; hệ thống đã tạo ít nhất một phương án hợp lệ; phương án không vi phạm hard constraints |
| **Completion rule** | Action hoàn tất khi user bấm phê duyệt và backend chuyển trạng thái campaign từ `draft/review` sang `approved` thành công |
| **Core value** | User có một phương án campaign khả thi, minh bạch về audience, incentive, ngân sách và các ràng buộc |
| **Evidence of value** | User chấp nhận phương án để triển khai thay vì bỏ, sửa lại toàn bộ hoặc huỷ |
| **Candidate event** | `campaign_plan_approved` |

---

## 01.3 Tự kiểm 5 tiêu chí

| Tiêu chí | Đạt? | Lý do |
|---|---:|---|
| **1. Gần core value** | ✅ | Phê duyệt nghĩa là user đánh giá phương án đủ tốt để đi tiếp tới triển khai |
| **2. Có thể lặp lại** | ✅ | Mỗi campaign mới lại phát sinh nhu cầu lựa chọn audience, incentive và budget |
| **3. Có thể quan sát** | ✅ | Backend có trạng thái rõ ràng khi campaign chuyển sang `approved` |
| **4. Có ý nghĩa** | ✅ | Tỷ lệ plan được duyệt tăng cho thấy hệ thống tạo đề xuất phù hợp hơn, nếu counter-metric không xấu đi |
| **5. Có thể tác động** | ✅ | Team có thể cải thiện data quality, uplift model, optimizer, explanation và UX review |

**Kết luận:** Core action đạt 5/5 tiêu chí và được giữ lại.

---

# 02 — Nature & Cadence

## 02.1 Action Nature Card

| Thành phần | Phân tích |
|---|---|
| **Actor** | Marketing/CRM Manager, ở cấp account/organization |
| **Intent** | Chuẩn bị một campaign có khả năng đạt mục tiêu kinh doanh trong giới hạn budget |
| **Trigger** | Chủ yếu từ nhu cầu kinh doanh: campaign mới, dịp lễ, sản phẩm mới, tồn kho, target doanh thu, ngân sách marketing mới hoặc hiệu quả campaign trước thấp |
| **Effort** | Trung bình đến cao: cần xác định mục tiêu, kiểm tra audience, budget, incentive, review kết quả optimizer và approval |
| **Value timing** | Value ban đầu xuất hiện ngay khi có plan đủ tốt để duyệt; business value thật xuất hiện trễ sau khi campaign chạy và có outcome |
| **State** | Lưu campaign configuration, selected audience, budget allocation, expected metrics, approval state và sau này là actual performance |
| **Dependency** | Phụ thuộc dữ liệu khách hàng, budget, business rules, model output, đôi khi có cấp quản lý/HITL phê duyệt |
| **Repeat condition** | Có campaign mới, budget mới, mục tiêu mới hoặc cần tối ưu lại dựa trên performance của campaign trước |

---

## 02.2 Dạng hành vi

**Workflow theo chu kỳ / campaign-based workflow.**

FIN-13 không phải sản phẩm mà Marketing Manager cần dùng nhiều lần mỗi ngày. Hành vi phụ thuộc vào nhịp lập và vận hành campaign của doanh nghiệp.

---

## 02.3 Kết luận cadence

> Đối với **Marketing/CRM Manager**, core action **phê duyệt một campaign plan đã được tối ưu** thường xuất hiện **mỗi khi có một campaign hoặc chu kỳ ngân sách mới**, vì nhu cầu tạo ưu đãi phát sinh theo kế hoạch marketing, sự kiện kinh doanh và kết quả campaign trước. Do đó, nhịp đo phù hợp là **theo campaign cycle, đồng thời tổng hợp theo tháng** ở cấp **organization/account**.

### Vì sao không dùng daily?

Frequency cao hơn không nhất thiết có nghĩa là value cao hơn. Nếu một Marketing Manager phải tạo hoặc sửa campaign mỗi ngày vì đề xuất kém chất lượng, đó thậm chí có thể là tín hiệu xấu.

---

# 03 — Metric System

## 03.1 Activation Metric

### Start event

`workspace_created`

Xảy ra khi organization/workspace FIN-13 được tạo và user bắt đầu sử dụng sản phẩm cho use case campaign optimization.

### Activation event

`campaign_plan_approved`

Đây là lần đầu user hoàn tất core action và chạm first value.

### Time window

**Trong vòng 14 ngày kể từ `workspace_created`.**

### Định nghĩa Activation

> Một organization được xem là **activated** khi có ít nhất **1 campaign plan được approved trong vòng 14 ngày kể từ lúc workspace được tạo**.

### Lý do chọn 14 ngày

Việc chuẩn bị data, cấu hình campaign và review recommendation có effort tương đối cao. Dùng D1/D3 sẽ ép cadence không phù hợp với nature của workflow B2B.

---

## 03.2 Engagement Metrics

### Metric 1 — Frequency

**Approved Campaign Plans per Active Organization per Month**

Công thức:

`Số campaign_plan_approved / số organization active trong tháng`

Mục đích: theo dõi organization có tiếp tục sử dụng FIN-13 cho các campaign mới hay không.

### Metric 2 — Depth

**Approval-without-major-rework rate**

Công thức:

`Số campaign được approved mà không cần major re-optimization / tổng số campaign được approved`

Một “major rework” là khi user thay đổi đáng kể audience, total budget hoặc incentive strategy sau khi hệ thống đã tạo plan đầu tiên.

Mục đích: đo mức độ hữu ích của plan ban đầu, không chỉ số lượng plan.

---

## 03.3 North Star Metric

### North Star

**Monthly Qualified Campaign Plans Approved**

> **Số campaign plan được Marketing/CRM Manager phê duyệt trong tháng, thỏa toàn bộ hard constraints và không bị rollback/cancel trước khi triển khai.**

### Công thức NSM

- **Unit of value:** một `campaign_plan`
- **Quality threshold:** pass hard constraints + được user phê duyệt + không bị rollback/cancel trước deployment
- **Frequency:** tính theo tháng ở cấp organization

### Vì sao metric này gần core value?

Mỗi đơn vị metric đại diện cho một campaign plan mà doanh nghiệp thực sự đánh giá là khả thi để triển khai. Nó tốt hơn “số plan AI generate” vì loại bỏ output không được user chấp nhận.

---

## 03.4 Leading Indicators

### 1. Valid plan generation rate

`Số plan pass toàn bộ hard constraints / tổng số optimization run`

**Giả thuyết:** nếu optimizer thường xuyên tạo được plan hợp lệ ngay từ đầu, xác suất user approve sẽ tăng.

### 2. First-plan acceptance rate

`Số campaign được approve từ phương án đầu tiên / số campaign có phương án được generate`

**Giả thuyết:** nếu recommendation, budget allocation và explanation sát nhu cầu, user ít phải rerun/rework và core action sẽ xảy ra nhanh hơn.

### 3. Median time-to-approval

Thời gian trung vị từ `campaign_created` đến `campaign_plan_approved`.

**Giả thuyết:** khi workflow rõ ràng và đề xuất hữu ích hơn, thời gian đi từ intent tới approved plan giảm, làm tăng khả năng workflow được hoàn thành.

---

## 03.5 Counter-metrics

### Counter-metric 1 — Constraint violation rate

`Số campaign plan vi phạm hard constraint / tổng số plan generated`

**Mục tiêu:** không được tăng khi cố tối ưu số lượng plan được approve.

### Counter-metric 2 — Post-approval rollback/cancel rate

`Số campaign đã approved nhưng bị rollback/cancel trước deployment / tổng số campaign approved`

**Mục tiêu:** approval tăng nhưng không được do UI ép duyệt hoặc recommendation chất lượng thấp.

### Counter-metric 3 — Budget overrun rate

`Số campaign deployment vượt spending cap / tổng số campaign deployed`

**Mục tiêu:** bằng 0 đối với hard budget cap.

---

# 04 — Retention Definition

## 04.1 Retention đầy đủ 6 thành phần

| Thành phần | Định nghĩa |
|---|---|
| **Unit** | Organization / workspace |
| **Cohort entry** | Organization có `first_campaign_plan_approved` |
| **Return event** | Có một `campaign_plan_approved` khác cho campaign mới |
| **Window** | Theo **campaign cycle**; dashboard vận hành tổng hợp theo **calendar month** |
| **Threshold** | Ít nhất 1 campaign plan mới được approved trong một cycle có campaign opportunity |
| **Segment** | Organization đã activated và có ít nhất 2 campaign opportunities trong giai đoạn quan sát |

---

## 04.2 Định nghĩa retention

> Một organization thuộc cohort tháng M được xem là **retained ở campaign cycle kế tiếp** nếu organization đó đã approve campaign đầu tiên trong tháng M và, khi phát sinh campaign opportunity tiếp theo, tiếp tục approve ít nhất một campaign plan mới bằng FIN-13.

### Lý do không dùng D7 retention

FIN-13 có cadence theo campaign. Một khách hàng chạy campaign mỗi tháng có thể hoàn toàn healthy dù không quay lại trong 7 ngày.

### Cách so retention

Retention nên được so với:

1. **Natural cycle:** chu kỳ campaign thật của từng nhóm khách hàng.
2. **Cohort đúng segment:** ví dụ SME chạy 1–2 campaign/tháng khác enterprise chạy liên tục.
3. **Benchmark category:** B2B MarTech / campaign management tools có workflow tương tự, nếu có dữ liệu phù hợp.

---

# 05 — Product Loop

## 05.1 Loại loop chính

**Workflow / progress loop ở cấp organization.**

---

## 05.2 Product Loop — hai chu kỳ

```text
[Chu kỳ 1]

Natural trigger
Có campaign mới / budget mới / mục tiêu doanh thu mới
        ↓
Core action preparation
Tạo campaign brief + chạy optimization
        ↓
Review
Kiểm tra audience + incentive + budget + constraints
        ↓
CORE ACTION
Approve campaign plan
        ↓
Immediate value
Có phương án khả thi để triển khai, giảm công sức chọn thủ công
        ↓
Saved state / investment
Lưu cấu hình campaign, approval, audience, budget, expected outcome
        ↓
Deploy + collect actual outcome


[Chu kỳ 2]

Next natural trigger
Campaign mới hoặc kết quả campaign trước đã có
        ↓
System sử dụng historical outcome + constraints mới
        ↓
Tạo / tối ưu campaign plan tiếp theo
        ↓
User review
        ↓
CORE ACTION
Approve campaign plan tiếp theo
        ↓
Repeat value
Ra quyết định nhanh hơn, plan phù hợp hơn và có dữ liệu quá khứ để tham chiếu
        ↓
Saved state tiếp tục dày lên
        ↺
```

---

## 05.3 Reason to return nếu bỏ notification

User vẫn có lý do quay lại vì:

- xuất hiện campaign mới;
- có budget mới;
- có dịp marketing mới;
- cần phản ứng với hiệu quả campaign trước;
- cần tối ưu audience/incentive cho một business goal mới.

Notification chỉ là nurture, không phải lý do cốt lõi để quay lại.

---

## 05.4 Metric Hypothesis

> Nếu loop này hoạt động, **Monthly Qualified Campaign Plans Approved** sẽ **tăng và Median Time-to-Approval sẽ giảm** trong **2–3 campaign cycles**, vì dữ liệu outcome và cấu hình từ các campaign trước giúp hệ thống tạo phương án sát constraints hơn, đồng thời user đã có workflow review quen thuộc và ít phải rework hơn.

---

# 06 — Tracking nhanh

## 06.1 Core events

| Tên event | Ý nghĩa | Thời điểm ghi nhận | Metric sử dụng |
|---|---|---|---|
| `workspace_created` | Một organization bắt đầu sử dụng FIN-13 | Khi backend tạo workspace thành công lần đầu | Activation cohort start |
| `campaign_created` | User tạo một campaign object có mục tiêu cụ thể | Khi campaign được lưu thành công với campaign_id | Time-to-approval, funnel |
| `optimization_completed` | Budget Optimizer hoàn tất một lần chạy và trả về plan | Khi job optimization kết thúc thành công và plan được persist | Valid plan generation rate |
| `campaign_plan_validated` | Plan đã pass toàn bộ hard constraints | Khi constraint engine xác nhận plan hợp lệ | Valid plan generation rate, NSM quality threshold |
| `campaign_plan_approved` | User phê duyệt plan để chuyển sang bước triển khai | Khi backend chuyển state sang `approved` thành công | Activation, Engagement, Retention, NSM |
| `campaign_plan_reoptimized` | User yêu cầu chạy lại optimizer sau khi đã có plan | Khi một optimization run mới được tạo cho cùng campaign | First-plan acceptance, rework analysis |
| `campaign_deployed` | Campaign đã được đưa sang trạng thái triển khai | Khi backend xác nhận deployment thành công | NSM qualification, downstream outcome |
| `campaign_cancelled` | Campaign đã approved nhưng bị huỷ/rollback trước deployment hoặc trong workflow | Khi state chuyển sang `cancelled`/`rolled_back` | Counter-metric: rollback/cancel rate |

---

## 06.2 Mapping event → metric

| Metric | Event chính cần dùng |
|---|---|
| Activation rate | `workspace_created`, `campaign_plan_approved` |
| Approved Campaign Plans / Organization / Month | `campaign_plan_approved` |
| Approval-without-major-rework rate | `campaign_plan_reoptimized`, `campaign_plan_approved` |
| Monthly Qualified Campaign Plans Approved | `campaign_plan_validated`, `campaign_plan_approved`, `campaign_deployed`, `campaign_cancelled` |
| Valid plan generation rate | `optimization_completed`, `campaign_plan_validated` |
| First-plan acceptance rate | `optimization_completed`, `campaign_plan_reoptimized`, `campaign_plan_approved` |
| Median time-to-approval | `campaign_created`, `campaign_plan_approved` |
| Campaign-cycle retention | `campaign_plan_approved` theo organization + campaign_id + thời gian |
| Post-approval rollback/cancel rate | `campaign_plan_approved`, `campaign_cancelled` |

---

## 06.3 Acceptance Criteria

### AC1 — Approval event chỉ bắn khi approval thật sự hoàn tất

Với mỗi `campaign_id`, hệ thống chỉ ghi `campaign_plan_approved` khi trạng thái campaign chuyển thành công từ trạng thái hợp lệ như `review` sang `approved`.

Việc user chỉ mở màn hình review, bấm nút nhưng API thất bại, hoặc request bị validation error **không được** tạo event `campaign_plan_approved`.

---

### AC2 — Không ghi trùng do reload/retry

Với cùng một `campaign_id` và cùng một `approval_version`, hệ thống chỉ ghi tối đa **một** `campaign_plan_approved`.

Reload trang, retry request, network retry hoặc frontend gửi lại cùng idempotency key không được tạo thêm event approval.

---

### AC3 — Validation phải phản ánh hard constraints thật

`campaign_plan_validated` chỉ được ghi sau khi toàn bộ hard constraints bắt buộc đã pass, ví dụ:

- total spend ≤ campaign budget;
- customer frequency cap không bị vi phạm;
- audience nằm trong tập eligible;
- incentive hợp lệ;
- các policy bắt buộc khác đều pass.

Không ghi event chỉ vì optimizer đã trả về output.

---

### AC4 — Cancel/Rollback phải giữ được quan hệ với approval

Mọi `campaign_cancelled` sau approval phải chứa cùng `campaign_id` và reference đến version plan đã approved để tính chính xác post-approval rollback/cancel rate.

---

# 07 — Tự soi lỗi

| Checklist | Kết quả |
|---|---:|
| Core action không phải thao tác giao diện hay output hệ thống | ✅ |
| Activation không phải login/onboarding | ✅ |
| Frequency không cao hơn nhu cầu thật | ✅ |
| Loop có reason to return ngoài notification | ✅ |
| Retention dùng cadence phù hợp với campaign workflow | ✅ |
| Mọi event đều map về metric | ✅ |
| Các metric chính đều có event để tính | ✅ |
| Core Action Card có actor/object/completion rule | ✅ |
| Retention đủ 6 thành phần | ✅ |
| Loop có metric hypothesis | ✅ |
| Tracking có 4–8 core events | ✅ |
| Có ít nhất 2 acceptance criteria | ✅ |

---

# 08 — Revision / Rationale

**Revision chính:** Không chọn `campaign_generated` hoặc `ask_ai` làm core action vì đây chỉ là output/thao tác trong hệ thống và chưa chứng minh user đã nhận value.

Core action cuối cùng được chọn là `campaign_plan_approved` vì nó nằm gần điểm user thực sự chấp nhận phương án do FIN-13 hỗ trợ để đưa vào workflow triển khai.

Cadence cũng được đổi từ cách nghĩ thông thường kiểu “weekly active” sang **campaign-based cadence**, vì nhu cầu sử dụng FIN-13 phát sinh theo campaign/business cycle chứ không có lý do tự nhiên để Marketing Manager phải dùng sản phẩm mỗi ngày.

---

# Tóm tắt Metrics Pack

| Hạng mục | Lựa chọn |
|---|---|
| **Persona** | Marketing/CRM Manager |
| **Core job** | Xây phương án ưu đãi đúng audience và budget |
| **Core action** | Approve optimized campaign plan |
| **Core value event** | `campaign_plan_approved` |
| **Natural cadence** | Theo campaign cycle, tổng hợp theo tháng |
| **Activation** | First approved campaign plan ≤ 14 ngày từ workspace creation |
| **Engagement** | Approved campaigns/org/month + approval-without-major-rework |
| **North Star** | Monthly Qualified Campaign Plans Approved |
| **Retention unit** | Organization |
| **Return event** | Approve một campaign plan mới trong campaign opportunity tiếp theo |
| **Loop** | Campaign trigger → optimize → approve → deploy/outcome → next campaign |
| **Counter-metrics** | Constraint violation, rollback/cancel, budget overrun |
| **Tracking core** | 8 events, tập trung vào campaign lifecycle |

