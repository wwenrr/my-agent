# My Agent Rules

Repo này chứa bộ rule để setup coding agent cho project: memory, git safety, phản biện, simplicity, surgical changes, goal-driven execution và model routing cho sub-agent.

## Có gì trong repo?

- `AGENTS.md`: rule chính, đặt ở root repo để agent tự đọc và tuân thủ.
- `.agent/memory.md`: memory index/router, agent đọc trước khi làm task.
- `.agent/memories/*.md`: các file memory con theo chủ đề.

## Cài nhanh bằng curl

### Cách 1: Chỉ tải `AGENTS.md`

Dùng khi bạn chỉ muốn rule agent, chưa cần memory skeleton.

```bash
curl -fsSL https://raw.githubusercontent.com/wwenrr/my-agent/main/AGENTS.md -o AGENTS.md
```

### Cách 2: Tải full bundle `AGENTS.md` + memory skeleton

Dùng khi bạn muốn bật luôn workflow memory nhiều file.

```bash
curl -fsSL https://raw.githubusercontent.com/wwenrr/my-agent/main/AGENTS.md -o AGENTS.md
mkdir -p .agent/memories
curl -fsSL https://raw.githubusercontent.com/wwenrr/my-agent/main/.agent/memory.md -o .agent/memory.md
for file in user-preferences project-context coding-style decisions workflows; do
  curl -fsSL "https://raw.githubusercontent.com/wwenrr/my-agent/main/.agent/memories/${file}.md" \
    -o ".agent/memories/${file}.md"
done
```

### Cách 3: One-liner full setup

```bash
curl -fsSL https://raw.githubusercontent.com/wwenrr/my-agent/main/AGENTS.md -o AGENTS.md && mkdir -p .agent/memories && curl -fsSL https://raw.githubusercontent.com/wwenrr/my-agent/main/.agent/memory.md -o .agent/memory.md && for file in user-preferences project-context coding-style decisions workflows; do curl -fsSL "https://raw.githubusercontent.com/wwenrr/my-agent/main/.agent/memories/${file}.md" -o ".agent/memories/${file}.md"; done
```

## Cài bằng git clone

Dùng khi bạn muốn copy thủ công hoặc fork chỉnh rule riêng.

```bash
git clone https://github.com/wwenrr/my-agent.git
cp my-agent/AGENTS.md ./AGENTS.md
mkdir -p .agent
cp -R my-agent/.agent/* ./.agent/
```

## Update rule từ remote

### Update chỉ `AGENTS.md`

```bash
curl -fsSL https://raw.githubusercontent.com/wwenrr/my-agent/main/AGENTS.md -o AGENTS.md
```

### Update full bundle

Cẩn thận: lệnh này có thể ghi đè memory skeleton hiện tại. Nếu project đã có memory riêng, backup trước hoặc chỉ update `AGENTS.md`.

```bash
cp -R .agent ".agent.backup.$(date +%Y%m%d-%H%M%S)" 2>/dev/null || true
curl -fsSL https://raw.githubusercontent.com/wwenrr/my-agent/main/AGENTS.md -o AGENTS.md
mkdir -p .agent/memories
curl -fsSL https://raw.githubusercontent.com/wwenrr/my-agent/main/.agent/memory.md -o .agent/memory.md
for file in user-preferences project-context coding-style decisions workflows; do
  curl -fsSL "https://raw.githubusercontent.com/wwenrr/my-agent/main/.agent/memories/${file}.md" \
    -o ".agent/memories/${file}.md"
done
```

## Memory workflow

- Trước mỗi task, agent đọc `.agent/memory.md` nếu tồn tại.
- `.agent/memory.md` chỉ là index/router, không nên nhồi mọi thứ vào một file.
- Memory dài/chuyên mục nằm trong `.agent/memories/*.md`.
- Agent chỉ ghi thẳng vào memory khi user yêu cầu rõ như `remember`, `ghi nhớ`, `save to memory`.
- Nếu agent tự phát hiện điều đáng lưu, agent phải hỏi xác nhận trước khi ghi.

## Ghi chú

- Nếu repo con cần rule riêng, tạo thêm `AGENTS.md` trong thư mục con; file sâu hơn sẽ override rule root cho phạm vi đó.
- Nếu đang dùng git, nhớ review diff trước khi commit vì `AGENTS.md` là rule vận hành dài hạn cho agent.
