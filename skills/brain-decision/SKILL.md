---
name: "brain-decision"
description: "登记决策到 brain/decisions.md：强制先用 brain-grill 逼清边界与取舍，再落一条含里程碑归属的自然语言总结。当用户拍板、要求登记决策时使用。"
---

# brain-decision：登记决策到 decisions.md

规则权威：`brain/rules.md`。格式：读 `brain/formats.md` §1。

## 步骤

1. **强制前置——先跑 brain-grill**：无论讨论看起来多收敛，都要以 grill 的设计树把决策的边界、方案取舍、验收口径过一遍，产出「已确认共识清单」。跳过 grill 不得写 decisions.md；清单即「总结」的素材来源。
2. 读 `brain/roadmap.md` 确定「里程碑：Mx」归属；归属不上 → 提议补里程碑，或经用户同意标"探索性任务"。
3. 取当前时刻生成时间戳 `YYMMDD-HHMMSS`（同秒已有条目则秒数 +1）。
4. 在 `brain/decisions.md` 对应区块（未开始 / 进行中）按 §1 追加条目；「事实」「计划」以"待生成"占位。
5. **展示条目原文，等用户确认无误**；确认后按仓库约定提交 git。

## 注意

- decisions.md 只保留 `## 未开始的任务`、`## 进行中的任务` 两区块。
- 同一任务的后续拍板更新原条目，不新增。
- 旧 `[thoughts-…]` 锚点条目（历史流程产物）不改动。
- 总结必须是一段可独立读懂的自然语言；细节由后续 trues/plans 承载。
