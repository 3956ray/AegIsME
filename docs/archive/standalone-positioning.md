# 【已归档】独立信用产品定位草案 / Archived standalone credit positioning

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.

- **状态 / Status:** 已归档（独立产品定位已作废；部分口号被主方案吸收） / **Superseded**
- **来源画布 / Source canvas:** [动态链上信用新产品：差异化定位草案](https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/7c61fe6b-4285-4cc6-9ffb-207aa3d5eb4a)
- **日期 / Date:** 2026-11-27（Asia/Shanghai）

## 中文

# 【已归档】动态链上信用新产品：差异化定位草案

> **已归档。** 本页是把 ERC-8498 动态信用当作独立新产品时的定位草案。用户已决定将其并入现名 AegisME 的产品。部分口号（尤其是 “Earn it. Lose it. Spend it once.”）被主方案吸收为**信用模块小标题**，不再作为独立产品的主 tagline。

口径（当时）：做过链上信用的项目都没做成规模，我们补上它们没解决的三件事。真人身份带来违约成本，信用状态可以降级，额度用一次就在链上核销。已按 2026-11-27 的决定更新：主 Tagline 暂定、第一付费方改为协议和金库、Credit 数据作为核心论据、Demo 主画面改为免押额度核销。

## 反例拆解：4 个项目卡在哪里

### 3Jane

- **服务谁：** 美国加密用户（3Jane 称为 merchants，主要是收益农民），初期要求总验证资产超过 15 万美元；现在资金池主要供给美国金融科技贷款方。来源：https://www.3jane.xyz/reports/reintroducing-3jane
- **身份：** 用 Plaid 核验银行数据，通过 zkTLS 读取 VantageScore 3.0，再叠加 Cred Protocol 和 Blockchain Bureau 的分数。
- **违约成本：** 违约会被降分，还会被催收并进入美国法律追索（NPCL 拍卖）。这套约束依赖美国的法律和征信体系。
- **可解释性：** 用自有算法定额度，对外不公开逐项因子。
- **卡在哪里：** 个人信用额度（CCL）进入维护模式，只能还款，不再新借；官方没有公布停发原因。来源：https://docs.3jane.xyz/backing/ccl 。Bitquery（2026-11-18）指出，USD3 中有 1.283 亿美元借给了 3Jane 自控的 Safe。来源：https://bitquery.io/investigations/3jane-usd3-one-borrower
- **推断：** 依赖美国征信，覆盖不了非美国用户。资金方还在，只是转去给金融科技贷款方供资。

### Credifi

- **服务谁：** 美国零售个人：标准路线做征信软查和银行核验，最高 2 万美元；Ethos 1800 分以上的匿名用户最高 3000 美元；Credifi Zero 面向匿名用户和 AI Agent。来源：https://credi.fi/
- **资金：** Credifi 本身不是放贷方，资金来自链上借贷金库（贷款合同以金库合约地址标明债权人），官网没有写明出资人是谁。所以不能由此推出：出资人愿意只凭真人身份长期出钱。
- **违约成本：** Ethos 路线靠声誉约束。截至 2026-10-05，首批借款零违约（团队自报，原文写的是“so far”）。来源：https://www.ethos.network/post/credifi-ethos-score-loans-zero-defaults
- **可解释性：** 规则只有一个分数门槛（1800 分以上）。
- **没做什么：** 放款总额未公开。没有找到它对外输出可降级的信用状态，也没有找到跨协议一次性核销。（这两项是“未找到”，不等于没有。）

### Wildcat

- **服务谁：** 只服务注册法人（做市商、机构），不接个人。来源：https://www.unlloo.com/blog/uncollateralized-crypto-lending-protocols-compared
- **身份：** KYB（企业身份核验）。文档写明 “We do not underwrite anyone”，由出借人自行判断。
- **违约成本：** 靠法人身份、借贷协议和声誉约束。（推断）
- **规模：** DefiLlama 在贷约 1.43 亿美元（2026-11-27）。来源：https://defillama.com/protocol/wildcat-protocol
- **没做什么：** 不面向普通用户，也没有个人信用状态。

### Cred Protocol

- **服务谁：** 做 B2B 风控 API，客户是借贷方和 Agent，自己不放贷。来源：https://credprotocol.com/use/agents
- **价目（基准）：** Pro 套餐 249 美元/月（按年付；按月付 279 美元），每月 50,000 Cred Units；也可以用 x402 按次付费，查一个地址的分数 0.01 美元。这只是价目表，没有找到订阅数或收入。来源：https://credprotocol.com/pricing
- **身份：** 按钱包打分；女巫检测是单独付费项目。
- **可解释性：** 300–1000 分，6 个因子（Andromeda 1.0 起就有），1.5 版新增最多 4 条原因码。来源：https://credprotocol.mintlify.app/model-release-notes
- **没做什么：** 分数只读、不可消费，没有额度核销，也不绑定真人身份。


补充背景：Spectral 已转向 AI Agent，MACRO 分数无法访问，但没有找到正式下线公告。Masa 2022 年做过 SBT 信用分，2024 年转向 AI 数据网络，2025-09 更名 Gopher（二手来源），2026-03 宣布公司清算。RociFi 2024 年并入 Gora。这些项目都停在一个静态分数上。

## 为什么必须是真实身份：Credit 的数据

| 指标 | 事实 | 说明了什么 | 来源 |
| --- | --- | --- | --- |
| 借款规模 | 2024-12 至 2026-11：922,307 人借了 1,491,654 笔无抵押贷款 | 需求是真的 | https://writing.divine.inc/credit/ |
| 首贷违约 | 首贷到期 90 天后仍有 53% 未还；第二笔是 33%，第十笔是 12% | 匿名小额放贷，第一笔贷款的违约代价太低 | https://writing.divine.inc/credit/ |
| 首贷金额 | 中位数约 2 美元，99% 不超过 5 美元 | 只能靠极小额度来试探借款人 | https://writing.divine.inc/credit/ |
| 代扣回收 | 首贷的已还款中，81% 是通过代扣收回的：直接从借款人领取 World 月度 WLD 发放的同一钱包里扣 | 早期还款主要靠空投代扣，而不是借款人主动还 | https://writing.divine.inc/credit/ |
| 资金池 | 金库 TVL 2026-01-18 最高约 318 万美元，2026-11-27 约 8.7 万美元 | 匿名资金池撑不起规模（推断） | https://defillama.com/protocol/credit |
| 转型 | Credit 金库须在 2026-12-31 前取回；改做独立 App Casia，用政府身份证保证一人一户、走本地支付通道，阿根廷已上线 | 出资方和运营方都在向实名身份靠拢 | https://credit.cash/ ; https://writing.divine.inc/credit/ |

路演讲法（当时已定）：92 万借款人说明需求是真的；53% 的首贷未还率说明匿名放贷撑不住，这正是要用真实身份的理由。注意：Credit 用了 World ID，属于“一人一号”的匿名身份，并非完全匿名；它的违约代价主要靠极小额度和空投代扣来兜。

> anyone that would lend using on-chain profile only is not smart. Uncollateralised lending needs real KYC on the borrower and legal recourse to get back the loan in case of default.
>
> — r/defi 评论者 u/in_potty_training，2026-09-14（不是出资机构的表态）
> 来源：https://www.reddit.com/r/defi/comments/1wg5zl2/how_do_you_feel_about_uncollateralized_lending/

> Onchain credit is a meme until you solve for identity.
>
> — Aave 论坛 ZentraScore TEMP CHECK 第 4 楼，@litostarr，2026-05-11
> 来源：https://governance.aave.com/t/temp-check-integrate-zentrascore-on-chain-credit-oracle-to-enable-risk-tiered-lending-on-aave-v3/24892/4

ZentraScore 在同帖回应说“需要的是违约后果，不一定是身份”，路演时可以顺势回答：真人身份就是让违约后果无法通过换钱包绕开。

## 定位语句与商业假设

> **一句话定位（当时，独立产品）：** 做过链上信用的项目都没做成规模，我们补上它们没解决的三件事：真人身份带来违约成本，信用状态可以降级，额度用一次就在链上核销。

- **为谁（付费方）：** 借贷协议和金库，它们想给真人用户提供小额免押额度或更低的抵押率。
- **为谁（受益方）：** 完成 ME ID 认证的普通 DeFi 用户，以及替他们操作的 AI Agent。他们不付订阅费，好处是更低的抵押率或小额免押额度。
- **问题：** 链上信用绑在钱包上，换个钱包就能甩掉违约；信用凭证是静态勋章，不会降级；同一笔额度可以在多处重复使用。
- **品类：** 动态链上信用状态层，附带 AI 信用诊断。我们不放贷。
- **商业假设：** 协议和金库按次查询或订阅付费。利息不算近期收入；AI 诊断和自然语言执行没有经过验证的付费证据，不计入收入。参照价：Cred Protocol Pro 249 美元/月、x402 每个地址 0.01 美元，这只是价目表，没有订阅数据。来源：https://credprotocol.com/pricing
- **关键差异：** 一个 ME ID 对应一个可降级的信用状态，额度用一次就在链上核销。

英文版（当时）：For lending protocols and vaults that want to extend small credit to real people, [Product] is a dynamic credit-state layer on ME Network: one record per verified human, downgradable on default, and each credit line written off on-chain the moment it is used. Others tried wallet scores, static badges and reputation thresholds; none scaled. We fix the three things they left open.

注意：当前 AegisME 的主叙事已改为代理身份与权限，信用是其中一层；付费假设在路演第 8 页是订阅（交易者与终端），不是向协议卖征信查询。本页商业假设不要直接当提交材料使用。

## Demo 主画面（当时）

主画面：ME ID 核验后签名绑定，状态升档，解锁 100 test MEC 免押额度；用一次，额度就在链上核销；同一额度第二次使用被拒；模拟逾期后状态降级。这一段正好对应 Tagline 的 “Spend it once”。扩展场景只用一句话带过：同一状态也可以把抵押率从 150% 降到 115%。

（完全合并后，循环额度与「额度用一次就核销」的冲突已用「一次性借款券」解决，见执行方案。）

## 为什么是现在

- 事实：Credit 两年做了 149 万笔无抵押贷款，最后关停匿名资金池、改用政府身份证。需求已被证明，身份是缺的那一块。来源：https://writing.divine.inc/credit/
- 事实：ERC-8498 的 PR #2171 于 2026-11-25 合并，状态为 Draft，核心接口是 stateOf、policyOf、applyTransition。来源：https://github.com/ethereum/ERCs/pull/2171
- 事实：Aave V4 于 2026-03-30 上线，采用 Hub-and-Spoke 架构，每个 Spoke 自带风险参数。（推断）将来可以有接入外部信用状态的专用 Spoke。来源：https://aave.com/blog/aave-v4-live-ethereum
- 事实：3Jane 停发个人额度，Credit 将于 12-31 关闭金库，面向个人的方案正在退场。
- 事实：MetaEarth 官方公布认证 ME ID 用户超过 850 万（2026-10-21，公司自报）。

## 英文 Tagline（当时）

| # | Tagline | Subtitle | 状态 |
| --- | --- | --- | --- |
| 主选 | Earn it. Lose it. Spend it once. | Dynamic on-chain credit for verified humans, built on ME ID and the draft ERC-8498. | 2026-11-27 暂定采用（后改为信用模块小标题，不再当主 tagline） |
| 备选 | One human. One credit state. No double dipping. | Credit tiers that follow the person, downgrade on default, and write off on-chain. | 备用 |
| 备选 | Credit that remembers who you are. | Real identity makes default costly; state changes make credit honest. | 备用 |

## 差异化对照表

| 维度 | 本产品（测试网 MVP） | 3Jane | Credifi | Wildcat | Cred Protocol |
| --- | --- | --- | --- | --- | --- |
| 目标用户 | ME ID 认证的普通用户，以及替他们操作的 Agent | 美国加密用户（已停新发），以及金融科技贷款方 | 美国零售用户、Ethos 高分匿名用户、Agent | 注册法人 | 借贷方和 Agent |
| 谁付钱 | 协议和金库按次查询或订阅付费；利息不算近期收入 | 借款利息 | 借款利息（资金来自链上金库） | 借款利息 | API 订阅或按次付费 |
| 支柱 1：真人身份与防女巫 | 一个 ME ID 对应一个凭证；后端核验后签名上链，按 DID 去重 | Plaid、征信、zkTLS | 征信软查，或 Ethos 声誉分 | KYB | 按钱包打分，女巫检测另付费 |
| 支柱 2：状态模型 | 按命名空间区分状态，可升级、降级、暂停、撤销、到期（基于 ERC-8498 Draft 核心接口） | 3Jane Score，违约降分 | 分数门槛 | 无个人状态 | 只读分数 |
| 对协议的可解释性 | 公开每个命名空间的状态、生效规则和版本号 | 自有算法 | 单一门槛 | 出借人自行判断 | 6 个因子加原因码 |
| 支柱 3：防双花与核销 | 100 test MEC 免押额度只能用一次，在我们自己的合约里链上核销（不属于 ERC-8498 核心 ABI） | 未找到 | 未找到 | 不适用 | 不适用 |
| AI 的角色 | 解释额度变化、执行自然语言意图；不参与授信，也不算已验证收入 | 未找到 | Credifi Zero 支持 Agent 借款 | 无 | 供 Agent 调用评分 |
| 状态与规模 | 测试网，没有真实放贷 | 个人额度维护中，停发原因未公开 | 已运营，首批零违约，放款总额未公开 | 在贷约 1.43 亿美元 | 已运营 API，订阅数未公开 |

本产品一列是计划中的测试网 MVP，不是已上线的功能。“未找到”表示没有公开资料。

## 最大的未知数

> **出资人和策展人愿不愿意凭 ME ID 状态出钱**
>
> 目前没有证据。Credifi 的标准路线靠征信加银行核验，资金来自未具名的链上金库；3Jane 停发个人额度的原因也没有公开。所以不能暗示出资人会只凭 ME ID 放款。计划在访谈中加 1–2 场出资人或策展人，专门验证这一点。

## 诚实口径：能说与不能说

**可以说**

- Built on the core interface of the draft ERC-8498 (stateOf / policyOf / applyTransition).
- ME ID is verified by our backend, which signs an EIP-712 proof; the contract checks it and dedupes by DID.
- The write-off lives in our own contract on ME testnet; it is not part of ERC-8498's core.
- Credit (Divine) made 1.49M unsecured loans to 922K people; 53% of first loans were unpaid 90 days past due (Divine, Nov 2026).
- Others tried and never scaled; we fix three gaps they left open.（注意：这是「具体缺口」，不要说成「市场空白」。）
- Protocols and vaults pay per query or by subscription; interest is not near-term revenue.（当前主方案的近期收入假设已改为订阅，见路演第 8 页。）

**不能说**

- “ERC-8498 standard / 协议级标准背书”：它只是 Draft。
- 负责人是 ERC-8498 共同作者：官方作者栏只有 XiaoHai，Leader 正在确认。公开证据出现前不得使用。
- “没人做过 / 市场空白”。
- “出资方愿意凭 ME ID 出钱”：还未验证。
- “已上线放贷 / 主网运行 / 零违约”。
- “AI 诊断已有收入”，或“AI 决定授信”。
- 把 Reddit 评论说成“出资人表态”。
- “Trustless identity”：签名后端是信任点。
- 把 155.9 亿美元说成 Aave V4 的 TVL。

## 评委可能问的问题（当时口径，部分已被主方案 Q&A 取代）

1. ME ID 由你们的后端签名，这不是中心化吗？是，签名后端是信任点，我们主动说明。缓解：签名带有效期和 nonce，合约按 DID 去重，签名密钥可以轮换，撤销操作上链。路线图：多签，并向 ME 申请原生读取接口。
2. 真人借了钱不还怎么办？谁来承担损失？违约后该 ME ID 的信用状态降级，换钱包也躲不开。我们不放贷，损失由接入的金库承担；额度只做小额，并且一次核销。不承诺零违约。
3. 谁付钱？当时假设是协议和金库按次查询或订阅。当前主方案路演第 8 页改为交易者与终端的订阅。出资方愿不愿意凭 ME ID 出钱仍是未知数。
4. ERC-8498 还是 Draft，也没有核销功能，为什么基于它做？只用已合并的核心状态迁移接口，核销放在自己的合约里。

## 依据与来源

- https://writing.divine.inc/credit/
- https://defillama.com/protocol/credit
- https://credprotocol.com/pricing
- https://governance.aave.com/t/temp-check-integrate-zentrascore-on-chain-credit-oracle-to-enable-risk-tiered-lending-on-aave-v3/24892/4
- https://eips.ethereum.org/EIPS/eip-8498
- Masa 更名 Gopher（二手来源）：https://meme-insider.com/en/article/masa-network-rebrands-to-gopher-ai-introducing-goai-token
- 原始画布：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/7c61fe6b-4285-4cc6-9ffb-207aa3d5eb4a

---

## English

# Archived: standalone on-chain credit positioning

**Status: superseded.** This was the positioning draft when ERC-8498 dynamic credit was treated as a standalone product. The user later merged it into AegisME (formerly AgentGuard). “Earn it. Lose it. Spend it once.” survives only as a **small heading on the credit module**, not as the product’s main tagline.

The then-current one-liner: projects that tried on-chain credit never scaled; fix three things they left open — real identity that makes default costly, a state that can be downgraded, and a line that is written off on-chain when used. After the full merge, the conflict between a revolving line and “spend it once” was resolved by one-time tickets (the line revolves; the ticket is consumed).

Payer assumption on this page (protocols and vaults paying per query) is **not** the current live-pitch story. Page 8 of the current pitch is a subscription for traders and terminals, not a loan book.

Do not say: ERC-8498 is a finalized standard; the team are co-authors (unverified; public author field shows XiaoHai); “nobody has done this / the market is empty”; funders will lend on ME ID alone; the product is live lending / mainnet / zero defaults; AI diagnostics already produce revenue; a Reddit comment is a funder statement; “trustless identity”; Aave’s US$15.59 billion figure as V4 TVL.

Credit (Divine) figures cited as facts: 1.49 million unsecured loans to 922 thousand people; 53% of first loans unpaid 90 days past due (Divine, Nov 2026). Credit used World ID (one-person, still anonymous in an important sense).

The largest unknown remains: whether funders or curators will advance funds on ME ID state. That requires interviews.

Peer write-ups, Credit data, the comparison table and the “can say / cannot say” list are in the Chinese section.
