---
name: "brain-init"
description: "初始化或体检 brain/ 文件夹结构：无 brain/ 则创建（rules/formats/decisions/目录），有则检查必要文件是否齐全并补缺。当用户要求启用 brain 工作流、初始化 brain、或检查 brain 结构时使用。"
---

# brain-init：初始化 / 体检 brain/

纪律：**不覆盖已有内容**；本技能只管结构与规则文件，roadmap 交给 brain-roadmap，任务流转交给各 brain-* 技能。

## 分支一：无 brain/（初始化）

1. 确认仓库可见性（public/private），提示敏感条目风险。
2. 创建结构（模板文件在本技能 references/ 下，**仅在写入此刻读取**）：

```
brain/
├── rules.md      # ← references/rules-template.md 原样生成
├── formats.md    # ← references/formats-template.md 原样生成
├── decisions.md  # 空骨架（下方内容）
├── trues/  plans/  archive/   # 空目录
```

3. decisions.md 初始内容：

```markdown
# 决策

> 历史决策不驻留本文件：条目完成后即时迁入 `archive/decisions-history.md`（按年份分节），本文件只保留未开始与进行中。

## 未开始的任务

## 进行中的任务
```

4. 展示文件清单，确认后按仓库约定提交 git；提示用户下一步运行 brain-roadmap 建立长期目标与里程碑。

## 分支二：已有 brain/（体检）

必要文件清单：`rules.md`、`formats.md`、`decisions.md`、`roadmap.md`、`trues/`、`plans/`、`archive/`。

1. 逐项检查，输出「齐全 / 缺失」报告；缺失项补建：
   - rules.md / formats.md 缺 → 用 references 模板重建，**先向用户确认**（可能存在本地定制）；
   - decisions.md 缺 → 只建空骨架；
   - roadmap.md 缺 → 建议运行 brain-roadmap；
   - 目录缺 → 建空目录。
2. 已有文件一律不改内容。
