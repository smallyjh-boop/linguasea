---
description: 规划：把要做的事拆成小任务写进 docs/TASKS.md（Opus，不写代码）
argument-hint: <要做的功能 / 要处理的事>
model: opus
---
需求：$ARGUMENTS

1. 先读 CLAUDE.md、docs/NEXT-STEPS.md、docs/TASKS.md；需要时读 docs/HANDOVER.md、docs/ROADMAP.md、docs/TEST-REPORT.md。要了解代码就交给 code-searcher 子代理，不要自己逐个打开文件。
2. 把需求拆成 3–8 个小任务，每个任务一个会话内能做完。
3. 每个任务写清：编号（接着 TASKS.md 里已有的最大编号）、谁做（开发 / 店主）、涉及文件、做法要点、验收标准（要跑哪些检查：`npm run check`，改了界面加 `npm run e2e`）。
4. 写明"不做的事"。
5. 写进 docs/TASKS.md 的「待做」，不要删已完成的记录。**不要改 docs/PLAN.md**：那是产品方案，不是任务清单。
6. 要店主本人做的事（密钥、账号、付款、商店后台、请人）标成"店主"，开发任务不能依赖它们才能验收。
7. 用 5 行以内总结方案；有需要店主决定的地方列出来问。不要写代码，不要开始执行。
