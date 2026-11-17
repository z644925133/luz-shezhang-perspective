# 实际使用检查结果（2026-11-18）

六个场景的旧版与增强版各产生一份回答，分别通过24/24项判据。**本轮没有观察到通过率提高**；出处题的可用第三方ASR定位从0条增为2条，两版都诚实区分了摘要、转写定位和原声确认。

| 比较项 | 旧版 | 增强版 |
|---|---:|---:|
| 场景数 / 回答数 | 6 / 6 | 6 / 6 |
| 逐项判据通过 | 24/24 | 24/24 |
| 出处题有效第三方ASR定位 | 0 | 2 |
| 本轮回听确认 | 0 | 0 |

新增定位均属于视频`YKXvrIxWrn0`的模型12相关片段：00:07.800–00:20.200、22:46.360–22:54.360；不是模型11时码。毫秒数来自第三方ASR分段，不代表人工精度；详见[模型证据索引](../references/MODEL_EVIDENCE_INDEX.md)。旧版诚实承认缺少时码，不因此扣分。

## 逐题原始回答与执行记录

题目和判据见[evals.json](evals.json)，完整评分、证据与回答哈希见[results.json](results.json)。下表分数链接实际回答；最后一列链接实际读取日志。

| 场景 | 旧版 | 增强版 | 读取日志 |
|---|---:|---:|---|
| 1：competing-causes | [4/4](runs/old/01-competing-causes.md) | [4/4](runs/enhanced/01-competing-causes.md) | [旧](runs/old/01-competing-causes-read-log.md) / [增强](runs/enhanced/01-competing-causes-read-log.md) |
| 2：offline-current-facts | [4/4](runs/old/02-offline-current-facts.md) | [4/4](runs/enhanced/02-offline-current-facts.md) | [旧](runs/old/02-offline-current-facts-read-log.md) / [增强](runs/enhanced/02-offline-current-facts-read-log.md) |
| 3：evidence-locators | [4/4](runs/old/03-evidence-locators.md) | [4/4](runs/enhanced/03-evidence-locators.md) | [旧](runs/old/03-evidence-locators-read-log.md) / [增强](runs/enhanced/03-evidence-locators-read-log.md) |
| 4：entity-identity-boundary | [4/4](runs/old/04-entity-identity-boundary.md) | [4/4](runs/enhanced/04-entity-identity-boundary.md) | [旧](runs/old/04-entity-identity-boundary-read-log.md) / [增强](runs/enhanced/04-entity-identity-boundary-read-log.md) |
| 5：restricted-and-endorsement | [4/4](runs/old/05-restricted-and-endorsement.md) | [4/4](runs/enhanced/05-restricted-and-endorsement.md) | [旧](runs/old/05-restricted-and-endorsement-read-log.md) / [增强](runs/enhanced/05-restricted-and-endorsement-read-log.md) |
| 6：counterexample-and-revision | [4/4](runs/old/06-counterexample-and-revision.md) | [4/4](runs/enhanced/06-counterexample-and-revision.md) | [旧](runs/old/06-counterexample-and-revision-read-log.md) / [增强](runs/enhanced/06-counterexample-and-revision-read-log.md) |

## 怎样执行与评分

旧版冻结于提交[`ee78df9`](https://github.com/z644925133/luz-shezhang-perspective/tree/ee78df9b058dc90e5f1dc287316aa333312b20f8)。增强版运行时文件哈希保存在`results.json`，与本次发布核对一致。运行记录日期来自答题环境（2026-11-17）；整理与发布于2026-11-18，时区Asia/Singapore。

两个新代理分别读取各自版本及同一组prompt，未获expected_output或评分表；每臂由同一代理批答六题，禁网，无账号或Git写操作。独立代理读取匿名A/B回答、日志、判据与参考事实后评分。逐题映射为：奇数题A=增强/B=旧，偶数题A=旧/B=增强；映射评分后公开。

评分未发现编造回听、缺失proof来源或已证师承/政治关系。此结论限于所提供回答、日志与参考事实的一致性；不等于独立系统审计或现实人物事实复核。维护者另核对了全部26条摘要映射、两段ASR源行、原模型正文及第三方许可。

## 局限与文件处理

- 开发期已知的六题，不是独立留出集；每臂一名新代理在同一上下文批答六题，没有逐题独立会话或重复运行。
- 同一宿主模型的旧版/增强版比较；未设置不加载skill的裸答臂。具体模型标识、耗时和token接口未提供，均记unknown/null。
- 独立代理按匿名A/B逐项评审，未获版本映射；附件路径仍可能泄露版本，不能称完全盲评。
- 评分检查题设事实、可核摘要/定位和执行边界；执行记录只做一致性审阅，没有独立系统级追踪。
- 两版均24/24通过，没有通过率提高的证据；二元判据区分力有限。唯一量化的材料差异是出处题有效第三方ASR定位0条对2条。
- 未回听原声、未验证现实政治预测、未测本人观点一致性、未证明跨宿主泛化或长期稳定性。
- 公开回答只规范化Markdown链接目标；文字、结论不改。读取日志原样保留，snapshot名称是历史执行目录标签。

原始答案与日志未作措辞润色。为在GitHub点击，回答中的本地快照链接改为旧版固定提交或增强版相对路径，并将`:行号`改为`#L行号`；旧/新答案哈希记录此转换。日志保留历史目录标签；`actor-prompts.json`内容即公开题表的id/name/prompt，不含预期结果。执行耗时、token和具体模型标识未知，不填零或推测值。

后续应增加未参与开发的留出题、逐题独立会话和重复运行，再讨论是否提高分析质量。本轮只支持出处可查性增加及这六题的边界遵守。
