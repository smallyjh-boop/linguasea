# 任务清单（`/plan` 规划写进这里，`/go` 逐条执行）

> 2026-11-01 建。这里只放**可以一项一项执行的任务**；为什么做、产品方案在 docs/PLAN.md，整体状态和店主要做的事在 docs/NEXT-STEPS.md，路线图在 docs/ROADMAP.md。
>
> 规则：编号只增不改；每项写清"谁做"（开发 = AI，店主 = 本人办的账号、密钥、付款、商店后台、请人）、"等什么"、验收标准。开发任务做完：`npm run check`（改了界面加 `npm run e2e`）通过 → 提交推送 → 勾选并移到「已完成」。工作方式见 CLAUDE.md「工作方式」。
>
> **现在（2026-11-01）店主说暂时不继续开发**：下面的开发任务都在等店主那边的事，店主说"继续"再执行。

## 待做

### 店主

- [ ] T1｜店主｜在威联通 NAS 上部署测试服务器｜按 docs/DEPLOY-QNAP.md 第 1–4 步；要在外面用手机测就做第 5a 步（临时 https 网址）｜验收：浏览器打开 `http://<NAS IP>:8090/app/` 能上课；把 https 网址告诉开发（→ T8）｜**进展 2026-11-12：店主已部署到正式服务器（不只是 NAS 局域网），进入部署测试阶段；等店主给网址做 T8 检查**
- [ ] T2｜店主｜到 Azure 门户看本月实际费用（2026-10-29 跑完 C–F 配音，估算约 US$25）｜确认没有意外费用
- [ ] T3｜店主｜申请 Apple Developer（每年 99 美元）、Google Play Console（一次 25 美元）｜审核要几天到几周（→ T10）
- [ ] T4｜店主｜定品牌名、买域名、开客服邮箱｜查商标和商店重名（→ T9、T10）
- [ ] T5｜店主｜请母语老师审四门课｜开发先跑 `npm run review:sheet` 给表格；顺便抽听配音：中文"得 děi"（zh-C2-04）单念、对话里的多音字（→ T12）
- [ ] T6｜店主｜准备密钥：Anthropic（AI 老师）、Resend（登录邮件）、RevenueCat + Stripe（订阅）｜只填进 NAS / 云端环境设置，不发在聊天里（→ T11）
- [ ] T7｜店主｜律师审法律文件（隐私政策、条款，泰国 PDPA）｜docs/legal/README.md 有 4 条待确认的承诺

### 开发（都在等店主）

- [ ] T8｜开发｜等 T1｜从外面检查 NAS 部署｜`npm run content && npm run smoke -- <https 网址>`，有问题就修｜验收：smoke 全部 PASS
- [ ] T9｜开发｜等 T4｜换掉品牌名、客服邮箱和法律页占位｜`app/app.json`、`app/src/lib/config.ts`（SUPPORT_EMAIL）、`server/public/`（support 页、`/legal/` 的 `[TBD: …]` / `[รอกรอก]`）、docs/STORE-LISTING.md｜验收：`grep -rE "\[TBD|รอกรอก|support@example.com" server/public app/src` 没有结果，`npm run check`、`npm run e2e` 通过
- [ ] T10｜开发｜等 T3、T4（固定 https 网址）｜手机内测版｜EAS preview 的 `EXPO_PUBLIC_API_URL` 设成固定网址，用 `.github/workflows/eas.yml` 打包（docs/LAUNCH.md 第 10 步）｜验收：店主手机上装好，能上课、同步、录音
- [ ] T11｜开发｜等 T6｜逐项真测密钥功能｜AI 老师一轮对话、发音打分、语音输入、登录邮件、RevenueCat 沙盒的购买 / 退款 / 延期事件｜验收：每项实测通过，结果记进 docs/TEST-REPORT.md
- [ ] T12｜开发｜等 T5｜按母语老师意见改课程｜按审校表 `lesson` / `id` 列改两层内容（content/_review/README.md），改了词条文字 / `say` 的重新 `npm run audio`｜验收：`npm run validate`、`npm run dupes -- --meanings`、`npm run check` 通过，配音缺 0
- [ ] T13｜开发｜等 T9、T12｜商店截图、视频脚本、文案定稿｜docs/STORE-LISTING.md；截图用审校后的内容｜验收：店主确认后上传
- [ ] T14｜开发｜等 T7、T11｜正式上线前设置｜`NODE_ENV=production` + Resend、固定域名 https、数据库每日备份（留 ≤30 天）、日志 ≤90 天（docs/DEPLOY-QNAP.md 第 10 节、docs/LAUNCH.md 第 7 步）｜验收：`npm run smoke` 通过，邮箱登录收到真实邮件

## 不做的事（第一版）

- LINE / Apple / Google 登录、模拟考、排行榜、离线下载：方案里有，第一版不做，宣传时不能提。
- 刷新页面后正在上的课从头开始、静态目录提供点开头的文件：已定的产品取舍，先不改（docs/TEST-REPORT.md 第 6 节）。
- 新国家（越南等）和 G 阶段以后的内容：上线后再规划（docs/ROADMAP.md 阶段 5）。

## 已完成

- 2026-10-29｜配音：四门课 A–F 全部生成（39,567 段，`npm run audio -- --dry-run` 缺 0）。
- 2026-10-29｜部署：威联通 NAS 部署包（GHCR 镜像 amd64 + arm64、`deploy/qnap/`、`npm run smoke`、docs/DEPLOY-QNAP.md）。
- 2026-10-29｜服务器：失败不扣次数、按曼谷午夜重置、manifest 短缓存、卡片 due 校验、验证码计数存数据库、`ACCOUNTS_PER_IP_PER_HOUR`。
- 2026-10-29｜校验：同字不同音会共用配音时 `npm run validate` 报错；e2e 160/160。
- 更早的开发记录见 docs/HANDOVER.md 第 3 节和 git 历史。
