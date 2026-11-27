# AegisME 路演叙事与 Demo 旁白 / Pitch and demo narration

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.


- **状态 / Status:** 当前草稿 / Current draft
- **来源画布 / Source canvas:** [AgentGuard 路演叙事与 Demo 旁白（英文草稿）](https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/9570d578-d686-4bdd-8df4-ea88d8d8f934)
- **日期 / Date:** 2026-11-27，并纳入 11-28 Gemini 口径更新（Asia/Shanghai）
- **旁白词数 / Voice-over length:** 390 words

## 中文说明 / Chinese orientation

本页是路演与 Demo 的工作稿：禁讲清单、10 页英文叙事、第 8 页仅现场使用的商业稿、9 步 Demo 旁白（约 390 词，约 3:23，含约 30 秒链上等待）、提交用项目简介和答辩问答。

**更名说明：** 正文仍按起草时的产品名 AgentGuard 保留。提交与幻灯片下一轮修改时，应将产品名替换为 **AegisME**，主 tagline 建议改为 “Every AI agent has a human behind it. AegisME proves who.” 合约演讲时如已完成更名，再改口为 `AegisVault` / `ERC8498AgentRegistry` / `MeIdGate`。

旁白与幻灯片本身已是英文；中文以「中文注」和本节说明为准。


> **录制注意事项 / Recording note：** 第 6 步与第 7 步必须在同一张券的 10 分钟有效期内连续录完，否则第 7 步的 revert 会显示 expired，而不是 “ticket already spent”。Demo 参数（100 / 50 / 40 / 60 / 400 MEC、3x、10x、7 天等）只是演示值，不是市场数据。



## 口径与评审覆盖

> **禁讲清单与口径（内部讲稿备注，不上屏；已合并销售第 8 页清单）**
>
> 1. 签证明的是我们的后端，合约只验签：不说 "Your identity signs"、「用户自己签」或「合约直接读 ME ID」。
> 2. 细分权限当基础能力讲，不说「只有我们能做」。
> 3. HyprEarn 只讲「有未授权成交」，同时说明根因、受影响账户数、金额均未公布；不写成已确认损失，不补任何数字。
> 4. 引号里只放和原帖一字不差的原话；不用 "Prompt limits are suggestions"，r/AI_Agents 只引完整原句。
> 5. 不主动引用 XMR1；评委问起时用第 4 节备用答法（来源 Bitquery）。
> 6. 幻灯片上不点名 Prow，只说 one bot-trading platform's own docs；prowdex 链接只放来源附录。
> 7. 定价不说成市场成交价，只是假设。
> 8. ERC-8498 只说 "built on the draft ERC-8498 interface"：不提共同作者，不说标准背书，不说市场空白；核销和借款券在我们自己的 AgentCredit 合约里，未审计，只上测试网。
> 9. 信用模型统一为循环额度 + 一次性借款券：循环的是额度，一次性的是券，不说额度用一次就没了。合约只有 MeIdGate、AgentPolicy、AgentCredit 三个。真实放贷只进路线图。
> 10. 借款券：主人链下用 EIP-712 签，一笔借款一张（agent、金额上限、nonce、过期时间），合约只记已用 nonce；不提券数或券余额。券的 maxAmount 不超过单笔上限 50 MEC，draw 按两者较小值执行。按时还款 tier + 1 只改凭证状态，不改额度（Demo 额度始终 100），不说还款提高额度。三个落点：Earn it = 凭证面板 tier 标签 Tier 0→1；Spend it once = 第 7 步 nonce 重用的真实 revert；Lose it = 过 dueAt 且有未还余额后任何人可调用的 suspend 交易，哈希在仓库（keeper 只是调用者之一，不说 keeper 是暂停开关）。
> 11. 对外材料不写 ME 测试网区块 gas 上限；「一次借款交易不超过 500k gas」只作内部检查，不当路演卖点。
> 12. 不说「泄露的密钥借不到钱」/ "a leaked key can't borrow" 这类绝对说法，对外只用原句 "Without a fresh owner-signed ticket, a leaked agent key cannot borrow."；合约只保证 expiry ≤ 10 分钟。
> 13. 对外不报任何分数：内部自评不进幻灯片、旁白、答辩和简介。本公开仓库已删除相关数字。
> 14. 不说「不能预签多张券」或 owners never pre-sign：合约强制不了，只是前端在交易时才弹签名；对外只说券 10 分钟内过期。

        
| 评审项（权重） | 在哪一页或哪一步体现 |
| --- | --- |
| 技术实现 30 | 第 5、7 页；Demo 第 3–8 步：三个合约（MeIdGate、AgentPolicy、AgentCredit）加一笔 Hub 原生交易，都有交易哈希 |
| ME 应用 25 | 第 6 页整页；Demo 第 3、4 步：ME ID 经 SDK 查询、子账户绑定、按 DID 铸凭证、ME EVM 合约、MEC 额度 |
| 产品价值 20 | 第 2、3 页的证据；第 8 页客群、定价假设与验证计划（销售定稿） |
| 创新程度 15 | 第 4 页：别人管能做什么，我们证明替谁做；第 5 页：一次性借款券让泄露的密钥借不到钱；Demo 第 4、6–8 步 |
| 用户体验 10 | Demo 第 5 步一页授权、第 7 步可读的拒绝原因、第 8 步一键换代理 |

        Demo 中的 100、50、40、60、400 MEC、3x、10x、7 天、券 maxAmount 50 和每次一张券均为演示参数，不是市场数据。没有依据的数字一律标 [TBD]。

---

## 1. 路演叙事（10 页） / 10-page pitch

### 第 1 页 · AgentGuard

- Every AI agent has a human behind it. AgentGuard proves who.
- Verified humans. Bounded agents. Credit that follows the person.
- Tracks: AI & Trust Infrastructure + On-chain Finance. Built on ME Network.

中文注：封面：主 tagline 加副标题（已由 Leader 定稿），点明跨两个赛道、跑在 ME 上。

### 第 2 页 · The problem: agents trade for us, but nobody can see who they act for

- On Nov 14, 2026, HyprEarn reported unauthorized trades on a small number of Hyperliquid accounts that had approved its agent wallets. The agents could not withdraw. Root cause, number of affected accounts and losses were not disclosed.
- Limits that live in a prompt or on a server can be bypassed: \u201c"Never spend more than $50" in a system prompt is a suggestion. A policy check in the signing service is a rule.\u201d (r/AI_Agents). One bot service also documents that its limits are checked on its own servers.
- Users feel it too: \u201cyou do not know the trader you are copytrading\u201d (r/hyperliquid1).

中文注：【事实】HyprEarn 只讲「有未授权成交」，同时说明根因、账户数、金额均未公布。两条 Reddit 引文已逐字核对原帖。Prow 不点名，评委追问再给链接。

### 第 3 页 · Why now: regulators are asking who is behind the agent

- Hong Kong's HKMA launched Project SAGE on Nov 2, 2026, with Know-Your-Agent (KYA) as one of four focus areas.
- Singapore's MAS announced a KYA protocol on Nov 19, 2026, and warned users not to hand account credentials to agents.
- Agent trading is already real: automated trades were 3.14% of Binance volume in the week ending Oct 19, 2026 (Binance-commissioned research).

中文注：【事实】三条都有来源；Binance 数据来自其委托研究，需注明。标题去掉了引号，避免像在引用原话。

### 第 4 页 · What exists today: tools limit what an agent can do, not who it acts for

- Safe's Zodiac Roles and ZeroDev session keys already scope agents by contract, function, parameters, amounts and time windows. We build on the same idea; fine-grained permissions are table stakes.
- Hyperliquid's approveAgent supports an expiry (valid_until, up to 180 days) but has no per-asset, size or leverage limits.
- None of these bind an agent to a unique, verified human, or tie credit to that human.

中文注：【事实】前两条有文档。【推断】第三条是我们的差异化判断。不要说「只有我们能做细分权限」。

### 第 5 页 · The solution: three layers

- Verified human: our backend checks the owner's ME ID and signs an EIP-712 attestation; the MeIdGate contract verifies it, checks the owner's EIP-712 consent signature (ownerSig), and registers one DID per owner.
- Bounded agent: the AgentPolicy contract enforces per-trade cap, asset allowlist, max leverage and expiry on-chain, so a leaked key or a compromised server cannot exceed them.
- Credit that follows the person \u2014 Earn it. Lose it. Spend it once. The AgentCredit contract keeps a revolving line of 100 test MEC in a soulbound credential built on the draft ERC-8498 interface and bound to the DID. Earn it: one verified ME ID, one credential; repaying restores the line, and an on-time repayment moves the credential up a tier (in this build that updates the credential state, not the limit). Spend it once: every agent draw needs a one-time ticket the owner signs off-chain with EIP-712, with the fields agent, didHash, maxAmount, nonce and expiry; maxAmount may not exceed the agent's per-trade cap (50 MEC in the demo), and draw enforces the smaller of the two; the contract tracks spentNonce, so a spent ticket is rejected. Our app asks for the ticket signature at the moment of borrowing, and the contract rejects any ticket that expires more than 10 minutes out. Without a fresh owner-signed ticket, a leaked agent key cannot borrow. Lose it: each loan records a due date; once it passes with a balance unpaid, anyone can call suspend (our keeper is just one caller), and the credential is suspended for every agent.

中文注：口径：签证明的是我们的后端；合约验签，不是合约直接读 ME ID。信用层已完全合并（用户 11-27 定）：循环额度 + 一次性借款券，小标题 “Earn it. Lose it. Spend it once.”。合约只有三个：MeIdGate、AgentPolicy、AgentCredit。接口（内部）：register(…, backendSig, ownerSig)：backendSig 为后端 ME ID 证明签名（原 sig），ownerSig 为主人对 didHash + deadline 的 EIP-712 同意签名，铸凭证时验；AgentPolicy 只读 preflight(Trade, Ticket, ownerSig) 返回所有未通过的检查项；EIP-712 domain 写死（name、version、chainId、verifyingContract）；draw(didHash, Ticket, ownerSig) 为 onlyPolicy，只能由 AgentPolicy 调用；execute(Trade, Ticket, ownerSig) 先检查 min(maxAmount, perTradeCap) 再调 draw；Ticket 字段 agent、didHash、maxAmount、nonce、expiry（didHash + 固定 domain 防跨部署、跨 DID 重放）；合约只检查 t.expiry ≤ block.timestamp + 10 minutes；「不预签多张」合约强制不了，只靠前端在代理发起交易时才弹签名，对外不承诺；每笔借款记 dueAt，suspend 仅在过 dueAt 且有未还余额时成功，任何人可调，keeper 只是调用者之一；maxAmount 不得超过 AgentPolicy 单笔上限 50 MEC，签券时检查，draw 按 min(maxAmount, 单笔上限) 执行；合约只记 spentNonce。循环的是额度，一次性的是每次动用额度的券，两者不矛盾。【推断】只说 built on the draft ERC-8498 interface。

### 第 6 页 · Why ME Network

- ME ID is native to ME Hub (x/did, x/kyc): KYC credentials come from issuers registered by the Global DAO, and each ME ID can bind exactly one EVM sub-account, enforced on-chain.
- We use ME end to end: ME ID lookup via the official JS SDK, a native ME Hub sub-account binding transaction, Solidity contracts on ME EVM, and MEC as the credit asset.
- Reach: ME says ME Pass connects 7.5 million KYC-verified users. A one-person, one-line credit model only works where identity is already one-per-human.

中文注：对应评审「ME 应用」25 分。【事实】模块与绑定规则来自 me-hub 源码；750 万是 ME 官方博客说法。

### 第 7 页 · Live demo on ME testnet

- Verify a real ME ID; mint one soulbound credit credential (100 test MEC line); sign an agent policy; the owner signs a one-time ticket off-chain.
- Agent A spends one ticket to borrow 40 and trades within limits; an injected instruction, reusing the spent ticket, is rejected with four reasons.
- Revoke Agent A, register Agent B: it sees 60 left and 40 owed, repays on time, and the full 100 is available again; the limit stays 100 and the credential records the on-time repayment. Every step leaves a tx hash on ME.

中文注：接约 3:23 的 Demo 视频（Leader 9 步版）；下一节是逐步旁白。

### 第 8 页 · [LIVE PITCH ONLY — not in the demo video] Business: a subscription, not a loan book

- Who we start with: retail traders who have already given a Hyperliquid agent or API wallet to a bot or AI; then terminals, AI trading assistants and copy-trading operators who ask users for that authorization. Lenders and credit protocols are an interview group only in this cycle.
- How we charge (hypotheses, not closed prices): Personal Guard $9–19/month, or free plus a fee per on-chain record; operator seat $49–99/month, then by connected accounts. Both sit below official bot-subscription prices (Cryptohopper $24.16–$107.50/month billed annually; Cornix $32.99 and $52.99/month). Near-term revenue is the subscription, not lending interest.
- Validation: 5–8 seed interviews before the 21 Dec 2026 submission deadline; no paid-conversion claims until they are done. Channels: ME developer community, Hyperliquid trader communities, teams that already request agent authorization.

中文注：仅现场路演讲，不进 Demo 视频（Leader 已定）；视频里只在第 9 步收尾前念半句 “Subscription, not a loan book.”。销售定稿（完整版见下一节「第 8 页完整英文稿」）。【事实】Cryptohopper、Cornix 价格 2026-11-27 已对官网核对一致。【推断】我们的定价是假设，不是成交价。

### 第 9 页 · Roadmap and honest limits

- Today: built on the draft ERC-8498 interface; the line, the used-ticket record and suspension live in our own AgentCredit contract, unaudited. Single attestation signer, testnet only (EVM chain ID 400), test MEC, no real lending.
- Next: multi-signer attestations, then native ME ID verification as ME exposes it; mainnet once fees are confirmed. Timeline: on the roadmap.
- Later: real credit lines with partners. Partners and timeline: on the roadmap.

中文注：主动讲清现阶段的信任假设。ERC-8498 只说 built on the draft ERC-8498 interface：不提共同作者，不说市场空白，不说标准背书。真实放贷只在这里提一句。

### 第 10 页 · Close

- Permissions limit what an agent can do. AgentGuard proves who it acts for.
- Swap the agent, keep the credit. One verified human behind it.

中文注：收尾句已由 Leader 定稿，与 Demo 最后一帧一致。


## 1b. 第 8 页完整英文稿（销售定稿，仅现场路演）与时长

> **仅现场路演**
>
> Leader 已定：第 8 页完整旁白只在现场路演时讲，不放进 3–5 分钟的 Demo 视频。视频里只在第 9 步收尾句前念半句 “Subscription, not a loan book.”（约 2 秒，Leader 9 步版已含）。

        
- **Business：** Others limit what an agent can do. AgentGuard proves who it acts for — and keeps that person's credit with them when the agent changes.
- **The problem, with evidence：**
  • A trading agent can place orders without proving which verified human it acts for. A leaked key can still cause losses through trades, even when withdrawals are blocked.
  • On 14 Nov 2026, after a small number of Hyperliquid accounts approved trading access to HyprEarn, unauthorized fills appeared. The root cause, the number of accounts, and any loss amount have not been published.
  • One bot-trading platform's own docs state that its bot-key limits are checked on its own servers; a leaked key can still trade outside those signed limits.
  • r/AI_Agents: \u201c"Never spend more than $50" in a system prompt is a suggestion. A policy check in the signing service is a rule.\u201d
- **Who we start with：**
  1. Retail traders who have already given a Hyperliquid agent or API wallet to a bot or AI.
  2. Terminals, AI trading assistants, and copy-trading operators who ask users for that authorization.
  3. Lenders or credit protocols — interview group only in this cycle, not a near-term revenue line.
- **How we charge (hypotheses, not closed prices)：**
  • Personal Guard: $9–19 / month, or free plus a fee per on-chain record.
  • Operator seat: $49–99 / month, then by connected accounts.
  • Below official bot-subscription bands: Cryptohopper $24.16 / $57.50 / $107.50 per month billed annually ($29 / $69 / $129 monthly); Cornix $32.99 and $52.99 per month.
  • Near-term revenue is the subscription, not lending interest.
- **Credit in this product：**
  • Anti-sybil: one certified ME ID, one credit record, booked by DID.
  • Credit follows the person. Every draw needs a fresh one-time ticket the owner signs at the moment of borrowing, valid for 10 minutes at most. Without a fresh owner-signed ticket, a leaked agent key cannot borrow.
  • Demo: agent A borrows 40 of a 100 test MEC limit with a one-time ticket; a reused ticket is rejected; after A is revoked and B is registered, B still sees 60 remaining and 40 unpaid; B repays, and the full 100 is available again.
  • No real loans or liquidations in the hackathon. Real lending is on the roadmap.
- **Channels and validation：**
  • ME developer community; Hyperliquid trader communities; teams that already request agent authorization.
  • 5–8 seed interviews before the 21 Dec 2026 submission deadline. No paid-conversion claims until they are done.
- **Primary closer (live pitch; Leader decision)：** The business is a subscription, not a loan book: traders, and the terminals that collect their agent authorization, pay monthly for verified, bounded agents.
- **Alternate closer (Sales' variant)：** The business is a subscription, not a loan book: traders and trading terminals pay monthly for a verified human and hard limits behind every agent.
- **Narration (147 words incl. primary closer, ~1:05 at ~135 wpm; live pitch only)：** We start with traders who have already handed an agent a trading key, then the terminals and copy-trading desks that collect that authorization. What they pay for is this: a verified human behind the agent, a hard stop when the agent steps out of policy, and a credit record that stays with the person when the agent is swapped. Personal plans we are testing at nine to nineteen dollars a month; operator seats at forty-nine to ninety-nine, before we add connected accounts — those are hypotheses, set below official bot-subscription prices, not closed deals. The credit you just saw is anti-sybil. Credit and debt follow the DID. The borrow and repay were a testnet illustration. We are not lending real funds in this build; that stays on the roadmap. The business is a subscription, not a loan book: traders, and the terminals that collect their agent authorization, pay monthly for verified, bounded agents.

        相对销售原稿的改动：① Prow 不点名，改为 one bot-trading platform's own docs（链接只在来源附录）；② HyprEarn 的 several 改为 a small number，与第 2 页和 Demo 第 1 步一致；③ “drain the account”改为“cause losses”，避免暗示已知损失规模；④ 「Credit in this product」一节已整段换成销售 11-27 完全合并后的定稿（逐字）。本页不提 ERC-8498 编号，编号只在第 9 页出现。数字核对：100 额度、借 40、重用的券被拒、换 B 后剩 60 欠 40、还款回到 100，与 Leader 9 步旁白第 4–8 步一致。唯一差别是表述层面：旁白里重用券的拒绝和 400 MEC 越权注入在第 7 步合成一笔交易，本页把它写成单独一项，不冲突。⑤ 现场旁白已去掉开头 “The business is a subscription, not a loan book.”，从 “We start with traders…” 开始，24 词完整版只在结尾作主收尾句。商业仍是订阅，不是放贷。

        
| 旁白版本 | 词数 | 时长（约 135 词/分） | 曾评估（销售原稿 132 词版）：加到原 Demo 视频（4:27，未含商业句）后 |
| --- | --- | --- | --- |
| 完整版 | 132 | 约 0:59 | 4:27 + 0:59 = 约 5:26，超过 5:00 上限 |
| 精简版：开头到 “when the agent is swapped” | 68 | 约 0:30 | 4:27 + 0:30 = 约 4:57，刚好在上限内，但吃掉链上等待余量 |

        
> **时长建议**
>
> 已定：第 8 页只在现场路演讲。上表是当时的评估：原视频 4:27 加完整版约 5:26 超限，加精简版约 4:57 只剩约 3 秒余量。现在视频换成 Leader 的 9 步版，仍含半句 “Subscription, not a loan book.”，总长约 3:23。销售说的“前四句”实际是前三句（68 词），到 “when the agent is swapped” 为止。时长均按语速估算，录制后以实测为准。

---

## 2. Demo 旁白（9 步，约 3:23） / Demo voice-over

### Step 1 · 0:00–0:19（旁白 19s；链上等待 —）

**画面：** HyprEarn notice with the three undisclosed items highlighted

**Voice-over：**

> On November 14, HyprEarn reported unauthorized trades on Hyperliquid accounts that had approved its agent wallets; the root cause, the number of affected accounts and the losses were never disclosed. Approved agents can trade, and nobody can see who they really act for.

中文注：痛点 2 句；只说未授权成交，三项未公布写在画面上。

### Step 2 · 0:19–0:33（旁白 14s；链上等待 —）

**画面：** Zodiac Roles and session keys acknowledged; title card with tagline

**Voice-over：**

> Zodiac Roles and session keys already limit what an agent can do, and we use that too. AgentGuard adds the missing piece. Every AI agent has a human behind it. AgentGuard proves who.

中文注：先承认竞品，再给差异化；主 tagline 不变。

### Step 3 · 0:33–1:02（旁白 29s；链上等待 ⏳ 约 8s：MeIdGate 登记 + Hub 子账户绑定两笔交易确认）

**画面：** ME ID lookup (DID active, KYC done); EIP-712 attestation; MeIdGate tx and Hub binding tx in the explorer

**Voice-over：**

> This is a teammate's real ME ID. Our backend checks it with the Meta Earth SDK: DID active, KYC complete. It signs an EIP-712 attestation; MeIdGate on ME testnet verifies it, and one native ME Hub transaction binds the owner's sub-account. One verified human, anchored on ME.

中文注：明确是后端签名、合约验签。

### Step 4 · 1:02–1:26（旁白 24s；链上等待 ⏳ 约 4s：铸造凭证 + 重复 DID revert）

**画面：** register verifies backendSig and the owner's EIP-712 consent (ownerSig over didHash + deadline); ERC-8498 credential minted: Active, small tier label 'Tier 0', revision 1, 100 test MEC line; fresh wallet without ME ID gets 0; same DID again reverts

**Voice-over：**

> Registering also mints one soulbound credit record, in the draft ERC-8498 format, bound to this DID: status active, a revolving line of 100 test MEC. A fresh wallet with no ME ID gets zero. The same DID again reverts. More wallets never mean more credit.

中文注：Earn it 起点；防女巫两种被拒。去重由 MeIdGate 按 DID 做。100 MEC 为演示参数。

### Step 5 · 1:26–1:48（旁白 22s；链上等待 ⏳ 约 4s：AgentPolicy 授权交易确认）

**画面：** Owner signs AgentPolicy for Agent A (per-trade cap 50 MEC); tickets are signed later, one per borrow, just-in-time

**Voice-over：**

> The owner authorizes Agent A: 50 MEC per trade, two assets, 3x leverage, seven days. Each draw needs a one-time credit ticket. These limits live in the AgentPolicy contract, so a leaked key or a compromised server cannot exceed them.

中文注：演示参数，非市场数据。券由主人在链下用 EIP-712 签，一笔借款一张，含 agent、金额上限、nonce、过期时间；链上没有券数计数。

### Step 6 · 1:48–2:10（旁白 22s；链上等待 ⏳ 约 6s：核销券 + 借用 + 下单交易确认）

**画面：** Owner signs one fresh EIP-712 ticket just-in-time (Ticket: agent, didHash, maxAmount 50 ≤ per-trade cap, nonce, expiry ≤ now + 10 min; the app prompts the signature at trade time); Agent A reasoning; AgentPolicy.execute checks min(maxAmount, cap) then calls draw; ticket nonce marked used; borrow 40 MEC; trade on the test pool; receipt hash

**Voice-over：**

> Agent A explains its reasoning, spends one ticket to borrow 40 MEC, and trades inside every limit. Its nonce is marked spent on-chain, and the borrow is booked to the owner's DID, not the agent's key.

中文注：录制提示：第 6、7 步必须在 10 分钟内连续录完，第 7 步重用的是第 6 步那张券；超过 10 分钟链上返回 expired，不是 ticket already spent。Spend it once：合约只记录这张券的 nonce 已用。借 40 ≤ min(maxAmount 50, 单笔上限 50)。test MEC，模拟借用。

### Step 7 · 2:10–2:30（旁白 20s；链上等待 —）

**画面：** Injected prompt; audit panel calls the read-only preflight(Trade, Ticket, ownerSig) and lists four reasons (over cap, asset not allowed, leverage too high, ticket already spent); the tx is sent anyway and ONE real on-chain revert is shown (e.g. nonce reuse: ticket already spent) under the 'Spend it once' sub-heading

**Voice-over：**

> Now we inject a malicious instruction: put 400 MEC into an unknown asset at 10x, reusing the spent ticket. The audit panel's pre-check flags four problems: over the cap, asset not allowed, leverage too high, ticket already spent. We send it anyway, and the contract reverts.

中文注：录制提示：紧接第 6 步、10 分钟内录完（重用第 6 步的券，超时会变成 expired）。保留第 7 步（Leader 已定）：四条拒绝原因由审计面板调用只读 preflight(Trade, Ticket, ownerSig) 预检后列出，再提交 execute；链上只演示一次真实的 revert（只带一条原因，如 nonce 重用 → ticket already spent）。旁白不说「链上返回四条原因」。

### Step 8 · 2:30–3:00（旁白 30s；链上等待 ⏳ 约 8s：撤销 A、登记 B、归还三笔交易确认）

**画面：** Revoke Agent A; register Agent B; panel: 60 MEC left, 40 owed; B repays 40; the full 100 is available again (limit stays 100); credential panel tier label changes Tier 0 → Tier 1 under the 'Earn it' sub-heading (no extra voiceover), revision +1

**Voice-over：**

> The owner revokes Agent A and registers Agent B. B has never traded, yet it sees 60 MEC left and 40 owed, because the record belongs to the person. B repays on time: the full 100 is available again, and the record moves up a revision. Earn it.

中文注：额度和债都跟着人走；还款恢复可用额度。按时还款 tier + 1：凭证面板的小标签从 Tier 0 变成 Tier 1，用画面上 “Earn it” 小标题带过，旁白不加词；黑客松期间 tier 只写进凭证状态、不改额度，Demo 里额度一直是 100；不要说还款会提高额度。

### Step 9 · 3:00–3:23（旁白 23s（含商业半句约 2s）；链上等待 —）

**画面：** 'Lose it' sub-heading: suspend tx after dueAt with an unpaid balance — callable by anyone, our keeper is one caller (hash in repo, not performed live); trust-assumption line; caption 'Subscription, not a loan book.'; closing card

**Voice-over：**

> Miss the due date and anyone can suspend the record for every agent at once; that transaction is linked in our repo. Lose it. Today our backend signs the ME ID attestation, and we say so. Subscription, not a loan book. Swap the agent, keep the credit. One verified human behind it.

中文注：Lose it 只讲一句，不现场演示；坦白信任假设；商业半句（Leader 版已含）；收尾句不变。


---

## 3. 项目简介（提交表单） / Submission brief

提交表单时请把产品名改为 **AegisME**。下面保留起草时的原文（约 150 词），不要把共同作者或市场空白写进去。

When submitting, change the product name to **AegisME**. The draft below is the historical text (~150 words). Do not add co-authorship or a market-gap claim.

```
AgentGuard binds every AI trading agent to a verified human on ME Network. Zodiac Roles and session keys limit what an agent can do; AgentGuard also proves who it acts for. Our backend checks the owner's ME ID through the Meta Earth JS SDK and signs an EIP-712 attestation. MeIdGate verifies it and the owner's consent signature, registers one DID per owner, and a native ME Hub transaction binds the owner's EVM sub-account. AgentPolicy enforces per-trade caps, asset allowlists, leverage limits and expiry on-chain. AgentCredit keeps a revolving 100 test MEC line in a soulbound credential, built on the draft ERC-8498 interface and bound to the DID. Every agent draw spends a one-time ticket. Without a fresh owner-signed ticket, a leaked agent key cannot borrow. Repayment restores the line; overdue debt suspends it. Target users: traders delegating to bots or AI agents. Status: testnet (EVM chain ID 400), test MEC.
```


---

## 4. 答辩问答 / Q&A

### Q1. Isn't trust just moved to your signing backend?

Yes, today it is, and we say so on stage. ME ID lives in ME Hub's native modules and ME's EVM has no precompile to read it, so an off-chain check is currently the only path. We limit the trust: the backend can only attest that an address has an active ME ID, the signer address is public, every attestation expires and can be revoked on-chain, and anyone can re-check the same ME ID through ME's public REST API. Spending limits never depend on the backend; they are enforced by AgentPolicy, and every borrow also needs a one-time ticket signed by the owner, whose nonce AgentCredit records as used. Suspension is not a switch we hold: each loan records a due date, and once it passes with a balance unpaid, anyone can call suspend; our keeper is just one caller. Next steps are multi-signer attestations and native ME ID verification.

中文注：承认 + 限定 + 可复核 + 路线图；强调权限执行和借款券都不依赖后端；暂停条件上链（过 dueAt 且有未还余额），任何人可调用，keeper 不是中心化开关。

### Q2. How is this different from Zodiac Roles or ZeroDev session keys?

They are excellent at limiting what a key can do, and AgentPolicy uses the same idea: caps, allowlists, expiry. What they do not answer is who is behind the key. AgentGuard binds every agent to one ME ID-verified human and keys credit to that person, so new wallets without a verified ME ID get no credit, a DID cannot be registered twice, and an owner can swap agents while the line and any debt stay with them. Every draw also spends a one-time ticket the owner signs just before use. Without a fresh owner-signed ticket, a leaked agent key cannot borrow. Hyperliquid's approveAgent, by comparison, offers an expiry of up to 180 days but no per-asset, size or leverage limits.

中文注：先肯定竞品，再讲「替谁做」和信用跟人走。对外材料可将产品名替换为 AegisME。

### Q3. Why ME ID, not a generic KYC or proof-of-personhood service?

Because on ME the identity is part of the chain. ME ID is a native ME Hub module, KYC credentials are issued by DAO-registered issuers, and the chain itself lets each ME ID bind only one EVM sub-account. On top of that, our MeIdGate contract deduplicates by DID, so one person, one credit line is anchored to an on-chain identity, not to a database promise. ME also says ME Pass connects 7.5 million KYC-verified users, a ready base for this model.

中文注：用源码事实回答；不说链上能识别“同一个人”，去重是 MeIdGate 按 DID 做的；750 万是 ME 官方说法。

### Q4. ERC-8498 is still a Draft. Why build on it, and who wrote the ticket logic?

We build on the draft ERC-8498 interface because it gives the credential a public, readable state: active or suspended, with a revision number that moves on every change. It is a Draft, so the interface may change, and we say so. The draft leaves one-time consumption to the application, so the revolving line, the used-ticket record and the due-date suspension are our own code in the AgentCredit contract. That code is unaudited and runs only on ME testnet with test MEC. If the draft changes, we update the interface layer; the ledger and ticket logic stay the same.

中文注：主动承认 Draft、未审计、仅测试网；核销和借款券是我们自己写在 AgentCredit 里的；不提共同作者，不说标准背书或市场空白。

### Q5. What if the owner already signed a ticket and the agent key leaks?

Our app asks the owner to sign a ticket at the moment of borrowing, one per borrow, and the contract rejects any ticket that expires more than 10 minutes out. Each ticket names the agent and the DID, is capped at the smaller of its maxAmount and the 50 MEC per-trade cap, and its nonce is spent on first use. So the exposure is one small borrow inside a short window. Without a fresh owner-signed ticket, a leaked agent key cannot borrow.

中文注：不说「泄露密钥一定借不到钱」；讲清残余风险是 10 分钟内、单张、最多 50 MEC；不承诺「不能预签」，那只是前端行为。

### Q6. Isn't the keeper a centralized kill switch?

No. Every loan records a due date on-chain, and suspend only succeeds after that date while a balance is still unpaid. Anyone can call it; our keeper is simply one caller that makes sure it happens on time. It cannot suspend an account that is current. Resuming is the remaining privileged action, held by a team multisig.

中文注：逾期条件上链、任何人可调用；resume 仍是特权操作（团队多签），如实说。

备用：如评委拿 11-20 的 XMR1/Wagyu 事件追问，回答是那次资金由部署者主密钥转出，不是代理代下单，所以不作为代理权限案例引用。来源：Bitquery 调查。


---

## 5. 证据来源 / Sources

- HyprEarn / Hyperliquid 11-14 公告（根因、账户数、损失金额均未公布）
- r/AI_Agents 完整原句：`"Never spend more than $50" in a system prompt is a suggestion. A policy check in the signing service is a rule.`
- 某 bot 交易平台文档（幻灯片不点名；链接只放附录）
- Hong Kong MA SAGE / MAS KYA 公开报道（见市场扫描文档）
- Zodiac Roles、ZeroDev session keys、Hyperliquid `approveAgent`
- ERC-8498 Draft：https://eips.ethereum.org/EIPS/eip-8498
- ME Network / ME ID 文档与 me-hub 源码
- Bitquery 对 XMR1/Wagyu 的调查（仅答辩备用，不主动引用）
- 原始画布：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/9570d578-d686-4bdd-8df4-ea88d8d8f934


---

## English orientation

This is the working pitch and demo script: the do-not-say list, a 10-page English narrative, the page-8 business script (live pitch only), a 9-step demo voice-over (about 390 words, ~3:23 including ~30 seconds of on-chain waits), a submission brief, and Q&A.

**Rename:** The body still uses the then-current product name AgentGuard. For registration and the next slide pass, replace it with **AegisME**. Suggested tagline: “Every AI agent has a human behind it. AegisME proves who.” Update contract names on stage only after the implementation uses `AegisVault` / `ERC8498AgentRegistry` / `MeIdGate`.

The slides, voice-over, brief and answers below are already in English. Chinese notes sit under each block.


The do-not-say list, ten slides, page-8 live-pitch business script, nine demo beats, brief, and Q&A are all in the sections above (the spoken and submitted text is English; Chinese notes follow each block). Recording constraint: steps 6 and 7 must be captured within the ticket’s 10-minute expiry, or the revert will say expired instead of “ticket already spent.”
