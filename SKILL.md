---
name: xiran-goal
description: Use when the user gives a goal and wants Codex to drive toward a concrete result, reduce ambiguity, produce stable decomposition, or create a condition tree for execution.
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
- **Each node must be under 20 characters.** 超过就说明你在写句子而非命名条件。
- Use verbs and concrete methods when possible, not only abstract nouns.
- Avoid duplicate sibling nodes.
- Put risk-control branches near the condition they constrain, or last if it applies globally.

### Depth Rule — 最硬的约束

**禁止任何形式的均匀深度。** 三层均匀、两层均匀、每个一级分支下面都是N层——全部是错的。

构建每个分支时单独问：**下一步动作是否已经足够明显？** 明显就停，不明显就继续拆。瓶颈分支深挖到底，辅助分支可以只有一层。

构建完成后的自检：如果任何两个一级分支的深度相同，必须重做。树的深度分布看起来"不整齐"才是正确的。

Bad（均匀三层——每个分支都是3级深）:

```text
目标
├─ 分支A
│  ├─ A1
│  │  └─ A1a
│  └─ A2
│     └─ A2a
├─ 分支B
│  ├─ B1
│  │  └─ B1a
│  └─ B2
│     └─ B2a
└─ 分支C
   ├─ C1
   │  └─ C1a
   └─ C2
      └─ C2a
```

Better（真实因果——瓶颈深挖，辅助早停）:

```text
目标
├─ 关键瓶颈
│  ├─ 子条件1
│  │  ├─ 为什么难：涉及习惯改变
│  │  └─ 必须解决：否则其他分支无效
│  └─ 子条件2
├─ 辅助条件A
│  └─ 一步可完成，不需再拆
└─ 辅助条件B
   └─ 动作明显，直接执行
```

## Practicality Filter

Every leaf node should pass at least one of these tests:

- It names an observable condition.
- It names an executable action.
- It names a decision criterion.
- It names a measurable constraint.
- It names a bottleneck that must be removed before progress is possible.

If a node is only a concept label, expand it into practical subconditions or replace it with a concrete method.

Before finalizing a tree, run this check:

- Which branch is the current bottleneck?
- Which branch can stop early because the next action is obvious?
- Which branch needs deeper decomposition because failure there is expensive?
- Which branch is only a supporting condition, not a main path?

Reflect those answers in the tree shape. Do not make the tree visually even if the answers are uneven.

Bad（概念链——只堆标签不命名动作）:

```text
社会能力 -> 高价值 -> 影响力 -> 个人品牌
```

Bad（均匀深度——每个分支都是2层，没有瓶颈意识）:

```text
社会能力
├─ 认识人
│  └─ 每周认识3个人
├─ 展示成果
│  └─ 每月完成1个作品
├─ 积累信任
│  └─ 守约交付
└─ 进入场域
   └─ 参加行业活动
```

Better（瓶颈深挖，辅助早停）:

```text
社会能力
├─ 守约交付以积累可信记录
├─ 每周认识3个同领域可合作的人
├─ 进入能带来机会的固定场域
│  ├─ 先贡献价值再建立关系
│  └─ 为什么：机会密度决定成长速度
└─ 每月至少完成1个可展示成果

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

Ask a question only when one missing fact would materially change the output and a reasonable assumption would be risky.

If asking, ask exactly one concise question.

Otherwise proceed with explicit assumptions.

## Anti-Drift Rules

Do not:

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

## Complete Example

For a goal like "how to build unconditional confidence," a proper output looks like this:

---

**Final Goal**
建立不依赖外部结果的自我确信——无论成败、他人评价、环境变化，内核保持稳定。

**Assumptions**
用户没有生存威胁、严重心理疾病或成瘾问题。追求可操作的行动框架而非哲学安慰。

**Condition Tree**

```text
无条件自信
├─ 切除条件依赖
│  ├─ 写下：我的自信什么时候会崩塌
│  └─ 对每个条件问：它消失了我还值不值得存在
│
├─ 建立自证闭环 ⚠️ 核心瓶颈
│  ├─ 自信 = 对自己的承诺 × 兑现率
│  ├─ 每天做一个小到不可能失败的承诺并兑现
│  │  ├─ 做到了 → 自我兑现率+1
│  │  ├─ 没做到 → 降低难度，不自我攻击
│  │  └─ 持续2-4周，根基从"别人怎么看我"转为"我能否信自己"
│  └─ 区分可控与不可控
│     ├─ 可控：投入质量、是否守约、是否复盘
│     └─ 不可控：结果、他人评价、运气（只作为信息输入）
│
├─ 提高失败容错率
│  ├─ 增加尝试频率降低单次 stakes
│  └─ 建立"失败→提取信息→再试"的肌肉记忆
│
├─ 切断社会比较
│  └─ 唯一的比较对象是昨天的自己
│
├─ 身体底线
│  └─ 睡眠不足会系统性压低自信基线
│
└─ 防回退
   └─ 每两周自检：自信有没有重新绑上外部条件
```

注意树的形状：自证闭环是瓶颈所以挖到4层；切断社会比较和身体底线动作明显所以只有1层。

**Priority Path**

1. 立即：写下自信最容易崩塌的3个场景
2. 第一周：每天一个极小承诺并兑现，开始自我兑现记录
3. 2-4周：增加尝试密度，主动经历"失败但不毁灭"，改写失败后的自我对话
4. 持续：每两周自检一次回退信号

**Verification**
- 被否定后1小时内恢复稳定，不产生持续自我攻击
- 一次失败后第二天正常行动，不进入逃避模式
- 看到同龄人成就时第一反应是"我能学什么"而非"我不行"
- 独处时不觉得必须证明什么才能被自己接受

---

## Completion Standard

The task is complete only when the requested artifact, answer, or verified result has been delivered.

If verification cannot be performed, state exactly what cannot be verified and why.
