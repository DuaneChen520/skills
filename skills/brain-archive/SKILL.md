---
name: "brain-archive"
description: "归档已完成的 brain 任务：决策条目迁 decisions-history，trues/plans 移入 archive，roadmap 里程碑联动更新。当用户确认任务完成并要求归档、收尾时使用。"
---

# brain-archive：任务归档

规则权威：`brain/rules.md`。history 条目格式：读 `brain/formats.md` §4。AI 提议归档、**用户确认后执行**；不得自行归档。

## 前置检查

目标 plans 文档中必须已有 brain-verify 的**通过**记录；没有 → 先建议运行 brain-verify。

## 动作（用户确认后，四份）

1. `brain/decisions.md` 该条目迁出至 `brain/archive/decisions-history.md`：按年份分节（`## 2026`），措辞不改、锚点不改；decisions.md 不保留历史区块。
2. `brain/trues/trues-<时间戳>.md` → `brain/archive/trues/`，文末追加 `> 已归档至 archive/trues/`。
3. `brain/plans/plans-<时间戳>.md` → `brain/archive/plans/`，文末追加 `> 已归档至 archive/plans/`。
4. 里程碑联动：decisions.md 条目原位与 `brain/roadmap.md` 对应里程碑「关联任务」处标记 ✓；若该里程碑任务清零 → **提议**用户确认后将里程碑标记完成。

## 注意

- 目标文件夹不存在时先创建（如 `archive/trues/`）。
- 归档不删除内容，随时可撤回；锚点解析顺序延伸到 archive/，原文件内链接不改。
- 搁置的任务不归档，留在 decisions.md 原区块并注明原因。
- 完成后按仓库约定提交 git。
