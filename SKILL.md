---
name: xiran-goal
description: Use when the user gives a goal and wants the agent to drive toward a concrete result, reduce ambiguity, produce stable decomposition, or create a condition tree for execution. Trigger: /xiran-goal, "帮我分解目标", "怎么做才能", "如何实现", "分析条件", "拆解一下".
---

# Xiran Goal

## Core Principle

Treat the user's request as a goal to finish, not as a prompt to improvise.

Always identify the final goal first, then choose the shortest verifiable path to reach it. Stability matters: for the same goal and same known facts, produce the same structure, same ordering logic, and same completion standard.

## Stable Output Contract

Unless the user asks for another format, answer in this fixed order:

1. `Final Goal`: one sentence.
2. `Assumptions`: only list assumptions that materially affect the answer.
3. `Condition Tree`: use the clearest tree format for the user; prefer horizontal Mermaid only when readable.
4. `Priority Path`: concrete actions in dependency order.
5. `Verification`: how the user can tell the goal is met.

If the user only asks a direct question and does not need a tree, skip `Condition Tree` but keep the same reasoning order internally.

Stability means the same goal uses the same causal judgment, not that every output has the same number of branches, same depth, or same visual shape.

The goal is to solve the user's actual problem. Do not optimize for looking balanced, polished, comprehensive, or pleasing if that weakens the diagnosis or makes the output less actionable.

Prefer evidence-driven asymmetry over decorative regularity. The output should feel useful because branches reflect real bottlenecks, tradeoffs, and next actions, not because it imitates a polished template.

## Causal Decomposition Rules

Use this fixed condition order whenever the goal is broad or social:

1. Survival baseline: health, safety, legality, mental stability.
2. Resource capacity: skills, income, assets, time, tools.
3. Social capacity: trust, reputation, network, status, cooperation.
4. Selection quality: choosing environments, people, opportunities, constraints.
5. Execution system: habits, feedback loops, measurement, iteration.
6. Risk control: downside avoidance, irreversible losses, conflict, addiction, debt.
7. Long-term compounding: durability, optionality, transfer to future goals.

Do not reorder these branches unless the user gives a domain where another order is clearly more direct. If reordered, state the reason in one sentence.

Do not force every branch to have the same number of children. Real goals are uneven. A branch with one decisive bottleneck should have one child; a branch with many independent conditions can have more.

Do not force every branch to have the same depth. Some branches should stop early because the next action is obvious; others should go deeper because the bottleneck is unclear or risky.

Do not create fake irregularity for style. Irregularity is only valuable when it comes from actual causal differences: one branch is a bottleneck, one branch is already solved, one branch is risky, one branch needs a decision, or one branch has an immediate next action.

## Tree Rules

When drawing a condition tree:

- Use `flowchart LR` only when the graph remains readable. If the user says it is hard to read, use an indented text tree.
- Root node is the user's final goal.
- Use as many first-level branches as the causal structure requires; prefer 3 to 8, but do not pad.
- Depth follows usefulness: stop when the next action is concrete enough to execute or verify.
- Uneven trees are correct when the real dependency structure is uneven.
- Use verbs and concrete methods when possible, not only abstract nouns.
- Avoid duplicate sibling nodes.
- Put risk-control branches near the condition they constrain, or last if it applies globally.

## Practicality Filter

Every leaf node should pass at least one of these tests:

- It names an observable condition.
- It names an executable action.
- It names a decision criterion.
- It names a measurable constraint.
- It names a bottleneck that must be removed before progress is possible.

If a node is only a concept label, expand it into practical subconditions or replace it with a concrete method.

Before finalizing a tree, run this check 🔴:

- Which branch is the current bottleneck?
- Which branch can stop early because the next action is obvious?
- Which branch needs deeper decomposition because failure there is expensive?
- Which branch is only a supporting condition, not a main path?

Reflect those answers in the tree shape. Do not make the tree visually even if the answers are uneven.

Bad:

```text
社会能力 -> 高价值 -> 影响力 -> 个人品牌
```

Better:

```text
社会能力
├─ 每周认识3个同领域可合作的人
├─ 每月至少完成1个可展示成果
├─ 守约交付以积累可信记录
└─ 进入能带来机会的固定场域
```

## Execution Loop

Use this loop until the goal is met or blocked:

1. Observe current state.
2. Identify the gap from the final goal.
3. Pick the shortest verifiable next action.
4. Execute or produce the requested artifact.
5. Record what changed.
6. Verify whether the requested result has been delivered.

Report only what helps the user move forward.

## Clarification Rule

⚠️ Ask a question only when one missing fact would materially change the output and a reasonable assumption would be risky.

If asking, ask exactly one concise question.

Otherwise proceed with explicit assumptions.

## Anti-Drift Rules（反例黑名单）

以下 12 条是 xiran-goal 明确禁止的行为，每条都是实战中踩过的坑：

- Expand endlessly into philosophy.
- Change the causal judgment between similar runs without new facts.
- Prioritize tool testing over the user's result.
- Make branches artificially symmetrical.
- Force identical depth across unrelated branches.
- Add filler nodes to make the tree look complete.
- Choose prettier structure over sharper diagnosis.
- Add randomness or artificial unevenness to appear human.
- Optimize for completeness when a smaller answer is enough.
- Replace concrete actions with impressive concept labels.
- Tell the user what sounds satisfying instead of what is most useful.
- Invent personal facts about the user.

When uncertain, prefer the stable default order in `Causal Decomposition Rules`, then let the actual causal structure determine branch count and depth.

## Failure Modes & Fallbacks

if-then 分支表——遇到以下情况不要卡住或跳过，按表执行：

| 触发条件 | 一线处理 | 仍失败时 |
|---|---|---|
| 用户目标太模糊，无法分解 | 问一个精确澄清问题（遵守 Clarification Rule） | 列出 2-3 个最可能的解读，各给一句话方案，让用户选 |
| 因果顺序不适用当前领域 | 选择最直接的顺序，一句话声明原因 | 回退到通用分解：输入→加工→输出→验证 |
| 条件树 >8 个一级分支 | 合并相似分支为更概括的条件组 | 优先保留瓶颈分支，辅助分支可合并为一句 |
| 验证标准无法量化 | 改用"可观察的行为变化"代替数字指标 | 明确声明"无法量化验证，以下为定性判断" |
| 用户对树结构有异议 | 问"哪个分支你觉得不对"，只改那一个 | 保留其余分支，标记争议分支待确认 |
| 目标是简单操作问题（如"怎么写贪吃蛇"） | 跳过 Causal Decomposition Rules 的 7 层顺序，直接用执行步骤拆解 | —（此类目标到执行层即可） |

## Complete Example

For a goal like "how to accumulate high-income skills," the output looks like this. 注意树的形状：瓶颈分支深挖到4层，辅助分支只到1-2层；每个节点不超过20字；所有分支深度不同。

---

**Final Goal**
拥有一项让市场持续付高价的技能，不依赖单一雇主。

**Assumptions**
合法路径；技能积累需要时间，不做短期暴富假设。

**Condition Tree**

```text
积累高收入技能
├─ 选对技能方向
│  ├─ 三个条件：有人付钱、不易替代、能做样品
│  └─ 交叉领域溢价更高
├─ 进入真实交易 ⚠️ 最大瓶颈
│  ├─ 学到能卖的最低水平就立刻卖
│  ├─ 接受前几次交付可能不合格
│  ├─ 定价策略
│  │  ├─ 第一个客户可以很低甚至免费
│  │  └─ 目的是换可展示的案例和推荐
│  └─ 客户反馈比课程更精准
├─ 把技能变成可脱离时间的资产
│  └─ 一对一服务 → 一对多产品
└─ 防贬值
   └─ 单一客户收入不超过50%
```

**Priority Path**

1. 列出3个有基础且市场付钱的方向，选交叉领域
2. 找到第一个付费客户（可低价），进入真实交易
3. 交付3-5个案例后从反馈中迭代并提价
4. 一年后思考如何把服务变成产品

**Verification**
- 有人未经过推销主动来找你付费
- 时薪在上升而非被压低
- 请假一个月，至少部分收入不中断

---

## Completion Standard

The task is complete only when the requested artifact, answer, or verified result has been delivered.

If verification cannot be performed, state exactly what cannot be verified and why.
