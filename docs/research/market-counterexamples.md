# 行业事实核查与反例 / Industry fact check and counterexamples

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.

- **状态 / Status:** 调研备查 / Research
- **来源画布 / Source canvas:** [动态链上信用新产品：行业事实核查与反例](https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/52139c49-b300-4d41-861f-e5a4f153e018)
- **日期 / Date:** 2026-11-27（Asia/Shanghai）

## 中文

# 动态链上信用新产品：行业事实核查与反例

核查 Leader 方案里的 10 条行业事实，并检验“面向普通用户的低抵押信用仍是空白”这一判断。核查时间 2026-11-27（Asia/Shanghai，UTC+8），每条附来源；“推断”另行标注。

**本页是调研，不是当前产品定位。** 「市场空白」不得写成既成事实。当时的判断是：**部分成立**——面向普通用户的低抵押 / 无抵押信用仍然稀缺且常常做不下去，但并不是「没有人做过」。

## 核查结果概览

10 条声明里没有整条错误的，但有 3 处需要改口径：Aave 的 155.9 亿美元不是 V4 的 TVL；Masa 更名 Gopher 是 2025 年，不是 2024 年；FinanceFeeds 2026-11 的盘点讲的是超额抵押借贷，不是链上信用。

## 任务 A：行业事实逐条核查

| # | 声明 | 结论 | 正确事实 / 说明 | 来源 |
| --- | --- | --- | --- | --- |
| 1 | ERC-8498 原帖存在 | 已证实 | 标题 ERC-8498: Namespaced State Transitions for SBTs，作者 Born2Win，2026-11-12 13:47（UTC+8）发帖，共 8 帖。帖子自称 pre-ERC 讨论、无审计实现。给出的 /4 链接指向第 4 楼（3956ray 提问隐私目标），不是主帖。论坛上看不到共同作者名单，“负责人是共同作者”无法从公开页面核实。 | https://ethereum-magicians.org/t/erc-8498-namespaced-state-transitions-for-sbts/30361 |
| 2 | Aave V4 2026-03 上线、TVL 约 155.9 亿美元 | 部分属实 | 上线日期正确：2026-03-30 Ethereum 主网。155.9 亿美元来自 FinanceFeeds 2026-11-06 文章，指的是整个 Aave 截至 10-30 的 TVL，不是 V4。DefiLlama 2026-11-27：Aave 全部版本约 169.9 亿美元，V3 约 157.0 亿美元，V4 只有约 9.2 亿美元。 | https://aave.com/blog/aave-v4-live-ethereum ; https://defillama.com/protocol/aave-v4 |
| 3 | S&P Global 2026-10 报告 The Engine of DeFi | 已证实 | S&P Global 与 S&P Global Ratings 联合发布，2026-10-13。属于思想领导力报告，不是评级。报告称截至 2026-09 Aave TVL 约 192 亿美元，主要在 V3。 | https://www.spglobal.com/en/research-insights/special-reports/defi-aave-lending-protocol-analysis |
| 4 | Maple 转向超额抵押（syrupUSDC）及 Q3 2026 更新 | 已证实 | Q3 2026 更新于 2026-10-15 发布：AUM 47 亿美元，在贷 17 亿美元，借款人是机构。syrupUSDC 透明度页显示抵押率 155.7%。 | https://maple.finance/insights/maple-q3-ecosystem-update ; https://maple.finance/transparency/products/syrupusdc |
| 5 | TrueFi 2026 年更名 Brila | 已证实 | TFIP-41 于 2026-03-05 提出，03-24 链上执行，TRU 迁移为 BRLA。转型方向是 NFT 金融（Cyan）、RWA 信贷金库和 Elara，不是重新做信用分。 | https://forum.truefi.io/t/tfip-41-truefi-reconstitution-and-transition-to-brila/2883 |
| 6 | Cred Protocol 300–1000 分、2026-11 发布 Andromeda 1.5、支持 AI Agent 按次付费 | 已证实 | 三点均有官方出处：Andromeda 1.5 发布于 2026-11，新增 7 年负面记录过期和原因码；Agent 可通过 x402/MPP 按次付费，1 CU = 0.01 美元，查一次分数 1 CU。 | https://credprotocol.mintlify.app/model-release-notes ; https://credprotocol.com/use/agents |
| 7 | Spectral 2023 年底放弃信用分转 AI Agent | 部分属实 | 方向基本对，时间不精确。2023-12-08 Spectral 宣布 Machine Intelligence Network（转向 ML 推理），AI Agent 产品 Syntax 在 2024-03 才推出。没有找到正式宣布停止 MACRO 分的公告，只确认它现在已不提供。 | https://spectralfinance.substack.com/archive ; https://blog.spectrallabs.xyz/spectralsyntax/ |
| 8 | Masa 2022 做 SBT 信用分、2024 转 Gopher、2026-03 宣布关停 | 部分属实 | 2022-08 测试网上线 Soulbound 身份和信用分（主网 2023-01），正确。更名 Gopher 是 2025-09-17，不是 2024，这一点有误（目前只有二手来源）。2026-03-25 宣布公司清算，正确；当时 Gopher 产品暂时仍可用。 | https://www.businesswire.com/news/home/20220822005553/en/ ; https://tg.me/gopherannouncements/1109 ; https://meme-insider.com/en/article/masa-network-rebrands-to-gopher-ai-introducing-goai-token |
| 9 | RociFi 1–10 分 NFCS、2024 并入 Gora | 已证实 | NFCS 分数 1 到 10，1 为最好，以 Polygon 上的代币持有；2024-04 与 Gora 合并，ROCI 换成 GORA。 | https://medium.com/@rocfi/rocifi-x-gora-groundbreaking-merger-pioneering-the-defi-risk-oracle-0bc5517e748c ; https://www.unlloo.com/blog/on-chain-credit-scores-compared |
| 10 | FinanceFeeds 2026-11 链上信用盘点 | 部分属实 | FinanceFeeds 2026-11 确实有一篇盘点，即 2026-11-06 的 6 Top Crypto Lending Protocols in 2026，但讲的是 Aave、Morpho 等超额抵押协议，没有提到信用分。没有找到 2026-11 的链上信用专题；相关的低抵押文章发于 2025-11-19。 | https://financefeeds.com/6-top-crypto-lending-protocols-in-2026/ ; https://financefeeds.com/under-collateralized-loans-crypto/ |

## 任务 B：反例对照

| 项目 | 用户 | 抵押 / 额度 | 身份 | 现状 | 说明了什么 |
| --- | --- | --- | --- | --- | --- |
| Credifi | 美国零售个人；另有 Ethos 路线面向匿名用户，Credifi Zero 面向 Agent | 无抵押；标准路线最高 2 万美元，Ethos 1800+ 最高 3000 美元 | 软查征信 + 银行核验；Ethos 路线无 KYC，只看声誉分 | 在运营。Ethos 路线 2026-08-27 上线，截至 10-05 首批零违约；放款总额未公开 | https://credi.fi/ ; https://www.ethos.network/post/credifi-unsecured-loans-ethos-score |
| Credit（Divine Research） | 零售个人，小额 | 无抵押，额度最高升到 1000 美元 | World ID（Orb 验证） | 累计 149 万笔、92.2 万人，但 DefiLlama 在贷仅约 65 万美元。正在关停：金库须在 2026-12-31 前取回，产品迁到阿根廷的 Casia App，改用本地身份证 + 银行核验 | https://credit.cash/ |
| 3Jane | 最初是美国加密“商户”（个人交易者）；现在主要资金给金融科技贷款方 | 无抵押信用额度 | VantageScore（zkTLS）+ Plaid 银行数据 + Cred、Blockchain Bureau 分 | 个人信用额度已进入维护模式，只能还款、不再新发；TVL 约 9923 万美元。Bitquery（2026-11-18）指 1.283 亿美元借给 3Jane 自控 Safe | https://docs.3jane.xyz/backing/ccl ; https://bitquery.io/investigations/3jane-usd3-one-borrower |
| Union | 任何有人担保的地址 | 社交担保：担保人质押稳定币 | 成员担保关系 | 在运营，规模很小：在贷约 7 万美元 | https://defillama.com/protocol/union-protocol |
| Unlloo | 个人钱包，P2P 众贷 | 无抵押，出借人自选 | 0–1000 聚合分（Human Passport、Ethos、zScore 等） | 2026-10-21 主网上线，记录最短 | https://www.unlloo.com/blog/uncollateralized-crypto-lending-protocols-compared |
| Wildcat | 仅注册法人，主要是做市商和机构 | 无抵押 / 部分准备金 | KYB；协议本身不做信用评估 | 在运营；DefiLlama 在贷约 1.43 亿美元 | https://defillama.com/protocol/wildcat-protocol |
| Maple | 机构 | 超额抵押（syrupUSDC 155.7%） | 机构尽调 | AUM 47 亿美元，在贷 17 亿美元（Q3 2026） | https://maple.finance/insights/maple-q3-ecosystem-update |
| Huma | 持牌支付机构、贸易融资 | 应收账款 / 支付流 | 机构准入；零售只能做存款方 | TVL 约 3.62 亿美元 | https://docs.huma.finance/products/huma-2.0/overview |
| Goldfinch | 线下放贷机构 | 无抵押（已停） | Backers 尽调 | 2026-06 起维护模式 | https://www.unlloo.com/blog/uncollateralized-crypto-lending-protocols-compared |
| Coinbase Borrow（Morpho） | 零售个人 | 超额抵押：约 32 亿美元 BTC 担保约 17 亿美元 USDC | Coinbase KYC | 超过 9 万用户；2026-11-17 扩展到纽约 | https://morpho.org/stories/coinbase ; https://www.theblock.co/news/business/2026-11-17-coinbase-borrow-new-york-morpho-442842 |
| Gearbox、Arcade、Teller | 零售 | 账户内杠杆或 NFT 抵押，本质仍有足额担保 | 无 | DefiLlama TVL 分别约 1646 万、15 万、72 万美元 | https://defillama.com/protocol/gearbox |

（表中最后一列如为链接，即为来源。）

## 判断：“普通用户低抵押信用仍是空白”——部分成立

已有 Credifi、Priors、Unlloo、Credit（Divine）、3Jane（后转入维护）等项目做过无抵押或低抵押尝试。它们的共同限制往往是：额度很小、身份层偏弱或可换钱包、信用状态难以降级、或同一额度可被重复使用。因此「还有没被解决的具体问题」可以谈，但「没人做过 / 市场空白」不能说。

## 定位启示

后来并入 AegisME 的要点：真人身份带来违约成本、信用状态可以暂停或降级、每次动用额度需要可核销的一次性授权。出资人是否愿意只凭 ME ID 状态出钱，当时没有证据，需要访谈验证。

原始画布：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/52139c49-b300-4d41-861f-e5a4f153e018

---

## English

# Industry fact check and counterexamples

**Status:** Research. **Date:** 27 Nov 2026, Asia/Shanghai.

Ten industry claims from an early credit-product brief were checked. None was wholly false; three needed wording fixes: Aave’s US$15.59 billion figure is not Aave V4 TVL; the Masa → Gopher rename is 2025, not 2024; a Nov 2026 FinanceFeeds recap is about over-collateralized lending, not on-chain credit.

The claim that “low-collateral credit for ordinary users is still a blank market” is only **partly** true. Credifi, Priors, Unlloo, Credit (Divine), 3Jane (later in maintenance) and others have tried unsecured or lightly collateralized products. Typical limits: small size, weak or swappable identity, credit state that does not downgrade, or lines that can be reused. It is fair to talk about specific unsolved problems. It is not fair to say “nobody has done this” or “the market is empty.”

Implications later absorbed into AegisME: real identity that makes default costly, a state that can be suspended or downgraded, and a one-time authorization for each draw. Whether funders will advance funds on ME ID state alone was unproven and reserved for interviews.

Tables (claim verdicts and peer comparison) are in the Chinese section, with sources.
