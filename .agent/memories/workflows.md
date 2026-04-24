# Workflows

### [2026-04-24 20:00] - Memory Read Workflow
Trước mỗi task, agent đọc `.agent/memory.md` nếu tồn tại; sau đó chỉ đọc các file con liên quan theo index.

### [2026-04-24 20:47] - Dùng sub-agent khi update rule
Khi user yêu cầu update/bổ sung rule hoặc memory vận hành tương tự, ưu tiên dùng sub-agent để xử lý phần cập nhật file nếu môi trường cho phép, giúp main agent tiết kiệm thời gian cho công việc chính. Main agent vẫn chịu trách nhiệm kiểm tra kết quả và tổng hợp lại.
