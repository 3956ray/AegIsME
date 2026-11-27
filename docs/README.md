# AegisME 文档索引

本目录整理 MetaEarth Hackathon 2026: HARBOR 筹备期间的讨论、方案、路演稿与评审记录，供写入 [3956ray/AegIsME](https://github.com/3956ray/AegIsME) 的 `docs/`。

**项目现名是 AegisME**（原名 AgentGuard）。计划中的合约名为 `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`。早期讨论与画布里仍使用 AgentGuard / `AgentPolicy` / `AgentCredit`，历史正文保留原名，不以新名称 silently 改写接口草图。

时区以 Asia/Shanghai（UTC+8）为准。提交材料须为英文；本目录采用中英对照。

**本仓库为公开仓库。** 内部评委规划分已从所有文档中删除。对外不得宣称 ERC-8498 共同作者身份，也不得把「市场空白」写成既成事实。

文档来源：团队画布（已转为 Markdown，去掉交互控件）、Gemini CLI 对抗评审、以及用户在 Gemini 网页版中的讨论记录。这些文件只在沙盒中生成，**没有克隆仓库，也没有推送**。

## 当前方案（以这些为准）

| 文档 | 说明 |
| --- | --- |
| [plan/full-merge-execution-plan.md](plan/full-merge-execution-plan.md) | 完全合并执行方案：三合约、「循环额度 + 一次性借款券」、Demo 9 步、开发排期与 12-07 检查点；文末附 11-27 已被取代的旧评估。 |
| [product/product-direction-v4.md](product/product-direction-v4.md) | 产品方向报告 v4（完全合并）：MVP 范围、接口草图、真实/模拟清单、两级退路、ME ID 约束与答辩准备。 |
| [pitch/pitch-and-demo-narration.md](pitch/pitch-and-demo-narration.md) | 英文路演 10 页、Demo 9 步旁白（约 390 词 / 3:23）、提交用项目简介、答辩问答与禁讲清单。 |
| [reviews/decisions-log.md](reviews/decisions-log.md) | 决策日志：用户拍板完全合并；Gemini 评审中采纳与驳回的条目。 |

## 评审与外部讨论

| 文档 | 说明 |
| --- | --- |
| [reviews/gemini-round-1-2026-11-27.md](reviews/gemini-round-1-2026-11-27.md) | 2026-11-27 23:59（Asia/Shanghai）Gemini CLI 第一轮对抗评审：提示词（已脱敏）与回复（内部评分数字已删）。 |
| [reviews/gemini-web-chat-harbor.md](reviews/gemini-web-chat-harbor.md) | 用户在 Gemini 网页版的「HARBOR 黑客松 AI 与链上金融创意策划」对话整理（轻度清理）。其中首次将项目定名为 AegisME；架构草稿与当前执行方案并不完全一致，以 `plan/` 为准。 |

## 调研（结论已被主方案吸收，正文保留备查）

| 文档 | 说明 |
| --- | --- |
| [research/market-scan.md](research/market-scan.md) | 第一轮市场扫描：赛制、近 3 个月趋势、标杆拆解、痛点与 7 个机会点（内部打分已删；当时推荐优先做 AgentGuard 与 ME ID 信用额度）。 |
| [research/fact-check-erc8498.md](research/fact-check-erc8498.md) | ERC-8498 方案核实：讨论帖、PR、参考实现、ME Network 可行性与风险。 |
| [research/market-counterexamples.md](research/market-counterexamples.md) | 行业事实核查与反例：10 条声明核对；「普通用户低抵押信用仍是空白」仅为部分成立。 |

## 已归档（已被完全合并方案取代）

| 文档 | 说明 |
| --- | --- |
| [archive/erc8498-standalone-scoring.md](archive/erc8498-standalone-scoring.md) | **已归档。** 曾把 ERC-8498 动态信用当作独立新产品评估；用户已决定并入 AegisME，本页定位不再使用。内部分数已删。 |
| [archive/standalone-positioning.md](archive/standalone-positioning.md) | **已归档。** 独立新产品的差异化定位草案（Earn it / Lose it / Spend it once 最初用于独立信用产品）。部分口号被主方案吸收为信用模块小标题。 |

`plan/full-merge-execution-plan.md` 文末的「11-27 旧评估」同样是归档内容（当时建议轻度结合，用户选择了完全合并）。

## 未纳入本目录的内容

- 与 HARBOR 无关的画布：月入约 3000 美元调研、市場機會研究 MAR-1、團隊知識庫与 Agent 检索迭代。
- 任何密钥、API key、token。
- 内部评委规划分与预测得分区间。
- 仓库里尚不存在的代码、README 或既有 `docs/`（检索时该公开仓库仅有 MIT LICENSE，尚无 README 或 docs）。
