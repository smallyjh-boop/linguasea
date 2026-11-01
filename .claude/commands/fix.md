---
description: 修 bug：定位根因 → 最小改动 → 补测试 → 检查（Sonnet）
argument-hint: <现象 / 报错 / 文件路径>
model: sonnet
---
问题：$ARGUMENTS

1. 先定位根因：给了路径就直接看；没给就交给 code-searcher 子代理查。
2. 用最小改动修复，不顺手重构别的代码。课程内容的问题两层（`content/courses/`、`content/l1/th/`）一起改，课号和词条 id 不改。
3. 补一个能复现这个 bug 的测试（内容问题能加进 `npm run validate` 的就加校验）。
4. 交给 test-runner 子代理跑 `npm run check`；改了界面再跑 `npm run e2e`。
5. 用中文回复：根因一句话 + 改了什么。修 2 次仍失败就停下，建议用 /model opus 接手。不要自己提交，除非我说提交。
