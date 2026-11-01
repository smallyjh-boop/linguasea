---
description: 执行 docs/TASKS.md 里下一个开发任务：实现 → 检查 → 提交推送 → 更新文档（Sonnet）
argument-hint: [可选：任务编号，如 T12]
model: sonnet
---
1. 读 CLAUDE.md 和 docs/TASKS.md，执行任务 $ARGUMENTS；没指定就做「待做」里第一个"谁做：开发"且没勾选的任务。只做这一个。标着"店主"的、或要等密钥 / 账号的任务跳过。
2. 只读这个任务涉及的文件；找不到位置时交给 code-searcher 子代理。
3. 按 CLAUDE.md 的约定实现（id 永远不改；两层内容一起改；引擎不用 node: 模块；不写死语言逻辑）。代码改动附带测试；大批量写课 / 审校按 docs/prompts/ 的流水线。
4. 交给 test-runner 子代理跑 `npm run check`；改了 App 界面再跑 `npm run e2e`。失败就修，最多修 3 轮，还不行就停下，告诉我卡在哪。
5. 通过后用 /commit 的规则提交，并 `git push -u origin main`（网络失败按 2s/4s/8s/16s 重试）。
6. 在 docs/TASKS.md 勾选该任务、写上日期和一句结果，移到「已完成」；状态有变化时同步 docs/NEXT-STEPS.md（以及 HANDOVER / ROADMAP / TEST-REPORT 里相关的那一两行），一起提交推送。
7. 用中文回复 3–5 行：改了哪些文件、为什么、检查结果。
