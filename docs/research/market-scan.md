# HARBOR 第一轮市场扫描 / First-round market scan

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.

- **状态 / Status:** 调研备查（推荐的两个方向已并入 AegisME） / Research; recommendations now merged into AegisME
- **来源画布 / Source canvas:** [HARBOR 黑客松第一轮市场扫描：链上金融 × AI](https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/5b710767-0faf-438c-b2c9-18e290ade689)
- **日期 / Date:** 2026-11-27（Asia/Shanghai）；窗口 2026-08-27 至 2026-11-27

## 中文

# HARBOR 黑客松第一轮市场扫描：链上金融 × AI

> 赛事规则与评审权重、近 3 个月（2026-08-27 至 11-27）链上金融与 AI 的趋势、7 个标杆拆解，以及 7 个机会点（内部加权打分已省略）。当时推荐优先做 AgentGuard 和 ME ID 信用额度；二者现已完全并入 AegisME。

## 1. 赛事要点

> **报名截止已延期（11-27 更新）**
>
> 【事实】官方开发者账号 @MetaEarthDevs 于 11-26 宣布报名延期至 11-29 23:59（UTC+8），与赛事页一致 https://x.com/MetaEarthDevs/status/2125808255213634040 。此前官方博客与 OpenBuild 写的 11-27 23:59（UTC+8）已过时。赛事页另写报名信息可改到 11-27 15:59 UTC，是否随之顺延未见说明。

        
| 评审维度（官方权重） | 分值 | 官方说明 |
| --- | --- | --- |
| 技术实现 | 30 | 功能完成度、代码质量、系统稳定性 |
| ME 应用 | 25 | 对 ME Network 能力的接入深度与运用程度 |
| 产品价值 | 20 | 是否解决真实需求，具备落地潜力 |
| 创新程度 | 15 | 构想、方案或体验上的独特性 |
| 用户体验 | 10 | 操作流畅度与上手难易度 |

        【事实】以上为赛事页公布的满分 100 分权重，来源 https://www.mec.me/en/hackathon/harbor 。建议产品同学把评分框架直接对齐这五项。

        
- **赛制：** 全球线上；2–5 人组队，全员完成 ME ID 进阶认证；每队一份作品；四赛道统一排名，每队只拿一个最高名次奖。已有项目可参赛，但只评本次新增部分（以 commit 标注）。代码不必开源，私有仓库需开放审查权限
- **硬门槛：** 至少一项可体验的核心功能运行在 ME Network 上；须提交 ME 上的合约、交易或调用记录（或 Rollapp 运行与 Hub 接入信息）
- **四个赛道：** 鏈上金融與交易（借贷、交易与做市工具、信用评估、可验证的金融流程）；消費級產品與支付（大众应用与游戏、支付分账订阅、无感体验）；開發者工具與基礎設施（开发部署工具、Rollapp 构建注册、链上数据可视化）；AI 與信任基礎設施（可验证身份与 AI 智能体、数据授权管理、AI 内容溯源存证）
- **奖金：** 总奖池 100,000 USDT，9 个名额：一等奖 1×40,000；二等奖 1×30,000；三等奖 2×10,000；优秀项目 1×4,000、1×3,000、3×1,000。另有 Grant 与生态扶持机会。Demo Day 后 15 个工作日内发到队长 ME ID 绑定钱包
- **提交物（全英文）：** 项目说明（目标用户、问题、核心功能、ME 接入方式）；代码仓库与最终 commit；3–5 分钟 Demo 视频（英文讲解或字幕）；在线体验入口或本地运行说明；ME 执行记录
- **赞助方偏好：** 【事实】博客称「尤其鼓励探索 MEC 的实际应用场景」，支付、结算、激励、价值流转与产品自然结合的作品更易脱颖而出；也鼓励跨赛道组合。ME 主网已 EVM 兼容，支持 Solidity 与 WASM 双虚拟机 https://www.mec.me/en-US/developer-blog/me-network-goes-evm-compatible-embracing-the-ethereum-ecosys
- **可用 ME 能力：** 【事实】ME ID：DID + SBT 真人证明 + 隐私可验证凭证 https://meta-earth.gitbook.io/white-paper/ecosystem-projects/me-id-decentralized-digital-identity-system/me-id-solution-identity-credential-model ；ME Pass 钱包与开放平台；JS SDK（钱包、MEC 转账、ME ID 查询、EVM/WASM 合约）https://github.com/openmetaearth/meta-earth-js-sdk ；Rollapp 以 ME Hub 为结算层 https://github.com/openmetaearth/openroll 。博客称链上真实用户即将突破 900 万

        
| 节点 | UTC | 北京时间（UTC+8） |
| --- | --- | --- |
| 开放报名 | 2026-11-16 02:00 | 11-16 10:00 |
| 技术 Workshop（ME 接入、Hub 部署、Rollapp 注册） | 2026-11-23 | 11-23（已过，可看回放） |
| 报名信息修改截止（赛事页 FAQ，是否顺延未说明） | 2026-11-27 15:59 | 11-27 23:59 |
| 报名截止（已延期，官方 X 11-26 确认） | 2026-11-29 15:59 | 11-29 23:59 |
| 作品提交截止 | 2026-12-21 15:59 | 12-21 23:59 |
| 作品评审 | 2026-12-24 | 12-24 |
| Demo Day 与颁奖 | 2027-01-15 06:00–08:30 | 01-15 14:00–16:30 |

        【推断】从今天到提交约 24 天，MVP 必须收敛在 1 个核心流程 + ME 上可查的链上记录。出席 Demo Day 不影响评审。

      

## 2. 赛道趋势（近 3 个月）

        
> **趋势结论**
>
> 【推断】三条线交汇在「信任层」：资产在上链（RWA），操作者在变成 AI（Agent），监管在要求身份与权限（KYA）。ME 手里最稀缺的牌是 ME ID 真人身份，最适合切的是「Agent 与用户的身份、权限、信用」，而不是再做一个交易所。

      

## 3. 标杆拆解对比

{bench === "hl" && (
          
| 项目 | 规模数据（日期·来源） | 增长/活跃数据（日期·来源） |
| --- | --- | --- |
| Hyperliquid | TVL 73.3 亿美元（11-27，DefiLlama API）；OI 93.2 亿美元，24h 永续成交 83.2 亿美元，占链上永续 50%（11-26，castlelabs.io/research/hyperliquid） | 30 日收入 8,010 万美元（11-26，同上）；Q3 日均交易者 65,161（cryptobriefing.com/hyperliquid-record-daily-traders-q3-2026）；52 个账户贡献 61% 成交（11-03，alearesearch.io） |
| Ondo | 代币化资产 AUM 40 亿美元，持币地址 32.48 万（11-24，dune.com/markets/rwa/ondo） | Global Markets 8.37 亿美元，30 日 -10.8%（11-27，rwatracker.app）；460+ 股票与 ETF 代币（11-25，ondo.finance/blog） |
| Ethena | USDe 流通 49.2 亿美元（11-27，DefiLlama 稳定币 API） | 10 月供应减少 3.6 亿美元；11 月反弹主要来自单个 Aave 循环借贷 Safe 铸造 3.62 亿（alearesearch.substack.com） |
| Pendle | TVL 7.95 亿美元，30 日 -24.9%（11-27，DefiLlama） | Boros 资金费率价差市场 OI 峰值 3.097 亿美元（tokenpost.com/news/investing/60442） |
| Aster | TVL 7.16 亿美元（11-27，DefiLlama API） | 自报日成交 17–21 亿美元，外部无法验证；DefiLlama 曾以刷量疑虑下架其数据（theblock.co，2025-10） |
| Polymarket | 国际版 TVL 3.17 亿美元（11-27，DefiLlama） | 11 月截至 25 日成交约 20 亿美元，日均交易钱包 46,098，均低于 10 月（polycopy.app/polymarket-stats） |
| Virtuals / ElizaOS | Virtuals 10 月手续费 231,919 美元、留存收入 70,429 美元（DefiLlama，经搜索摘要，未直接核验） | ElizaOS 基金会 8 月收缩，代币无收入模型，框架仍开源（hoge.gg） |

        )}
        {bench === "ondo" && (
          
| 项目 | 它解决什么 | 增长引擎 |
| --- | --- | --- |
| Hyperliquid | 自建 L1 上的链上订单簿永续，CEX 级体验与自托管 | HIP-3 让外部团队上架股票、商品、Pre-IPO 永续，补上传统市场休市时段 |
| Ondo | 把美债、美股与 ETF 代币化，卖给美国以外的投资者，7×24 铸造赎回 | 多链分发（10 条链）+ 钱包渠道（如 Tangem）+ 作为 DeFi 抵押品 |
| Ethena | 以现货 + 空永续的基差交易生成合成美元 USDe 与收益 | 资金费率为正时的收益，叠加借贷循环 |
| Pendle | 把收益拆成本金 PT 与收益 YT，可做固定收益或押注收益率 | 积分与空投预期、新上线的资金费率交易 Boros |
| Aster | BNB 生态的永续 DEX，高杠杆与隐藏订单 | 激励与高杠杆 |
| Polymarket | 链上预测市场，用 UMA 乐观预言机结算 | 大事件与短周期加密市场 |
| Virtuals / ElizaOS | AI Agent 发行平台与开源 Agent 框架 | Agent 代币交易费，而非 Agent 付费服务 |

        )}
        {bench === "others" && (
          
| 项目 | 未解决的问题（【事实】附来源） | 对我们的启发（【推断】） |
| --- | --- | --- |
| Hyperliquid | 周末盘口脱离预言机引发连环强平（bitquery 10-19）；鲸鱼集中；香港证监会警示（11-18） | 休市风险与合规身份是缺口 |
| Ondo | 美加不可用；赎回需 KYC，二级买家可能被拒（docs.ondo.finance）；Global Markets 30 日 -10.8% | 资格可见、可验证的访问层 |
| Ethena | 供应增长依赖少数循环借贷者（alearesearch.substack.com） | 收益来源与风险需要可解释 |
| Pendle | PT/YT 概念对新手门槛高，Reddit 新手讨论频繁（reddit.com/r/defi/comments/1tbu036） | AI 解释与风险可视化 |
| Aster | 11-15 新账户推高标记价 15%，触发强平与 ADL，未宣布补偿（dexwatch 11-20） | 可验证的风控与事件留痕 |
| Polymarket | 九个大户主导 UMA 争议投票（predictionmarkets.org）；裁员（CoinDesk 11-12） | 一人一票的裁决层 |
| Virtuals / ElizaOS | 有用户、少有付费客户（ownyourmind 10-21） | Agent 要先有可信身份与可验证产出 |

        )}
        

        TVL 或流通规模，美元，2026-11-24 至 11-27 拉取（DefiLlama、Dune）。口径不同，只看量级。

      

## 4. 用户痛点清单

> The SK Hynix perp's order book fell 6.4% in ten minutes. The oracle price it tracks fell 1.5%.

        
> My $60,000 position was suddenly liquidated after the price appeared to move by 2x due to what seems to be an oracle pricing issue.

        
> HIP-3 markets rely on custom oracle feeds—how does Entropy price funding if Nasdaq triggers a volatility halt?

        
> Is there any legal issue in buying and holding it then? Tax issues? Can they get seized or the wallet confiscated?

        
> So the referee is cheaper than the game.

        
> 一些用户正在将他们的金融账户登录凭证提供给代理。我建议不要给予个人代理此类访问权限，因为安全保障不足。

        
| 痛点 | 证据 | 类型 |
| --- | --- | --- |
| AI Agent 权限过大，被注入指令即可转走资金 | Grok × Bankrbot 被摩斯码提示注入转走约 15.5 万美元（2026-05，超出窗口）https://swarmproof.github.io/agent-postmortems/2026-grok-bankr-morse-wallet-drain/ | 【事实】 |
| 休市时段股票永续价格脱锚、强平连锁 | 4,380 万美元 25 分钟强平（bitquery） | 【事实】 |
| 资金费率不可预期 | Grvt 调查 56% 交易者因此放弃或平仓（CoinDesk 11-17）；HIP-3 上 COST 资金费率年化 -1026% https://x.com/Blockmetriclive/status/2125020484349907361 | 【事实】 |
| 刷量让 Agent 支付与 DEX 数据不可信 | x402 95% 来自单一 facilitator（chainward.ai）；Aster 数据被称黑箱 | 【事实】 |
| RWA 资格与赎回规则不透明 | Ondo 文档与 Reddit 困惑 | 【事实】 |
| 无抵押信用缺可靠身份，只能小额试水 | Priors 5–500 美元、Credifi 上限 3,000 美元 | 【推断】由额度上限反推 |
| Agent 项目缺真实付费客户 | ownyourmind 评测 | 【事实】 |

      

## 5. 机会点（内部打分已省略）

原画布按官方权重（技术 30、ME 应用 25、价值 20、创新 15、UX 10）做了内部初评，具体数字已从本公开仓库删除。下面保留 7 个机会点的用户、切入、证据与 MVP 描述，顺序沿用原稿编号（O1–O7）。当时的推荐结论见第 6 节。

### O1. AgentGuard：有身份、有边界的 AI 交易代理金库

- **赛道：** AI 与信任 + 链上金融
- **用户：** 想把交易或理财交给 AI、但不敢把私钥或 API 全权交出去的散户与小团队；以及需要合规留痕的机构试点方
- **切入：** Agent 绑定 ME ID 派生身份；用户在 EVM 合约里签一份授权策略（额度、标的白名单、杠杆上限、有效期、单笔上限），合约强制执行，越权即拒；每次决策的输入摘要与执行结果哈希上链，可回放审计；一键撤销
- **为何现在：** 【事实】香港金管局 11/2 启动 SAGE 项目，把 KYA（认识你的代理）列为四大范畴之一 https://www.hkma.gov.hk/gb_chi/news-and-media/press-releases/2026/11/20261102-4/ ；新加坡金管局 11/19 宣布制定 KYA 协议，并提醒用户不要把金融账户凭证交给代理 https://www.businesstimes.com.sg/zh-hans/companies-markets/mas-lays-groundwork-ai-agents-make-payments-manage-funds-proposed-safeguards ；Binance 自动化交易占比 3.14%，MCP 日调用一个月涨 8.8 倍 https://www.theblock.co/research/intelligence/binance-intelligence-agentic-finance-stack-437309 。【推断】监管与交易所都在补「代理权限层」，链上开放实现仍空缺
- **MVP：** 策略合约（Solidity，部署 ME EVM）+ ME ID 身份绑定 + 一个 LLM 交易 Agent（模拟盘或 ME 上的测试 DEX 池）+ 审计面板。Demo：Agent 正常下单 → 尝试超额被合约拒绝 → 用户撤销授权
- **与官方权重的贴合（定性，不含内部打分）：** 技术 30：合约 + Agent + 前端闭环可跑；ME 25：ME ID、EVM 合约、MEC 计费三处真实调用；价值 20：对应监管议程；创新 15：权限与留痕在链上强制；UX 10：一页式授权

### O2. ME ID 信用分 + 小额无抵押信用额度（人与 Agent 通用）

- **赛道：** 链上金融（信用评估赛道原题）
- **用户：** 有链上历史但缺抵押品的用户、做小额周转的商户与创作者、需要预付算力或 API 费用的 AI Agent
- **切入：** 用 ME ID 的一人一证（DID + SBT）解决无抵押借贷最大的女巫与多号违约问题；信用分由链上行为计算并以可验证凭证发放；资金池给出 5–500 美元级别的循环额度，按时还款即提额
- **为何现在：** 【事实】10–11 月出现多例信誉型无抵押借贷：Priors 给 ERC-8004 Agent 身份放 5–500 美元微贷 https://www.woofun.ai/en/news/detail/113842 ，Credifi 按 Ethos 分无抵押放款至 3000 美元 https://www.ethos.network/post/credifi-unsecured-loans-ethos-score ，Unlloo 10 月主网上线 https://www.unlloo.com/blog/unlloo-uncollateralized-loans-ethereum-mainnet-launch ；3Jane 的 Crypto Credit Lines 已转入维护模式 https://docs.3jane.xyz/backing/ccl 。【推断】需求被反复验证，但都缺一个可靠的真人或真 Agent 身份层，ME 恰好有
- **MVP：** 信用评分合约 + 凭证发放 + 借贷池合约（MEC 或测试稳定币）+ 借款/还款/提额前端。Demo：两个账户（有/无 ME ID 认证）得到不同额度，还款后提额
- **与官方权重的贴合（定性，不含内部打分）：** 赛道一原文点名「信用评估与链上信用应用」；ME ID 是 ME 最独特的能力，ME 应用分最好拿

### O4. MEC 计价的 Agent 按次付费结算 + 真实需求信誉

- **赛道：** 消费级支付 + AI 与信任
- **用户：** 卖数据、模型或 API 给 AI Agent 的开发者；需要按调用付费的 Agent 运营方
- **切入：** HTTP 402 风格的按次付费网关，用 MEC 结算；付款方须持 ME ID 派生身份，网关输出「去刷量后」的真实付费调用统计，给卖家一个可信的需求证明
- **为何现在：** 【事实】x402 在 Base 上 10 月的 22 倍增长中 95% 来自一家 facilitator 自己的钱包 https://chainward.ai/decodes/x402-one-platforms-own-volume ；Oct 27–Nov 25 有机成交仅 290,634 美元，平均单笔 0.0243 美元 https://agentgdp.io/gdp ；赛事博客明确鼓励在支付、结算、激励中体现 MEC 价值 https://www.mec.me/zh-TW/developer-blog/harbor-2026-a-total-prize-pool-of-100-000-usdt-build-the-nex 。【推断】机器支付的协议已有，缺的是「谁在真付钱」的可信度
- **MVP：** 网关中间件 + MEC 微支付合约 + 卖家看板（有机调用 vs 疑似刷量）。Demo：Agent 调用付费 API，MEC 自动结算，看板实时更新
- **与官方权重的贴合（定性，不含内部打分）：** ME 应用与 MEC 场景契合度最高；产品价值受 Agent 支付整体需求偏小拖累

### O5. 可验证 AI 投研：信号存证 + 事后绩效对账

- **赛道：** AI 与信任（内容溯源）
- **用户：** 付费订阅 AI 信号或 KOL 观点的交易者；想证明自己战绩的研究员与 Agent 开发者
- **切入：** 每条 AI 研报或交易信号在发布时把内容哈希与时间戳写上 ME；到期后自动与行情对账，生成不可篡改的战绩榜；订阅用 MEC 支付
- **为何现在：** 【事实】独立评测称 Agent 代币项目「有用户、少有付费客户」，Virtuals 收入主要来自代币交易而非 Agent 付费服务 https://newsletter.ownyourmind.ai/p/agent-tokens-have-users-few-have ；超过一半 Binance AI Pro 提示是让 Agent 搭建并运行策略 https://www.theblock.co/research/intelligence/binance-intelligence-agentic-finance-stack-437309 。【推断】信号市场的核心矛盾是战绩无法验证
- **MVP：** 存证合约 + 信号生成 Agent + 对账任务 + 战绩榜前端，两周内可完成
- **与官方权重的贴合（定性，不含内部打分）：** 技术风险最低；创新与价值中等，易与 O1 合并成审计模块

### O6. 一人一票的可验证裁决层（预测市场与链上争议）

- **赛道：** AI 与信任 + 链上金融
- **用户：** 预测市场与链上保险、对赌类应用的结算方；被大户投票左右结果的用户
- **切入：** 以 ME ID 认证的真人陪审团替代代币加权投票；AI 负责整理证据与生成裁决草案，陪审团投票，结果与理由上链
- **为何现在：** 【事实】报道称九个匿名大户主导 Polymarket 的 UMA 争议投票 https://www.predictionmarkets.org/nine-crypto-whales-dominate-polymarket-disputes-worth-billions/ ；Polymarket 11 月截至 25 日成交约 20 亿美元、低于 10 月 27 亿 https://polycopy.app/polymarket-stats ，并在投资人压力下裁员 https://www.coindesk.com/business/2026/11/12/polymarket-trims-workforce-under-investor-pressure-as-kalshi-surges-ahead 。【推断】痛点真实，但赛道热度在降，且需要自建一个市场来演示
- **MVP：** 争议提交 + AI 证据摘要 + ME ID 陪审投票合约 + 结算回调，演示一个迷你预测市场
- **与官方权重的贴合（定性，不含内部打分）：** ME ID 用法独特；工程量偏大，产品价值需讲清楚谁会接入

### O3. 休市时段 RWA 永续风险雷达与守护单

- **赛道：** 链上金融（交易工具）
- **用户：** 在 Hyperliquid HIP-3 等平台交易股票、商品永续的散户
- **切入：** 实时比对盘口价与预言机价、资金费率极值、周末流动性，给出风险分与预警；用户可在 ME 上订阅预警、托管条件止损规则
- **为何现在：** 【事实】10/17 周六晚 HIP-3 芯片股永续 10 分钟跌约 6%，25 分钟强平 4,380 万美元，同期预言机只跌 1.5% https://bitquery.io/investigations/hyperliquid-stock-perps-saturday-crash ；BRENTOIL 资金费率年化 -271% https://x.com/laevitas1/status/2108216578219065430 ；Grvt 调查中 56% 交易者因资金费率不稳定放弃或平仓 https://www.coindesk.com/zh/markets/2026/11/17/decentralized-exchange-grvt-makes-commodity-trading-more-predictable-with-stable-funding-perps 。【推断】需求最硬，但数据与交易都在别的链上，ME 接入深度难做足
- **MVP：** 读 Hyperliquid 公开 API 的风险引擎 + 预警前端 + ME 上的订阅与规则存证合约
- **与官方权重的贴合（定性，不含内部打分）：** 产品价值与 UX 高，但 ME 应用（25 分）是短板

### O7. 合规分层的 RWA 访问网关（ME ID 资格凭证）

- **赛道：** 链上金融
- **用户：** RWA 发行方与分销钱包；搞不清自己能否买、能否赎回的海外用户
- **切入：** 用 ME ID 发放地区与投资者资格的可验证凭证；RWA 代币转账与赎回合约按凭证白名单放行，用户提前看到「我能不能买、能不能赎」
- **为何现在：** 【事实】Ondo Stocks 不对美国、加拿大居民开放，赎回须满足 KYC，二级市场买家也可能被拒绝赎回 https://docs.ondo.finance/ondo-stocks/eligibility https://docs.ondo.finance/ondo-stocks/secondary-market-restrictions ；Reddit 用户困惑在券商买到后是否合法、钱包会不会被冻结 https://www.reddit.com/r/Wealthsimple/comments/1uqf075/ondo_tokenized_stocks_dex/ （约 5 个月前，超出 3 个月窗口）。【推断】黑客松无法接入真实 RWA，只能用模拟资产演示
- **MVP：** 资格凭证合约 + 受限转账代币（ERC-3643 风格）+ 资格自检页面
- **与官方权重的贴合（定性，不含内部打分）：** ME ID 契合好；创新度一般，现有许可代币标准已覆盖大半

## 6. 推荐 Top 2 与定位草案

1. AgentGuard（85 分）。一句话定位草案：「让 AI 替你交易，但永远越不过你签下的那条线：ME ID 认证的 Agent 身份 + 链上强制的权限合约 + 可回放的操作存证。」英文：Give your AI agent a wallet, not your keys.
2. ME ID Credit（83 分）。一句话定位草案：「一人一证的链上信用：用 ME ID 真人身份解决无抵押借贷的女巫问题，给人和 Agent 发可循环的小额信用额度。」英文：Credit for verified humans and their agents, no collateral required.

        
> **组合建议**
>
> 【推断】两者可以合成一个产品：Agent 先通过 AgentGuard 获得受限授权，再凭主人的 ME ID 信用分拿到小额额度去付 API 或交易保证金。这样同时覆盖「AI 与信任」和「链上金融」两个赛道的关键词，并让 ME ID、EVM 合约、MEC 结算三项能力都有真实调用，对应 ME 应用 25 分。风险是范围变大，建议先把 O1 做完整，O2 作为加分模块。

      

## 7. ME ID / ME Network 开发者接口与可行性

> **结论：能做，用签名证明方案**
>
> 【推断】「ME ID 认证 → 合约强制执行 AI 代理权限」在 3 周内可以做出来。但 EVM 合约无法直接读取 ME ID：没有预编译合约，也没有 EVM 侧的注册表。推荐由我们的后端通过官方 REST 查询 ME ID 状态，签发 EIP-712 证明；合约用 ecrecover 验签后，写入链上的 MeIdGate 注册表，权限合约以此为前提。这就是产品同学提出的过渡方案，代码证据显示它也是目前唯一可行的路径。

        
| 项目 | 测试网（Beta） | 主网 | 依据 |
| --- | --- | --- | --- |
| 链类型 | Cosmos SDK + CometBFT 的 ME Hub，内置 Ethermint EVM（EVM 与 WASM 双虚拟机），Rollapp 以 Hub 为结算层 | 同左；EVM 已开启（enable_create 与 enable_call 均为 true，11-27 实测） | 【事实】github.com/openmetaearth/me-hub（x/evm 封装 ethermint） |
| Cosmos Chain ID | mechain_400-1 | me-chain（代码中 EVM 映射为 mechain_2404-1） | 【事实】RPC /status 实测；me-hub types/version.go |
| EVM Chain ID | 400（eth_chainId 返回 0x190，11-27 实测） | 2404（源码常量，未找到公开 RPC 实测） | 【事实】 |
| EVM JSON-RPC | http://118.175.0.249:8545（SDK 默认值）；HTTPS 可用 https://beta-hub-8545.explorer-testnet.me（实测返回 400，文档未列出） | 缺失：SDK 写明主网须自行配置 evmRpcUrl | 【事实】meta-earth-js-sdk src/config/define.ts |
| Cosmos RPC / REST | https://beta-hub-26657.explorer-testnet.me ；REST https://beta-hub-1317.explorer-testnet.me 或 http://118.175.0.249:1317 | RPC http://118.175.0.247:16657 ；REST http://118.175.0.247:11317（仅 HTTP 裸 IP） | 【事实】me-docs rollup.md、SDK 配置；11-27 实测块高：测试网 5,541,920，主网 16,262,206 |
| 水龙头 | 存在（官方 X 称升级期间暂停 faucet），网址未找到；文档写联系官方获取测试币 | 不适用 | 【事实】https://x.com/MetaEarthDevs/status/2125808255213634040 ；me-docs js-sdk.md FAQ |
| 区块浏览器 | 存在（同一条 X 帖），网址未找到 | https://explorer.mec.me（ME Scan） | 【事实】me-docs account-model.md |

        
- **ME ID 在哪：** 【事实】ME ID 是 ME Hub 上的 Cosmos 原生模块 x/did 与 x/kyc：DID 记录含 did、address、status、regionId、kycLevel、subAccount 等字段；KYC 凭证只能由 Global DAO 登记的 KYC issuer 签发，开发者不能自己发。https://github.com/openmetaearth/me-hub/tree/main/x
- **EVM 能否直读：** 【事实】不能。ME 的 ethermint 分支只启用 geth 标准预编译（GetPrecompiles 仅返回 Berlin 等内置集合），me-hub 的 x/evm 只是薄封装，没有 EVM hooks 或 DID 预编译。https://github.com/openmetaearth/ethermint/blob/main/x/evm/vm/geth/precompiles.go
- **官方 SDK / API：** 【事实】JS SDK 的 sdk.identity 提供 getMeIdByAddress、getMeIdByDid、getMeIdBySubAccount、bindSubAccount；对应 REST 为 /metaearth/did/did?address=、/metaearth/did/didInfo?did=、/metaearth/kyc/QuerySubAccountDidResponse?sub_account=。11-27 在主网与测试网实测均正常返回（不存在时返回 DID not found）。另有 Python SDK。https://github.com/openmetaearth/me-docs/blob/main/docs/development-guides/developer-guide/js-sdk.md
- **EVM 地址怎么挂到 ME ID：** 【事实】MsgCreateSubAccount 允许已 KYC 且 DID 状态为 ACTIVE 的主账户绑定一个 ETH 子账户，链上校验两者出自同一私钥；每个 ME ID 只能绑定一个子账户。绑定后可按 EVM 地址反查 ME ID。来源 me-hub x/kyc/keeper/msg_server_sub_account.go
- **官方推荐集成方式：** 【事实】文档与 SDK 只给出「链下通过 REST/SDK 查询 + 绑定子账户」这一条路；ME Pass Open Platform 目前只是应用提交与上架入口，未公开登录或授权 API。https://www.mec.me/en-US/developer-blog/me-pass-open-platform-is-now-live-calling-all-developers-to 。【推断】官方未提供链上读取方案，签名证明属于我们自己的设计
- **MEC 在合约里：** 【事实】MEC 是 EVM 原生币（evm_denom = umec），用 msg.value 和 payable 收付，不是 ERC20；链上未见 erc20 模块，如需 ERC20 形态要自部署 WMEC 包装合约。umec 精度为 8 位（链上 denom metadata 实测 exponent 8），合约里 1 MEC = 1e8 个最小单位，不是 1e18；而部分脚本注释写的是 1e18，两处矛盾

        

        
        【事实】11-23 的 Workshop 回放在 YouTube、X 与 OpenBuild 等公开渠道均未找到，可能只在开发者社群内发布。本节结论基于 GitHub 文档仓库 https://github.com/openmetaearth/me-docs 、me-hub 与 ethermint 源码（11-26 有提交）、JS SDK，以及 11-27 对公开接口的只读实测。

      

## 信息源与缺口


原始画布：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/5b710767-0faf-438c-b2c9-18e290ade689

---

## English

# First-round market scan: on-chain finance × AI

**Status:** Research, still useful as background. The two recommendations (AgentGuard and a ME ID credit line) have since been fully merged into AegisME. **Window:** 27 Aug–27 Nov 2026. **Canvas:** 27 Nov 2026, Asia/Shanghai.

## Official rules (facts)

HARBOR tracks include on-chain finance and AI (or both). Official weights: technical implementation 30, ME application 25, product value 20, innovation 15, UX 10. Demo video 3–5 minutes, English. Registration was extended to 29 Nov 2026, 23:59 Beijing time. Submission 21 Dec. Materials must be in English. Team size 2–5 with advanced ME ID certification.

## Trends (inference on top of cited facts)

In the three months before 27 Nov 2026, public discussion concentrated on: agent permission failures and KYA (MAS / HKMA); unsecured or lightly collateralized crypto credit experiments that stayed small and often lacked a strong identity layer; RWA access and redemption rules that stay off-chain; and bot/agent trading volume growing faster than on-chain enforcement. These are reasons to look at identity-bound agent limits and identity-bound credit — not a claim that a market is empty.

## Opportunity list

Internal numeric scores are omitted. The seven ideas (O1–O7) are described in the Chinese section: AgentGuard; a ME ID credit line; a MEC pay-per-call gateway; verifiable AI research logs; a verifiable adjudication layer; an RWA off-hours risk radar; and an RWA eligibility gateway. At the time, the recommendation was to prioritize AgentGuard and the ME ID credit line. Both are now merged into AegisME.

## ME Network constraints (facts)

ME Network is Cosmos SDK + Ethermint EVM. Testnet chain ID 400, London EVM (go-ethereum v1.10.26). MEC has 8 decimals. EVM contracts cannot read ME ID; the official query path is the JS SDK or REST. One ME ID binds one EVM sub-account. A backend EIP-712 attestation is therefore required, and should be disclosed honestly.

Treat later plan/product docs as authoritative for the current design.
