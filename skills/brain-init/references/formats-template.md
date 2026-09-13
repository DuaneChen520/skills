# brain/ 文档模板（权威格式源）

> 按需读取对应小节；本文件由 [rules.md](rules.md) 引用，是各阶段文档的格式权威。

## §0 roadmap.md（长期目标与里程碑）

> 最终目标保持一段自然语言、极少改动；里程碑状态由关联任务聚合（进行中/已完成），归档联动更新。

```markdown
# roadmap

> 最终目标：（一段自然语言）

## 里程碑

### M1 标题 — 进行中
- 描述：（一句话）
- 完成标志：（可验证条件）
- 关联任务：[decisions-YYMMDD-HHMMSS]
```

## §1 decisions.md 条目

```markdown
- [decisions-YYMMDD-HHMMSS] 标题
  - 里程碑：Mx（或"探索性任务"）
  - 总结：一段自然语言，精炼记录讨论的最终结论（做了什么决定、为什么、边界是什么）。
  - 事实：[trues-YYMMDD-HHMMSS](trues/trues-YYMMDD-HHMMSS.md)（生成后回填链接）
  - 计划：[plans-YYMMDD-HHMMSS](plans/plans-YYMMDD-HHMMSS.md)（生成后回填链接）
```

## §2 trues 文档

```markdown
## [YYMMDD-HHMMSS] 标题

- 记录时间：YYYY-MM-DD
- 对应决策：[decisions-YYMMDD-HHMMSS](../decisions.md)
- 对应计划：[plans-YYMMDD-HHMMSS](../plans/plans-YYMMDD-HHMMSS.md)（生成后回填）
- 状态：待用户确认

### 代码事实

- 事实 1（附文件路径 / 行号 / 调用路径）

### 未核实项

- （明确列出没能从代码 / 图谱确认的点，留待实测）
```

## §3 plans 文档

```markdown
## [YYMMDD-HHMMSS] 标题

- 创建时间：YYYY-MM-DD
- 对应决策：[decisions-YYMMDD-HHMMSS](../decisions.md)
- 代码事实依据：[trues-YYMMDD-HHMMSS](../trues/trues-YYMMDD-HHMMSS.md)
- 状态：待用户确认

### 目标

（一句话说清要达成什么）

### 方案

1. 步骤一（依据：trues 事实 N）
2. 步骤二（依据：…）

### 验收标准

- [ ] 可验证的完成条件
```

计划变更时改文档本身并在文末追加变更记录（日期 + 一句话）；重大变更需用户确认。

## §4 decisions-history.md（归档）

按年份分节；迁入条目措辞不改、锚点不改：

```markdown
## 2026

- [decisions-YYMMDD-HHMMSS] 标题（同 decisions.md 原文）
```
