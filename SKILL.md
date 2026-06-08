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

Before finalizing a tree, run this check:

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

For a goal like "maximize long-term survival and reproduction in modern society," a proper output looks like this:

---

**Final Goal**
In modern society, maximize your long-term probability of survival, resource acquisition, mate selection success, stable family formation, and offspring development.

**Assumptions**
The path must be legal, sustainable, and executable — not short-term exploitation, manipulation, or extreme risk-taking.

**Condition Tree**

```text
Maximize Survival & Reproduction
├─ Don't Get Eliminated: Avoid Irreversible Losses
│  ├─ No illegal activity, no violence, no high-leverage gambling
│  ├─ No addiction takeover: alcohol, gambling, drugs, porn, gaming, short-video all count
│  ├─ Protect the physical baseline
│  │  ├─ Sleep is consistently restorative
│  │  ├─ Weight, fitness, sexual health within manageable range
│  │  └─ Health checkups and basic medical awareness
│  └─ Maintain minimum cash buffer
│     └─ Goal is not wealth first — it's not being destroyed by one job loss, illness, or family emergency
│
├─ Resource Capacity: Make Society Continue to Need You
│  ├─ Find one monetizable skill
│  │  ├─ Someone is already willing to pay for it
│  │  ├─ You can produce a demonstrable sample
│  │  ├─ You can measurably improve within 6 months
│  │  └─ It won't be cheaply replaced too quickly
│  ├─ Place the skill in a real marketplace
│  │  ├─ Job-seeking, freelancing, sales, content, products — pick at least one
│  │  └─ Don't just study without entering real transactions
│  ├─ Build income stability
│  │  ├─ Primary income covers living expenses
│  │  ├─ Gradually reduce dependence on a single boss, client, or platform
│  │  └─ Reserve time for continued skill upgrading
│  └─ Convert income into risk-resistant assets
│     ├─ Save first, invest later
│     └─ Don't use conspicuous consumption to prove yourself
│
├─ Social Position: Make Others Willing to Entrust Opportunities and Relationships to You
│  ├─ Trust record
│  │  ├─ Do what you said you would
│  │  ├─ Notify early when you can't deliver
│  │  └─ Make results visible, not just explain intentions
│  ├─ Enter higher-quality environments
│  │  ├─ Go to better industries, cities, communities, learning environments
│  │  └─ Find people stronger than you who are willing to exchange with you
│  └─ Cut draining relationships
│     └─ People who consistently lead you toward illegality, debt, addiction, broken trust, or internal depletion are not resources — they are risks
│
├─ Mate Selection Competitiveness: Make the Right Person Willing to Choose You
│  ├─ Minimum threshold
│  │  ├─ Clean, healthy, normal physical condition
│  │  ├─ Emotionally stable, not losing control
│  │  ├─ Basic income or clear upward trajectory
│  │  └─ Life is not a complete mess
│  ├─ Long-term value
│  │  ├─ Has a sense of responsibility
│  │  ├─ Can handle conflict
│  │  ├─ Has realistic commitment to family and children
│  │  └─ Not just promising — can sustain action
│  └─ Increase encounter probability
│     ├─ Appear in settings where target partners also appear
│     ├─ Build connections through friends, work, interests, learning
│     └─ Initiate clearly, without harassment or manipulation
│
├─ Partner Screening: This Matters More Than "Winning Someone Over"
│  ├─ Must ask
│  │  ├─ Do you want children?
│  │  ├─ When do you want them?
│  │  ├─ How do you view money, fidelity, parents, housework, childcare?
│  │  └─ When conflict arises: communicate, withdraw, cold-shoulder, or attack?
│  ├─ Must observe
│  │  ├─ How has the person handled past commitments?
│  │  ├─ Is the person long-term stable?
│  │  └─ What is the quality of their close relationships?
│  └─ Must exclude
│     ├─ Addiction, violence, chronic deception
│     ├─ Extreme debt and uncontrolled spending
│     └─ Complete unwillingness to shoulder family responsibilities
│
├─ Relationship Maintenance: Reproduction Goals Have a High Probability of Dying Here
│  ├─ Don't place short-term thrills above long-term trust
│  ├─ Money, sex, parents, housework, children — must be discussable, not guessed
│  ├─ Repair after conflict, don't accumulate resentment
│  └─ If the relationship chronically destroys your life baseline, cut losses
│
└─ Raising Offspring: "Giving Birth" Is Not the Finish Line
   ├─ Before having children
   │  ├─ Both parties explicitly willing
   │  ├─ Physical conditions permit
   │  ├─ Income and living arrangements are basically sustainable
   │  └─ At least one stable care plan exists
   ├─ After having children
   │  ├─ Provide the child with security and order
   │  ├─ Invest time, not just money
   │  ├─ Provide medical care, education, social environment
   │  └─ Manage parents' own emotions and relational conflicts
   └─ Intergenerational outcome
      └─ Let children inherit better health, cognition, resources, relationships, and behavioral patterns
```

**Priority Path**

1. Clear landmines first: illegality, addiction, high debt, health collapse, cash flow rupture — these reset everything to zero.
2. Find one skill the real market pays for, enter transactions quickly, don't stay stuck in the learning illusion.
3. Use reliable delivery to accumulate trust records, enter higher-quality environments.
4. Build mate selection competitiveness on "long-term reliability," not surface-level attraction.
5. When screening partners, prioritize: reproductive willingness, sense of responsibility, money values, conflict handling, and stability.
6. Enter child-rearing only after relationship stability — otherwise reproduction becomes a long-term risk amplifier.

**Verification**
If the path is working, you will see: life risks decreasing, cash flow stabilizing, skills converting to income, others trusting you more, social environments improving, suitable partner encounter probability rising, relationships becoming less draining, and conditions for raising children becoming increasingly realistic.

---

## Completion Standard

The task is complete only when the requested artifact, answer, or verified result has been delivered.

If verification cannot be performed, state exactly what cannot be verified and why.
