---
description: 跑检查，只看结论（Haiku）：默认 npm run check，加 e2e 参数再跑端到端
argument-hint: [可选：e2e / validate zh / smoke <网址>]
model: haiku
---
交给 test-runner 子代理运行：$ARGUMENTS（没写就是 `npm run check`；写 `e2e` 就先 `npm run content` 再 `npm run e2e`；写 `smoke <网址>` 就 `npm run smoke -- <网址>`）。
只回复它的结论，不贴日志。
