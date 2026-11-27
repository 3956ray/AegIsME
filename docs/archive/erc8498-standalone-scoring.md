# 【已归档】ERC-8498 独立产品评估 / Archived standalone ERC-8498 evaluation

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.

- **状态 / Status:** 已归档（已被完全合并方案取代） / **Superseded**
- **来源画布 / Source canvas:** [ERC-8498 动态信用 · 机制拆解与可行性评分](https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/d616bf93-453c-4215-ab99-00eb53f387b8)
- **日期 / Date:** 2026-11-27（Asia/Shanghai）

## 中文

# ERC-8498 动态信用 · 机制拆解与可行性评分

> 独立新产品（不并入 AgentGuard）的产品侧评估：ERC-8498 机制与社区反馈、在 ME Network 上的可行性、官方五项权重的内部评估（数字已省略）、测试网最小档 MVP 与 Demo。

> **已并入 AgentGuard，详见 v4；原内容保留作参考。**
>
> 【事实】用户已拍板把信用额度和 ERC-8498 完全并进 AgentGuard，对外是一个产品；本页「独立新产品」的定位不再使用。详见 `product/product-direction-v4.md` 与 `plan/full-merge-execution-plan.md`。

      

      

## 结论

> **能做，但只能做测试网最小档。** 当时的内部规划分低于「AgentGuard + 信用额度」方案（具体数字已省略）。用户后来选择完全合并，本页定位作废。
>
> 【推断】叙事按 Leader 定的口径：做过的人都没做成规模，我们补上他们没解决的三件事，即真人身份带来违约成本、信用状态可以降级、额度在链上核销。Tagline 暂定 "Earn it. Lose it. Spend it once."（来源：）。第三件事（核销）不在 ERC-8498 核心 ABI 里，MVP 用我们自己的合约实现。

        
- 【事实】ERC-8498 是 Draft：EIP 创建于 2026-11-13，ERCs PR #2171 于 2026-11-26 00:37（北京时间）合并，官方作者栏只有 XiaoHai (@XiaoHai67890)。来源：[EIP] ；[PR]
- 【事实】核心只有 3 个方法加 1 个事件；一次性权益核销、私有呈示、恢复都写明在核心之外。来源：[EIP]
- 【推断】分差主要来自技术实现（Draft 标准 + 自建核销 + EVM 版本兼容）和产品价值（出资人是否愿凭 ME ID 状态出钱尚未验证）。
- 【推断】「负责人是共同作者」在公开页面上看不出来，本页不作为事实使用；Leader 正在向负责人确认。来源：[LEADER]

      

## 打分（官方五项权重）

内部五项加权对照表已删除（本仓库为公开仓库）。定性结论：独立做 ERC-8498 动态信用，在黑客松周期内只能做到测试网最小档；技术上受 London EVM 与 Draft 接口约束，产品价值证据弱于已有代理权限叙事，体验也偏「状态演示」而非完整交易闭环。

## ERC-8498 现状与楼层

| 楼层 | 作者 · 时间（北京时间） | 内容 |
| --- | --- | --- |
| #1 | Born2Win · 11-12 13:47 | 主帖上半：动机、三件事分离（历史记录 / 当前是否满足应用要求 / 权益是否已消费）、核心接口、命名空间与权限、有效期。自称 pre-ERC discussion，无审计实现 |
| #2 | Born2Win · 11-12 13:47 | 主帖下半：私有呈示、一次性权益（nullifier）、恢复、示例、待讨论问题 |
| #3 | Born2Win · 11-13 13:28 | 发布参考实现 v0.1（XiaoHai67890/evolving-sbt），51 项测试通过；写明未实现逐条撤销、一次性消费、迁移、恢复，历史上限 32 条 |
| #4 | 3956ray · 11-13 17:10 | 问隐私目标：只隐藏经历，还是连用的是哪枚 SBT 都隐藏（Leader 给的 /30361/4 链接指向这一楼，不是主帖） |
| #5 | Born2Win · 11-18 14:16 | v0.2：新增可选的撤销登记合约和入场合约，演示撤销后入场被拒、同一账户不能二次入场；核心仍是 3 个方法 1 个事件 |
| #6 | Born2Win · 11-18 14:34 | 回复 #4：会议场景两者都要隐藏，考虑按活动作用域的 nullifier |
| #7 | JintolChan · 11-25 04:04 | 回复 #4：核心不保证隐私或不可关联，范围只是命名空间状态发现与按策略校验的状态转移 |
| #8 | LAnH · 11-25 04:05 | 质疑复杂度、前驱同步、gas 成本，并给出分层校验、transitionId 绑定、批量更新等建议；截至本页时间作者未回复 |

        【事实】以上均来自原帖全部 8 楼： 。ERCs PR #2171 于 2026-11-26 00:37（北京时间）合并，EIP 状态 Draft，requires 165、712、721、5192： ；

      

## 机制拆解

- **接口：** 【事实】IEvolvingSBT：`stateOf(tokenId, namespace)` 读当前状态头；`policyOf(namespace, policyId)` 读不可变策略定义与实时开关；`applyTransition(change, evidence, authorization)` 提交转移；事件 `StateTransitioned`。interfaceId 0x86ebb4d4。来源：[EIP]
- **命名空间与状态：** 【事实】状态按 (chainId, 合约, tokenId, namespace) 定位；每个命名空间有 revision、stateRoot、policyId、status、validUntil。状态只能 Uninitialized→Active，Active↔Suspended，任一→Revoked，Revoked 为终态；到期不自动改状态。来源：[EIP]
- **谁能写入：** 【事实】由策略 profile 定义，可用签名、授权的链上调用方或证明；转发交易本身不授予权限；初始化须持有人同意；持有 SBT 不等于能给自己加记录。参考实现分 issuer（追加与更正）和 controller（初始化、暂停、恢复、到期），用 EIP-712 签名并支持 ERC-1271。来源：[EIP] ；[THREAD]/3
- **防重放与防双花：** 【事实】每次转移必须匹配前驱 revision 与状态哈希，带 deadline 和策略 epoch；暂停再恢复会让旧授权失效。同一经历按 experienceId 去重，不会重复计分。来源：[EIP]
- **核销：** 【事实】一次性权益核销不在核心里：规范写明应用须自行用作用域 nullifier 等方式记录消费；transitionId 不是 nullifier。参考实现 v0.2 只有活动入场的一次性准入示例，没有额度核销。来源：[EIP] ；[THREAD]/5
- **明确不提供：** 【事实】不建立「一人一凭证」，也不阻止共享密钥或卖号；去重只在 profile 的标识范围内有效。这正是 ME ID 要补的地方。来源：[EIP]

      

## 与已有 SBT 标准的区别

| 标准 | 已有能力 | 与 ERC-8498 的关系 |
| --- | --- | --- |
| ERC-5192 | 锁定检测与转账限制 | 【事实】作为基础并要求永久锁定 |
| ERC-5484 | 发行时双方同意、固定销毁权限、发行后元数据不变 | 【事实】不定义命名空间转移；符合 8498 不代表符合 5484 |
| ERC-5727 | 半同质 SBT，发行、撤销、到期、恢复等扩展 | 【事实】已支持动态；8498 增加同一凭证内多个独立版本化命名空间和前驱绑定的转移接口 |
| ERC-7508 / 7208 | 动态属性与权限 / 数据与管理逻辑分离 | 【事实】可作实现底座，但不规定证据校验的转移协议 |
| ERC-4973 | 账户绑定代币，铸造需双方同意，可解绑 | 【推断】8498 正文和讨论帖都没有对比 4973；4973 同样只表达静态「有或没有」，承载不了降级和核销 |

        来源： 的 Relationship to existing standards 一节；ERC-4973 一行为产品侧推断。

      

## 社区质疑与作者回应

| 质疑或建议 | 楼层 | 回应 |
| --- | --- | --- |
| 隐私目标是否包括隐藏所用 SBT | #4 | 作者 #6：会议场景要隐藏；JintolChan #7：核心不保证隐私，属于呈示 profile |
| 状态机加命名空间加策略太重，易出实现偏差 | #8 | 未回复 |
| 前驱绑定让前端和索引器同步负担变大 | #8 | 未回复 |
| 复杂校验 gas 偏高，建议分层与批量 | #8 | 未回复；作者 #5 给过本地 gas 数据（两条贡献入场约 10.6 万 gas） |

        【推断】讨论只有 3 位非作者参与，社区验证有限；路演只能说「基于 Draft ERC 的核心接口」，不能说「标准背书」。来源： ；

      

## 在 ME Network 上的可行性

- **me.staking 数据从哪来：** 【事实】ME EVM 只有以太坊标准预编译，没有 staking 预编译；ME Hub 用自定义 wstaking 模块，REST 路径含 `/metaearth/wstaking/delegation/{delegator_addr}` 与 `/metaearth/wstaking/fixed_deposit_amount_by_meid/{account}`。【推断】后端按这两个接口查询后作为 issuer 签名写入；接口尚未实测。来源：https://github.com/openmetaearth/ethermint/blob/main/x/evm/vm/geth/precompiles.go ；https://github.com/openmetaearth/me-hub/blob/main/proto/metaearth/wstaking/query.proto
- **defi.repay 怎么写入：** 【推断】借还发生在我们自己的测试网合约里，规范允许「授权的链上调用方」作为写入方，因此还款记录可由该合约直接写入，不经后端。逾期需要一笔 keeper 交易触发暂停，因为时间流逝不会自动改状态（规范原文）。来源：[EIP]
- **信任集中在哪：** 【推断】签名后端同时是 ME ID 证明和 me.staking 证据的签发方，是最大信任点；暂停与恢复由 controller（建议团队多签）掌握；defi.repay 由借还合约写入，信任最小。规范自身写明签名型策略依赖被认可的签发方。来源：[EIP] ；[LEADER]
- **已知约束：** 【事实】ME ID 在 x/did、x/kyc，EVM 无预编译，只能后端核验后 EIP-712 上链；一个 ME ID 绑定一个 EVM 子账户；测试网 chainId 400；MEC 8 位小数。来源：[LEADER]
- **12-21 前能做出什么：** 【推断】测试网最小档（见下节）。第一周先验证两件事：参考实现按 london 目标重编后能否在 ME 测试网部署；wstaking REST 能否按地址查到质押数据。

      

## MVP（测试网最小档）与 Demo

          

### 必做

- 后端核验 ME ID，签 EIP-712 证明；MeIdGate 验签并按 DID 去重
- 测试网铸造并绑定 1 枚 ERC-8498 SBT（复用参考实现核心）
- 2 个命名空间：me.staking（后端签）、defi.repay（借还合约写）
- 1 次升档：解锁 100 test MEC 免押额度
- 自建 CreditLedger 核销：按 DID 作用域 nullifier，用一次即核销，二次使用被拒
- 1 次降级：逾期后暂停 defi.repay，额度冻结
- 轻量诊断界面：AI 只解释状态变化，不参与授信

          

### 可选

- 扩展场景：抵押率 150% 降到 115%（Demo 只一句话带过）
- 参考实现 v0.2 的撤销登记合约
- 自然语言意图生成交易，由用户签名

          

### 不做

- 真实放贷、计息与清算
- ZK 私有呈示
- 主网部署与 Aave、Morpho 接入
- 把 AI 诊断算作收入点
- AI 自主授信或自动执行

        
        
> **一句话 Demo**
>
> 同一个 ME ID：质押达标后解锁 100 test MEC 免押额度，用一次就在链上核销、第二次被拒；没有 ME ID 的新钱包拿不到额度；逾期一次，额度命名空间被暂停、档位降级。对应 Earn it. Lose it. Spend it once.

        

        【推断】MVP 与 Demo 已对齐市场定位草案：

      

## 商业假设与产品价值证据

- 【推断】Leader 已定：第一付费方是协议和金库，按查询收费；利息不算近期收入；普通用户通过小额免押或更低抵押率间接受益。
- 【事实】Cred Protocol Pro 档 249 美元/月；x402 按次查一次评分 0.01 美元。只是价目表，没有订阅数或收入数据。来源：https://credprotocol.com/pricing ；https://credprotocol.com/use/agents
- 【事实】Credifi 给 Ethos 1800 分以上的用户开最高 3,000 美元额度，年息 10%，期限三个月；Ethos 称截至 2026-10-05 首批零违约（原文保留 so far）。来源：https://credi.fi/ ；https://www.ethos.network/post/credifi-ethos-score-loans-zero-defaults ；销售 credit-layer-demand-v1.md
- 【事实】Credit（Divine）2024-12 至 2026-11 向约 92.2 万人发放 149 万笔无抵押贷款，首笔贷款 90 天后仍有 53% 未还；12-31 转去阿根廷，改用身份证加本地银行。来源：销售 credit-demand-v1.md
- 【事实】有社区评论认为只凭钱包画像放贷不明智（出自一条 Reddit 评论，不是出资人原话）。来源：销售 credit-demand-v1.md
- 【事实】DefiLlama 无抵押借贷分类 TVL 约 1.16 亿美元，大头是 3Jane（约 9,923 万美元，商户预付加链下评分）。来源：销售 credit-layer-demand-v1.md
- 【事实】Spectral 已转型，RociFi 2024 年并入 Gora；Masa 2025-09 更名 Gopher（二手来源），2026-03 宣布准备关停。【推断】所以不做成又一个分数，而是可降级、可核销的状态。来源：[LEADER] ；[MARKET]
- 【事实】AI 诊断和自然语言执行没有找到独立付费证据，MVP 中只作体验层。来源：销售 credit-layer-demand-v1.md

      

## 最大的 3 个风险

1. 出资人是否愿意凭 ME ID 状态出钱（最大未知数）。【推断】Credit 53% 首贷未还说明匿名放贷撑不住，Credit 自己也转向身份证加本地银行；出资人是否接受 ME ID 状态作为放款依据，目前没有任何证据。应对：访谈加 1–2 场出资人或策展人，接在 AgentGuard 场次后面，答卷分开记；约人由负责人决定，我们不对外联系。
2. 标准与实现成熟度。【事实】ERC-8498 是 Draft，核销不在核心 ABI，参考实现没有额度核销，#8 的复杂度与同步质疑未获回复。【推断】核销合约是自写未审计代码；参考实现需从 cancun 降到 london 目标才能上 ME EVM，第一周必须实测。
3. 信任集中在签名后端。【推断】ME ID 证明和 me.staking 证据都由我们后端签发，规范写明签名型策略依赖签发方可信；路演主动说明，并给出签名有效期、按 DID 去重、密钥轮换、撤销上链和多签路线图。另需注意：「共同作者」未经公开证实，路演前不使用。

      

## 来源

销售报告 credit-layer-demand-v1.md 与 credit-demand-v1.md 未公开链接，以销售在群内贴出的内容为准。


原始画布：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/d616bf93-453c-4215-ab99-00eb53f387b8

---

## English

# Archived: ERC-8498 as a standalone product

**Status: superseded.** On 27 Nov 2026 the user chose to merge the credit line and ERC-8498 fully into the AgentGuard product (now AegisME). This page’s “standalone new product” framing is no longer in use.

The earlier conclusion was: it can be built, but only as a testnet-minimum MVP. Internal planning scores (omitted here) were lower than the AgentGuard + credit-line option. Constraints that remain relevant to the merge: the Draft interface may change; consumption is application-defined; the reference implementation must be retargeted from Cancun to London; ME ID must be attested by a backend; do not claim co-authorship (the public author field shows XiaoHai) or a market gap; say “built on the draft ERC-8498 interface.”

Mechanism, community questions, MVP scope and the three main risks are kept in the Chinese section for reference.
