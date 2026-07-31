# Review PRD — Senior QE, User & Business Lens

Một Codex skill để review PRD, Jira ticket hoặc feature specification theo ba góc nhìn:

- **Business:** mục tiêu, KPI, trade-off, rollout.
- **Senior QE:** rule, edge case, integration, lỗi và khả năng test.
- **User:** sự rõ ràng, kiểm soát, trust và recovery trong hành trình sử dụng.

Kết quả ưu tiên là một danh sách ngắn các quyết định cần chốt trước khi test hoặc release — không phải checklist QA chung chung.

## Vì sao có skill này?

PRD và Jira ticket thường đã mô tả được happy path, nhưng thiếu hoặc mâu thuẫn ở các quyết định khiến team phải tự đoán khi build, test và vận hành: điều gì xảy ra khi lỗi, ai được áp dụng, khi nào thay đổi có hiệu lực, hoặc success được đo bằng gì.

Skill này tạo một cách review thống nhất để phát hiện sớm các khoảng trống đó. Nó gộp business, user và QE vào **cùng một quyết định**, giúp PM/PO/BA, engineer và QC trao đổi trên tác động thực tế thay vì tạo nhiều danh sách câu hỏi trùng nhau.

Mục tiêu là giảm rework, hạn chế bug do requirement mơ hồ và bảo đảm user nhận đúng trải nghiệm mà business kỳ vọng.

## Cài đặt

Clone repository hoặc tải riêng folder `review-prd`.

Sau đó copy folder này vào thư mục skills của Codex:

```bash
mkdir -p ~/.codex/skills
cp -R review-prd ~/.codex/skills/
```

Cấu trúc sau khi cài:

```text
~/.codex/skills/
└── review-prd/
    └── SKILL.md
```

Mở một task mới hoặc khởi động lại Codex để skill được nhận diện.

## Cách dùng

Gửi PRD, nội dung ticket, file, hoặc một link có thể truy cập. Ví dụ:

```text
Review PRD này theo góc nhìn senior QE, user và business:
https://confluence.example.com/...
```

```text
GE-12345 - review ticket này
```

```text
Chỉ review phần rollout và error handling của PRD bên dưới.
```

Codex sẽ tự nhận skill khi yêu cầu phù hợp. Bạn cũng có thể nhắc rõ tên `review-prd` trong prompt.

## Đầu ra

Review mặc định gồm:

1. Các điểm đã rõ trong requirement.
2. Bảng **Quyết định cần chốt** gồm mức độ cần chốt, quyết định, tác động nếu chưa chốt và nguồn tham chiếu.
3. Kết luận readiness: `READY`, `READY_WITH_CONDITIONS` hoặc `NOT_READY`.

Skill tránh lặp lại cùng một vấn đề ở nhiều bảng và không tự gán người chịu trách nhiệm.

## Quyền truy cập Jira/Confluence

Skill chỉ chứa workflow review; để Codex đọc Jira hoặc Confluence từ link, người dùng cần:

- Có quyền xem nội dung trên Jira/Confluence.
- Cài và đăng nhập Atlassian connector/MCP trong Codex.

Nếu không truy cập được link, hãy dán phần PRD hoặc description/comment của ticket vào chat để review.
