---
name: "brain-roadmap"
description: "建立或核查 brain/roadmap.md：无则用逼问+代码核实建立长期目标与里程碑，有则用实际代码核查进展是否漂移并报告偏差。当用户要求建立 roadmap、检查进展漂移、或调整里程碑时使用。"
---

# brain-roadmap：建立 / 漂移核查 roadmap.md

定位：roadmap 是**用户查看进展与漂移的仪表盘**，不是开发会话的必注入上下文。规则权威：`brain/rules.md`。

## 分支一：无 brain/roadmap.md（建立）

1. 前置：`brain/` 不存在时先跑 brain-init。
2. **必用 brain-grill**：以逼问轮次收敛——最终目标（用户原话，不得代拟）、里程碑划分、每个里程碑的完成标志。
3. 用 codegraph_explore 了解实际代码现状，确保里程碑与代码现实对得上。
4. 按 `references/roadmap-template.md` 写入 `brain/roadmap.md`（仅此刻读模板）。
5. 展示全文等用户确认；确认后按仓库约定提交 git。

## 分支二：已有 roadmap.md（漂移核查）

1. 读 `brain/roadmap.md` + `brain/decisions.md` 在办任务。
2. 用 codegraph_explore 核实相关代码现状（图谱未覆盖当场实测），逐里程碑核对：
   - 已完成的任务是否真实落地在代码里；
   - 里程碑「完成标志」当前是否达成（可验证的事实）；
   - 是否存在 roadmap 未覆盖却正在做的任务（偏离）。
3. 输出**偏差报告**：里程碑 / 预期 vs 实际 / 证据（文件路径·行号），不下结论不擅自改文件。
4. 用户决定调整（增删里程碑、改完成标志）→ 用 brain-grill 收敛调整方案 → 改 roadmap → 用户确认后提交 git。
