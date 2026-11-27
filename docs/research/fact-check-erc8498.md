# ERC-8498 信用方案核实报告 / ERC-8498 fact check

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.

- **状态 / Status:** 调研备查 / Research
- **来源画布 / Source canvas:** [ERC-8498 信用方案核实报告](https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/c7684069-0f06-44fa-94d3-ae1d57836c96)
- **日期 / Date:** 2026-11-27（Asia/Shanghai）

## 中文

# ERC-8498 信用方案核实报告

> **编辑注：** 本报告撰写时，仍把 ERC-8498 信用当作独立新产品来核查。用户随后已决定并入 AegisME（原 AgentGuard）。下列核实结论、风险和建议仍然有用，但「独立参赛产品」的定位已作废。

> 把草稿当成独立新产品，按一级来源核查 28 条主张，并只按 HARBOR 官方评审标准评估可行性。核实截止 2026 年 11 月 27 日（北京时间）。

## 核实结论

> **方向可以做成独立参赛产品，但不能按现稿直接上路演。**
>
> 草稿的主线清楚：用 ME ID 给身份加上违约成本，用 ERC-8498 做可升级、可降级、可核销的小额信用状态，AI 只做诊断和语言意图。这一套和 HARBOR 的“信用评估”、“可验证身份与 AI 智能体”赛道对得上。但草稿把市场说成“依然空白”、把 Draft ERC 说成“协议级标准背书”，还把 Aave V4 和 Morpho 的架构混在一起。这三处若不改，评委一追问就会伤可信度。

        共核查 28 条主张。草稿里提到的 3–5 分钟 Demo 影片规划没有贴进来，本报告无法评估演示脚本。

        

      

## 逐条核实表

| claim | verdict | fact | source |
| --- | --- | --- | --- |
| ERC-8498 Ethereum Magicians 讨论帖存在，标题为 Namespaced State Transitions for SBTs | 已证实 | 帖子存在。Born2Win 于 2026-11-12 分两帖发表讨论（表示这是 pre-ERC discussion）。给出的 /30361/4 是 3956ray 的跟帖，不是开篇帖。 | https://ethereum-magicians.org/t/erc-8498-namespaced-state-transitions-for-sbts/30361 |
| ERC-8498 已把历史记录、动态有效性、权益核销三者彻底解耦，并作为可用的协议级标准 | 部分属实 | 讨论帖确实区分了 Accepted historical records、当前是否满足应用要求、某项 entitlement 是否已被消费。但正式 EIP 核心只规范 stateOf、policyOf、applyTransition；权益核销、私有呈示和恢复明确写在核心 ABI 之外。参考实现 v0.1 也尚未实现 one-time consumption。现状是 Draft，不是已定稿标准。 | https://eips.ethereum.org/EIPS/eip-8498 |
| 提案已进入 Ethereum Magicians 讨论，并已提交 ERCs 仓库 | 已证实 | EIP 创建于 2026-11-13，标注为 [DRAFT]。ethereum/ERCs PR #2171 于 2026-11-25 合并，标签为 s-draft。官方作者栏仅 XiaoHai (@XiaoHai67890)。参考实现仓库为 XiaoHai67890/evolving-sbt，Born2Win 在 11-13 的 3 楼公布该仓库。社区讨论不多，已见 3956ray 询问隐私目标。 | https://github.com/ethereum/ERCs/pull/2171 |
| 这份标准是草稿作者与朋友一起提出的 | 未找到证据 | 官方 EIP 作者栏只有 XiaoHai (@XiaoHai67890)一人。讨论帖开帖人是 Born2Win，3 楼公布了 XiaoHai 的仓库，两个账号可能是同一人，但公开材料里没有第二作者姓名。路演中若要称“联合作者”，需先补到官方作者栏，或改口径说“参与了讨论草稿”。 | https://eips.ethereum.org/EIPS/eip-8498 |
| HARBOR 评分为技术实现 30% + ME 接入深度 25%，合计 55% | 已证实 | 官方权重是：技术实现 30、ME 应用 25、产品价值 20、创新程度 15、用户体验 10。草稿将官方名称“ME 应用”写成“ME 接入深度”，与官方解释“对 ME Network 能力的接入深度与运用程度”一致，但应使用官方名称。 | https://www.mec.me/zh-TW/hackathon/harbor |
| MetaEarth 拥有庞大的真实链上用户基数 | 部分属实 | 这是公司自述，非第三方审计的活跃链上用户数。2026-06-23 官方通稿：验证用户超过 630 万；2026-10-21 官方 BEACON 公告：全球 ME ID 用户超过 850 万；HARBOR 开发者博客写“接近 900 万真实链上用户”。应写“官方公布的验证 ME ID 用户数”，并附日期。 | https://www.mec.me/en-US/govern-announcement/metaearth-hackathon-2026-beacon-is-live-taiwan-s-ready-compe |
| Aave V4 于 2026 年 3 月上线 | 已证实 | 2026-03-30 在 Ethereum 主网启用，采用 Hub-and-Spoke 架构，首批三个 Liquidity Hub，并带保守型上下限。 | https://aave.com/blog/aave-v4-live-ethereum |
| Aave TVL 超 155 亿 / 155.9 亿美元 | 部分属实 | FinanceFeeds 引用的 155.91 亿美元是 2026-10-30 的 Aave 全协议 TVL，不是 V4 单独数字。DefiLlama 于 2026-11-27：Aave 合计约 170.2 亿美元，V4 约 9.16 亿美元。S&P 报告里 2026 年 9 月的数字是约 192 亿美元，以 v3 为主。草稿把这个数字写在 V4 之后，容易误导读者认为是 V4 的 TVL。 | https://defillama.com/protocol/aave |
| S&P Global 2026 年 10 月发布了 The Engine of DeFi: Inside the Aave Crypto Lending Protocol | 已证实 | 报告存在，发布于 2026-10-13，标明不是评级行动。 | https://www.spglobal.com/en/research-insights/special-reports/defi-aave-lending-protocol-analysis |
| S&P 指出：2025 年 10 月闪崩中 Aave 靠机械清算扛住冲击，这也证明 DeFi 仍高度依赖超额抵押、资本效率受限 | 部分属实 | 报告写到 2025-10-10 flash crash：随后 24 小时内超过 200 亿美元杠杆仓位被清算（这一句讲的是市场层面，不必全是 Aave）；Aave v3 的清算峰值出现在 2025 年 2 月、2025-10-10 和 2026 年 2 月。报告确认清算机制在压力测试中表现出韧性，且通篇讲的是超额抵押模型。但“资本效率受限”是草稿的推断；S&P 另一处还写 Aave 让 DeFi 更加 capital efficient。 | https://www.spglobal.com/en/research-insights/special-reports/defi-aave-lending-protocol-analysis |
| Maple 现已转为超额抵押机构借贷，并有 syrupUSDC与 KYC/KYB | 已证实 | 借款人文档写明：担保、超额抵押的机构信贷；入驻须完成 KYC/KYB 和信用审查。syrupUSDC 存在，Q3 2026 更新也提到其收益。 | https://docs.maple.finance/maple-for-borrowers/introduction |
| Maple 采用 24 小时抵押品监控 | 部分属实 | 这是误译。Maple 做的是 24/7/365 实时监控；触发追保后，借款人有 24 小时补足抵押品。不能写成“24 小时监控”。 | https://maple.finance/insights/yield-generation-underwriting-and-risk-management |
| Maple Q3 2026 生态更新可用来佐证从无抵押彻底回归超额抵押 | 部分属实 | 文章存在，2026-10-15 发布，回顾 10-13 的季报会，讲的是 AUM 47 亿美元、贷款余额、syrup 收益等。它并不讲 2022 年后的无抵押转型。转型应引自借款人文档或更早的公司说明，不要用这篇季报作为佐证。 | https://maple.finance/insights/maple-q3-ecosystem-update |
| TrueFi 于 2026 年更名为 Brila | 已证实 | TFIP-41 提议 TrueFi reconstitution and transition to Brila。Cred Protocol 2026-11-23 文章写：治理提案于 2026 年 3 月执行，迁至 Brila。Brila 文档与令牌 BRLA 均已上线。 | https://forum.truefi.io/t/tfip-41-truefi-reconstitution-and-transition-to-brila/2883 |
| TrueFi 早期靠 TRU 质押者投票加内部信用模型审批贷款 | 已证实 | 早期 stkTRU 可对单笔无抵押贷款投票；后来 V3 增加了治理批准的内部信用模型（0–255 分）。 | https://medium.com/trust-token/truefi-v3-credit-model-new-asset-support-a7cf73a37270 |
| Cred Protocol 分数为 300–1000，Andromeda 1.5 于 2026 年 11 月发布 | 已证实 | 分数范围 300–1000 自 Andromeda 1.0（2024-12）就已确定。Andromeda 1.5 确实在 2026 年 11 月发布，主要增加了 7 年不利信息台账窗口与最多 4 条 key_factors 原因码。 | https://credprotocol.mintlify.app/model-release-notes |
| Andromeda 1.5 带 6 维度因子解释 | 部分属实 | 六个因子（Borrowing History、Wallet Composition、Wallet Health、Interactions、Trust、New Credit）从 Andromeda 1.0 起就有。1.5 没有新增“6 维度解释”，而是增加了最多 4 条逆向操作原因码（R01–R11）。 | https://credprotocol.mintlify.app/model-release-notes |
| Cred Protocol 支持 AI Agent 按次付费调用，并以 B2B 风险 API 为生，不自己放无抵押贷款 | 已证实 | 官方 Agents 页面：可通过 MCP、REST，或用 x402 / MPP 按次付 USDC，无需账号。一次评分 1 Cred Unit（$0.01）。产品定位是给借贷方和 Agent 用的评分与屏查 API。 | https://credprotocol.com/use/agents |
| Spectral MACRO Score 于 2023 年底放弃信用分，全面转向 AI Agent | 部分属实 | Cred Protocol 2026-11-23 盘点写道：公司从 2023 年底转向链上 AI Agent；查验时 MACRO 应用和文档已不可访问，但没有找到正式下线公告。Syntax 于 2024 年 3 月公开亮相。路演中应写“转向 AI Agent，MACRO 已不可访问，未见正式废止声明”。 | https://credprotocol.com/blog/onchain-credit-and-reputation-scores-compared |
| Masa 2022 年尝试灵魂绑定信用分，结合链上历史与用户授权的链下数据 | 已证实 | 多源记载一致。Cred Protocol 还写道：其在 Celo 测试网上的首个信用分令牌由 Cred Protocol 的分数驱动。 | https://credprotocol.com/blog/onchain-credit-and-reputation-scores-compared |
| Masa 于 2024 年转向 AI 数据网络，并定名为 Gopher | 部分属实 | 2024 年转向 AI 数据网络有多源支持。Gopher 这个名称出现得更晚，二手资料常写作 2025 年重新品牌。不要把 2024 年转型和 Gopher 命名写成同一件事。 | https://credprotocol.com/blog/onchain-credit-and-reputation-scores-compared |
| Masa 于 2026 年 3 月宣布逐步关停（winding down） | 部分属实 | Cred Protocol 于 2026-11-22/23 核对后写道：3 月公告频道称公司正准备 wind down。搜索可见 2026-03-25 Gopher Announcements 帖。本次核实没有完整读到该公告原文，应附二手来源，或再找原帖后再引。 | https://credprotocol.com/blog/onchain-credit-and-reputation-scores-compared |
| RociFi 铸造 1–10 分的不可转让信用 NFT（NFCS），并于 2024 年并入 Gora | 已证实 | NFCS 为不可转让 ERC-721，分数 1–10（1 最优、10 最差）、2024 年 3 月与 Gora 宣布合并。公告未说清分数和贷款池的后续安排。 | https://www.gora.io/blog-post/gora-announces-merger-with-rocifi |
| Health Factor = Σ(抵押品价值 × 清算阈值) / 总债务，跌破 1 触发清算 | 已证实 | 与 Aave 官方公式等价。官方也写作 (抵押品总价值 × 加权平均清算阈值) / 总借款价值。HF < 1 可被清算。 | https://aave.com/help/borrowing/liquidations |
| Morpho Blue 采用隔离市场，并有外部风控策展人 | 已证实 | Morpho Blue 市场是单抵押、单借款资产的隔离市场；独立策展人管理的 vault 负责配置流动性与风险参数。 | https://financefeeds.com/6-top-crypto-lending-protocols-in-2026/ |
| 2026 年 3 月上线的 Aave V4 和 Morpho Blue 一并转向隔离市场与外部风控策展人 | 错误 | 这是两套不同的架构。Aave V4 是 Hub-and-Spoke：流动性集中在 Liquidity Hub，Spoke 自带抵押品、风险参数和清算规则。隔离市场加外部策展人是 Morpho 的模型。且 Morpho Blue 上线早于 2026 年 3 月。 | https://aave.com/blog/aave-v4-live-ethereum |
| FinanceFeeds 于 2026 年 11 月发布了行业盘点，记有 Aave V4、Morpho Blue、Compound V3 | 已证实 | 文章《6 Top Crypto Lending Protocols in 2026》于 2026-11-06 发表。写明 Aave V4 于 2026-03-30 上线，截至 2026-10-30 的 Aave TVL 为 155.91 亿美元；并讲了 Morpho Blue 隔离市场与策展人，以及 Compound V3（Comet）按基础资产分市场。 | https://financefeeds.com/6-top-crypto-lending-protocols-in-2026/ |
| 面向普通用户的低抵押/信用分层金融，以及 AI Agent 的链上风控边界，依然是空白 | 错误 | 这一市场并非空白。3Jane 曾向美国加密用户和 AI Agent 发放无抵押 USDC 额度，但 CCL 已进入关停维护；Credifi 仍在做无担保小额借款；Wildcat 为验证法人开设隔离的低抵押市场；Gearbox 有 Credit Account（仍是健康因子风控）；Zodiac Roles 与 ZeroDev session keys 能约束 Agent 权限；Cred Protocol 已提供 Agent 交易前评分。更准确的切口是：绑定真人身份、可升级可降级、额度在链上核销的小额信用，而且落在 ME Network 上。 | https://docs.3jane.xyz/backing/ccl |

## ERC-8498 到底是什么

这是一份 2026 年 11 月的 Draft ERC：给永久不可转让的 SBT（必须实现 ERC-721、ERC-165、ERC-5192）增加分命名空间、受策略约束的版本化状态迁移。每个 namespace 独立治理，stateOf 返回当前头部（revision、stateRoot、policyId、validUntil），applyTransition 必须绑定前驱状态和策略 epoch。

        
- **官方作者：** XiaoHai (@XiaoHai67890)
- **状态：** Draft；PR #2171 已于 2026-11-25 合并
- **核心接口：** stateOf、policyOf、applyTransition + StateTransitioned
- **核心之外：** 私有呈示、资格证明、权益核销、账户恢复
- **v0.1 边界：** 每个命名空间最多 32 条历史；未实现单次核销、独立撤销、策略迁移、恢复；不建立真人唯一性

        EIP 明确写道：锁定代币只保证拥有地址在存续期间不变，“不建立自然人唯一性”。这一点必须由 ME ID 补上，不能说成 ERC-8498 自己解决了女巫问题。

      

## 按 HARBOR 标准的评估

官方赛道明确包含“信用评估与链上信用应用”以及“可验证身份与 AI 智能体”。以下只按官方五项权重评估这份独立方案，不与其他候选方案比较。

        
**优点**
- 创新程度：ERC-8498 是 2026 年 11 月才进入 Draft 的真实提案，确实钉上“静态 SBT 找不到动态信用”这个短板。
- ME 应用：ME ID 能补上 ERC-8498 明确不提供的真人唯一性，和赛事对 ME 接入深度的要求一致。
- 产品口径收敛：不做纯无抵押大额放贷，只做可解释、可降级的小额额度，避开了 Maple / TrueFi / RociFi 曾经踩过的坑。
- 立论基础大部分经得起核查：女巫成本、静态 SBT、黑盒总分三个死穴，和行业史对得上。
**缺点 / 代价**
- 产品价值：链上信用产品多次折戟或转型，3Jane 的 CCL 现已关停。普通用户的付费意愿仍缺少公开证据。
- 创新若说成“市场依然空白”，评委可以用 Credifi、Wildcat、Cred Protocol、Zodiac、ZeroDev 当场反驳。
- 技术实现：三周里做不完完整 ERC-8498（ZK 呈示、多命名空间、核销账本、借贷副驾）。参考实现自身还没做核销。
- 事实错误会拖下可信度：Aave 与 Morpho 混淆、TVL 口径混用、“24 小时监控”误译、作者身份无法从公开作者栏证实。

      

## 关键风险

ME ID 不能被 EVM 合约直接读取。ME Network 是带 Ethermint 的 Cosmos SDK 链，ME ID 在 Hub 原生模块 x/did、x/kyc 中，EVM 里没有预编译合约。现有可行路径只有：后端核验 ME ID，签发 EIP-712 证明，合约验签后再绑定或铸造 ERC-8498 SBT。主网 EVM 链 ID 为 2404，MEC 精度是 8 位。

        

        
1. 信任集中在签名后端。这一点要写进路演答辩，不要说成合约直接读到了 ME ID。
2. 测试网新账户很可能没有 ME ID。Demo 可能要读主网队员的真实 ME ID，再把证明写进测试网合约。
3. ERC-8498 v0.1 不建立真人唯一性，也还没做 entitlement consumption。核销要自己写进应用合约，不能算在标准里已经现成。
4. 不做真实放贷和清算。三周里只能用测试网小额 MEC 演示授信、降级、核销。

      

## 建议

建议把这份方案当独立产品继续做，但先改事实、再收窄 MVP，再补上没有贴出来的 Demo 脚本。

        
- 定位改为：绑定 ME ID 的动态链上信用状态 + 轻量 AI 诊断。不要说“市场仍是空白”，要说清自己比 Masa / RociFi / 纯钱包评分多了什么：真人身份带来违约成本，状态可降级，额度在链上核销。
- MVP 只做最小档：后端核验 ME ID、测试网铸或绑定一枚 ERC-8498 SBT、一到两个命名空间（身份与额度）、一次升级或降级、一笔小额 test MEC 的核销，再加一个轻量诊断界面。不做 ZK、不做真实放贷、不上主网。
- ERC-8498 只说成 Draft 提案和讨论中的接口，不要说“核心技术标准背书”。作者身份只按官方作者栏来讲。
- 补齐 3–5 分钟英文 Demo。官方要求展示核心功能与使用流程，并有英文解说或字幕。建议必做：ME ID 绑定、额度生成、越权或重复兑付被拒、一次降级或核销。

      

## 草稿应改的地方

1. 删掉“依然是空白”。改成：已有多次尝试，但少有绑定真人身份、可降级且额度在链上核销的方案落在 ME Network 上。可以点名 3Jane、Credifi、Wildcat、Cred Protocol、Zodiac、ZeroDev。
2. 删掉“协议级标准背书”。改成 Draft ERC，PR 已合并，社区讨论仍有限。说清：核心标准的是状态迁移，权益核销要自己做在应用合约里。
3. 作者只写官方作者栏上的 XiaoHai (@XiaoHai67890)。若要称联合作者，先补到 EIP 作者栏。
4. 拆开 Aave V4 与 Morpho Blue：V4 是 Hub-and-Spoke；隔离市场加策展人是 Morpho。
5. TVL 写清口径与日期：Aave 全协议在 2026-10-30 为 155.91 亿美元，2026-11-27 约 170 亿美元；V4 单独约 9.16 亿美元。
6. Maple改成“7×24 小时监控，追保后 24 小时补足”。Q3 2026 更新不要用来佐证 2022 年的转型。
7. Andromeda 1.5 只写 FCRA 台账窗口和最多 4 条原因码。六个因子归于 Andromeda 1.0。
8. Spectral 写“转向 AI Agent，MACRO 已不可访问，未见正式废止公告”。Masa 的 Gopher 命名与 2026 年 3 月关停，要区分年份，关停宜附二手来源或补原帖。
9. ME 用户数写“官方公布的验证 ME ID 用户”，并标出 850 万（2026-10-21）这一数。评审项用官方名称“ME 应用”。
10. S&P 对 2025-10-10 闪崩的转述要写清：200 亿美元是市场层面的杠杆清算；“资本效率受限”标成推断，不要写成 S&P 原话。
11. 补上没有贴出来的 Demo 影片规划，并与上述 MVP 对齐。

      

## 主要来源


原始画布：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/c7684069-0f06-44fa-94d3-ae1d57836c96

---

## English

# ERC-8498 credit-scheme fact check

**Status:** Research, still valid as a source check. **Date:** 27 Nov 2026, Asia/Shanghai.

The Magicians thread “ERC-8498: Namespaced State Transitions for SBTs” exists (author Born2Win / XiaoHai, 12 Nov 2026). PR #2171 was merged; the document is a **Draft**. The core interface is `stateOf`, `policyOf`, `applyTransition`. One-time consumption is left to the application. The official author field on public pages shows XiaoHai; a “co-author” claim is **not** treated as fact in this archive.

The reference implementation (`evolving-sbt`) targets Cancun and must be retargeted to London for ME’s Ethermint (go-ethereum v1.10.26). EVM contracts cannot read ME ID, so a backend attestation is required. ME testnet is chain ID 400.

Risks highlighted in the check: Draft instability; trust concentrated in the signing backend; no public audit; entitlement consumption is application-defined, not part of the core interface. Recommendations that were later adopted in the full-merge plan include saying “built on the draft ERC-8498 interface,” putting ticket logic in the team’s own contract, and disclosing the backend.

The item-by-item table is in the Chinese section (claim / verdict / fact / source).
