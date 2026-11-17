# DELTA · luz-shezhang-perspective Batch3

- 时间：2026-11-01（Asia/Singapore）
- 范围：仅改 workspace 源 `/workspace/skills/luz-shezhang-perspective/`（**未**改 UpdateSkill 已写入的 workflows 文件；主 agent 再 sync）
- 语料增量：Batch3 本地 ASR **10** 条（见 `batch3.json` / `distill/BATCH3_DIGEST.md`）

## 实质升级

1. **新心智模型**
   - **模型9 文宣/春晚流量阀**：国家级晚会/主平台=流量与合法性阀门；飞轮钉阀则关闸优先。
   - **模型10 宗教统战管道**：自己人标签决定护短/激活原罪；靠山常是整套宗教管理系统。
2. **加固**
   - 模型3/5：张高丽人设崩塌仪式；赵薇/黄有龙大哥链断裂的杠杆人生。
   - 启发式 +15–17（文宣阀门、宗教自己人标签、错派早站队窗口）。
3. **研究协议** Step2 增 H/I 维。
4. **METHOD_SEEDS** 增 §16–19；索引挂上 B3-1…B3-10。

## 未改 / 刻意不动

- `/home/box/agent-data/workflows/skill-1793511422907` — 留给主 agent sync。
- 未改 workflows；未把 Batch3 人事叙述升格为已证史实。

## 文件清单

| 路径 | 动作 |
|---|---|
| `SKILL.md` | 模型9/10 + 启发式 + 研究维 H/I |
| `DELTA_batch3.md` | 本说明 |
| `references/sources/transcripts/*` | +10 raw/srt |
| `references/sources/articles/*` | +10 meta json + BATCH3_DIGEST + 更新 METHOD_SEEDS |
| `/workspace/yt-channel-asr/.../distill/BATCH3_DIGEST.md` | 新建 |
| `/workspace/yt-channel-asr/.../distill/METHOD_SEEDS.md` | 扩写 §16–19 |
| `batch3.json` / `run_batch3_asr.log` / `progress.json` | 进度与清单 |
