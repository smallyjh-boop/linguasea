# 任务清单（`/plan` 规划写进这里，`/go` 逐条执行）

> 2026-11-01 建。这里只放**可以一项一项执行的任务**；为什么做、产品方案在 docs/PLAN.md，整体状态和店主要做的事在 docs/NEXT-STEPS.md，路线图在 docs/ROADMAP.md。
>
> 规则：编号只增不改；每项写清"谁做"（开发 = AI，店主 = 本人办的账号、密钥、付款、商店后台、请人）、"等什么"、验收标准。开发任务做完：`npm run check`（改了界面加 `npm run e2e`）通过 → 提交推送 → 勾选并移到「已完成」。工作方式见 CLAUDE.md「工作方式」。
>
> **现在（2026-11-01）店主说暂时不继续开发**：下面的开发任务都在等店主那边的事，店主说"继续"再执行。
>
> **2026-11-12 更新：店主已部署到正式服务器，试用后决定上线前先做"大手术"改造学法**（原话："这种非图形化的没讲解的学法正常人学不会"；"参考 Duolingo，先做完大手术再上线，但量不是全参考，还要参考其它软件，有些认字的东西还是要考试填空阅读的"）。改造任务是 T15–T24，按顺序做；T15 的设计稿要店主确认（T16）后才开工 T17 以后的开发。

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

### 大手术：改造学法（2026-11-12 规划，上线前做完）

> 现状（code-searcher 查的）：题型只有 4 种四选一（看词选意思、听音选意思、看意思选词、听音选词）和跟读打分；没有填空、排序组句、配对、打字；内容和界面没有任何图片；讲解（`notes`）排在学词和对话之后；游戏化只有 XP 和连续天数；课程地图是 `app/src/app/index.tsx` 的长列表。现有内容（约 1.4 万词条、对话、讲解、读物、配音）全部保留，**课号和词条 id 不改**。

- [x] T15｜开发｜**2026-11-12 已交，同日按店主"语音更重要，要先说出来才有信心，前期用短语，不要太长，要有趣"改版：docs/LEARNING-DESIGN.md + docs/design/ 8 张草图，等店主 T16 拍板**｜学法设计稿（只写方案和界面草图，不改产品代码）｜新建 docs/LEARNING-DESIGN.md：逐项对比 Duolingo（路线图、短步骤、即时反馈、连胜和每日目标）、HelloChinese / Super Chinese（汉字拆解、声调图示、拼音练习、填空和阅读）、LingoDeer（讲解卡片在前、语法小结），定下：① 一课的新流程（讲解卡 → 学词带图 → 小练习穿插 → 对话 → 总结）；② 新题型清单（见 T17）和每课 / 练习课 / 单元测验 / 阶段考试的题型配比；③ 课程地图和游戏化；④ 配图方案（见 T19，含费用）。用网页版做 3–5 张静态草图截图放 `docs/design/`｜验收：店主看过并在 T16 回复确认
- [ ] T16｜店主｜看 T15 设计稿并拍板｜重点决定（docs/LEARNING-DESIGN.md §8）：免费用户每天发音打分次数；要不要"心 / 生命值"（答错扣心，Duolingo 式，可能劝退）；配图用免费图标库还是付费 AI 插画（见 T19）；阶段考试不通过能不能跳过；另外在正式服务器填 `AZURE_SPEECH_KEY` / `AZURE_SPEECH_REGION`（发音打分要用）｜验收：在会话里说"按设计稿做"或提出修改
- [ ] T17｜开发｜等 T16｜引擎：新题型｜`packages/contract/src/schema.ts`（Exercise 加新类型）、`packages/contract/src/exercises.ts`、`packages/core/src/steps.ts`、`practice.ts`。新题型全部**由引擎用现有词条、对话、读物自动生成，不用重写课**：**口语优先**——跟读短语、跟读句子（按阶段限句长：A ≤ 约 8 音节、B ≤ 约 12）、角色扮演（用户演对话一方）、听后回答（B 起）；以及填空（对话 / 读物句子挖掉一个学过的词，四选一或从词块选）、排序组句（把句子拆成词块按顺序点）、配对（词和意思 / 读音 5 对连线）、认字（看字选读音、看读音选字，zh / ja / ko 都适用）、听音组句。每个题型带单元测试，core 的"用四门课全部真实内容生成每一课并核对答案"测试覆盖新题型｜验收：`npm run check` 通过
- [ ] T18｜开发｜等 T17｜App：上课流程和新题型界面｜`app/src/components/lesson/`（runner、steps、新题型组件）、`app/src/app/lesson/[id].tsx`、`content/l1/th/ui.json`。**先开口**：每个短语学完马上跟读（逐字颜色、星级、回放自己的声音、连击、鼓励语气，没过也能继续），课尾角色扮演，"现在不方便说话"跳过 15 分钟，没麦克风 / 没打分服务时录音回放自评；讲解拆成小卡放在用到的地方；每屏一个小步骤，小练习穿插在学词中间；答题即时反馈（对 / 错颜色、正确答案和一句解释、可选音效）；声调用图示（四声走势线，配泰语例字）；完成页显示本课学会的词。改了界面文字同步 e2e｜验收：`npm run check`、`npm run e2e` 通过，截图给店主看
- [ ] T19｜开发｜等 T16｜配图管线和 A 阶段配图｜schema 加可选的"概念"字段（同一意思跨语言共用一张图，如 zh 苹果 / en apple），母语层不受影响；`tools/` 加配图清单工具：列出能画的具体词（物品、食物、动作、地点、人物）和不配图的抽象词；图片放 `content/images/`，`npm run content` 打包，App 的学词和选择题显示图片，没图时不占位。先给 A 阶段配齐。默认用可商用的开源图标库（如 OpenMoji，署名写进关于页）；店主选付费 AI 插画时另开任务（要店主的图片生成密钥）｜验收：`npm run check`、`npm run e2e` 通过；A 阶段能配图的词覆盖率 ≥ 90%，`npm run validate` 检查图片文件都存在
- [ ] T20｜开发｜等 T17、T18｜App：路线图式课程地图和游戏化｜`app/src/app/index.tsx`、`app/src/lib/course-map.ts`：长列表改成一条弯曲路线上的圆形节点（正课、练习、读物、测验图标不同），每个单元一条主题横幅；每日目标（XP 目标可选）、连胜、单元完成奖励动画；心 / 生命值按 T16 决定做或不做。进度数据格式不变（不能让已有进度丢失）｜验收：`npm run check`、`npm run e2e` 通过（课程地图相关检查按新结构改写），手机宽度和深色模式截图给店主看
- [ ] T21｜开发｜等 T17｜考试型测验：单元测验和阶段考试｜`packages/core/src/practice.ts`、`path.ts`：单元测验改成"听力 + 认字 + 填空 + 排序 + 阅读"的组合卷；每个阶段末加一次阶段考试（类似 HSK / TOEIC 的题型分布，用该阶段学过的内容自动组卷，读物题直接复用），显示分项得分；通过线和能否跳过按 T16 决定｜验收：`npm run check`、`npm run e2e` 通过
- [ ] T22｜开发｜等 T17｜内容：A–B 阶段补讲解和阅读（A 阶段现在没有读物）｜按 docs/prompts/ 的流水线：A、B 阶段每课讲解改写成"一句结论 + 2 个例句 + 和泰语对比"，例句用本课已学的词；A 阶段每单元加 1 篇短读物（id 用新的 `-r` 号，不动已有课号）；中文加汉字部首 / 拆解小讲解，日语假名、韩语字母的认读讲解。两层一起改，新句子跑 `npm run audio` 补配音｜验收：`npm run validate`、`npm run dupes -- --meanings`、`npm run hours`、`npm run check` 通过，配音缺 0
- [ ] T23｜开发｜等 T18–T22｜全面回归和部署到正式服务器｜更新 e2e（新题型、新地图、考试各走一遍）、docs/TEST-REPORT.md；推送后等 GitHub 构建新镜像，店主更新正式服务器，AI 用 `npm run smoke -- <正式网址>` 检查｜验收：e2e 全部 PASS，smoke 全部 PASS
- [ ] T24｜店主｜在正式服务器上试用改造后的版本｜四门课各上 2–3 课、做一次单元测验，把觉得别扭的地方告诉开发；满意后再继续 T5（请母语老师审课，审的是改造后的内容）和上线流程

## 不做的事（第一版）

- LINE / Apple / Google 登录、排行榜、离线下载：方案里有，第一版不做，宣传时不能提。（模拟考 2026-11-12 改为做：T21 的阶段考试。）
- 大手术里不做：手写识别和笔顺描红、AI 生成付费插画（除非店主在 T16 选了）、好友 / 对战 / 排行榜、改课号和词条 id、重写已有课文（新题型由引擎从现有内容自动生成）。
- 刷新页面后正在上的课从头开始、静态目录提供点开头的文件：已定的产品取舍，先不改（docs/TEST-REPORT.md 第 6 节）。
- 新国家（越南等）和 G 阶段以后的内容：上线后再规划（docs/ROADMAP.md 阶段 5）。

## 已完成

- 2026-10-29｜配音：四门课 A–F 全部生成（39,567 段，`npm run audio -- --dry-run` 缺 0）。
- 2026-10-29｜部署：威联通 NAS 部署包（GHCR 镜像 amd64 + arm64、`deploy/qnap/`、`npm run smoke`、docs/DEPLOY-QNAP.md）。
- 2026-10-29｜服务器：失败不扣次数、按曼谷午夜重置、manifest 短缓存、卡片 due 校验、验证码计数存数据库、`ACCOUNTS_PER_IP_PER_HOUR`。
- 2026-10-29｜校验：同字不同音会共用配音时 `npm run validate` 报错；e2e 160/160。
- 更早的开发记录见 docs/HANDOVER.md 第 3 节和 git 历史。
