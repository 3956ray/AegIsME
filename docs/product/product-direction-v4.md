# AegisME 产品方向报告 v4（完全合并） / Product direction report v4

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.

- **状态 / Status:** 当前 / Current
- **来源画布 / Source canvas:** [HARBOR 黑客松 · 产品方向报告 v4（完全合并）](https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/79418235-761c-4d21-89bb-b3f5e1bd8a3a)
- **日期 / Date:** 2026-11-27，并纳入 11-28 Gemini 口径（Asia/Shanghai）

## 中文

# AegisME 产品方向报告 v4（完全合并）

> v4 主方案：将信用额度与 ERC-8498 完全并入一个产品（现名 AegisME，原名 AgentGuard）。定位：别人管 AI 代理能做什么，本产品证明它替谁做。内部规划分已省略。

## 结论与版本变更

> **v4 主方案：将信用额度与 ERC-8498 完全并入一个产品（现名 AegisME，原名 AgentGuard）。定位：别人管 AI 代理能做什么，本产品证明它替谁做。**
>
> 【事实】用户已拍板完全合并，对外仍是一个产品，以执行方案为准（见 `plan/full-merge-execution-plan.md`）。【推断】在 12-07 三项检查通过之前，技术项自评低于 v3；差距主要在技术实现，按两级退路处理。叙事主线是「一个代理对应一个经过认证的真人，信用额度跟着人走，每次动用都要一张一次性券」。它把 ME 最独特的 ME ID 用在两个核心环节：代理身份与信用防女巫，同时覆盖「AI 与信任」与「链上金融」赛道关键词。对照方案为 MEC 按次付费网关（最贴官方 MEC 偏好）与 RWA 合规资格网关（ME ID 合规用法最直接），三者方向差异大，便于收敛。内部规划分已省略。

        
- v2 变更：评分改为官方五项权重，市场验证不再单独成维度，并入「产品价值」作为打分依据（按 Leader 最新更正，1.5 倍规则已取消）
- v2 变更：合并市场 7 个机会点，去重后统一清单 11 个；每个补「过往产品没做到的具体一点」并点名竞品、附来源
- v2 变更：新增合并方案与两个对照方案的 MVP、英文 Demo 流程，并写明哪项核心功能跑在 ME Network 上
- v2 变更：补充官方硬门槛；报名截止已按官方 X 更新为 11-29 23:59
- v2.1 变更：按 ME ID 接口核实结论重写主候选的架构、风险、MVP 与 Demo；信用额度升为必做；定位改为「别人管 AI 代理能做什么，AgentGuard 证明它替谁做」
- v3 定稿：销售市场验证强度并入「产品价值」（具体数字已省略）；新增「痛点证据与付费信号」；信用额度以防女巫为主线，Demo 加一笔模拟借用与归还；真实放贷与清算列入不做；新增 5-8 场种子用户访谈
- v4（完全合并）：按用户拍板把信用额度和 ERC-8498 完全并进 AgentGuard，原「ERC-8498 独立产品、不合并」的说法作废；信用模型改为「循环额度 + 一次性借款券」，合约为 MeIdGate、AgentPolicy、AgentCredit；因引入 Draft 标准与自写核销，技术项自评在 12-07 检查通过前更为审慎（数字已省略）；新增接口草图、真实与模拟清单、12-07 检查点与两级退路；Demo 换成 9 步版（约 3:21）

        本页标注：【事实】= 来源原文或数据直接给出；【推断】= 基于事实的判断。时间均为北京时间（UTC+8）。

      

## 官方硬门槛与时间线

> **报名已延期至 11-29 23:59（北京时间），资料修改期限是否顺延未知。**
>
> 【事实】官方 X 于 11-26 宣布报名延期至 11-29 23:59（北京时间），与赛事页一致；此前官方博客写的 11-27 截止已作废。来源：https://x.com/MetaEarthDevs/status/2125808255213634040 ；https://www.mec.me/zh-TW/hackathon/harbor 。【事实】赛事页 FAQ 写「报名信息可于 11-27 15:59 UTC 前修改」，官方未说明是否一并顺延。【推断】需要改报名资料的话，仍按今晚 11-27 23:59 前改完处理。

        
| 硬门槛 | 要求 | 对我们的含义 |
| --- | --- | --- |
| 全英文 | 【事实】所有提交资料统一使用英文，使用报名时的团队名与队长 ME ID | 【推断】README、项目说明、UI 文案、视频旁白全部英文 |
| Demo 视频 | 【事实】3-5 分钟，展示核心功能与使用流程，英文讲解或英文字幕 | 【推断】主方案 9 步旁白约 3:21，录完按实测核对不超过 4:30 |
| ME 链上记录 | 【事实】必须提交 ME Network 上的合约、交易或调用记录；或 Rollapp 运行与 Hub 接入信息 | 【推断】README 列出合约地址、关键交易哈希与浏览器链接 |
| 运行在 ME 上 | 【事实】至少一项可体验的核心功能运行于 ME Network | 【推断】核心合约必须部署在 ME，不能只在别的链 |
| 组队与认证 | 【事实】2-5 人，全员完成 ME ID 进阶认证；每队一份作品 | 【推断】今天核对全员认证状态 |
| 代码 | 【事实】提交仓库链接、最终 commit、运行说明；私有仓库需开放评审权限；已有项目只评新增 commit | 【推断】从新仓库开始，commit 按天提交 |

        
| 节点 | UTC | 北京时间 |
| --- | --- | --- |
| 报名信息修改截止（赛事页 FAQ；是否顺延未知） | 2026-11-27 15:59 | 11-27 23:59 |
| 报名截止（已延期，官方 X 确认） | 2026-11-29 15:59 | 11-29 23:59 |
| 作品提交截止 | 2026-12-21 15:59 | 12-21 23:59 |
| 作品评审 | 2026-12-24 | 12-24 |
| Demo Day 与颁奖 | 2027-01-15 06:00-08:30 | 01-15 14:00-16:30 |

        【事实】赛事页页首写赛期为 2026.11.16 - 2027.01.05，与赛程表 Demo Day 01-15 不一致。奖金：一等 40,000、二等 30,000、三等 2×10,000、优秀 4,000 / 3,000 / 3×1,000 USDT，合计 100,000 USDT（博客确认总奖池）。官方博客鼓励在支付、结算、激励中使用 MEC。

      

## 评分方法

【事实】权重来自赛事页官方评审标准。【推断】每项 1-5 分（可取 0.5），加权和除以 5 即换算到满分 100。市场验证不再单独打分，也不再乘 1.5，而是作为「产品价值」打分的证据，列在每个 idea 的「价值依据」中。

      

## 统一 Idea 清单

内部五项加权打分表已删除（本仓库为公开仓库）。下面保留每个 idea 的问题、用户、方案和「相对已有产品的具体差异」（这是具体差异陈述，不是“市场空白”断言）。

去重规则（【推断】）：AgentGuard 吸收产品侧的 Agent Leash；ME ID 信用额度吸收 ME Credit Line；可验证 AI 投研吸收 Proof-of-Alpha；RWA 合规资格网关吸收 Compliant Yield Vault。v4 主方案是 AgentGuard + 信用额度再加 ERC-8498 的完全合并，详见下一节。产品价值项按销售验证强度做了定性调整（数字已省略）。

### M. AgentGuard 完全合并（信用额度 + ERC-8498）

- **来源：** A + B + ERC-8498（用户 11-27 拍板）
- **赛道：** AI 与信任 + 链上金融
- **问题：** 用户不敢把钱交给 AI 代理：看不到代理替谁做、权限没上限、泄露的代理密钥还能借钱。对外说法（Leader 11-28 定）：Without a fresh owner-signed ticket, a leaked agent key cannot borrow.
- **用户：** 已把 Hyperliquid agent 或 API 钱包交给 bot / AI 的交易者；收集这类授权的终端与跟单运营方。
- **方案：** ME ID 真人绑定代理；AgentPolicy 合约强制限额；循环额度 100 test MEC 存在绑定 ME ID 的 ERC-8498 凭证里，代理每借一笔花一张主人临用现签的一次性借款券（expiry 不超过 10 分钟）；过了 dueAt 仍有欠款时，任何人都可以暂停凭证。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【推断】Zodiac Roles、ZeroDev 能细分权限但只认密钥；Cred、Credifi 有信用但不绑定代理授权；少有方案把真人身份、可暂停的信用状态和一次性动用授权绑在一起并落在 ME 上。
- **差异来源：** https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570 ；https://docs.roles.gnosisguild.org/ ；https://docs.zerodev.app/smart-accounts/permissions/intro
- **价值依据：** 【推断】产品价值沿用销售对 AgentGuard 的验证强度（数字已省略）；出资人需求无新证据。技术项自评在 12-07 三条检查都通过后才考虑上调。

### A. AgentGuard：有 ME ID 身份、权限由合约强制的 AI 交易代理金库

- **来源：** 市场 O1 + 产品 Agent Leash
- **赛道：** AI 与信任 + 链上金融
- **问题：** 用户不敢把钱交给 AI 代理：权限没上限、出错无回放、不能随时撤销。
- **用户：** 想让 AI 代为交易或理财的散户与小团队；需要留痕的机构试点方。
- **方案：** 用户在合约里签授权策略（额度、标的、杠杆、有效期），代理绑定 ME ID 子账户，越权即被合约拒绝，每次操作哈希存证可回放。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】Hyperliquid 的 approveAgent 只有 agentAddress、agentName（可附 valid_until，最长 180 天）等字段，没有标的、额度、杠杆参数；agent 可交易但不能转账或提币。【事实】Safe 的 Zodiac Roles、ZeroDev session keys 已能按合约、函数、参数、时间、频率细分权限。【推断】细分权限本身不新，缺口在于：没有产品把代理权限绑定到 KYC 级唯一真人身份，并与信用额度联动。
- **差异来源：** https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint ；https://docs.roles.gnosisguild.org/ ；https://docs.zerodev.app/smart-accounts/permissions/intro
- **价值依据：** 【推断】销售验证强度有记录（数字已省略；按合并方案计）。【事实】HyprEarn 11-14 披露少数授权其代理钱包的 Hyperliquid 账户出现未授权成交（根因、账户数、损失均未公布）；Prow 文档写明限额在其服务器检查；香港 SAGE 把 KYA 列为四大范畴之一。

### B. ME ID 信用额度：一人一证的小额无抵押循环额度

- **来源：** 市场 O2 + 产品 ME Credit Line
- **赛道：** 链上金融（信用评估）
- **问题：** 地址可无限生成，链上借贷只能超额抵押，信用无法积累。
- **用户：** 有链上历史但缺抵押品的个人、小商户，以及需要预付 API 费的 AI 代理的主人。
- **方案：** ME ID 真人凭证防女巫，链上行为算出可解释信用分，开放 5-500 美元级循环额度，按时还款即提额；AI 只解释分数。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】3Jane 的 Crypto Credit Lines 已进入维护模式只收还款；Credifi 依据 Ethos 社交分放款、上限 3,000 美元；Priors 只给 5-500 美元。【推断】共同缺口是缺少一人一证的 KYC 级身份，只能靠小额度控风险。
- **差异来源：** https://docs.3jane.xyz/backing/ccl ；https://www.ethos.network/post/credifi-unsecured-loans-ethos-score ；https://www.woofun.ai/en/news/detail/113842
- **价值依据：** 【推断】销售验证强度：信用模块单独约 3.0/5。【事实】10-11 月 Priors、Credifi、Unlloo 上线信誉型无抵押借贷，但额度普遍很小（Priors 5-500 美元）。

### C. MEC 按次付费网关：Agent 调 API 按次用 MEC 结算 + 去刷量统计

- **来源：** 市场 O4
- **赛道：** 消费级支付 + AI 与信任
- **问题：** 机器支付笔数暴涨，但卖家看不出哪些是真实付费调用。
- **用户：** 向 AI 代理卖数据、模型或 API 的开发者。
- **方案：** HTTP 402 式网关，付款方须持 ME ID 派生身份，MEC 微支付结算，卖家看板区分有机调用与疑似刷量。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】x402 在 Base 上 10 月的 22 倍增长中 95% 来自一家 facilitator 自己的钱包。【推断】x402 只解决「怎么付」，没解决「付款方是不是真实独立用户」。
- **差异来源：** https://chainward.ai/decodes/x402-one-platforms-own-volume
- **价值依据：** 【推断】销售验证强度 3.5/5；用户是否愿用 MEC 支付未验证。【事实】ChainWard 10-31 复盘 Base 10-19 至 10-30 共 2,479,685 美元（约 247.97 万）x402 交易额，95.05% 来自 Central City（https://chainward.ai/decodes/x402-one-platforms-own-volume）；官方博客鼓励 MEC 支付场景。

### D. RWA 合规资格网关（含 KYC 门控收益库）

- **来源：** 市场 O7 + 产品 Compliant Yield Vault
- **赛道：** 链上金融
- **问题：** RWA 能不能买、能不能赎回，买之前看不到；二级买家可能被拒绝赎回。
- **用户：** RWA 发行方与分销钱包；海外散户。
- **方案：** ME ID 发放地区与投资者资格凭证，代币转账、赎回按凭证放行；用户购买前即可自检资格；可附模拟国债收益代币演示。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】Ondo Stocks 不对美加居民开放，赎回须 KYC，二级市场买家可能被拒绝赎回。【推断】Ondo 的资格校验在发行方链下完成，持有人与 DeFi 协议在链上无法提前验证。
- **差异来源：** https://docs.ondo.finance/ondo-stocks/eligibility ；https://docs.ondo.finance/ondo-stocks/secondary-market-restrictions
- **价值依据：** 【推断】销售验证强度 3.5/5。【事实】官网显示 USDY TVL $2.38B、Ondo Stocks $1.40B（https://ondo.finance）；Ondo 条款写明二级市场买家可能无法赎回（https://docs.ondo.finance/ondo-stocks/secondary-market-restrictions）。

### E. SplitPay：ME ID 实名分账与订阅

- **来源：** 产品
- **赛道：** 消费级产品与支付
- **问题：** 群体分账与周期扣款在链上体验差，收款方是否真人不可知。
- **用户：** 小团队、创作者、社群组织者。
- **方案：** 规则化自动分账与订阅扣款，收款方须持 ME ID。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【推断】0xSplits 等分账合约只认地址，不校验收款方是否唯一真人，也不做订阅扣款。
- **差异来源：** https://splits.org
- **价值依据：** 【推断】需求普遍但缺少本轮付费信号证据。

### F. 可验证 AI 投研：信号哈希存证 + 到期自动对账战绩榜

- **来源：** 市场 O5 + 产品 Proof-of-Alpha
- **赛道：** AI 与信任（内容溯源）
- **问题：** AI 信号与喊单事后改口、战绩无法核验。
- **用户：** 付费订阅信号的交易者、信号提供者。
- **方案：** 信号发布即哈希上链，到期按行情自动对账，提供者绑定 ME ID 防马甲。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】评测称 Virtuals 等 Agent 代币「有用户、少有付费客户」，收入主要来自代币交易。【推断】这些 Agent 平台没有可验证的历史战绩，付费理由不足。
- **差异来源：** https://newsletter.ownyourmind.ai/p/agent-tokens-have-users-few-have
- **价值依据：** 【事实】过半 Binance AI Pro 提示是让 Agent 搭建并运行策略（The Block）。

### G. 休市 RWA 永续风险雷达

- **来源：** 市场 O3
- **赛道：** 链上金融（交易工具）
- **问题：** 周末与休市时段股票永续盘口脱离预言机，引发连环强平。
- **用户：** 在 Hyperliquid HIP-3 等平台交易股票、商品永续的散户。
- **方案：** 比对盘口与预言机价、资金费率极值，给风险分与预警；预警订阅与规则存证放在 ME。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】10/17 周六 HIP-3 芯片股永续 10 分钟跌约 6%，预言机只跌 1.5%，25 分钟强平 4,380 万美元。【推断】Hyperliquid 未提供休市时段偏离预警。
- **差异来源：** https://bitquery.io/investigations/hyperliquid-stock-perps-saturday-crash
- **价值依据：** 【事实】Grvt 调查 56% 交易者因资金费率不稳定放弃或平仓（CoinDesk 11-17）。需求最硬。

### H. ME Pulse：自然语言链上数据分析代理

- **来源：** 产品
- **赛道：** 开发者工具 / AI
- **问题：** 新链缺少数据分析工具，查数据要写 RPC 脚本。
- **用户：** ME 生态开发者、运营与评审。
- **方案：** LLM 把自然语言转成 Hub/Rollapp/EVM 查询，返回图表与可复现查询。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】截至 11-27，DefiLlama 链列表中没有 Meta Earth。【推断】通用分析工具尚未覆盖 ME。
- **差异来源：** https://api.llama.fi/v2/chains
- **价值依据：** 【推断】需求方主要是生态内部，付费信号弱。

### I. 一人一票裁决层：ME ID 真人陪审 + AI 整理证据

- **来源：** 市场 O6
- **赛道：** AI 与信任 + 链上金融
- **问题：** 预测市场争议由代币加权投票决定，被少数大户左右。
- **用户：** 预测市场、链上保险与对赌类应用的结算方。
- **方案：** ME ID 真人陪审团投票，AI 生成证据摘要与裁决草案，结果与理由上链。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】报道称九个匿名大户主导 Polymarket 的 UMA 争议投票。【推断】UMA 的代币加权机制无法做到一人一票。
- **差异来源：** https://www.predictionmarkets.org/nine-crypto-whales-dominate-polymarket-disputes-worth-billions/
- **价值依据：** 【事实】Polymarket 11 月成交低于 10 月并裁员，赛道热度下降（CoinDesk 11-12）。

### J. AutoBounty-ME：AI 初审的托管赏金

- **来源：** 产品
- **赛道：** AI 与信任
- **问题：** 赏金验收慢、易扯皮。
- **用户：** 开源项目方、DAO、自由开发者。
- **方案：** 资金进托管合约，AI 按验收标准初审，ME ID 实名双方，争议转人工。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】GenLayer 黑客松已有 AutoBounty 获奖。【推断】其差异空间只剩「实名防刷单」，创新有限。
- **差异来源：** https://x.com/RitaCryptoTips/status/2048670712970289409
- **价值依据：** 【推断】无本轮付费信号。

### K. HLP-on-ME：社区做市金库

- **来源：** 产品
- **赛道：** 链上金融与交易
- **问题：** 新链流动性薄，做市收益集中。
- **用户：** ME 生态 LP 与交易者。
- **方案：** 社区出资的协议做市金库，分享做市与清算收益。
- **相对已有产品的具体差异（陈述，非“市场空白”断言）：** 【事实】Hyperliquid HLP 由社区出资做市与清算，但只服务 Hyperliquid 自身订单簿。【推断】ME 缺订单簿与成交量，金库无从获益。
- **差异来源：** https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/protocol-vaults
- **价值依据：** 【推断】ME 上暂无成交量证据。

## 主方案：AgentGuard 完全合并（信用额度 + ERC-8498）

> **v4：用户已拍板完全合并。ERC-8498 不再是独立产品，信用额度和 ERC-8498 凭证都并进 AgentGuard，对外仍是一个产品。**
>
> 【事实】以 Leader 的完全合并执行方案为准：信用模型统一为「循环额度 + 一次性借款券」，合约只有 MeIdGate、AgentPolicy、AgentCredit 三个，Demo 用 9 步版。来源：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570 。原「ERC-8498 独立产品」评估页已归档，只作参考：见 `archive/erc8498-standalone-scoring.md`

        
- **定位：** 别人管 AI 代理能做什么，AgentGuard 证明它替谁做。英文：Every AI agent has a human behind it. AgentGuard proves who.
- **叙事：** 一个代理对应一个经过 ME ID 认证的真人；权限由合约强制；信用额度存在绑定这个人的 ERC-8498 凭证里，换代理也跟着走；代理每动用一次额度都要花掉一张主人签发的一次性借款券。信用模块小标题：Earn it. Lose it. Spend it once.；收尾句：Swap the agent, keep the credit. One verified human behind it.
- **信用模型：** 【推断】循环额度 + 一次性借款券：额度 100 test MEC，存在绑定 ME ID 的 ERC-8498 凭证（命名空间 agentguard.credit）里，还款后恢复；借款券由主人在链下用 EIP-712 签名，一笔借款一张，券里写明 agent、金额上限、nonce 和过期时间；合约只记录哪个 nonce 已经用过，同一张券再用被拒（ticket already spent）；按时还款后 tier + 1，黑客松期间只写进凭证状态、不改额度，所以 Demo 里额度一直是 100；逾期由 keeper 暂停凭证，所有代理同时借不了。【事实】券的格式与 tier 规则由 Leader 于 11-27 在团队群里定下。循环的是额度，一次性的是每次动用的授权，所以 Spend it once 和「还款回到 100」不冲突。来源：执行方案页「信用模型」一节
- **架构：** 【推断】后端用 SDK 查 ME ID → 签 EIP-712 证明 → MeIdGate 验签、按 DID 去重，并调用 AgentCredit 为该 DID 铸一枚 ERC-8498 凭证 → AgentPolicy 限定代理的单笔上限、白名单、杠杆、有效期，借用时验主人签的借款券再调 AgentCredit.draw → keeper 脚本在逾期后调 suspend；另加一笔 ME 原生的子账户绑定交易。原 CreditScore 与核销账本并入 AgentCredit。
- **内部打分：** 已省略（公开仓库）。定性理由如下。
- **打分理由（不含数字）：** 【口径】团队内部自评不是评委会给的分，对外不报任何分数。Gemini 曾给出更低的预估，团队未采纳其数字。【推断】技术项比 v3 更审慎：ERC-8498 是 Draft，借款券核销是自写、未审计的代码，参考实现要从 Cancun 降到 London 重编，且 12-01 前开发者尚未到位；要等 12-07 在 ME 测试网真正跑通才考虑上调。ME 应用：ME ID 查询、子账户绑定、EVM 合约、MEC 结算四处真实调用。产品价值：沿用销售对 AgentGuard 的验证强度，出资人需求没有新证据，不加分。创新：借款券把信用和代理安全接在一起（没有主人现签的券，泄露的代理密钥借不到钱），但细分权限已有 Zodiac Roles、ZeroDev 先例。体验：一套连贯的信用模型替代了两套说法，Demo 约 3:21 不超时。来源：`plan/full-merge-execution-plan.md`
- **过往产品没做到：** 【事实】Hyperliquid agent 钱包只有有效期（最长 180 天），没有标的、额度、杠杆限制；Zodiac Roles 与 ZeroDev session keys 能细分权限，但只认密钥地址，不验证背后是否为唯一真人；Credifi、Priors 有信用无 KYC 级身份。【推断】少有方案把「代理背后是谁（ME ID 真人）」「代理能做什么（链上强制的限额）」「代理能借多少、每次借要不要主人授权（凭证 + 一次性券）」绑在一起并落在 ME 上；不说「市场空白」。来源：https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint ；https://docs.roles.gnosisguild.org/ ；https://docs.zerodev.app/smart-accounts/permissions/intro ；https://www.ethos.network/post/credifi-unsecured-loans-ethos-score
- **差异化论点：** 【推断】别人能限制 AI 代理「做什么」，AgentGuard 还能证明代理「替谁做」：每个代理都对应一个 ME ID 认证的唯一真人，权限由合约强制，信用额度跟着这个真人走，每次动用都要一张一次性券，泄露的密钥借不到钱。
- **跑在 ME 上的核心功能：** MeIdGate、AgentPolicy、AgentCredit 全部部署在 ME 测试网 EVM（链 ID 400）；子账户绑定走 Hub 原生交易。提交合约地址与「绑定子账户」「登记 ME ID 证明并铸凭证」「花券借款」「越权与重用券被拒」「新代理还款」「keeper 暂停」交易哈希

        
          

### 必做

- 签名后端：SDK getMeIdByAddress 或 REST /metaearth/did/did 查主人 ME ID，签 EIP-712 证明（地址、DID 哈希、过期时间）
- MeIdGate：验签、按 DID 去重（重复 DID revert）、调用 AgentCredit 铸凭证、可撤销、事件留痕
- 子账户绑定交易（bindSubAccount），作为 ME 原生链上记录
- AgentCredit：复用 ERC-8498 参考实现核心（stateOf、policyOf、applyTransition），按 London 重编；加 agentguard.credit 命名空间的循环额度账本（100 test MEC，8 位精度）、已用券 nonce 记录（按 DID，用过即拒）、按时还款 tier + 1（只写凭证状态，不改额度）、suspend / resume
- AgentPolicy：单笔上限、标的白名单、杠杆上限、有效期、一键撤销；execute 时验主人的 EIP-712 借款券签名（agent 必须是调用者、金额不超过券上限、未过期）再调 draw；先撤旧代理再登记新代理
- keeper 脚本（只是调用者之一，任何人都可调）：过了 dueAt 后发一笔 suspend 交易（用很短的到期时间制造逾期，不进视频，哈希放仓库）
- LLM 交易代理：链下推理，成交记录到测试地址，每次动作存输入摘要与结果哈希
- 审计面板（额度、券、revision、拒绝原因）+ 前端 RPC 代理（测试网 RPC 是 HTTP 裸 IP）
- 英文 README 列出所有合约地址与交易哈希

          

### 可选

- MEC 支付代理调用费（贴官方 MEC 偏好）
- 止损规则与风险预警
- 部署独立 Rollapp 并在 Hub 注册
- AI 生成每日操作报告

          

### 不做

- 主网部署（主网 EVM 链 ID 2404，先只上测试网）
- 真实放贷、计息与清算：只在 Roadmap 提一句
- me.staking 升档、ZK 私有呈示
- 按 tier 调整额度（黑客松期间额度固定 100 test MEC）
- AI 自主决定额度或放款
- 接入真实 DEX、跨链、外部交易所
- 代币经济与治理、移动端

        
        

### 三个合约的接口草图

```solidity
// 【推断】接口草图，取自执行方案页，字段名可改

// 1. MeIdGate
function register(address owner, bytes32 didHash, uint256 deadline, bytes backendSig, bytes ownerSig) external;
//   【事实】Leader 11-27 已定：加 ownerSig，主人用 EIP-712 签同意，铸凭证时验这个签名
//   调用方：任何人提交（须带后端 EIP-712 签名 + 主人同意签名）
//   验 backendSig 与 ownerSig -> didHash 去重（重复 revert "DID already registered"）
//   -> AgentCredit.mintFor(didHash, owner, ownerSig)
event Registered(bytes32 indexed didHash, address indexed owner);   // 【推断】事件名为产品侧补充

// 【事实】Leader 11-28 定：EIP-712 Domain 写死 
//   所有签名（register 的 ownerSig、借款券）都用这个 Domain，防跨链、跨部署重放（name/version 取值为产品侧补充）

// 2. AgentCredit = ERC-8498 核心 + 循环额度账本 + 借款券核销
//   IEvolvingSBT（复用参考实现）
function stateOf(uint256 tokenId, bytes32 ns) external view returns (StateHead memory);
function policyOf(bytes32 ns, bytes32 policyId) external view returns (Policy memory);
function applyTransition(Change calldata c, bytes calldata evidence, bytes calldata auth) external;
event StateTransitioned(...);                                        // ERC-8498 规定
//   信用扩展（命名空间 agentguard.credit）
function mintFor(bytes32 didHash, address owner, bytes ownerSig) external; // onlyMeIdGate
function creditOf(bytes32 didHash) external view
  returns (uint64 limit, uint64 outstanding, uint8 tier, uint8 status, uint64 revision);
//   链上不计券的张数；只记已花掉的 nonce
mapping(bytes32 didHash => mapping(uint256 nonce => bool)) public spentNonce;
function draw(bytes32 didHash, Ticket calldata t, bytes calldata ownerSig, uint64 amount) external; // onlyPolicy（只有 AgentPolicy 能调）
//   【事实】Leader 11-28 定：单笔上限由 AgentPolicy.execute 先查 min(t.maxAmount, perTradeCap)，再调 draw
//   require status == Active; require t.didHash == didHash; require 签名人 == DID 主人（按上方固定 Domain 验签）;
//   require t.agent == 发起交易的代理; require block.timestamp  revert "ticket already spent"
mapping(bytes32 didHash => uint64) public dueAt;          // 【事实】Leader 11-28 定：每笔借款记 dueAt（单笔在借时一个字段即可，【推断】多笔并存时取最早一笔）
function repay(bytes32 didHash, uint64 amount) external;  // 任何人可代还；在 dueAt 前还清 -> tier + 1，只写凭证状态，limit 不变（100）
function suspend(bytes32 didHash) external;               // 任何人可调；require now > dueAt && outstanding > 0；keeper 只是调用者之一
function resume(bytes32 didHash) external;                // onlyController（团队多签）
event TicketSpent(bytes32 indexed didHash, uint256 nonce, uint64 amount); // 【推断】产品侧补充
event Repaid(bytes32 indexed didHash, uint64 amount);                               // 【推断】产品侧补充

// 3. AgentPolicy
// 借款券：主人链下 EIP-712 签名，一笔借款一张
// 【事实】Leader 11-28 定：临用现签，expiry 不超过签发后 10 分钟，不允许一次预签多张；加 didHash 防跨 DID 重放
// 【推断】产品侧补充：合约里可加 require t.expiry  AgentCredit.draw(didHash, t, ownerSig, amount) -> 记录成交
//   券的签名、didHash、agent、expiry、nonce 在 draw 里校验
event Executed(address indexed agent, bytes32 indexed didHash, bytes32 tradeHash);  // 【推断】产品侧补充
event Rejected(address indexed agent, bytes32 reason);                              // 【推断】审计面板读取
// 【事实】Leader 11-27 已定：第 7 步四条拒绝原因由审计面板在链下预检后列出，链上只演示一次真实 revert；旁白不说“链上返回四条原因”
// 【推断】产品侧补充：preflight 是 view，审计面板用 eth_call 在链下调用，不发交易
function preflight(Trade calldata tr, Ticket calldata t, bytes calldata ownerSig)
  external view returns (bytes32[] memory failedReasons); // 单笔上限 / 白名单 / 杠杆 / 有效期 / 券（签名、maxAmount、expiry、spentNonce）/ 额度
```

          【事实】ERC-8498 核心只规定 stateOf、policyOf、applyTransition 和 StateTransitioned；一次性消费须由应用自己用作用域 nullifier 记录，规范允许签名、授权的链上调用方作为写入方，时间流逝不会自动改状态。【推断】所以核销放进 AgentCredit，draw 只认 AgentPolicy；suspend 按 Leader 11-28 的决定改为链上逾期条件（过 dueAt 且有欠款），任何人可调，keeper 不再是中心化开关。函数签名与调用权限来自执行方案页，借款券结构按 Leader 11-27 的决定改为链下 EIP-712 签名 + 链上只记已用 nonce，已删掉链上 ticketsLeft 计数；标「产品侧补充」的事件是我加的，方案页未写。来源：https://eips.ethereum.org/EIPS/eip-8498 ；https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570

        

### 真实与模拟清单

| 环节 | ME 测试网上真实跑 | 模拟 / 链下 |
| --- | --- | --- |
| ME ID | 队友真实 ME ID，SDK 查询；一笔 Hub 原生子账户绑定交易 | 证明签名由我们的后端发（路演如实说） |
| 3 个合约 | 全部部署在链 ID 400，每步留交易哈希 | — |
| 额度与借还 | 额度、欠款、已用券 nonce、tier、revision 都在链上；借款券签名在链下生成、上链验签 | 用 test MEC，不是真实放贷，没有利息和清算 |
| 代理交易 | execute 交易和越权、重用券 revert 都在链上 | 成交记录到测试地址，不接真实 DEX；AI 推理在链下 |
| Lose it（逾期暂停） | keeper 的 suspend 交易是真实链上交易 | keeper 是脚本；逾期用很短的到期时间制造，不进视频，哈希放仓库 |
| 不做 | — | me.staking 升档、ZK 私有呈示、主网、真实放贷 |

          【事实】以上清单取自执行方案页。来源：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570

        

### 12-07 检查点与两级退路

| # | 检查标准（已定） |
| --- | --- |
| ① | 8498 核心在链 ID 400 上跑通 applyTransition |
| ② | 券核销与重用 revert 在测试网通过 |
| ③ | 一次借款交易不超过 500k gas |

          
| 结果 | 方案 | 改动 |
| --- | --- | --- |
| 三条都过 | 完全合并（本页主方案） | 维持完全合并；技术项自评仅在检查通过后才考虑上调（数字不对外） |
| ① 过，② 或 ③ 没过 | 第一级退路：轻度结合 | 去掉借款券；ERC-8498 凭证只承载额度状态与暂停；Demo 第 7 步删掉 ticket already spent 这一条拒绝原因 |
| ① 没过，或 12-01 前开发者未到位 | 第二级退路：回到 v3 | 防女巫 + 模拟借还，CreditScore 按 DID 记账，不用 8498；路演不提 8498 |

          【事实】已定（Leader 11-27 在团队群里拍板）：三条检查全部通过才做完全合并；① 过了、② 或 ③ 没过，降到轻度结合（去掉借款券，第 7 步删一个拒绝原因）；① 没过，回到 v3（CreditScore，路演不提 8498）。第 ③ 条为「一次借款交易不超过 500k gas」。另有硬前提：「12-01 Solidity 开发到位。到不了位，直接按 v3（CreditScore，不用 8498）做。」【事实】ME 测试网的区块 gas 上限尚未实测，列入第一周实测清单，确认之前不写进对外材料。来源：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570

        

### Roadmap 口径

- Credit record built on the draft ERC-8498 interface; a missed repayment suspends the record.
- Replace the backend signer with VC-based ME ID verification or a threshold of signers.
- Mainnet deployment, then real lending with partners; no real loans in the hackathon build.

          【推断】Roadmap 只写 "built on the draft ERC-8498 interface"，不提共同作者，也不说市场空白。来源：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570

        

### v4 新增风险

1. 签名后端是信任点：【推断】ME ID 证明由我们的后端签发，凭证暂停权在 controller（团队多签）；路演主动讲，并给出签名有效期、按 DID 去重、可撤销和多签路线图。来源：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570
2. ERC-8498 是 Draft，核销不在核心 ABI：【事实】EIP 状态 Draft，一次性消费须应用自己实现，参考实现没有额度核销。【推断】AgentCredit 的核销是自写、未审计代码，只做内部代码评审；路演只说 built on the draft ERC-8498 interface。来源：https://eips.ethereum.org/EIPS/eip-8498 ；https://github.com/ethereum/ERCs/pull/2171
3. EVM 版本：【事实】参考实现按 evm_version = cancun 编译，ME 的 Ethermint 依赖 go-ethereum v1.10.26（London）。【推断】需显式写 evm_version = london，清理 PUSH0、tstore、tload、mcopy 和 OpenZeppelin Transient 类合约，51 项测试按 London 重跑，并在链 ID 400 实际部署；这正是 12-07 检查 ①。来源：https://github.com/XiaoHai67890/evolving-sbt ；https://github.com/openmetaearth/me-hub/blob/main/go.mod
4. 开发人力：【推断】12-01 前招不到 Solidity 开发，直接走第二级退路（v3）。来源：执行方案页排期

        

### 痛点证据与付费信号

| 证据 | 内容 | 来源 |
| --- | --- | --- |
| HyprEarn（11-14） | 【事实】少数授权了 HyprEarn API（代理）钱包的 Hyperliquid 账户出现未授权成交；代理钱包不能提币；用户须到 Hyperliquid 官网自行撤销授权。根因、受影响账户数、损失金额均未公布 | https://x.com/HyprEarn/status/2121673806704243178 ；https://www.0xcert.com/advisory/0xCERT-2026-0362 |
| Prow 文档 | 【事实】用户签的限额在 Prow 自己的服务器上检查，不由交易所强制；密钥泄露后仍可超出限额下单，直到撤销或过期 | https://prowdex.com/docs/bots/bot-key ；https://prowdex.com/docs/bots/overview |
| r/defi（10-07） | 【事实】讨论 AI 交易代理的限制应放在哪里，观点是限额必须放在代理控制不了的地方 | https://www.reddit.com/r/defi/comments/1wzsquv/if_an_ai_trader_had_limited_wallet_authority_what/ |
| r/AI_Agents（约 1 个月前） | 【事实】帖子正文原话：「"Never spend more than $50" in a system prompt is a suggestion. A policy check in the signing service is a rule.」（已于 11-27 核对原帖）。此前页面引用的「Prompt limits are suggestions」出自另一帖的评论，路演改用这句完整原话 | https://www.reddit.com/r/AI_Agents/comments/1xinuur/if_youre_giving_an_ai_agent_a_wallet_put_these/ |
| r/hyperliquid1（10-21） | 【事实】原话「you do not know the trader you are copytrading」，对应「替谁做」 | https://www.reddit.com/r/hyperliquid1/comments/1xbh94t/what_problems_have_you_encountered_copytrading_on/ |
| 付费信号：Cryptohopper | 【事实】年付 24.16、57.50、107.50 美元/月；月付 29、69、129 美元/月 | https://www.cryptohopper.com/pricing |
| 付费信号：Cornix | 【事实】32.99 和 52.99 美元/月 | https://cornix.io/pricing/ |
| 付费信号：3Commas、Bitsgap | 【事实】价格来自第三方汇总，官网未核对 | https://coinbureau.com/analysis/best-crypto-ai-trading-bots ；https://tradenorte.com/en/tools/trading-bot-cost-comparison/ |
| 我们的定价 | 【推断】路演中的假设，按上述竞品价位推出：个人档 9-19 美元/月；运营席位 49-99 美元/月起 | 无外部来源（团队假设） |
| 不引用 XMR1/Wagyu（11-20） | 【事实】Bitquery 写明 Hyperliquid 上转出代币是 user-signed action，须由账户自己的密钥签名，原文「API wallets are for trades」；转出方很可能持有部署者主密钥。不属于代理权限案例，路演不用 | https://bitquery.io/investigations/xmr1-hyperliquid-hack |

          
> **路演口径：HyprEarn 只讲「有未授权成交」**
>
> 【事实】HyprEarn 未公布根因、受影响账户数和损失金额。路演和答辩只说「有未授权成交」，并明说这三项未公布；不说「被盗」「被清空」，也不推测金额。来源：https://x.com/HyprEarn/status/2121673806704243178

        

### 核实：Hyperliquid API 钱包权限与可比产品（2026-11-27）

| 核实项 | 结论 | 来源 |
| --- | --- | --- |
| approveAgent 完整字段 | 【事实】type、hyperliquidChain、signatureChainId、agentAddress、agentName（可选）、nonce；外层另有 nonce、signature。Python SDK 的 approve_agent 只接收 name 参数 | https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint ；https://github.com/hyperliquid-dex/hyperliquid-python-sdk/blob/master/hyperliquid/exchange.py |
| 有效期 | 【事实】有：在 agentName 后追加 valid_until ，最长 180 天；到期后钱包会被清理。原推断「没有有效期」被推翻 | https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/nonces-and-api-wallets |
| 标的白名单、额度、杠杆上限 | 【事实】approveAgent 无任何此类字段，授权后可代主账户或子账户签署交易类动作 | https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint |
| 不能做什么 | 【事实】官方 SDK 示例写明 agent 无权转账或提币；agentSendAsset 只能在自己账户的永续与现货之间划转（目标地址必须等于来源地址） | https://github.com/hyperliquid-dex/hyperliquid-python-sdk/blob/master/examples/basic_agent.py |
| 可授权数量 | 【事实】每账户 1 个未命名 + 最多 3 个命名 agent；每个子账户另加 2 个命名 agent；新的未命名授权会注销旧的 | https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint |
| 替代做法 | 【事实】子账户与 vault 无私钥，由主账户签名并设置 vaultAddress 代为操作；【推断】实践中靠「只往子账户放愿意亏的钱」来隔离风险，属资金隔离而非规则约束 | https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/exchange-endpoint |
| 可比：Safe Zodiac Roles | 【事实】链上权限模块：按目标地址、函数、函数参数条件授权，支持额度（allowances） | https://docs.roles.gnosisguild.org/ ；https://github.com/gnosisguild/zodiac-modifier-roles |
| 可比：ZeroDev session keys | 【事实】权限 = 1 个签名者 + N 个策略：调用策略（合约、函数、参数、转账上限）、频率限制、时间窗口、gas 上限 | https://docs.zerodev.app/smart-accounts/permissions/intro ；https://docs.zerodev.app/smart-accounts/permissions/policies/call |

          
> **不能宣称「没人做到细分权限」。**
>
> 【推断】评委很可能知道 Zodiac Roles 与 session keys。路演应把细分权限讲成「必要底座」，把新意放在 ME ID 真人绑定与信用联动上；Demo 中可直接对比「Hyperliquid agent 只有有效期」与「AgentGuard 按标的、额度、杠杆拒绝越权」。

        

### ME ID 接入：已查实的约束与方案

| 项目 | 结论 | 来源 |
| --- | --- | --- |
| 链架构 | 【事实】ME Network 是 Cosmos SDK 链（ME Hub），内置 Ethermint EVM | https://github.com/openmetaearth/me-hub |
| 合约能否读 ME ID | 【事实】不能。ME ID 是 Hub 原生模块 x/did、x/kyc，EVM 没有对应预编译合约 | https://github.com/openmetaearth/ethermint/blob/main/x/evm/vm/geth/precompiles.go |
| 官方查询方式 | 【事实】只能链下查询：JS SDK getMeIdByAddress，或 REST /metaearth/did/did；一个 ME ID 绑定唯一一个 EVM 子账户 | https://github.com/openmetaearth/me-docs/blob/main/docs/development-guides/developer-guide/js-sdk.md |
| 链 ID 与 MEC | 【事实】测试网 EVM 链 ID 400，主网 2404；MEC 是 EVM 原生币，精度 8 位（合约与前端换算不能按 18 位） | https://github.com/openmetaearth/meta-earth-js-sdk ；市场报告第 7 节 https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/5b710767-0faf-438c-b2c9-18e290ade689 |
| 架构 | 【推断】后端查 ME ID → 签 EIP-712 证明 → MeIdGate 验签 → MeIdGate 调 AgentCredit 铸 ERC-8498 凭证 → AgentPolicy 限权、验借款券并调 AgentCredit.draw；外加一笔子账户绑定交易 | 同上 |

          
**优点**
- 测试网新账户大概率没有 ME ID
- 信任集中在我们的签名后端
- 测试网 RPC 是 HTTP 裸 IP，HTTPS 前端无法直连
- 主网 EVM 基础费率偏高
**缺点 / 代价**
- 读队员在主网的真实 ME ID，把证明写进测试网合约；同时去开发者群问测试网 KYC 办法
- 签名者地址公开、证明带过期时间、可撤销、每次签发留事件；路线图写明改为 ME 原生 VC 校验
- 后端加 HTTPS 反向代理转发 RPC
- MVP 只部署测试网

          

#### 路演答辩准备：信任集中在签名后端

- Q：签名后端作恶怎么办？A：后端只能证明「这个地址有 ME ID」，查询结果评委可用公开 REST 接口复核；签名者地址公开，证明有过期时间，错误证明可链上撤销
- Q：为什么不在合约里直接验？A：【事实】ME EVM 目前没有 ME ID 预编译合约；这是现阶段唯一可行路线
- Q：之后怎么去中心化？A：多签名者阈值签名，或改用 ME ID 发行方签发的 VC，或推动 ME 增加预编译

        

### Demo 流程（9 步，约 3:21，英文）

【事实】采用执行方案页的 9 步版：旁白 384 词，按 135 词/分加约 30 秒链上等待，约 3:21；再给录屏操作留 30 秒约 3:51，低于 4:30。第 7 步保留，并加上重用已花的券被拒（ticket already spent）。结尾商业部分只念 "Subscription, not a loan book." 半句；第 8 页商业部分只在现场路演讲。Lose it（逾期暂停）只在第 9 步说一句，keeper 交易哈希放仓库。录完按实测时长再核。来源：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570

      

## 对照方案一：MEC 按次付费网关

- **内部打分：** 已省略。价值项曾按销售验证强度上调。
- **过往产品没做到：** 【事实】ChainWard 10-31 复盘 Base 10-19 至 10-30 共 2,479,685 美元（约 247.97 万）x402 交易额，95.05% 来自 Central City；【推断】x402 只管怎么付，不验证付款方是否真实独立。来源：https://chainward.ai/decodes/x402-one-platforms-own-volume
- **跑在 ME 上的核心功能：** MEC 微支付结算合约与付款方 ME ID 校验；提交每次 API 调用的结算交易哈希
- **必做：** 402 网关中间件、MEC 预付与扣费合约、ME ID 付款方校验、卖家看板（有机调用与疑似刷量）
- **可选：** 批量结算以降手续费、卖家信誉凭证、AI 识别刷量模式
- **不做：** 法币结算、多链、支付卡接入

      

## 对照方案二：RWA 合规资格网关

- **内部打分：** 已省略。价值项按销售验证强度与原先一致。
- **过往产品没做到：** 【事实】Ondo Stocks 赎回须 KYC，二级市场买家可能被拒绝赎回；【推断】资格只能事后由发行方判定，买家和 DeFi 协议无法在链上提前验证。来源：https://docs.ondo.finance/ondo-stocks/secondary-market-restrictions
- **跑在 ME 上的核心功能：** 资格凭证登记、受限转账代币的转账与赎回校验；提交「合格地址转账成功」「不合格地址被拒」交易哈希
- **必做：** 资格 Registry（地区、投资者类型）、受限转账模拟国债代币、申购赎回、资格自检页面
- **可选：** 模拟 NAV 预言机与收益累积、AI 用白话解释「你为什么不能买」、独立 Rollapp
- **不做：** 真实资产托管、法币出入金、真实证券发行

      

## ME Network 能力

- **架构：** 【事实】模块化链：ME Hub 为结算层，Rollapp 为执行层，另有 DA 层
- **合约环境：** 【事实】EVM（Ethermint，Solidity）+ WASM（Rust）双虚拟机；官方博客称主网已 EVM 兼容
- **ME ID：** 【事实】DID 身份：KYC 后获得不可转让 SBT 作为真人证明；VC 可用零知识证明选择性披露。实现为 Hub 原生模块 x/did、x/kyc，EVM 无预编译，合约不能直接读取（https://github.com/openmetaearth/ethermint/blob/main/x/evm/vm/geth/precompiles.go）
- **JS SDK：** 【事实】钱包、转账、ME ID 查询、子账户绑定（bindSubAccount）、质押、治理、WASM/EVM 合约部署与调用
- **EVM 网络：** 【事实】测试网链 ID 400（SDK 默认 RPC 为 HTTP 裸 IP，HTTPS 页面需代理），主网链 ID 2404；MEC 为 EVM 原生币、精度 8 位；测试币需联系 ME 团队

        来源：https://meta-earth.gitbook.io/white-paper/technical-overview/architecture/modular-architecture-of-me-network ；https://github.com/openmetaearth/meta-earth-js-sdk ；https://github.com/openmetaearth/openroll

      

## 标杆拆解：Hyperliquid 与 Ondo

| 维度 | Hyperliquid | Ondo Finance |
| --- | --- | --- |
| 核心用户 | 【推断】链上高频与杠杆交易者、做市商、前端开发者 | 【事实】美国以外的个人与机构投资者（需 KYC） |
| 关键机制 | 【事实】自研 L1（HyperBFT），HyperCore 链上订单簿；HLP 社区金库做市与清算；API（agent）钱包可代签交易、不能提币，可设最长 180 天有效期 | 【事实】USDY、OUSG、Ondo Stocks（480+ 资产），第三方托管与审计；Intelligent Portfolios 由 BlackRock 等模型提供方定权重 |
| 生态开放 | 【事实】Builder codes 前端可收费（永续最多 0.1%）；HIP-3 质押 50 万 HYPE 自建永续市场 | 【事实】代币可自由转让并用于 DeFi，多链分发 |
| 增长飞轮 | 【推断】积分拉用户 → 深度 → 更好成交 → 更多前端分成 → 手续费回馈社区 | 【推断】合规资产 → 作为 DeFi 抵押品 → TVL 与持有人增长 → 更多发行方 |
| 数据（2026-11-27） | 【事实】DefiLlama：Bridge TVL $5.69B，HLP $152M；永续手续费近 30 天 $101.7M | 【事实】官网：USDY $2.38B，OUSG $315.9M，Ondo Stocks $1.40B |
| 短板 | 【事实】周末盘口脱离预言机引发强平（bitquery）；agent 钱包无标的、额度、杠杆限制，也不绑定真人身份 | 【事实】美加不可用；二级买家可能被拒赎回 |

        来源：https://hyperliquid.gitbook.io/hyperliquid-docs ；https://defillama.com/protocol/hyperliquid ；https://ondo.finance ；https://docs.ondo.finance/intelligent-portfolios/model-providers

      

## 社区讨论与方法论

        
> Chasing the top APY is the easy demo. Making people comfortable when the agent is wrong is the product.

      

## 关键未知项与下一步

1. 11-29 23:59（北京时间）前完成报名；需改报名资料的，按今晚 11-27 23:59 前改完（是否顺延官方未说明）；确认全员 ME ID 进阶认证
2. 已确认合约不能直接读 ME ID，按后端签名方案开发；待官方回答：测试网如何获得 ME ID / KYC、主网 EVM 手续费、ME Pass 能否导出助记词绑定 MetaMask 子账户
3. 测试币、HTTPS RPC、区块浏览器：向 ME 团队申请
4. 自建 Rollapp 是否额外加分：向主办方确认
5. 提交前做 5-8 场种子用户访谈：提纲由销售起草，约谁由负责人决定，团队不对外联系；访谈结论回填「痛点证据」与「产品价值」
6. 12-01 前招到 Solidity 开发（硬前提，到不了位直接按 v3 做）；12-01 至 12-06 参考实现按 London 重编、51 项测试重跑并部署到链 ID 400，同时搭 MeIdGate、AgentPolicy、AgentCredit，并实测 ME 测试网的区块 gas 上限（确认前不写进对外材料）和一次借款交易的 gas（标准为不超过 500k）；12-07 按三条标准决定完全合并、轻度结合或回到 v3

### 来源

- 原始画布：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/79418235-761c-4d21-89bb-b3f5e1bd8a3a
- 执行方案：`plan/full-merge-execution-plan.md`
- 路演稿：`pitch/pitch-and-demo-narration.md`

---

## English

# AegisME product-direction report v4 (full merge)

**Status:** Current. **Source:** product canvas v4, 27 Nov 2026 (Asia/Shanghai), updated after the Gemini review.

The user chose a **full merge**: one product, now named AegisME (formerly AgentGuard). Positioning: others limit what an AI agent can do; this product proves who it acts for. A revolving line lives in an ERC-8498 credential bound to a ME ID; every draw spends a just-in-time owner-signed ticket.

Internal planning scores have been omitted from this public repository. Qualitatively, tech is more conservative than v3 until the 7 Dec checks pass (Draft standard, unaudited ticket logic, London retarget, no developer yet). ME application is strong if ME ID lookup, sub-account binding, EVM contracts and MEC settlement all run for real. Product value follows existing sales-validation strength; funder demand is still unproven. Innovation is the ticket that ties credit to agent safety, with the caveat that fine-grained permissions already exist in Zodiac Roles and ZeroDev. UX benefits from one coherent credit model and a demo of about 3:21.

## Official gates and timeline (Beijing time, UTC+8)

- All submission materials in English, under the registered team name and captain ME ID.
- Demo video 3–5 minutes, English voice-over or English subtitles, showing the core flow.
- At least one experienceable core feature must run on ME Network, with contract / transaction records.
- Registration deadline: 29 Nov 2026, 23:59 (officially extended; confirmed on the official X account). A FAQ time of 27 Nov 15:59 UTC may not have been updated — treat 29 Nov 23:59 Beijing time as binding.
- Submission: 21 Dec 2026, 23:59. Judging 24 Dec. Demo Day 15 Jan 2027.
- Team size 2–5; every member needs advanced ME ID certification.

## Idea list

Numeric ranking tables are omitted. Dedup: AgentGuard absorbs Agent Leash; the ME ID credit line absorbs ME Credit Line; verifiable AI research absorbs Proof-of-Alpha; the RWA gateway absorbs Compliant Yield Vault. The Chinese section lists each idea’s problem, user, solution, and a **specific difference versus existing products** (a concrete contrast, not a “market gap” claim). The v4 primary idea is the full merge of AgentGuard + credit line + ERC-8498. Alternatives kept for contrast: a MEC pay-per-call gateway (closest to official MEC preferences) and an RWA eligibility gateway (the most direct compliance use of ME ID).

## Primary idea — must / optional / must-not

**Must:** a signing backend that looks up ME ID via the official SDK or REST and signs an EIP-712 attestation; `MeIdGate.register` with `backendSig` + `ownerSig`; `AgentCredit` holding the ERC-8498 core, per-DID ledger and ticket consumption (London EVM, no PUSH0 / tstore / tload / mcopy); `AgentPolicy` with authorize / revoke / preflight / execute; just-in-time tickets (10-minute expiry, `spentNonce`); permissionless `suspend` after `dueAt`; a 9-step English demo including “ticket already spent”; honest disclosure that the backend signs ME ID.

**Optional:** a short-due-date `suspend` transaction whose hash goes in the repo (not in the video); a Tier 0→1 label after on-time repayment (limit stays 100); a keeper script as one caller.

**Must not:** real lending or liquidation; claiming repayment raises the limit; claiming the line itself is one-time; claiming co-authorship or a market gap; publishing internal scores; putting the block gas limit in external materials; claiming the contract reads ME ID; claiming “a leaked key cannot borrow” as an absolute (use the agreed sentence only).

Interface sketch, real-vs-simulated list, and the 9-step demo match `plan/full-merge-execution-plan.md` and `pitch/pitch-and-demo-narration.md`.

## 7 Dec checkpoint and fallbacks

1. `applyTransition` runs on chain 400.
2. Ticket consume and reuse-revert pass on testnet.
3. One borrow transaction stays under 500k gas (the testnet block gas limit is not yet measured; do not put it in external materials).

All three pass → stay on full merge. (1) passes but (2) or (3) fails → light merge (drop tickets; drop “ticket already spent” from step 7). (1) fails, or no developer by 1 Dec → v3 CreditScore, do not mention 8498.

## ME ID constraint and Q&A posture

EVM contracts cannot read ME ID (no precompile). The official path is off-chain (SDK / REST). The backend attests via EIP-712; the contract verifies the signature and dedupes by DID. Say this honestly on stage: trust is limited (public signer, expiry, on-chain revoke, anyone can re-query ME’s API); spending limits and tickets do not depend on the backend; suspend is permissionless after `dueAt`. Roadmap: multi-signer attestations and a native read path.

## Evidence and benchmarks

Pain evidence includes the 14 Nov 2026 HyprEarn incident (unauthorized fills after agent-wallet approval; root cause, account count and losses unpublished), MAS / HKMA KYA agenda items, and bot-platform docs that enforce some limits only on their own servers. Hyperliquid `approveAgent` has an expiry (up to 180 days) but no per-asset, size or leverage caps. Zodiac Roles and ZeroDev session keys limit what a key can do, not who is behind it. Do not invent loss figures. Do not cite XMR1 as an agent-permission case (funds moved with the deployer’s master key).

## Open items

Find a Solidity developer by 1 Dec; finish registration by 29 Nov 23:59 Beijing time under the name AegisME; provide public evidence before any co-authorship claim; run seed and funder interviews; ask the three prepared questions in the ME developer Telegram group. External outreach is done by the user.
