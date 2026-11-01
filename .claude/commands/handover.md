---
description: 结束会话前更新交接文档（NEXT-STEPS / TASKS），之后可以放心 /clear（Sonnet）
model: sonnet
---
根据本次会话做的事更新交接文档。**不要压缩或删掉已有内容**，只改变化的部分：

1. docs/NEXT-STEPS.md：开头的更新日期、「现在的状态」、「店主要做的事」里已完成的打 ✅、「开发这边下一步」。新的店主决定写进「店主的决定（已定）」。
2. docs/TASKS.md：勾选完成的任务并移到「已完成」（写日期和一句结果），新发现要做的加进「待做」。
3. 新发现的坑、已知问题：写进 docs/HANDOVER.md 第 5 节；店主的新要求（原话）追加到第 2 节的列表。
4. 测试数量、没修的问题有变化：同步 docs/TEST-REPORT.md。
5. 提交（`文档：交接……`）并 `git push -u origin main`。
完成后回复："已交接，可以 /clear。"
