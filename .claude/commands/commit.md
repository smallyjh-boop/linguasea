---
description: 按本仓库格式写提交信息并提交（Haiku）
model: haiku
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git log:*)
---
1. 看 `git status`、`git diff`、`git log --oneline -5`。
2. 确认没有密钥、`.env`、签名文件、`app/dist/`、`app/src/content/generated/` 被加进来；有就停下告诉我。
3. 提交信息格式（本仓库习惯）：`范围：中文说明`，范围用 App / 服务器 / 引擎 / 内容 / 配音 / 工具 / 部署 / 文档 之一；一行标题，必要时空一行加 2–4 行正文说明为什么。
4. 改动包含几件不相关的事，建议拆成几次提交，先问我。
5. 否则 `git add -A` 并提交，回复提交信息。不要 push（/go 会负责推送）。
