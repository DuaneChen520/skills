# brain/ 协作规则（简化版 v2.1）

> 本文件是 brain/ 的权威规则源，只含核心契约，一屏读完。各文档模板见 [formats.md](formats.md)（按需读取对应小节）。

## 职责

| 文件 / 文件夹 | 内容 |
| --- | --- |
| `roadmap.md` | 长期目标与里程碑（一屏）；一切任务的准入门槛与进度总账 |
| `decisions.md` | 任务清单唯一权威：每任务一段自然语言总结，须标注归属里程碑 |
| `trues/` | 代码事实（每任务一份），只记经 codegraph 核实的事实 |
| `plans/` | 开发计划（每任务一份），每步须回溯 trues 事实 |
| `formats.md` | 各阶段文档模板（权威格式源） |
| `archive/` | 已完成任务的归档（AI 默读禁入） |

## 流程与门禁

```
讨论 → brain-decision → brain-plan（含代码事实核实） → 开发 → brain-verify → brain-archive
```

每环节为独立技能，可显式调用；每环节产出经**用户确认**后进入下一环节，禁止自动连跳。
brain-init（初始化/体检）与 brain-grill（逼问澄清）按需调用；brain-decision 强制先跑 brain-grill。

## 里程碑联动

- brain-decision 登记决策必须标注「里程碑：Mx」；归属不上的任务先补 roadmap 或显式标记"探索性任务"。
- brain-archive 归档后检查所属里程碑：关联任务清零时 AI 提议将该里程碑标记完成（用户确认后改 roadmap）。
- roadmap 不是开发会话的必注入上下文：它是用户查看进展与漂移的入口（brain-roadmap）。

## 命名与锚点

- 一任务一个时间戳 `YYMMDD-HHMMSS`（同秒冲突秒 +1），trues / plans 文件同名。
- 锚点 `[decisions-YYMMDD-HHMMSS]`；归档移动后不改锚点，解析顺序 `decisions.md` → `archive/`。
- 三份文档相互链接可跳转（decisions 条目 ↔ trues ↔ plans）。

## 红线

1. 事实只出自 codegraph_explore 或当场实测；不确定写「未核实项」。
2. 逐段确认；"继续/你看着办"但确认缺失时停下。
3. git 提交/推送、改数据、发布等外部动作先列清单等确认。
4. 归档由 AI 提议、用户确认后执行（decisions 条目 → decisions-history.md，trues/plans → archive/）。
5. decisions.md 只保留「未开始的任务」「进行中的任务」两区块；历史即时迁出，措辞不改。
