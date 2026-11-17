# INSTALL_AMMO — 弹药栈安装笔记

> 落地时间：2026-11-01（Asia/Singapore, box 本地钟）  
> 约束：不烧 TubeAlfred；未对 `luz-shezhang-perspective` 正文做 darwin 长优化。

## 总览

| 组件 | 路径 | 状态 |
|------|------|------|
| source-to-skill | `/workspace/skills/source-to-skill` | ✅ 克隆 + venv CLI；skills 已装到 `~/.agents/skills` / `~/.cursor/skills` |
| darwin-skill | `/workspace/skills/darwin-skill` | ✅ 克隆；副本在 `~/.agents/skills/darwin-skill` |
| brain-mcp | `/workspace/skills/brain-mcp` | ✅ 克隆 + venv；索引完成；冒烟搜到「话事人」「白手套」 |
| Ollama | `/usr/local/bin/ollama` | ✅ 手动解压安装（apt/zstd 不可用）；`nomic-embed-text` 已 pull |
| brain vault | `/workspace/skills/brain-vault` | ✅ distill/*.md + 32 条 transcript `.md`（从 raw.txt 转换） |

---

## 1) michalstrnadel/source-to-skill

### 路径
- 源码：`/workspace/skills/source-to-skill`
- 可复用 symlink：`/workspace/skills/registered/source-to-skill` → `.../skills/source-to-skill`
- Agent skills 副本：
  - `/home/box/.agents/skills/source-to-skill`（及 skill-study / skill-eval / skill-library）
  - `/home/box/.cursor/skills/source-to-skill`（同上）
- CLI venv：`/workspace/skills/source-to-skill/.venv/bin/source-to-skill`
- UpdateSkill 载荷：`/workspace/skills/luz-shezhang-perspective/_register_payloads/source-to-skill.SKILL.md`
- 已尝试写入 workflows：`/home/box/sand-data/workflows/source-to-skill/SKILL.md`（**父代理仍需 UpdateSkill 正式入库**）

### 触发 / CLI
```bash
# 版本与帮助
/workspace/skills/source-to-skill/.venv/bin/source-to-skill --version
/workspace/skills/source-to-skill/.venv/bin/source-to-skill check

# 抽取（确定性 extractor；蒸馏由 agent 按 SKILL 做）
/workspace/skills/source-to-skill/.venv/bin/source-to-skill extract "<url-or-file>"

# 校验已有 skill 目录
/workspace/skills/source-to-skill/.venv/bin/source-to-skill validate /workspace/skills/luz-shezhang-perspective

# 对话触发（注册后）：/source-to-skill <url> 或「把这个视频/论文做成 skill」
```

### 冒烟
- `source-to-skill check`：yt-dlp ✅、PyMuPDF ✅、Whisper ❌（未装 faster-whisper / mlx-whisper；无字幕 YouTube 仍可用）
- `validate /workspace/skills/luz-shezhang-perspective` → `OK: skill is valid`

### 缺口
- **UpdateSkill 对本 executor 不可用**（cursor 命名空间无此工具）→ 需父代理 `UpdateSkill write` 用 `_register_payloads/source-to-skill.SKILL.md`
- Whisper 可选：`/workspace/skills/source-to-skill/.venv/bin/pip install faster-whisper`（体积大，未装）

---

## 2) alchaincyf/darwin-skill

### 路径
- 源码：`/workspace/skills/darwin-skill`
- symlink：`/workspace/skills/registered/darwin-skill`
- 副本：`/home/box/.agents/skills/darwin-skill`、`/home/box/.cursor/skills/darwin-skill`
- UpdateSkill 载荷：`_register_payloads/darwin-skill.SKILL.md`
- workflows 草稿：`/home/box/sand-data/workflows/darwin-skill/SKILL.md`

### 如何对鲁社长 skill 跑一轮优化（**不要自动开跑**）
口头触发（Skill 注册后）：
- 「用达尔文优化 luz-shezhang-perspective」
- 「优化 `/workspace/skills/luz-shezhang-perspective/`」
- 「skill评分 luz-shezhang-perspective」

操作注意（README）：
1. 目标目录最好在 git 仓库内；先 commit/stash 本地改动。
2. 每轮有人机 checkpoint；失败用 `git revert` 而非 `reset --hard`。
3. 本安装**只验证可调用/可加载**，**未**对鲁社长正文跑长优化。

### 冒烟
- `SKILL.md` frontmatter 可解析；helpers（`references/` `scripts/` `templates/` `test-prompts.json`）在位。
- 未跑 Phase1+ 评估循环（按主人约束）。

### 缺口
- 同需父代理 **UpdateSkill** 正式注册。

---

## 3) irahulstomar/brain-mcp

### 路径
- 源码：`/workspace/skills/brain-mcp`
- venv：`/workspace/skills/brain-mcp/.venv`
- 数据：`BRAIN_HOME=/home/box/.brain`（config / chroma / sqlite）
- Vault：`/workspace/skills/brain-vault`
  - `distill/` ← 复制自 `/workspace/yt-channel-asr/data/channels/zrzjpl/distill/*.md`
  - `transcripts/*.md` ← 由同目录 `*.raw.txt` 转换（brain 只扫 `.md`）
- 本地 MCP 配置：
  - `/home/box/.cursor/mcp.json`（`brain_cli.py mcp --client cursor` 已写入）
  - `/workspace/skills/brain-mcp/mcp.local.json`（带 BRAIN_VAULT env）

### Ollama
- 二进制：`/usr/local/bin/ollama`（从 GitHub `ollama-linux-amd64.tgz` 解压；install.sh 因缺 zstd + apt 镜像失败）
- lib：`/usr/local/lib/ollama`
- 模型：`nomic-embed-text:latest`（274 MB）
- 重启：`/workspace/skills/brain-mcp/start-ollama.sh`
- 当前会话已 `ollama serve` 在跑；**重启 box 后需再起 serve**

### 索引状态（冒烟时）
```json
{"vault":"/workspace/skills/brain-vault","indexed_files":36,"indexed_chunks":316,"chroma_vectors":316}  # post-Batch3 2026-11-01
```

### 触发（MCP / CLI）
父代理需 **AddMcpServer**（本 executor 无此工具）。建议参数：
```
command: /workspace/skills/brain-mcp/.venv/bin/python
args:    ["/workspace/skills/brain-mcp/brain_cli.py", "serve"]
env:     OLLAMA_KEEP_ALIVE=-1
         BRAIN_VAULT=/workspace/skills/brain-vault
         BRAIN_HOME=/home/box/.brain
```
MCP 工具：`hybrid_search_tool`（主）、`keyword_search_tool`、`semantic_search_tool`、`reindex_tool` 等。

离线冒烟（不经 MCP）：
```bash
/workspace/skills/brain-mcp/start-ollama.sh
/workspace/skills/brain-mcp/.venv/bin/python /workspace/skills/brain-mcp/smoke_search.py '话事人'
/workspace/skills/brain-mcp/.venv/bin/python /workspace/skills/brain-mcp/smoke_search.py '白手套'
# 或
/workspace/skills/brain-mcp/.venv/bin/python /workspace/skills/brain-mcp/brain_cli.py index
/workspace/skills/brain-mcp/.venv/bin/python /workspace/skills/brain-mcp/brain_cli.py status
```

### 冒烟结果
| 查询 | hybrid hits | keyword hits | 代表路径 |
|------|-------------|--------------|----------|
| 话事人 | 5 | 0（FTS 对中文弱） | `distill/METHOD_SEEDS.md`（「话事人坐标系」） |
| 白手套 | 5 | 1 | `distill/BATCH2_DIGEST.md` |

→ **SMOKE_OK**（语义检索命中；未假装未索引）

### 缺口 / 阻塞
- **Grok Bot 运行时 MCP**：需父代理 `AddMcpServer`；仅写 `~/.cursor/mcp.json` 不一定进入本 bot 的动态工具目录。
- box 重启后要：`start-ollama.sh` + 确认 `brain` MCP 进程。
- 语料更新后：重新转写 md（或改 vault 结构）再 `brain_cli.py index`。
- apt 不可用 → 未装系统 `zstd`；Ollama 走手动 tarball。

---

## 父代理待办（协议工具仅主会话有）

1. `UpdateSkill` action=write  
   - name=`source-to-skill`，body= `_register_payloads/source-to-skill.SKILL.md`（去 frontmatter 后的 body + description 字段）  
   - name=`darwin-skill`，同上用 darwin 载荷  
2. `AddMcpServer`：按上文 brain command/args/env  
3. 确认后可用 Skill / MCP 冒烟各一次；**仍不要**自动开 darwin 长优化。

## 明确未做
- TubeAlfred 调用：无  
- 对 `luz-shezhang-perspective` SKILL 正文的 darwin 改写：无  
- faster-whisper 安装：无  
