# AMMO_SCAN · 服务「鲁社长顾问 / 知识库 / 小说高维视角」的 skill & 项目

- 调研日：2026-11-01（Asia/Singapore）
- 需求画像：口播政经蒸馏 → 可调用思维顾问 + KB；可服务小说权力/派系；本机已有 yt-dlp+faster-whisper ASR 与女娲生成的 `luz-shezhang-perspective`
- 来源：WebSearch + GitHub `search_repositories` + 项目 README/PyPI（**排除**知乎/微信公众号作论据）
- 筛选原则：真正可装可跑 > 星标；空壳/纯镜像降权

---

## 强烈建议（最多 3）

### 1. `michalstrnadel/source-to-skill` — **强烈建议装**
- **是什么**：把 YouTube 视频/频道、播客 RSS、本地录音、论文/书/笔记蒸馏成 Agent Skill（`SKILL.md` + 按需 segment 文件 + 时间戳深链）；本地 Whisper（faster-whisper / mlx-whisper），无云端 ASR API。PyPI `source-to-skill==0.7.0`，`npx skills add michalstrnadel/source-to-skill`。
- **为何贴需求**：与现有「频道 ASR 语料」同构；可把已转写或新片批量升级为**可引用时间戳的顾问 skill**；频道 `--limit N`、playlist→course、多源 topic skill + `disagreements.md` 很适合政经口播母题沉淀。
- **局限**：GH 星标仍低（镜像/fork 多）；蒸馏阶段仍消耗本机 agent token；默认频道只取最新 N 条，长频道要分批；不替代「人物心智模型」级女娲蒸馏，偏「课程/语料 skill」。
- **建议**：装。用作鲁社长语料的**第二流水线**（结构索引+时间戳），与现有 `luz-shezhang-perspective` 互补，不互相覆盖。
- **链接**：https://github.com/michalstrnadel/source-to-skill · https://pypi.org/project/source-to-skill/

### 2. `alchaincyf/darwin-skill` — **强烈建议装**
- **是什么**：女娲生态配套——对已有 Skill 做 Evaluate→Improve→Test→Keep/Revert 棘轮优化（autoresearch 风格）；`npx skills add alchaincyf/darwin-skill`。
- **为何贴需求**：鲁社长 skill 已有 v1；batch2 语料增量后最怕「手改漂移 / 模型糊」。达尔文可对 `luz-shezhang-perspective` 做可回滚的质量进化与回归评测。
- **局限**：优化循环会烧 agent 额度；需 git 管理 skill 目录才能干净 keep/revert；不产 KB、不产 ASR。
- **建议**：装。在 METHOD/BATCH2 合并后跑一轮「优化鲁社长 skill」，对照保留 DELTA。
- **链接**：https://github.com/alchaincyf/darwin-skill

### 3. `irahulstomar/brain-mcp` — **强烈建议装（KB 缺口）**
- **是什么**：本地 Markdown/Obsidian 第二脑 MCP：Ollama 嵌入 + Chroma + SQLite FTS，hybrid_search / read/write note；无云、无 API key。
- **为何贴需求**：当前缺口是「转写堆在 `transcripts/`，顾问 skill 只吃蒸馏摘要」。把 `*.raw.txt` / distill md 挂进 vault → 顾问可按需检索原片证据，服务小说设定核对与框架溯源。
- **局限**：依赖本机 Ollama + 嵌入模型；中文分词/嵌入质量需实测；不是「人物视角」skill，是检索层。
- **建议**：装并指向 `/workspace/yt-channel-asr/data/channels/zrzjpl/{transcripts,distill}`（或导出为 markdown vault）。备选同型：`bernabranco/claude-code-vault`（本地 transformers+sqlite-vec，无 Ollama）。
- **链接**：https://github.com/irahulstomar/brain-mcp · 备选 https://github.com/bernabranco/claude-code-vault

---

## 其他候选（一行级）

| 候选 | 是什么 | 贴合点 | 局限 | 建议 | 链接 |
|------|--------|--------|------|------|------|
| `nuwa-skills/awesome-nuwa` | 女娲蒸馏人物 skill 目录（159+） | 对照生态、找权力/战略视角 | 本身是列表不是顾问 | **只读对照，不必整仓装** | https://github.com/nuwa-skills/awesome-nuwa |
| `alchaincyf/nuwa-skill` | 女娲造人术本体 | 已装并产出鲁社长 | 重复装无增益 | 已有，跳过 | https://github.com/alchaincyf/nuwa-skill |
| `nuwa-skills/darwin-skill` | 达尔文**思维**人物 skill（进化论视角） | 易与 alchaincyf/darwin-skill **混淆** | 不是 skill 优化器 | 不装（除非要进化论顾问） | https://github.com/nuwa-skills/darwin-skill |
| `nuwa-skills/hanfeizi-skill` | 法术势 / 参验 / 制度优先 | 小说组织治理、赏罚可信、反腐流于形式 | 古典法家≠当代政经口播；星标低 | **可选装**：与鲁社长对照「制度 vs 话事人」 | https://github.com/nuwa-skills/hanfeizi-skill |
| `nuwa-skills/machiavelli-skill` | 君主论现实主义 / virtu-fortuna | 派系站队、残酷一次做完、权力动态 | 西方宫廷隐喻，需与鲁坐标翻译 | **可选装**：小说权力副顾问 | https://github.com/nuwa-skills/machiavelli-skill |
| `nuwa-skills/foucault-skill` | 权力/知识/话语 | 治理对象化、祭品叙事的理论层 | 偏学术话语，落地口播弱 | 可缓装 | https://github.com/nuwa-skills/foucault-skill |
| `nuwa-skills/guiguzi-skill` | 纵横/说服/博弈 | 说客线、联盟话术 | 与鲁社长「评委团」部分重叠 | 低优先 | https://github.com/nuwa-skills/guiguzi-skill |
| `nuwa-skills/clausewitz-skill` | 摩擦/迷雾/重心 | 政斗「必杀局」、备战反腐隐喻 | 军事理论外推需克制 | 可选，小说战备线 | https://github.com/nuwa-skills/clausewitz-skill |
| `nuwa-skills/caocao-skill` / `liubang-skill` | 用人与乱世权谋 | 群像派系小说 | 史传蒸馏，非当代政经 | 低优先 | awesome-nuwa 军事类 |
| `leezythu/maoxuan-skill` | 矛盾论/持久战/统一战线等 | 战略分层、主要矛盾；社区星标高 | 方法论≠鲁社长政经坐标；政治敏感表述需自控 | 可选对照，非替代鲁 | https://github.com/leezythu/maoxuan-skill |
| `legendtkl/youtube-channel-distill` | 频道→progressive-disclosure Claude skill 元技能 | 与现流水线几乎同目标（list→caption/ASR→fan-out distill） | 公开页星标近 0；ASR 偏远程兼容端点 | **观望**：概念贴，成熟度不如 source-to-skill+自研管线 | https://github.com/legendtkl/youtube-channel-distill |
| `koren-source/skillforge` | CLI：YT 字幕→按创作者归档 skill + recall | 轻量「按人建库」 | 依赖字幕；与自研 ASR 重叠 | 可作 recall UX 参考，非必须 | https://github.com/koren-source/skillforge |
| `openpodhq/openpod` | 本地播客捕捉：转写+briefing+语义检索+MCP/skills | 口播库本地化合 | 偏播客产品形态；GH 检索易撞名 OpenPods | 若改吃 RSS/会员播客再评 | https://github.com/openpodhq/openpod |
| `bradleesand/query-my-pod` | RSS→Whisper→SQLite 向量→Ollama RAG | 可跑的播客 KB | 星标极低；Ruby 栈重 | 不优先（brain-mcp 更贴 md 语料） | https://github.com/bradleesand/query-my-pod |
| `janvrsinsky/jv-podcast-rag` / The Librarian | hybrid BM25+dense、分钟级引用、离线 eval | 检索评测意识好 | 案例型仓库，非通用安装器 | 借鉴 eval，不整装 | https://github.com/janvrsinsky/jv-podcast-rag |
| `catlabs/podcast-parser` | Whisper+Chroma+多 LLM 聊天 UI | 学习型完整 RAG | 组合重，运维成本高 | 不优先 | 搜索名 Podcast RAG / catlabs |
| `dasportillo/brain-rag` | Claude/Codex 会话记忆 MCP | 决策记忆 | **会话**第二脑，非口播语料 | 不贴主需求 | https://github.com/dasportillo/brain-rag |
| `thetenzinwoser/recall-mcp` | md+会议转写+Claude session 语义检索 | 本地 MCP | 源类型偏会议/会话 | 次选 | https://github.com/thetenzinwoser/recall-mcp |
| `patrick-elmore/second-brain` | FTS5 + HTTP MCP + `/brain` skill | 笔记检索 | Windows 安装脚本痕迹；非 ASR | 次选 | https://github.com/patrick-elmore/second-brain |
| colleague-skill 系（多 fork） | 「蒸馏同事」爆款原型 | 女娲叙事起源 | 大量空壳/镜像；与已装女娲重复 | **不装** | 避免 titanwings 等营销站当论据 |
| `titanwings/distilly` 等 | 蒸馏产品站/聚合 | 市场热度信号 | 非本地可复现管线 | 不当弹药 | — |

---

## 与现有栈的拼装建议（不自动执行）

```
[已有] yt-channel-asr (audio→whisper→transcripts)
    → [建议] source-to-skill 生成带时间戳的课程/语料 skill
    → [已有] 女娲/luz-shezhang-perspective（心智模型顾问）
    → [建议] darwin-skill 棘轮升级 luz
    → [建议] brain-mcp 索引 transcripts+distill 作证据层
可选副顾问：hanfeizi / machiavelli（小说权力对照，勿混为情报源）
```

## 扫描失败 / 未核实项

- GitHub `repo:a OR repo:b…` 超 5 运算符一次查询被 422 拒绝 → 已拆查询；部分仓库星标以单次 search 为准，可能滞后。
- `nuwa-skills/*` 多数人物 skill 星标显示个位数（生态新），以 awesome-nuwa 可安装性为准而非星标。
- 未实际 `npx skills add` / 未跑 brain-mcp 索引（本回合只扫描评价，不擅自改用户全局 skills，除已约定的 workspace 源更新）。
- TubeAlfred 按任务禁止用于字幕烧点；未使用。

