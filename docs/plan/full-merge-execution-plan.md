# AegisME 完全合并执行方案 / Full-merge execution plan

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.

- **状态 / Status:** 当前方案（文末 11-27 评估为归档） / Current (27 Nov section archived)
- **来源画布 / Source canvas:** [AgentGuard × 信用额度 × ERC-8498 结合评估](https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570)
- **日期 / Date:** 2026-11-27，并在 2026-11-28 凌晨纳入 Gemini 评审决定（Asia/Shanghai）

## 中文

# AegisME 完全合并执行方案（原名 AgentGuard × 信用额度 × ERC-8498）

> 已定：完全合并。最上面是执行方案：3 个合约、「循环额度 + 一次性借款券」信用模型、约 3:21 的 Demo、开发排期和 12-07 检查点；缓解措施已写入方案。12-07 检查点通过后可上调技术项自评（数字已省略）。下方保留 11-27 的原评估（已归档）。

## 完全合并执行方案

> **一个产品：AgentGuard。信用记录是绑定在 ME ID 上的 ERC-8498 灵魂绑定凭证，里面是循环额度；代理每借一笔要花掉一张一次性借款券。**
>
> 【推断】合约压到 3 个（核销并进信用合约），Demo 估算约 3:21（含约 30 秒链上等待），再给界面操作留 30 秒也只有约 3:51，第 7 步不删。缓解后内部规划分略有提高；12-07 检查点全部通过后，技术项才有上调理由（具体数字因本仓库为公开仓库而省略）。最大的前提仍是 12-01 前招到 Solidity 开发。

### 来自 Gemini 评审（11-28）的 5 条决定

- **1. 借款券只能现签：** 【决定】主人在每次借款前即时签券，expiry 不超过 10 分钟，不允许批量预签。对外口径："Without a fresh owner-signed ticket, a leaked agent key cannot borrow." 【推断】预签的券如果存在代理端，密钥泄露时会一起泄露，「泄露的密钥借不到钱」就不成立。
- **2. EIP-712 Domain 与 Ticket：** 【决定】Domain 固定为 name、version、chainId、verifyingContract；Ticket 字段为 agent、didHash、maxAmount、nonce、expiry。【推断】加 didHash 和 chainId 是为了防止同一张券被拿到别的 DID、别的链或别的合约上重放。
- **3. 到期与暂停不依赖 keeper：** 【决定】每笔 draw 在链上记录 dueAt；`suspend(didHash)` 任何人都能调用，只有在 block.timestamp > dueAt 且 outstanding > 0 时才成功；keeper 只是调用方之一。
- **4. 权限与限额检查的位置：** 【决定】`AgentCredit.draw` 为 onlyPolicy；`AgentPolicy.execute` 在调用 draw 之前检查 amount 不超过 min(maxAmount, perTradeCap)。
- **5. 分数口径：** 【决定】内部规划分不对外展示。本公开仓库已删除所有相关数字。【推断】完整闭环的评委实际打分，会低于团队内部规划分。

### 合约架构（3 个）

**模块关系（原画布示意图，改为文字）：**

`签名后端`（SDK 查 ME ID，签 EIP-712）→ `MeIdGate`（验签、DID 去重、触发铸造）→ `AgentCredit`（ERC-8498 SBT + 账本 + 借款券核销）

代理 A / B → `AgentPolicy`（下单、借用）→ `AgentCredit`（draw / repay）

任何人（含 keeper）→ `AgentCredit`（仅当过 dueAt 且有欠款时 suspend）

```solidity
// 接口草图（【推断】供开发参考，字段名可改）

// 1. MeIdGate：不变，多一步 mint
function register(address owner, bytes32 didHash, uint256 deadline, bytes backendSig, bytes ownerSig) external;
//   backendSig：后端对 ME ID 核验结果的 EIP-712 证明（原参数名 sig）
//   ownerSig：主人对 (didHash, deadline) 的 EIP-712 同意签名，满足 ERC-8498 「初始化须持有人同意」
//   验 backendSig -> 验 ownerSig -> didHash 去重 -> AgentCredit.mintFor(didHash, owner, ownerSig)

// 2. AgentCredit：ERC-8498 核心 + 信用账本 + 借款券核销（合并原 CreditScore 和 CreditLedger）
//   IEvolvingSBT（复用参考实现）
function stateOf(uint256 tokenId, bytes32 ns) external view returns (StateHead memory);
function policyOf(bytes32 ns, bytes32 policyId) external view returns (Policy memory);
function applyTransition(Change calldata c, bytes calldata evidence, bytes calldata auth) external;
event StateTransitioned(...);
//   信用扩展（命名空间 agentguard.credit）
function creditOf(bytes32 didHash) external view
  returns (uint64 limit, uint64 outstanding, uint64 dueAt, uint8 tier, uint8 status, uint64 revision);
//   EIP-712 Domain（来自 Gemini 评审 11-28）：{ name, version, chainId, verifyingContract }
//   Ticket = { address agent; bytes32 didHash; uint64 maxAmount; uint256 nonce; uint64 expiry }
//   链上不计券的张数；只记已花掉的 nonce
mapping(bytes32 didHash => mapping(uint256 nonce => bool)) public spentNonce;
function draw(bytes32 didHash, Ticket calldata t, bytes calldata ownerSig, uint64 amount) external;   // onlyPolicy
//   主人在每次借款前即时签一张，expiry  revert "ticket already spent"
function repay(bytes32 didHash, uint64 amount) external;  // 按时还清 -> 只在 ERC-8498 状态里 tier + 1；黑客松期间 limit 固定 100
function suspend(bytes32 didHash) external;               // 任何人可调；require block.timestamp > dueAt && outstanding > 0
function resume(bytes32 didHash) external;                // onlyController（团队多签）

// 3. AgentPolicy：借用时带上借款券，并新增只读预检
function authorize(address agent, Limits calldata l, uint64 expiry) external;     // owner
function revoke(address agent) external;                                          // owner
function preflight(Trade calldata tr, Ticket calldata t, bytes calldata ownerSig) external view returns (bytes32[] memory failedChecks);
//   只读，返回所有没通过的检查项（超单笔上限 / 资产不在白名单 / 杠杆过高 / 券已花掉……），供审计面板显示
function execute(Trade calldata tr, Ticket calldata t, bytes calldata ownerSig) external; // agent
//   链上 revert 只返回第一条失败原因
//   检查白名单 / 杠杆 / 有效期，require amount  AgentCredit.draw(didHash, t, ownerSig, amount) -> 记录成交
```

- **为什么是 3 个：** 【推断】规范只要求应用自己用作用域 nullifier 记录消费，没规定必须另起合约（【事实】来源：[EIP]）。所以把「账本 + 核销」和 8498 核心放在同一个 AgentCredit 合约里，少一次跨合约调用，也少一个要审的合约。代价是这个合约变大，单元测试要按「核心 / 账本 / 核销」三块分开写。
- **谁能写入：** 【事实】规范允许签名、授权的链上调用方或证明作为写入方，初始化须持有人同意，时间流逝不会自动改状态。【推断】draw 只认 AgentPolicy；suspend 的最终决定见上文第 3 条（任何人可调，仅当逾期且有欠款时成功，keeper 只是调用方之一——本句旧稿写「只认 keeper」已作废）；resume 留给团队多签。来源：[EIP]
- **London 重编：** 【事实】参考实现按 evm_version = cancun 编译；ME 的 Ethermint 依赖 go-ethereum v1.10.26，属于 London。【推断】① foundry 里显式写 evm_version = "london"（solc 0.8.20 起默认会生成 Shanghai 的 PUSH0）；② 全局搜索 tstore、tload、mcopy，以及 OpenZeppelin 里的 Transient 类合约，有就换普通存储写法或锁住较早的 OZ 版本；③ 51 项测试用 london 目标全部重跑；④ 在链 ID 400 上实际部署并跑通一次 applyTransition。来源：[REPO] ；[GOMOD]

| 环节 | ME 测试网上真实跑 | 模拟 / 链下 |
| --- | --- | --- |
| ME ID | 队友真实 ME ID，SDK 查询；一笔 Hub 原生子账户绑定交易 | 签名由我们的后端发（路演如实说） |
| 3 个合约 | 全部部署在链 ID 400，每步留交易哈希 | — |
| 额度与借还 | 额度、欠款、借款券核销、revision 都在链上 | 用 test MEC，不是真实放贷，没有利息和清算 |
| 代理交易 | execute 交易和越权 revert 都在链上 | 成交记录到一个测试地址，不接真实 DEX；AI 推理在链下 |
| Lose it（逾期暂停） | dueAt 记在链上；suspend 是任何人可调的真实链上交易 | 调用方用 keeper 脚本；逾期用很短的还款期制造，不进视频，哈希放仓库 |
| 不做 | — | me.staking 升档、ZK 私有呈示、主网、真实放贷 |

### 信用模型：循环额度 + 一次性借款券

> **额度是人的，可以循环用；借款券是一次性的，用完就在链上核销。**
>
> 【推断】ME ID 主人的 ERC-8498 凭证里有一份 100 test MEC 的循环额度，还款就恢复；代理每借一笔，都要花掉一张主人签发的一次性借款券，券一旦用掉就被核销，泄露的密钥、换下来的代理都不能再用。这样 Spend it once 不再和「还款后回到 100」冲突：循环的是额度，一次性的是每一次动用额度的授权。

|  | 链上发生什么 | Demo 里在哪 |
| --- | --- | --- |
| Earn it | 真人 ME ID 登记得到 100 test MEC 额度；按时还清，revision + 1、tier + 1，只记在 ERC-8498 状态里，黑客松期间额度仍是 100 | 第 4、8 步 |
| Spend it once | 主人每次借款前现签一张 EIP-712 借款券（agent、didHash、maxAmount、nonce、expiry，10 分钟内有效，不预签）；AgentCredit 只记已花掉的 nonce，重用即 revert（来自 Gemini 评审 11-28） | 第 6 步核销，第 7 步重用被拒 |
| Lose it | 每笔借款记 dueAt；过期且有欠款时任何人都能调 suspend，状态 Active → Suspended，所有代理同时借不了（来自 Gemini 评审 11-28） | 第 9 步一句话，交易哈希放仓库 |

          【推断】借款券把信用和 AgentGuard 的安全主线接在一起：就算代理密钥泄露，对方手里也没有主人签过且未用的券，借不到钱。

### Demo（第 7 步不删）

| 步 | 画面与动作 | 词数 | 链上等待 | 累计 |
| --- | --- | --- | --- | --- |
| 1 痛点 | HyprEarn 公告，三项未公布高亮 | 43 | — | 0:19 |
| 2 定位 | 承认 Zodiac 和 session keys；封面 tagline | 33 | — | 0:33 |
| 3 身份 | ME ID 查询、EIP-712、MeIdGate 与 Hub 绑定两笔交易 | 47 | 8s | 1:02 |
| 4 信用凭证 | 铸出 ERC-8498 凭证：Active、100 MEC；无 ME ID 钱包得 0；重复 DID revert | 45 | 4s | 1:26 |
| 5 授权代理 A | 限额、白名单、杠杆、有效期；只授权，不预签券 | 40 | 4s | 1:48 |
| 6 花券借 40 | 主人现签一张券（10 分钟内有效）、代理推理、券的 nonce 标记为已用、借 40、下单、回执 | 36 | 6s | 2:10 |
| 7 注入被拒（保留） | 400 MEC、10x、未知资产、重用已花的券；审计面板先调 preflight 列出四条原因，再提交 execute，得到一次真实的链上 revert | 42 | — | 2:28 |
| 8 换代理、还款 | 撤 A、登记 B；B 看到剩 60、欠 40；还 40 后 100 重新可用，revision + 1；凭证面板小标签 Tier 0 → Tier 1（旁白不加词） | 47 | 8s | 2:58 |
| 9 收尾 | Lose it 一句（哈希在仓库）、信任假设、商业半句、收尾句 | 51 | — | 3:21 |

          【推断】旁白 385 词（第 7 步旁白只说审计面板显示原因，不说链上返回四条），按 135 词/分加 30 秒链上等待，约 3:21。再给录屏点击、切换窗口留 30 秒，仍约 3:51，距 4:30 还有余量，高于 3 分钟下限。省下来的时间来自：第 2、3、5、6 步压短；Lose it 不单独演；Spend it once 并进第 7 步，作为第四条拒绝原因。录完按实测时长再核。

```
1. On November 14, HyprEarn reported unauthorized trades on Hyperliquid accounts that had approved its agent wallets; the root cause, the number of affected accounts and the losses were never disclosed. Approved agents can trade, and nobody can see who they really act for.
2. Zodiac Roles and session keys already limit what an agent can do, and we use that too. AgentGuard adds the missing piece. Every AI agent has a human behind it. AgentGuard proves who.
3. This is a teammate's real ME ID. Our backend checks it with the Meta Earth SDK: DID active, KYC complete. It signs an EIP-712 attestation; MeIdGate on ME testnet verifies it, and one native ME Hub transaction binds the owner's sub-account. One verified human, anchored on ME.
4. Registering also mints one soulbound credit record, in the draft ERC-8498 format, bound to this DID: status active, a revolving line of 100 test MEC. A fresh wallet with no ME ID gets zero. The same DID again reverts. More wallets never mean more credit.
5. The owner authorizes Agent A: 50 MEC per trade, two assets, 3x leverage, seven days. Each draw needs a fresh owner-signed ticket. These limits live in the AgentPolicy contract, so a leaked key or a compromised server cannot exceed them.
6. Agent A explains its reasoning, spends one ticket to borrow 40 MEC, and trades inside every limit. Its nonce is marked spent on-chain, and the borrow is booked to the owner's DID, not the agent's key.
7. Now we inject a malicious instruction: put 400 MEC into an unknown asset at 10x, reusing the spent ticket. AgentPolicy reverts. The audit panel shows why: over the cap, asset not allowed, leverage too high, ticket already spent. The contract said no.
8. The owner revokes Agent A and registers Agent B. B has never traded, yet it sees 60 MEC left and 40 owed, because the record belongs to the person. B repays, and the full 100 is available again. The record moves up a revision. Earn it.
9. Miss a repayment and anyone can suspend the record for every agent at once; that transaction is linked in our repo. Lose it. Today our backend signs the ME ID attestation, and we say so. Subscription, not a loan book. Swap the agent, keep the credit. One verified human behind it.
```

### 叙事层级

| 层级 | 文案 | 出现在哪 |
| --- | --- | --- |
| 主 tagline | Every AI agent has a human behind it. AgentGuard proves who. | 封面、Demo 第 2 步 |
| 副标题 | Verified humans. Bounded agents. Credit that follows the person. | 封面 |
| 信用模块三拍 | Earn it. Lose it. Spend it once. | 第 5 页信用一层的小标题；Demo 第 8、9 步各点一次 |
| 收尾句 | Swap the agent, keep the credit. One verified human behind it. | Demo 最后一帧、第 10 页 |

          【推断】三拍只做信用模块的小标题，不和主 tagline 并列，评委看到的仍是一个产品。对外只说 "built on the draft ERC-8498 interface"；共同作者在拿到公开证据前不提。

### 开发排期与 12-07 检查点

### 重新打分

【决定】内部规划分只用于方案比较，不写进路演、提交材料或任何对外文字。本公开仓库已删除所有具体数字。

定性结论（【推断】）：

- **体验**因「循环额度 + 一次性借款券」把原先冲突的两套说法收成一套，Demo 不超时，第 7 步拒绝原因更好懂，因而上调。
- **技术**在没有开发者、仍依赖 Draft 标准与自写未审计核销逻辑的情况下保持审慎；只有 12-07 在 ME 测试网真正跑通三项检查后，才有理由上调。
- **创新**肯定「借款券把信用和代理安全接在一起」；产品价值不变，因为出资人需求仍无证据。
- 评委现场打分预计会低于团队内部规划分。

### 给市场、产品、销售的改动说明

```
用户已定：AgentGuard 完全合并信用额度和 ERC-8498，仍是一个产品。信用模型统一为「循环额度 + 一次性借款券」：额度（100 test MEC）存在绑定 ME ID 的 ERC-8498 凭证里，还款即恢复；代理每借一笔核销一张主人签发的券，重用被拒；逾期由 keeper 暂停凭证。合约为 MeIdGate、AgentPolicy、AgentCredit 三个。@HARBOR 市场：路演稿第 5 页信用一层改为凭证 + 券，小标题用 "Earn it. Lose it. Spend it once."，主 tagline 和收尾句不变；Demo 旁白按本页 9 步（384 词，约 3:21，第 7 步保留并加「ticket already spent」）替换；第 9 页 Roadmap 加 "built on the draft ERC-8498 interface"，不提共同作者，不说市场空白。@HARBOR 产品：打分表和产品报告改为完全合并（12-07 通过后可上调技术项；数字不对外），MVP 范围、接口草图、真实/模拟清单和 12-07 检查点三条标准写进产品页，并写好两级退路（轻度结合 / v3）。@HARBOR 销售：第 8 页商业部分仍是订阅，不是放贷；信用一条改为「额度跟人走，每次动用都要一次性券，泄露的密钥借不到钱」；访谈提纲加一题：终端和交易者是否看重「泄露密钥也借不到钱」。所有人只改文件，不对外发送。
```

## 11-27 旧评估（已被上方完全合并方案取代）

以下是用户决定完全合并之前的分析，只作备查，不是当前建议。其中「当时不建议完全合并」的结论已被上方执行方案取代；「Spend it once 不用」已被「循环额度 + 一次性借款券」模型取代。

### 结论

> **（11-27 原评估，保留备查；用户已决定完全合并，以上方执行方案为准）当时建议轻度结合：AgentGuard 仍是唯一的产品，ERC-8498 只当信用状态的底层格式，路演里讲一句。**
>
> 【推断】当时认为把 Earn it / Lose it / Spend it once 三段一起演，视频旁白可能超过 5 分钟，评委还可能觉得是两个产品拼在一起，因而建议轻度结合。用户已决定完全合并，该时长问题已通过压缩旁白与「循环额度 + 一次性借款券」模型解决。第一周测试网实测不通过，仍可退回 CreditScore。

- 【事实】当时对「AgentGuard + 信用额度」与「ERC-8498 独立新产品」分别做了内部评分（数字已省略）。来源：产品方向报告与独立评分页（现已归档）。
- 【推断】ERC-8498 真正能给 AgentGuard 加的是：信用状态可以被暂停或降级，并且是对外可读的标准接口。「用一次就核销」和 AgentGuard 的循环额度（借 40、还 40、回到 100）有冲突，不建议放进主产品。
- 【推断】ERC-8498 独立产品不放弃，留到黑客松之后；出资人访谈有了正面结果再重新评估。

### 打分（官方五项权重）

内部打分对照表已删除（公开仓库）。定性上，11-27 时轻度结合与当时的主方案接近，完全合并被下调（主要是技术与体验），独立 8498 产品更低。该比较已被上方执行方案取代。

### 来源

- 产品方向报告 v4（现为完全合并）：见本目录 `product/product-direction-v4.md`
- 路演叙事与 Demo 旁白：`pitch/pitch-and-demo-narration.md`
- ERC-8498 独立评估（已归档）：`archive/erc8498-standalone-scoring.md`
- ERC-8498 核实报告：`research/fact-check-erc8498.md`
- 行业事实核查与反例：`research/market-counterexamples.md`
- 新产品定位草案（已归档）：`archive/standalone-positioning.md`
- [ERC-8498 Draft](https://eips.ethereum.org/EIPS/eip-8498)
- [ERCs PR #2171](https://github.com/ethereum/ERCs/pull/2171)（2026-11-26）
- [讨论帖](https://ethereum-magicians.org/t/erc-8498-namespaced-state-transitions-for-sbts/30361)（2026-11-12）
- [evolving-sbt 参考实现](https://github.com/XiaoHai67890/evolving-sbt)
- [me-hub go.mod](https://github.com/openmetaearth/me-hub/blob/main/go.mod)
- 原始画布：https://cursor.com/canvas/store-db231139-7440-40ce-b560-d8d91d4da60e/922b552f-e54a-43be-b80f-9e4933147570

---

## English

# AegisME full-merge execution plan (formerly AgentGuard × credit line × ERC-8498)

**Status:** Current (the 27 Nov evaluation at the end is archived). **Source canvas date:** 27 Nov 2026, updated after the Gemini review in the early hours of 28 Nov 2026, Asia/Shanghai.

The user chose a **full merge**: one product, now named AegisME. A revolving credit line lives in an ERC-8498 soulbound credential bound to a ME ID. Every agent draw spends a one-time ticket the owner signs at the moment of borrowing.

The historical interface sketch still uses three contracts: `MeIdGate`, `AgentPolicy`, `AgentCredit`. Intended names going forward are `MeIdGate`, `ERC8498AgentRegistry`, and `AegisVault`. This document does not silently rewrite the sketch.

## Decisions from the Gemini review (28 Nov 2026)

1. **Tickets are signed just in time.** The owner signs immediately before each borrow; `expiry` is at most 10 minutes; no batch pre-signing. External line: “Without a fresh owner-signed ticket, a leaked agent key cannot borrow.” The contract can only check expiry; the front end is what prevents pre-signing.
2. **Fixed EIP-712 domain; ticket includes didHash.** Domain: `name`, `version`, `chainId`, `verifyingContract`. Ticket: `{ agent, didHash, maxAmount, nonce, expiry }`.
3. **Overdue suspension does not depend on a keeper.** Each `draw` records `dueAt`. Anyone may call `suspend(didHash)`; it succeeds only if `block.timestamp > dueAt` and `outstanding > 0`. A keeper is one caller, not a switch.
4. **Where caps are checked.** `AgentCredit.draw` is `onlyPolicy`. `AgentPolicy.execute` checks `min(maxAmount, perTradeCap)` before calling `draw`.
5. **Scores stay internal** and have been omitted from this public repository.

An older bullet in the architecture notes that said “only the keeper may call suspend” is **superseded** by decision 3.

## Contract architecture (three contracts)

Signing backend (SDK reads ME ID, signs EIP-712) → `MeIdGate` (verifies, dedupes DID, triggers mint) → `AgentCredit` (ERC-8498 SBT + ledger + ticket consumption).

Agent A/B → `AgentPolicy` (orders and borrows) → `AgentCredit` (`draw` / `repay`).

Anyone (including a keeper) → `AgentCredit` (`suspend` only when overdue with a balance).

See the Solidity sketch in the Chinese section (compile with `evm_version = "london"`; avoid PUSH0, tstore, tload, mcopy; ME Ethermint is go-ethereum v1.10.26 / London). `register` takes `backendSig` and `ownerSig` (the latter is the holder’s EIP-712 consent). On-chain we record `spentNonce` only; there is no tickets-left counter. `preflight` is a view that returns every failed check; `execute` reverts with the first reason.

**Why three:** the ERC-8498 draft leaves consumption to the application and does not require a separate contract, so ledger + tickets live in `AgentCredit`. The cost is a larger contract; unit tests should be split into core / ledger / tickets.

**Real vs simulated on ME testnet:** real ME IDs and a Hub sub-account bind; all three contracts on chain ID 400 with tx hashes; limit, debt, ticket consumption and revision on-chain; `execute` and unauthorized reverts on-chain; `dueAt` and a real `suspend` tx (hash in the repo). Simulated: backend signs the ME ID attestation (said honestly on stage); test MEC only, no interest or liquidation; fills go to a test address, no real DEX; AI inference off-chain; a short due date is used to produce the suspend tx, and that step is not in the video. Out of scope: `me.staking` upgrades, ZK presentation, mainnet, real lending.

## Credit model: revolving line + one-time tickets

The line belongs to the person and revolves; the ticket is one-time and is consumed on-chain. A ME ID owner has a 100 test MEC revolving line that restores on repayment. Each borrow spends a fresh owner-signed ticket, so a leaked key or a replaced agent cannot reuse it. “Spend it once” refers to the ticket, not the line.

| Beat | On-chain | In the demo |
| --- | --- | --- |
| Earn it | A verified ME ID is registered and receives 100 test MEC; on-time repayment increments revision and tier in ERC-8498 state only; the limit stays 100 during the hackathon | Steps 4 and 8 |
| Spend it once | The owner signs an EIP-712 ticket just before the borrow (10-minute expiry, no pre-sign); `AgentCredit` records spent nonces; reuse reverts | Step 6 consumes; step 7 rejects reuse |
| Lose it | Each borrow records `dueAt`; once overdue with a balance, anyone can `suspend` (Active → Suspended); all agents are blocked at once | One line in step 9; tx hash in the repo |

## Demo (step 7 is kept)

Nine steps, about 3:21 including ~30s of on-chain waits, plus ~30s of UI slack ≈ 3:51, under the 4:30 comfort line and above the 3-minute minimum. Step 7 is kept: the audit panel calls `preflight` (four reasons) and then a real `execute` revert. Record steps 6 and 7 inside 10 minutes, or the revert will say expired instead of “ticket already spent.” Voice-over text is in the Chinese section (and in `pitch/`).

## Narrative hierarchy

- Main tagline: “Every AI agent has a human behind it. AgentGuard proves who.” (cover, demo step 2). For current materials, prefer substituting AegisME for AgentGuard in this line when slides are next edited.
- Subtitle: “Verified humans. Bounded agents. Credit that follows the person.”
- Credit-module three-beat (small heading only, not beside the main tagline): “Earn it. Lose it. Spend it once.”
- Close: “Swap the agent, keep the credit. One verified human behind it.”
- External wording: “built on the draft ERC-8498 interface.” No co-authorship claim until public evidence exists.

## Schedule and 7 Dec checkpoint

1. Before 29 Nov 23:59 — finish registration under the name **AegisME**.
2. 1 Dec (hard gate) — a Solidity developer is in place; otherwise ship v3 CreditScore and do not use 8498.
3. 1–3 Dec — retarget the reference implementation to London, rerun the 51 tests, deploy to chain ID 400; scaffold `MeIdGate`, `AgentPolicy`, and backend signing.
4. 4–6 Dec — `AgentCredit`: ledger, ticket consumption, suspend/resume; tests in three blocks.
5. **7 Dec checkpoint** — (1) `applyTransition` runs on chain 400; (2) ticket consume and reuse-revert pass on testnet; (3) one borrow transaction (`execute` → `draw`, including `applyTransition`) stays under 500k gas (the testnet block gas limit is not yet verified). All three pass → stay on full merge. (1) passes but (2) or (3) fails → light merge (drop tickets; drop “ticket already spent” from step 7). (1) fails → v3 CreditScore, do not mention 8498 on stage.
6. 8–12 Dec — front-end panel, off-chain agent reasoning, keeper script; one real `suspend` tx on testnet.
7. 13–14 Dec — freeze contracts, internal review (not an audit), demo rehearsal.
8. 15–17 Dec — record the demo; confirm duration ≤ 4:30.
9. 18–20 Dec — English submission materials; README lists addresses and tx hashes; submit a draft on 20 Dec.
10. 21 Dec 23:59 Beijing time — final deadline.

## Internal scoring (numbers omitted)

Planning scores were used only to compare options and must not appear in the pitch, submission, or any external text. Qualitatively: UX was raised because one coherent credit model replaced two conflicting stories and step 7 is clearer; tech stays conservative until the 7 Dec checks actually pass on ME testnet; innovation credits the ticket-to-security link; product value is unchanged because funder demand is still unproven. Actual judge scores are expected to come in below the team’s internal planning figures.

## Note to market, product, and sales (from the original brief, lightly updated)

The user chose a full merge into one product. Unify the credit model as “revolving line + one-time tickets.” Market: keep the main tagline and close; use the three-beat only as a small heading on the credit layer; keep demo step 7 with “ticket already spent”; say “built on the draft ERC-8498 interface”; do not claim co-authorship or a market gap. Product: write MVP scope, the interface sketch, the real/simulated list, the 7 Dec checks and the two fallbacks into the product page. Sales: page 8 stays a subscription, not a loan book; credit follows the person; a leaked agent key cannot borrow without a fresh ticket; add an interview question on whether traders and terminals value that property. No external sends.

The original brief still said “a keeper suspends the credential”; that is superseded by permissionless `suspend`.

## Archived: the 27 Nov evaluation

Before the user chose a full merge, the recommendation was a **light merge**: AgentGuard remains the only product; ERC-8498 is only the format of the credit state, mentioned in one sentence on stage. The concern was that playing all three beats in full would overflow the video and look like two products glued together. That timing issue was later solved by compressing the voice-over and reconciling the revolving line with one-time tickets. If week-one testnet work fails, the fallback is still CreditScore. A standalone ERC-8498 product was deferred until after the hackathon, pending positive funder interviews. The numeric comparison table has been omitted.

## Sources

Listed in the Chinese section (EIPs, PR #2171, Magicians thread, reference implementation, me-hub go.mod, and the sibling docs in this folder).
