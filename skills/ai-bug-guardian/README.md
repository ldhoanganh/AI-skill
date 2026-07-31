# AI Bug Guardian

Skill Codex hỗ trợ QE biến một tin nhắn mô tả lỗi thành bug report tiếng Anh theo chuẩn GE, review độ đầy đủ và tạo Jira ticket sau khi QE xác nhận.

## Vì sao có skill này?

Bug report giữa các team thường không đồng nhất và dễ thiếu Expected Result, môi trường test, bước tái hiện hoặc impact. Dev vì vậy phải hỏi lại QE trước khi có thể hiểu và reproduce lỗi.

AI Bug Guardian giảm phần công việc lặp lại khi log bug, nhưng không thay thế QE. QE vẫn là người reproduce lỗi, xác nhận business expectation, xác nhận Severity được AI gợi ý và quyết định Priority. Skill giúp chuẩn hóa cách trình bày evidence, phát hiện thông tin quan trọng còn thiếu và giữ ticket đủ rõ để Dev xử lý nhanh hơn.

Kỳ vọng khi dùng chung trong team:

- Tăng tỷ lệ bug report đủ template.
- Giảm thời gian viết bug report lặp lại.
- Giảm số vòng hỏi lại giữa QE và Dev.
- Giữ format Jira nhất quán cho Growth Enablement.

## Dùng để làm gì?

- QE chỉ cần gửi một message tự do bằng tiếng Việt hoặc tiếng Anh, kèm screenshot nếu có.
- AI tạo Jira-safe bug report đầy đủ: Description, Test Environment, Steps, Actual/Expected, Notes, Workaround và Reproducibility table. Summary chỉ nằm ở title của Jira ticket, không lặp lại trong description.
- AI hiển thị phần Internal QE Review riêng: Component gợi ý, label, kiểm tra duplicate bug, Root Cause Guess, Impact, Readiness, Quality Score và câu hỏi cần thiết.
- Chỉ khi QE nhắn **“Đẩy ticket này lên Jira”**, AI mới tạo issue thật.

AI có thể gợi ý Severity theo mapping chính thức (kèm lý do và độ tin cậy), nhưng QE phải xác nhận trước khi Jira được tạo. AI không tự quyết định Priority hoặc business rule.

Duplicate Check và Root Cause Guess chỉ là thông tin nội bộ để QE review. Chúng không được đưa vào mô tả Jira và không thay thế việc xác nhận của QE/Dev.

Khi QE/Dev đã cung cấp nguyên nhân kỹ thuật đã xác nhận, AI chỉ ghi thông tin đó ở **Notes** của Jira. Title, Description, Actual Result và Expected Result luôn tập trung vào symptom và hành vi mong đợi.

## Cài đặt

### 1. Clone repository

```bash
git clone <REPOSITORY_URL>
```

### 2. Cài skill vào Codex

Nếu repository chứa folder `ai-bug-guardian/`, copy folder này vào thư mục skills của Codex:

```bash
mkdir -p ~/.codex/skills
cp -R ai-bug-guardian ~/.codex/skills/
```

Mở lại Codex sau khi cài xong.

## Cách dùng

Gửi trực tiếp một message, ví dụ:

```text
Log bug giúp mình: User cannot complete the loyalty task after placing an order.
UID: 250523000006509
Environment: PROD
Platform: ZPA Android
Device: Galaxy Note8
```

AI sẽ trả bug report và Internal QE Review. QE chỉnh hoặc bổ sung thông tin nếu cần.

Khi đã review xong, nhắn:

```text
Đẩy ticket này lên Jira
```

## Jira MCP cần thiết

Mỗi người dùng phải tự cấu hình Atlassian MCP bằng tài khoản Jira của mình và có quyền tạo `Bug` trong project `GE`.

Không commit hoặc gửi lên Git các thông tin sau:

- Jira PAT/API token/password
- File `~/.codex/config.toml` cá nhân
- Screenshot chứa dữ liệu khách hàng nhạy cảm

## Quy tắc Jira GE

| Field | Rule |
|---|---|
| Project | `GE` |
| Issue Type | `Bug` |
| Product Domain | Tự set `Growth Enablement` |
| Severity | AI gợi ý Blocker, Critical, Major, Medium, Minor hoặc Trivial theo mapping chính thức; QE phải xác nhận trước khi tạo Jira |
| Component | AI gợi ý `CRM` hoặc `Marketing Solutions`; QE có thể sửa trước khi push |
| Sprint | CRM dùng board `GE - CRM Backlog`; MS dùng board `GE - MS Backlog`; chọn sprint theo date range hiện tại, không chỉ dựa vào trạng thái `active` của Jira |
| Labels | Luôn thêm `RC_CodeQuality`; chỉ thêm `BUG_FE` / `BUG_BE` khi evidence đủ rõ |
| Bug in Environments | Tự map `PROD` thành `Production`; giữ nguyên `SBQC` và `Staging` |

Sub Domain chỉ tự điền khi flow rõ: CRM/CRM Tool → `CRM`; NBA → `NBA`; loyalty/tier/membership → `Loyalty`; Notification Campaign → `Notification Service`; voucher/reward/promotion code/Direct Discount/Cashback → `Promotion Abilities`; Lucky Wheel/campaign game → `Campaign events & gamification`. Với case mơ hồ, AI hỏi QE chọn Sub Domain trước khi tạo Jira; nếu QE không biết thì để trống.

Với bug Web, Test Environment chỉ hiển thị các thông tin được cung cấp; không tự thêm `UID` hoặc `Devices: TBU`.

Pre-condition chỉ được ghi khi đó là điều kiện thật sự cần có trước khi reproduce; nếu không có evidence thì ghi `N/A`.

## Cập nhật Sprint sau khi tạo ticket

QE có thể nhắn, ví dụ: `Thêm GE-26147 vào sprint hiện tại`. AI sẽ lấy active sprint của board đúng Component (`CRM` hoặc `Marketing Solutions`) rồi thêm ticket vào sprint. Nếu có nhiều active sprint, AI sẽ hỏi QE chọn sprint nào.
