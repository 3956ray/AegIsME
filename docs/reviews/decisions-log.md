# AegisME 决策日志 / Decision log

> **项目现名 / Project name:** AegisME（原名 AgentGuard / formerly AgentGuard）  
> **计划合约名 / Intended contract names:** `AegisVault`、`ERC8498AgentRegistry`、`MeIdGate`  
> 早期方案正文仍可能使用 AgentGuard、`AgentPolicy`、`AgentCredit` 等历史名称，本文不擅自改写接口草图。  
> Early planning text may still use those historical names; interface sketches are left as written.
>
> **公开仓库说明 / Public-repo note:** https://github.com/3956ray/AegIsME 为公开仓库。内部评委规划分（self-score）已全部省略，不得写入路演、提交材料或对外简介。不得把「ERC-8498 共同作者」或「市场空白 / market gap」写成既成事实。  
> This repository is public. Internal judging scores have been omitted. Do not claim ERC-8498 co-authorship or a market gap as fact.

## 中文

# AegisME 决策日志

- 日期：2026-11-27 至 2026-11-28（Asia/Shanghai，UTC+8）
- 状态：当前
- 项目现名：AegisME（原名 AgentGuard）

## 1. 用户拍板：完全合并

用户先要求把 ERC-8498 当作独立新产品评估，随后要求评估「以 AgentGuard 为主，结合信用额度与 ERC-8498」，并在组件中选择「我想完全合并」。

因此当前唯一主方案是：**一个产品**（现名 AegisME）：绑定在 ME ID 上的 ERC-8498 灵魂绑定信用凭证里放循环额度；代理每借一笔必须消耗一张主人现签的一次性借款券。

执行方案见 [../plan/full-merge-execution-plan.md](../plan/full-merge-execution-plan.md)。11-27 当时建议的「轻度结合」只作为 12-07 检查点的第一级退路保留。

## 2. 来自 Gemini CLI 评审（2026-11-27 23:59 Asia/Shanghai）的决定

模型为 `gemini-3-flash-preview`（免费密钥无 Pro 配额；`gemini-3.1-pro-preview` 与 `gemini-2.5-pro` 当时不可用）。完整提示词与回复见 [gemini-round-1-2026-11-27.md](gemini-round-1-2026-11-27.md)。

### 已采纳

1. **借款券只能现签。** 主人在每次借款前即时签名；`expiry` 不超过 10 分钟；不允许批量预签。对外口径固定为：`Without a fresh owner-signed ticket, a leaked agent key cannot borrow.` 预签若存在代理端，密钥泄露时券会一起泄露。合约只能检查过期时间，禁止预签由前端执行。
2. **固定 EIP-712 Domain，Ticket 含 didHash。** Domain 为 `name`、`version`、`chainId`（测试网 400）、`verifyingContract`。Ticket 字段为 `{ agent, didHash, maxAmount, nonce, expiry }`，防止跨 DID / 跨链 / 跨合约重放。
3. **到期与暂停不依赖 keeper。** 每笔 `draw` 在链上记录 `dueAt`；`suspend(didHash)` 任何人可调用，仅当 `block.timestamp > dueAt` 且 `outstanding > 0` 时成功。keeper 只是调用方之一，不是暂停开关。
4. **权限与限额检查的位置。** `draw` 为 `onlyPolicy`；`AgentPolicy.execute` 在调用 `draw` 之前检查金额不超过 `min(maxAmount, perTradeCap)`（Demo 单笔上限 50 test MEC）。
5. **分数只作内部规划，不对外展示。** 本公开仓库中相关数字已全部删除。

### 已驳回或不采纳

1. **「preflight 会死锁」。** 否决。`preflight` 是只读预检，与 `execute` 之间出现状态变化是正常竞态，`execute` 直接 revert 即可，不构成死锁。
2. **「给 Ticket 增加 deadline」。** 否决。字段 `expiry` 已经存在，不必再加一个 deadline。
3. **Gemini 给出的评委得分预估。** 未采纳其数字；团队另有内部推断区间。两类数字均不写入本公开仓库。
4. **删掉审计面板、只展示一行错误字符串。** 未采纳。审计面板仍先展示 `preflight` 返回的四条原因，再提交一笔真实的链上 revert（只返回第一条失败原因）。
5. **视频中不要出现 keeper 执行过程。** 部分采纳：视频不演示 keeper 脚本；`suspend` 交易哈希放进仓库；旁白说「任何人可暂停」。keeper 脚本仍可作为及时调用的工具保留。
6. **不要暗示还款会提高额度。** 已采纳（与原方案一致）：按时还款只把凭证 `tier` + 1，黑客松期间额度固定 100 test MEC。

## 3. 命名（2026-11-27 / 11-28）

用户在 Gemini 网页版讨论中把项目名定为 **AegisME**，金库合约 **AegisVault**，注册表 **ERC8498AgentRegistry**，身份桥 **MeIdGate**。该网页对话见 [gemini-web-chat-harbor.md](gemini-web-chat-harbor.md)。

网页版里的架构草稿（例如把额度写成可消耗的 `agent.quota`、示例 500 MEC 等）**不是**当前执行方案。当前方案以 `plan/` 与 `product/` 为准：循环 100 test MEC 额度 + 一次性借款券，历史接口名仍为 `MeIdGate` / `AgentPolicy` / `AgentCredit`。

## 4. 仍待用户完成的事项

- 11-29 23:59（北京时间）前完成报名；项目名使用 AegisME。
- 12-01 前找到 Solidity 开发者（硬前提；否则退回 v3 CreditScore，路演不提 ERC-8498）。
- 若要对外部使用「共同作者」表述，需提供可公开核验的证据（官方讨论帖作者栏目前只能核到 XiaoHai）。
- 提交缺失的官方 Demo 视频计划章节。
- 完成种子用户与出资人/策展人访谈；在 ME 开发者 Telegram 群提出已拟定的三个问题。
- 对外访谈与发帖由用户亲自执行；代理人不得对外发送或下单。

---

## English

# AegisME decision log

- Dates: 27–28 Nov 2026, Asia/Shanghai (UTC+8)
- Status: current
- Project name: AegisME (formerly AgentGuard)

## 1. The user chose a full merge

The user first asked for ERC-8498 to be evaluated as a standalone product, then asked for an evaluation of combining AgentGuard with a credit line and ERC-8498, and selected “I want a full merge.”

The only current primary product is **AegisME**: a revolving credit line lives in an ERC-8498 soulbound credential bound to a ME ID, and every agent draw must consume a fresh, owner-signed, one-time ticket.

See [../plan/full-merge-execution-plan.md](../plan/full-merge-execution-plan.md). The 27 Nov “light merge” recommendation is kept only as the first fallback after the 7 Dec checkpoint.

## 2. Decisions from the Gemini CLI review (27 Nov 2026, 23:59 Asia/Shanghai)

The model was `gemini-3-flash-preview` (the free key had no Pro quota; `gemini-3.1-pro-preview` and `gemini-2.5-pro` were unavailable). Full prompt and reply: [gemini-round-1-2026-11-27.md](gemini-round-1-2026-11-27.md).

### Adopted

1. **Just-in-time tickets.** The owner signs immediately before each borrow; `expiry` is at most 10 minutes; no batch pre-signing. External wording is fixed: `Without a fresh owner-signed ticket, a leaked agent key cannot borrow.` If tickets were pre-signed and stored with the agent, a leaked key would leak the tickets too. The contract can only check expiry; the front end is what prevents pre-signing.
2. **Fixed EIP-712 domain, ticket includes didHash.** Domain: `name`, `version`, `chainId` (400 on testnet), `verifyingContract`. Ticket fields: `{ agent, didHash, maxAmount, nonce, expiry }`, to block replay across DIDs, chains, or contract deployments.
3. **Overdue suspension does not depend on a keeper.** Each `draw` records `dueAt` on-chain. Anyone may call `suspend(didHash)`; it succeeds only if `block.timestamp > dueAt` and `outstanding > 0`. A keeper is one caller, not a kill switch.
4. **Where caps are checked.** `draw` is `onlyPolicy`. `AgentPolicy.execute` checks that the amount is at most `min(maxAmount, perTradeCap)` (demo cap: 50 test MEC) before calling `draw`.
5. **Scores stay internal.** All such numbers have been removed from this public repository.

### Rejected or not adopted

1. **“Preflight deadlock.”** Rejected. `preflight` is a view. A state change between `preflight` and `execute` is an ordinary race; `execute` simply reverts. That is not a deadlock.
2. **“Add a deadline to the ticket.”** Rejected. The `expiry` field already exists.
3. **Gemini’s predicted judge-score range.** Not adopted. The team has a separate internal inferred range. Neither set of numbers is published here.
4. **Drop the audit panel and show only one error string.** Not adopted. The panel still shows all reasons returned by `preflight`, then one real on-chain revert (which returns only the first failure).
5. **Do not show the keeper running in the video.** Partially adopted: the video does not show a keeper script; the `suspend` transaction hash goes in the repo; narration says anyone can suspend. A keeper script may still exist as one timely caller.
6. **Do not imply that repayment raises the limit.** Adopted (already in the plan): on-time repayment only increments `tier`. The demo limit stays at 100 test MEC.

## 3. Naming (27–28 Nov 2026)

In the Gemini web chat, the user settled on the project name **AegisME**, vault contract **AegisVault**, registry **ERC8498AgentRegistry**, and identity bridge **MeIdGate**. See [gemini-web-chat-harbor.md](gemini-web-chat-harbor.md).

Architecture sketches in that chat (for example treating `agent.quota` as a consumed entitlement, or using 500 MEC examples) are **not** the current execution plan. The plan in `plan/` and `product/` is authoritative: a revolving 100 test MEC line plus one-time tickets. Historical interface names remain `MeIdGate` / `AgentPolicy` / `AgentCredit`.

## 4. Still waiting on the user

- Complete registration before 29 Nov 2026, 23:59 Beijing time, under the name AegisME.
- Find a Solidity developer by 1 Dec (hard gate; otherwise fall back to v3 CreditScore and do not mention ERC-8498).
- Provide public evidence before any external co-authorship claim (the official thread’s author field currently shows only XiaoHai).
- Send the missing official Demo video plan section.
- Run the seed and funder/curator interviews; ask the three prepared questions in the ME developer Telegram group.
- External outreach is done by the user. Agents must not send messages externally or place orders.
