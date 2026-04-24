# My Agent Rules

Repo này chứa bộ rule dùng để cấu hình coding agent khi làm việc trong project.

## Nội dung chính

- `AGENTS.md`: rule bắt buộc cho agent trong repo.
- Memory rules: lưu ghi nhớ dài hạn vào `.agent/memory.md` khi user yêu cầu.
- Git rules: tránh tự ý commit, push, reset, revert hoặc xoá thay đổi ngoài phạm vi.
- Karpathy-inspired rules: tư duy trước khi code, ưu tiên đơn giản, sửa đúng phạm vi, verify theo mục tiêu.
- Critical thinking rules: agent cần phản biện lịch sự, không hùa theo user khi yêu cầu có rủi ro.
- Model routing rules: dùng sub-agent `gpt-5.1-codex-mini` cho tác vụ đọc/khám phá source nếu môi trường hỗ trợ.

## Cách dùng

Copy hoặc giữ `AGENTS.md` ở root của repo để agent tự đọc và tuân thủ rule trong toàn bộ project.

Nếu cần rule riêng cho thư mục con, tạo thêm `AGENTS.md` trong thư mục đó; file sâu hơn sẽ override rule root cho phạm vi tương ứng.
