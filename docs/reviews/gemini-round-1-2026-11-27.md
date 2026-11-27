# Gemini CLI 第一轮对抗评审（2026-11-27）

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.


- **时间：** 2026-11-27 23:59:06 Asia/Shanghai（UTC+8）
- **模型：** gemini-3-flash-preview
- **尝试顺序：** gemini-3.1-pro-preview（429），gemini-2.5-pro（404），gemini-3-flash-preview（200）
- **状态：** 第一轮已完成。已采纳与驳回的条目见 [decisions-log.md](decisions-log.md)。
- **说明：** 提示词中的内部评分数字已删除。回复第 4 节的具体自评/预测数字已删除，定性批评保留。

## 中文说明

这是团队通过 Gemini API 做的第一轮对抗评审，角色是「持怀疑态度的 HARBOR 评委 + 智能合约安全审查」。评审对象是当时的完全合并方案（产品名仍为 AgentGuard）。主要批评包括：尚未找到 Solidity 开发者、后端签名造成的信任集中、London EVM 兼容风险、测试网信用缺乏真实经济后果，以及「泄露的密钥无法借款」在「主人已签券、代理随即被盗」窗口内并不成立。

团队已采纳即时签券、固定 Domain、链上 dueAt + 任何人可暂停、`draw` onlyPolicy 等修改；驳回了「preflight 死锁」和「再加一个 deadline」；未采纳其得分预估。

## English summary

This is the first adversarial review run through the Gemini API, with the model asked to act as a skeptical HARBOR judge and a smart-contract reviewer. The target was the full-merge plan (then still named AgentGuard). Main criticisms: no Solidity developer yet; trust concentrated in the signing backend; London EVM compatibility risk; the testnet credit line has little real economic consequence; and the claim that a leaked agent key cannot borrow does not hold in the window where the owner has already signed a ticket.

The team adopted just-in-time tickets, a fixed EIP-712 domain, on-chain `dueAt` with permissionless `suspend`, and `draw` as `onlyPolicy`. It rejected the “preflight deadlock” finding and the request to add a separate ticket deadline (expiry already exists). It did not adopt Gemini’s predicted score range. Numbers are omitted in this public repository.

---

## Redacted prompt

# Role

You are a skeptical MetaEarth Hackathon 2026 (HARBOR) judge and a smart-contract security reviewer. You are independent of the team. Be adversarial, specific, and evidence-based. Do not be polite at the expense of truth. Do not rewrite the team's documents, slides, or narration. Do not invent official rules that are not in the brief. If something is unknown or cannot be verified from the materials, say so.

Write your entire answer in Simplified Chinese. Use short headings. For each finding, say whether it is a fact about the design as written, or an inference. Cite the relevant contract method, demo step, or scoring line when you can.

# What we need (one round only)

1. **Top 5 weaknesses judges would hit.** Rank by how much they would actually move a score, not by how clever they sound.
2. **Security / logic holes** in MeIdGate, AgentPolicy, and AgentCredit, and in the ticket model (EIP-712 owner-signed per-draw tickets, `spentNonce`, `min(maxAmount, 50)`), `preflight`, keeper suspension, and backend trust. Include replay, authorization, signature binding, nonce policy, overdue detection, and any mismatch between the marketing claim "a leaked agent key cannot borrow" and the actual ticket flow.
3. **Coherence:** is "Earn it. Lose it. Spend it once." consistent with a revolving 100 test MEC limit plus one-time tickets? Where does the slogan over-claim?
4. **Scoring:** the team had internal planning scores for the full-merge plan (on the official 0–5 scale, weighted 30 / 25 / 20 / 15 / 10), a higher figure if the 7 Dec testnet checks all pass, and similar figures for both fallbacks. Those numbers are omitted here because this repository is public. Qualitatively: is the team's scoring realistic, too high, too low, or internally inconsistent?
5. **Concrete improvements**, ranked by expected score impact per developer-day, given that the team still has **no Solidity developer**, registration is due 11-29 23:59 Asia/Shanghai, a developer must be in place by 12-01, checks are on 12-07, and submission is 12-21.
6. **Anything to cut** from the MVP, demo, or story so the remaining loop is more likely to work and to be believed.

Do not produce a rewritten pitch, a rewritten interface, or a new document. Recommendations should be brief and actionable.

# Official context (treat as given)

- Event: MetaEarth Hackathon 2026: HARBOR. Tracks include On-Chain Finance and AI (or both).
- Judging weights: Technical implementation 30, ME application 25, Product value 20, Innovation 15, User experience 10.
- Demo video: 3–5 minutes, English voiceover or English subtitles, must show core flow.
- Must run at least one experienceable core feature on ME Network, and submit ME Network contract / tx records (or Rollapp + Hub info).
- Submission deadline: 2026-12-21 23:59 Asia/Shanghai. Registration deadline: 2026-11-29 23:59 Asia/Shanghai.
- Team size 2–5; all members need advanced ME ID certification. All submission materials in English.
- ME Network: Cosmos SDK ME Hub + Ethermint EVM. Testnet EVM chain ID 400, mainnet 2404. MEC is the EVM native coin, 8 decimals. Ethermint depends on go-ethereum v1.10.26 (London EVM). Testnet RPC is a bare HTTP IP; HTTPS pages need a proxy.
- ME ID lives in Hub native modules `x/did` and `x/kyc`. EVM contracts cannot read ME ID (no precompile). The official query path is off-chain: JS SDK `getMeIdByAddress` or REST `/metaearth/did/did`. One ME ID binds exactly one EVM sub-account.
- Therefore the team attests ME ID via a backend EIP-712 signature that MeIdGate verifies. They plan to say this honestly on stage.
- Team has **no developer yet**. Hiring a Solidity developer by 12-01 is a hard gate; if it slips, they fall back to the v3 design (CreditScore, no ERC-8498).
- ERC-8498 is a Draft (namespaced state transitions for SBTs). Reference implementation: https://github.com/XiaoHai67890/evolving-sbt (compiled for Cancun; must be rebuilt for London). Ticket spend / revolving credit is application-specific and is not in the core ERC ABI.
- No real lending, interest, or liquidation in the hackathon build. Demo uses test MEC. Real lending is "on the roadmap."
- Business line is a subscription, not a loan book.

# Document A — Full-merge execution plan (current; ignore the folded 11-27 old evaluation)

Product name: AgentGuard. One product, not two. Credit is a soulbound ERC-8498 credential bound to an ME ID / DID, holding a revolving line; each agent borrow spends one one-time ticket signed by the owner.

## Contracts (3)

Backend (SDK looks up ME ID, signs EIP-712) → MeIdGate (verify sigs, DID dedup, trigger mint) → AgentCredit (ERC-8498 SBT + ledger + ticket spend). Agents talk to AgentPolicy (authorization and caps), which calls AgentCredit `draw` / `repay`. A keeper script calls AgentCredit `suspend` on overdue debt.

Interface sketch (field names may change; this is the agreed sketch):

```
// 1. MeIdGate
function register(address owner, bytes32 didHash, uint256 deadline, bytes backendSig, bytes ownerSig) external;
//   backendSig: backend EIP-712 attestation of ME ID check (address, DID hash, expiry)
//   ownerSig: owner's EIP-712 consent over (didHash, deadline), to satisfy ERC-8498 "initialization requires holder consent"
//   verify backendSig -> verify ownerSig -> dedup didHash -> AgentCredit.mintFor(didHash, owner, ownerSig)

// 2. AgentCredit: ERC-8498 core + credit ledger + ticket spend (merges former CreditScore and CreditLedger)
function stateOf(uint256 tokenId, bytes32 ns) external view returns (StateHead memory);
function policyOf(bytes32 ns, bytes32 policyId) external view returns (Policy memory);
function applyTransition(Change calldata c, bytes calldata evidence, bytes calldata auth) external;
event StateTransitioned(...);
function mintFor(bytes32 didHash, address owner, bytes ownerSig) external; // onlyMeIdGate
function creditOf(bytes32 didHash) external view
  returns (uint64 limit, uint64 outstanding, uint8 tier, uint8 status, uint64 revision);
mapping(bytes32 didHash => mapping(uint256 nonce => bool)) public spentNonce;
function draw(bytes32 didHash, Ticket calldata t, bytes calldata ownerSig) external;   // onlyAgentPolicy
//   Ticket = EIP-712 { address agent; uint64 maxAmount; uint256 nonce; uint64 expiry }
//   owner signs one ticket off-chain per draw
//   require status == Active
//   require signer == DID owner
//   require t.agent == the calling agent
//   require block.timestamp <= t.expiry
//   require amount <= min(t.maxAmount, perTradeCap)   // perTradeCap is AgentPolicy's per-trade cap; Demo = 50 MEC
//   require !spentNonce[didHash][t.nonce]
//   Front/back-end also reject maxAmount > per-trade cap at signing time
//   spentNonce = true; outstanding += amount <= limit; applyTransition(revision + 1)
//   reuse -> revert "ticket already spent"
function repay(bytes32 didHash, uint64 amount) external;  // anyone may repay for the owner; on-time full repay -> tier + 1 in ERC-8498 state only; limit stays 100 during the hackathon
function suspend(bytes32 didHash) external;               // onlyKeeper, only when overdue
function resume(bytes32 didHash) external;                // onlyController (team multisig)
event TicketSpent(...); event Repaid(...);                // product-side additions

// 3. AgentPolicy
struct Ticket { address agent; uint64 maxAmount; uint256 nonce; uint64 expiry; }
function authorize(address agent, Limits calldata l, uint64 expiry) external;     // owner
function revoke(address agent) external;                                          // owner
function preflight(Trade calldata tr, Ticket calldata t, bytes calldata ownerSig)
  external view returns (bytes32[] memory failedChecks);
  // read-only; returns ALL failed checks (over cap / asset not allowlisted / leverage too high / ticket already spent / …)
  // audit panel calls this off-chain, then submits execute
function execute(Trade calldata tr, Ticket calldata t, bytes calldata ownerSig) external; // agent
  // on-chain revert returns only the first failure reason
  // checks per-trade cap / allowlist / leverage / expiry -> AgentCredit.draw(didHash, t, ownerSig) -> record fill
```

## Credit model: revolving line + one-time tickets

The team's reconciliation of a former slogan clash: the **line** revolves (100 test MEC, repayment restores availability); the **ticket** is one-time (nonce marked spent). A leaked agent key, or a revoked agent, cannot reuse a spent ticket.

- Earn it: a verified ME ID gets a 100 test MEC line; on-time repayment writes revision+1 and tier+1 into ERC-8498 state only; the limit stays 100 during the hackathon. Shown in demo steps 4 and 8 (small Tier 0→1 badge, no extra voiceover).
- Spend it once: owner signs one EIP-712 ticket per draw; AgentCredit records spent nonces; reuse reverts. Steps 6 and 7.
- Lose it: after overdue, keeper calls `suspend`; Active → Suspended; all agents cannot borrow. Step 9 is one sentence; the tx hash is in the repo, not performed live in the video.

The security sales claim: even if an agent key leaks, the attacker has no unused owner-signed ticket, so they cannot borrow.

## 9-step demo (voiceover ~389 words, ~3:23 including ~30s on-chain waits; ~3:51–3:53 with UI clicks; stay under 4:30)

1. HyprEarn (14 Nov 2026) reported unauthorized trades on Hyperliquid accounts that had approved its agent wallets; root cause, account count, and losses were never disclosed.
2. Zodiac Roles and session keys already limit what an agent can do; AgentGuard adds "who it acts for." Tagline: "Every AI agent has a human behind it. AgentGuard proves who."
3. Teammate's real ME ID; backend checks via Meta Earth SDK (DID active, KYC complete); EIP-712 attestation; MeIdGate on testnet verifies; one native ME Hub tx binds the owner's sub-account.
4. Register mints one soulbound credit record in draft ERC-8498 format, bound to the DID: Active, 100 test MEC revolving line. Wallet with no ME ID gets 0. Same DID again reverts.
5. Owner authorizes Agent A: 50 MEC per trade, two assets, 3x leverage, seven days. Each draw needs a one-time credit ticket. Limits live in AgentPolicy.
6. Agent A reasons off-chain, spends one ticket to borrow 40 MEC, trades inside limits. Nonce marked spent; borrow booked to the owner's DID, not the agent key. Trade is recorded to a test address (no real DEX).
7. Inject a malicious instruction: 400 MEC into an unknown asset at 10x, reusing the spent ticket. Audit panel preflight lists four reasons; then one real on-chain revert is shown (e.g. "ticket already spent"). Voiceover must not say the chain returned four reasons.
8. Revoke A, register B. B sees 60 left and 40 owed. B repays; the full 100 is available again; revision +1; tier badge 0→1. Limit stays 100.
9. "Miss a repayment and a keeper suspends the record for every agent at once; that transaction is linked in our repo. Lose it. Today our backend signs the ME ID attestation, and we say so. Subscription, not a loan book. Swap the agent, keep the credit. One verified human behind it."

Narrative hierarchy: main tagline as above; subtitle "Verified humans. Bounded agents. Credit that follows the person."; credit-module three-beat "Earn it. Lose it. Spend it once." only as a small heading, not beside the main tagline. Externally say only "built on the draft ERC-8498 interface"; do not claim co-authorship or a market gap until public proof exists.

## Schedule and 12-07 checks

- 11-29 23:59: finish registration, project name AgentGuard.
- 12-01 hard gate: Solidity developer in place, else ship v3 (CreditScore, no 8498).
- 12-01 to 12-03: rebuild reference implementation for London, re-run 51 tests, deploy to chain 400; scaffold MeIdGate, AgentPolicy, backend signer.
- 12-04 to 12-06: AgentCredit ledger, ticket spend, suspend/resume; unit tests in three blocks. Measure ME testnet block gas limit (do not put the number in external materials until measured) and gas of one borrow tx.
- **12-07 checks:** (1) 8498 core `applyTransition` works on chain 400; (2) ticket spend and reuse-revert work on testnet; (3) one borrow transaction (`execute` → `draw`, including `applyTransition`) uses at most 500k gas.
  - All three pass → stay on full merge; the technical self-score may be raised. (Number omitted.)
  - (1) passes but (2) or (3) fails → light merge: drop tickets; ERC-8498 credential only carries line state and suspension; demo step 7 drops the "ticket already spent" reason. (Internal score omitted.)
  - (1) fails, or no developer by 12-01 → v3 CreditScore, do not mention 8498. (Internal score omitted.)
- 12-08 to 12-12: frontend (line, tickets, revision, audit reasons), off-chain agent reasoning, keeper script; one real suspend tx on testnet.
- 12-13 to 12-14: freeze contracts, internal review (not an audit), demo rehearsal.
- 12-15 to 12-17: record demo, verify runtime ≤ 4:30.
- 12-18 to 12-21: English submission materials; README lists addresses and tx hashes.

## Team self-score

The team's numeric self-score table (0–5 per official category, weighted 30 / 25 / 20 / 15 / 10) is omitted because this repository is public. Qualitatively, the team told the reviewer:

- UX was raised after mitigation because the credit story is now coherent and the demo fits the time box.
- Tech stays conservative until testnet proof: still a Draft standard + custom unaudited spend logic + no developer; only the 7 Dec checks would justify a raise.
- Innovation credits the ticket that binds credit to agent safety, with room for judges to go higher if they like that link.
- Product value is unchanged: no evidence yet of lender demand. 5–8 seed interviews are planned before submission; value uses a recorded sales validation strength (number omitted).

# Document B — Product report v4 (full merge), key points only

Current official primary idea: AgentGuard full merge (credit line + ERC-8498). Internal planning scores omitted. Positioning: others limit what an AI agent can do; AgentGuard proves who it acts for.

Must-build: backend signer; MeIdGate; Hub `bindSubAccount` tx; AgentCredit (London rebuild of 8498 core + `agentguard.credit` namespace, 100 test MEC at 8 decimals, spent nonces, tier+1 without raising the limit, suspend/resume); AgentPolicy caps + ticket check then draw; revoke-then-register; keeper suspend script (overdue manufactured with a short expiry, not shown in the video); off-chain LLM agent with hashed I/O; audit panel + HTTPS RPC proxy; English README with addresses and hashes.

Optional: MEC fee for agent calls; stop-loss; own Rollapp; daily AI reports.

Out of scope: mainnet; real lending/interest/liquidation; `me.staking` tier-ups; ZK private presentation; changing the limit by tier; AI deciding the line or originating loans; real DEX / cross-chain / CEX; tokenomics; mobile.

Real vs simulated: real teammate ME ID and a real Hub binding tx; all three contracts on chain 400; line, debt, spent nonces, tier, revision on-chain; ticket signatures created off-chain and verified on-chain; execute / unauthorized / reuse reverts on-chain; keeper suspend is a real testnet tx. Simulated: backend (not ME) issues the ME ID attestation (said on stage); test MEC, no interest or liquidation; fills go to a test address, no real DEX; agent reasoning off-chain; overdue is manufactured; keeper is a script.

Known risks already listed by the team:
1. Backend signer is a trust point; credential pause rights sit with a team controller/multisig.
2. ERC-8498 is Draft; one-time consumption is custom, unaudited.
3. Reference implementation targets Cancun; ME Ethermint is London — must strip PUSH0 / tstore / tload / mcopy / OZ Transient helpers and re-run 51 tests on chain 400.
4. No Solidity developer yet.

Prepared answers: backend can only attest "this address has an ME ID"; signer address public; attestations expire and can be revoked; anyone can re-check via public REST; spending limits and tickets do not depend on the backend; later: multi-signer or native VC / precompile.

Comparison ideas kept only as alternatives: MEC pay-per-call gateway; RWA eligibility gateway. (Internal scores omitted.)

# Document C — Pitch and demo narration (current draft)

External wording rules (not shown on slides): never imply the user or the contract reads ME ID; never claim unique fine-grained permissions; HyprEarn facts only, no invented loss numbers; ERC-8498 wording limited to "built on the draft ERC-8498 interface"; do not say the line itself is one-time; do not say repayment raises the limit; do not put the block gas limit in external materials.

10-page live pitch: (1) cover + tagline, two tracks, on ME; (2) problem / HyprEarn / prompt-or-server limits; (3) KYA / MAS / agent-trading volume context; (4) Zodiac / ZeroDev / Hyperliquid approveAgent — tools limit what, not who; (5) three layers: verified human (backend + MeIdGate + ownerSig), bounded agent (AgentPolicy), credit + tickets (AgentCredit); subtitle for credit: "Earn it. Lose it. Spend it once."; (6) Why ME Network, including ME's claim of 7.5M KYC-verified ME Pass users; (7) live demo pointer; (8) business — live pitch only, not in the 3–5 min video; subscription hypotheses $9–19 / $49–99, not closed prices; 5–8 interviews not yet done; (9) honest limits and roadmap without dates, "on the roadmap"; (10) close: "Swap the agent, keep the credit. One verified human behind it."

Q4 already admits Draft, unaudited ticket logic, testnet only.

# Constraints for your answer

- Answer in Simplified Chinese.
- One review only; do not rewrite the docs.
- Prefer fewer, sharper points over a long laundry list.
- When you mention ERC-8498 or ME Network behavior, be careful: if you are not sure, mark it as something that must be verified, do not state it as fact.


---

## Redacted response

# Gemini review — 20261127-235849

- created: 2026-11-27 23:59:06 Asia/Shanghai
- prompt: see “Redacted prompt” below (original path on the build machine omitted)
- model: gemini-3-flash-preview
- http_status: 200
- ok: true
- finish_reason: STOP
- usage: {"promptTokenCount": 4908, "candidatesTokenCount": 1617, "totalTokenCount": 7784, "promptTokensDetails": [{"modality": "TEXT", "tokenCount": 4908}], "thoughtsTokenCount": 1259, "serviceTier": "standard"}
- attempted: gemini-3.1-pro-preview@429, gemini-2.5-pro@404, gemini-3-flash-preview@200

## Response

作为一名持怀疑态度的 MetaEarth Hackathon 2026 评委与安全审计员，以下是针对 AgentGuard 项目的评审报告。

### 1. 评委最关注的 5 大弱点（按扣分权重排序）

1.  **核心开发力缺失 (Technical Implementation):** 截至 11-27 仍无 Solidity 开发人员。对于一个依赖 Draft 标准 (ERC-8498) 且需在 London EVM 环境重构代码的项目，这是致命的。若 12-01 无法到位，项目大概率沦为 PPT。 (事实)
2.  **后端中心化信任风险 (ME Application):** 营销声称“验证人类”，但合约逻辑完全依赖后端 EIP-712 签名（`MeIdGate.register`）。后端一旦被黑或伪造签名，整个 DID 绑定机制崩溃。评委对“诚实告知”加分，但对架构脆弱性扣分。 (推理)
3.  **London EVM 兼容性风险 (Technical Implementation):** ERC-8498 参考实现针对 Cancun (PUSH0, TLOAD 等)。在 Ethermint (London) 上重构若出现指令集错位，可能导致 `applyTransition` 逻辑在测试网静默失败或 Gas 溢出。 (事实)
4.  **“信用”逻辑的经济空洞 (Product Value):** 缺乏清算、利息和真实资产抵押。100 MEC 的额度只是一个计数器。如果“Lose it”只是停用一个测试网权限而无实际经济损失，产品的“信用”属性难以说服金融赛道评委。 (推理)
5.  **代理密钥泄露的防御边界模糊 (UX/Security):** 团队宣称“泄露代理密钥无法借款”，但如果 Owner 已签署 Ticket 且 Agent 在执行前被黑，黑客**可以**利用该 Ticket 借款。宣传语存在过度承诺。 (推理)

### 2. 安全与逻辑漏洞分析

*   **Ticket 绑定与重放 (Replay):** `spentNonce` 仅在 `AgentCredit` 中记录。如果 EIP-712 Domain Separator 未严格包含 `verifyingContract` 地址和 `chainId` (400/2404)，Ticket 可能在不同部署版本间重放。 (事实)
*   **签名绑定漏洞:** `AgentCredit.draw` 校验了 `t.agent == msg.sender`。但如果 Agent 逻辑存在漏洞被注入恶意指令，由于 Ticket 已由 Owner 签名，Agent 仍能合法调用 `draw`。Ticket 无法绑定具体的交易内容（如买什么资产），只能限制金额。 (事实)
*   **`preflight` 逻辑不一致:** `preflight` 是 `view` 函数。在 `preflight` 检查通过到 `execute` 实际执行之间，如果 `spentNonce` 或 `outstanding` 发生变化，`execute` 仍会 revert。这会导致 Agent 策略层出现逻辑死锁。 (推理)
*   **Keeper 悬挂风险:** `suspend` 依赖外部 Keeper 脚本。若 Keeper 离线或 Gas 不足，逾期账户将持续保持 `Active` 状态，Agent 可继续抽干额度。 (事实)
*   **后端信任链:** `MeIdGate` 无法验证 `didHash` 是否真的属于 `owner` 地址，只能信任 `backendSig`。这是一个典型的“预言机信任问题”。 (事实)

### 3. 一致性审查：“Earn it. Lose it. Spend it once.”

*   **口号冲突:** 100 MEC 的“循环额度” (Revolving) 与 “Spend it once” 存在语义矛盾。
*   **事实:** 循环的是**额度总额**，单次消耗的是**Ticket 授权**。
*   **过度承诺点:** “Spend it once” 容易让用户误以为信用额度是一次性的。实际上，如果用户一次性签发了多个 Nonce 的 Ticket，Agent 依然可以多次提款。口号在强调安全性时掩盖了“授权管理”的复杂性。

### 4. 评分合理性评估（内部数字已省略）

*   **结论：偏高且内部不一致。**
*   **理由：**
    *   **技术项：** 在没有开发者的前提下，给出的技术分已属“潜力分”。若 12-07 仅通过基础测试，不足以支撑上调，因为 Draft 标准的生产环境安全性未经验证。
    *   **ME 应用：** 给到该项满分可能过誉。虽然解决了 DID 读取问题，但引入了中心化后端签名，这在去中心化网络中是减分项。建议下调。
    *   **创新：** 该项判断合理。将 ERC-8498 用于 AI 代理准入具有新意。
    *   **体验：** 偏高。用户每笔借款都要签名 Ticket，对于“自动化代理”来说，这种交互体验非常割裂。
*   **预测得分：** Gemini 给出了具体预估区间（数字已省略，因本仓库为公开仓库）。团队未采纳该预估。前提是：除非 Demo 能展示极高的完成度和流畅的 London EVM 兼容性，否则其认为自评偏高。

### 5. 具体的改进建议（按开发人天产出比排序）

1.  **强化 EIP-712 Domain (高影响/0.5天):** 确保 Ticket 签名包含 `verifyingContract` 和 `chainId`，防止跨链/跨合约重放。 (Security)
2.  **Ticket 增加 `deadline` (中影响/0.2天):** 在 `Ticket` 结构体中强制加入短效过期时间，减少 Ticket 被截获后的攻击窗口。 (Security)
3.  **公开 Backend 验证逻辑 (中影响/0.5天):** 在 README 中提供简单的 JS 脚本，允许评委自行调用 REST 接口验证 `didHash` 与地址的对应关系，缓解中心化质疑。 (Trust)
4.  **精简 ERC-8498 (高影响/2天):** 移除所有 London EVM 不支持的指令，仅保留 `applyTransition` 核心逻辑，确保 12-07 检查必过。 (Technical)

### 6. 建议从 MVP/Demo 中删减的内容

*   **删掉“Tier 提升增加额度”的暗示:** 既然 Hackathon 期间额度固定为 100，就不要在 Demo 中提“未来会涨”，避免评委追问额度计算模型。
*   **删掉复杂的“Audit Panel” UI:** 只要展示 `preflight` 返回的错误字符串即可。过多的 UI 细节会暴露后端逻辑的延迟。
*   **删掉“Real Lending”路线图:** 在没有清算机制的情况下谈借贷会招致金融合规和坏账处理的质疑，专注于“AI 代理行为准入” (Guardrail) 更有说服力。
*   **删掉视频中的 Keeper 执行过程:** 仅展示 `suspend` 后的结果（Agent 调用失败）。演示脚本运行过程容易出错且浪费时间。

