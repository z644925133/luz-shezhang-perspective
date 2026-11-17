# 政经鲁社长 · 思维操作系统（luz-shezhang-perspective）

> Agent skill：把 YouTube 频道 **@zrzjpl（政经鲁社长）** 的口播复盘，蒸馏成可复用的**政经分析框架**（不是情报库、不是金句复读机）。

**全量状态**：公开可下 ASR **172** 成功 / **1** 年龄墙失败；Stream1–7 **8/8**、Stream8 **5/5**、Shorts **20/20** 均已蒸馏。模型仍为 **1–13**（METHOD 至 §327；模型 14 未开）。  
**调研/蒸馏时区**：Asia/Singapore（UTC+8）。  
**创作路径**：女娲方法论 + 本机 faster-whisper ASR；**非**频道本人授权背书。

---

## 一句话介绍

用鲁社长反复出现的「坐标系」看人事、政商与叙事：先问**谁的眼睛在打分**，再拆弹药库、分期清算、政策潮汐与陪伴权——框架硬、情报软。

## 触发词

- 「用鲁社长视角」「鲁社长会怎么看」「政经鲁社长模式」
- 「luz shezhang perspective」「切换到鲁社长」

一般闲聊不自动触发。退出：「退出」「切回正常」。

## 安装 / 使用（Agent）

1. 将本仓库（或 `SKILL.md`）安装为 agent skill，名称：`luz-shezhang-perspective`。
2. 用户说出触发词后，**直接以鲁社长第一人称**回答（见 `SKILL.md` 角色扮演规则）。
3. 需要事实的问题：先 WebSearch/公开源核实，再套模型；禁止把口播叙述当已证史实。
4. 小说/政斗写作：优先用「【小说可复用】」级母题（见 digests / METHOD_SEEDS），勿照搬具体人事断言。

本地开发路径：

```text
/workspace/skills/luz-shezhang-perspective/SKILL.md
```

已注册 workflows 副本：`skill-1793511422907`

---

## 心智模型地图（1–13）

| # | 模型 | 一句话 | 主要证据批次 |
|---|------|--------|--------------|
| 1 | 话事人坐标系 | 先找最高话事人 KPI 与评委团；民间声望常错位 | Top10 / METHOD |
| 2 | 嫡系保质期与祭旗对称 | 亲信有时间戳；运动公信力常要对称祭旗 | Top / B2 |
| 3 | 必杀局与引爆点分离 | 公开爆点多是导火索；必杀靠多源弹药库 | Top |
| 4 | 派系拆解分期付款 | 先脏后净、分期切割知情责任 | Top / B5 |
| 5 | 白手套与政策潮汐 | 成也潮汐败也潮汐；靠山必须迭代 | Top / B2 |
| 6 | 食利型 vs 进化型资本 | 纯关系套利绑定周期；机构化才可能穿越 | Top |
| 7 | 元老管道断流 | 定一尊后断干政管道往往大于断肉体 | B2 |
| 8 | 饭局电压表 | 高压期酒桌可从感情翻转为自毁证据 | B2 |
| 9 | 文宣/春晚流量阀 | 国家级阀门一关，飞轮比账面更脆 | B3 |
| 10 | 宗教统战管道 | 「自己人」标签决定护短或激活旧罪 | B3 |
| 11 | 陪伴权坐标系 | 被需要沟通 > 虚衔；岗位陪伴 ≠ 宠臣陪伴 | B4 |
| 12 | 跳级生诅咒与消藩深度轴 | 无铁信任的突击座位是诅咒；夺权后向下消藩 | B4 / B5 |
| 13 | 接班人废约与布局三阶段 | 旧约三前提拆除后，储君赛改陪伴权+履历火箭 | B5 |

更细的启发式、研究协议与表达 DNA：见 `SKILL.md`。横切方法种子：`METHOD_SEEDS.md`（至 §327）。

---

## 证据批次

| 批次 | 内容 | Digest |
|------|------|--------|
| Top10 | 热度 Top 长片 | `references/sources/articles/TOP10_DIGEST.md` |
| Batch2–5 | 长片批次 | `references/sources/articles/BATCH2`…`BATCH5_DIGEST.md` |
| Batch6–8 | 长片批次 | 仓库根目录 `BATCH6`…`BATCH8_DIGEST.md` |
| Stream1–7 | 直播回放各 8 条（框架优先） | `BATCH_STREAM1`…`7_DIGEST.md`（均 **8/8**） |
| Stream8 | 剩余直播 5 条 | `BATCH_STREAM8_DIGEST.md`（**5/5**） |
| Shorts | 短视频框架簇 | `BATCH_SHORTS_DIGEST.md`（**20/20**） |

语料管线：本轮实际是 `yt-dlp` bestaudio → `faster-whisper`（zh, small/int8）→ 蒸馏 → skill（不是字幕优先）。

---

## 全量进度（收口）

| 项 | 数值 |
|----|------|
| 公开可列目标 | ≈ **173** |
| ASR done | **172** |
| ASR failed | **1**（`b64ekVis8ZE` 年龄墙） |
| pending | **0** |
| Digests | Stream1–7 8/8；Stream8 5/5；Shorts 20/20 |
| METHOD | §1–§327 |
| 模型 | **1–13**（14 未开） |
| 本表刷新 | **2026-11-17 Asia/Singapore**（文档债补记；语料收口仍为 2026-11-09） |

详见 `LOCKED_OR_FAILED.md`。

---

## 诚实边界（必读）

1. **公开口播 ≠ 已证史实**。具体人事、动机、数字 =「鲁社长叙述/推断」；Skill 学的是分析框架，不是情报库。
2. **无系统著作**可作页码精引；口述存在事后解释偏见。
3. **ASR 错字多**，禁止把字幕当精确语录（除非另有核对）。
4. **不能预测密室投票**；只能演示坐标系提问法。
5. 外部评价两极（高 credit vs 听床/外宣）**未裁决**，并列保留。
6. **非本人授权**；创作路径为粉丝向蒸馏，用于写作/分析练习。
7. 会员锁定内容不在本仓库语料内。

---

## 仓库建议布局（发布时）

```text
luz-shezhang-perspective/
  README.md                 ← 可由本文件改名/裁剪
  SKILL.md
  SUMMARY_FOR_GITHUB.md
  METHOD_SEEDS.md
  LOCKED_OR_FAILED.md
  BATCH*_DIGEST.md / BATCH_STREAM*_DIGEST.md / BATCH_SHORTS_DIGEST.md
  DELTA*.md
  references/research/      ← 调研笔记
  references/sources/       ← 可选 meta；raw 字幕体积大可不进 git
```

**隐私/体积**：完整 `.raw.txt` / `.srt` 建议 LFS 或不入库，仅保留 digests + METHOD_SEEDS + SKILL。

---

## 待办（GitHub）

- [x] 公开队列 ASR+蒸馏完成（videos → streams → shorts）
- [x] 更新 workspace `SKILL.md` / METHOD / digests
- [x] UpdateSkill 同步 workflows（主 agent）
- [x] 定稿 SUMMARY 状态栏
- [ ] **推送 GitHub**（需用户建空仓库后授权推送；Cursor 不能代建 GitHub 仓库）

建议仓库名：`luz-shezhang-perspective`（账号 `z644925133`）。建好空仓后把 URL 发我即可推。

---

## 许可证 / 署名建议

- 框架归纳：贡献者自拟（注明蒸馏自公开口播）。
- 勿暗示 @zrzjpl 官方背书。
- 转载具体节目观点请回链原视频；本 skill 不替代原片。
