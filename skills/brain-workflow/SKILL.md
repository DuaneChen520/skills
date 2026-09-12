---
name: "brain-workflow"
description: "初始化并维护 brain/ 文件夹的「想法→决策→计划→开发→归档」人机协作工作流。当用户要求初始化 brain、记录想法、登记拍板决策、展开开发计划、归档已完成任务，或提到 brain 文件夹这套流程时使用。"
metadata:
  author: DuaneChen520
  version: "1.1.0"
---

# brain-workflow：想法 → 决策 → 计划 → 开发 → 归档

把用户想法沉淀为可追溯、可审计、上下文开销最小的工作流。所有内容存放在项目根目录的 `brain/` 文件夹中。

## 何时使用

- 用户要求在新项目中**初始化**这套协作流程
- 用户要求**记录想法**（"把这个想法记下来/提交为想法文档"）→ `thoughts/`
- 用户**拍板**某个决策 → `decisions.md`
- 拍板后的决策需要**展开为开发计划** → `plans/`
- 任务**经用户确认完成** → 双归档
- 用户要求查阅或维护 `brain/` 文件夹

## 流转链路（一一对应，全程锚点可追溯）

```
thoughts/（想法，每想法一个 md，命名 thoughts-YYMMDD-HHMMSS.md）
   │ 用户拍板
   ▼
decisions.md（一行一句，[thoughts-YYMMDD-HHMMSS] 锚点唯一对应）
   │ 方案展开
   ▼
plans/（计划文档 plans-YYMMDD-HHMMSS.md，与 thoughts 同一时间戳命名）
   │ 按计划开发
   ▼
用户确认完成
   ▼
thoughts md → archive/thoughts/；plans md → archive/plans/
```

**状态权威源**：decisions.md 是状态的唯一权威；thoughts / plans 中的状态仅是镜像，冲突以 decisions.md 为准。

**锚点解析**：`[thoughts-YYMMDD-HHMMSS]` 按 `thoughts/` → `archive/thoughts/` 顺序解析；文件归档移动后**不修改锚点**。

## 一、初始化（新项目首次使用）

1. 创建目录骨架：

```
brain/
├── rules.md            # 交互规则（AI 与用户每次会话先读）
├── decisions.md        # 决策登记
├── thoughts/           # 用户想法条目
├── plans/              # 开发计划
└── archive/
    ├── thoughts/       # 已完成想法归档
    └── plans/          # 已完成计划归档
```

2. `decisions.md` 初始内容为三个空区块：

```markdown
# 决策

## 未开始的决策

## 进行中的决策

## 历史决策
```

3. 以 [references/rules-template.md](references/rules-template.md) 为底稿生成 `brain/rules.md`。**生成前必须询问用户**：
   - **事实引用源**是什么（如 codegraph 知识图谱、权威文档、数据库、数据契约文件），填入模板「引用纪律」；不得留空或凭空指定
   - 仓库若为**公有**且 thoughts 可能含敏感内容，由用户决定 `brain/` 整体或部分排除出 git
   - 项目已有**工单系统**时，声明边界：`brain/` 管"为什么做、做什么、是否做完"，工单管"执行分派与排期"

4. 在项目入口文档（`AGENTS.md` 或 `CLAUDE.md`）注册**指针**（只指路，不复制内容）：

```markdown
本项目的想法、决策与交互规则在 **`brain/`**，动手前先读 `brain/rules.md`。
```

## 二、记录想法（thoughts/）

用户显式要求记录想法时，新建 `brain/thoughts/thoughts-YYMMDD-HHMMSS.md`（时间戳取当前时刻；同秒冲突时秒数 +1）：

```markdown
## [YYMMDD-HHMMSS] 标题

- 提出时间：YYYY-MM-DD
- 状态：未开始

（用户的想法正文，忠实记录，不改写）

### AI 评语

> YYYY-MM-DD

（AI 的判断、风险、建议，先结论后展开）

### 进度

- [ ] 待办动作
```

## 三、拍板决策（decisions.md）

条目格式：

```markdown
- [状态] 一句话决策描述 [thoughts-YYMMDD-HHMMSS]
```

- **一句话原则**：每个决策写成一句可独立读懂的话，只写"拍板了什么"，不展开理由、不贴正文；细节回 thoughts 条目查看。
- **唯一对应**：一条决策对应且仅对应一个 thoughts 条目，句末以锚点注明出处。无对应 thoughts 条目的拍板，先补建 thoughts 条目再登记。同一想法的后续拍板更新原句，不新增条目。
- **状态前置 + 三分区展示**：条目按 `## 未开始的决策` / `## 进行中的决策` / `## 历史决策` 三个区块组织，用户一屏即可了解全部决策态势。
- **唯一权威状态源**：本文件是状态的唯一权威；thoughts / plans 中的状态仅是镜像，冲突以本文件为准。
- **简洁纪律**：整个文件保持一屏可读完；条目进入「历史决策」区块后措辞不再改动。
- **历史膨胀控制**：历史决策条目超过 30 条时，AI 提议将已归档任务对应的条目迁出至 `archive/decisions-history.md`（按年份分节），原位置留一行指针。
- **计划衔接**：决策进入「进行中」前，应先在 `plans/` 建立对应计划文件。

## 四、展开计划（plans/）

决策拍板且需要开发时，AI 新建 `brain/plans/plans-YYMMDD-HHMMSS.md`（时间戳与对应 thoughts 条目一致）：

```markdown
## [YYMMDD-HHMMSS] 标题

- 创建时间：YYYY-MM-DD
- 对应决策：[thoughts-YYMMDD-HHMMSS]
- 状态：进行中

### 目标

（一句话说清要达成什么）

### 方案

（展开的实施步骤 / 设计要点，按可执行粒度编号）

### 验收标准

- [ ] 可验证的完成条件
```

- 计划由 AI 起草，**用户确认后方可按计划开发**。
- 进度在计划「验收标准」与 thoughts 条目「进度」中同步勾选；状态以 decisions.md 为准。
- 计划变更直接改文档，文末追加变更记录（日期 + 一句话）；重大变更需用户确认。
- 计划中的可分派步骤可进入项目工单系统，在 plans 文档中注明工单号。

## 五、归档

- **触发**：任务**经用户确认完成**（decision 状态为 `已完成`）后，AI 提议归档；AI 不得因开发结束自行归档。
- **双份动作**：
  1. thoughts 条目移入 `archive/thoughts/`，文末留一行 `> 已归档至 archive/thoughts/`
  2. plans 文档移入 `archive/plans/`，文末留一行 `> 已归档至 archive/plans/`
  3. decisions.md 中该条已在「历史决策」区块，措辞不动，**锚点不改**
- 归档由 AI 提议、**用户确认后执行**；归档不删除内容，随时可撤回。
- 搁置的决策**不归档**，留在 decisions.md 原区块（状态 `搁置`），待重启后再处理。

## 状态词表（固定，便于检索）

| 状态 | 含义 |
| --- | --- |
| `未开始` | 已记录，尚未评估 |
| `评估中` | AI 已读，正在查证 |
| `进行中` | 已确认方案，正在实施 |
| `已完成` | 交付完成，可归档 |
| `搁置` | 主动暂停，需写明原因 |
| `待澄清` | 缺少关键信息，需用户回复才能推进 |

## AI 行为纪律

1. **先读后写**：每次进入 brain/ 的会话，先读 `rules.md` 再动手。
2. **不改动用户原文**：AI 只在 thoughts 条目下方追加 `### AI 评语` / `### 进度` 区块；修正用户原意应在评语中指出。
3. **先结论后展开**：评语首句给判断，再给理由。
4. **不编造事实**：涉及项目数据的计数、字段、比例，按 rules.md「引用纪律」指定的引用源查证后给出；无法核实时明说"未核实"。
5. **进度可审计**：用清单勾选，不写"基本完成"这类模糊表述。
6. **含糊指令不自动延续**：用户说"继续""你看着办"时，先停下确认，不自主推进外部动作。
7. **外部动作需显式确认**：git 提交/推送、改数据文件、对外发布，先列变更清单等用户确认。
8. **archive 默读禁入**：除非用户显式要求查阅 `archive/` 内容，AI 不阅读该文件夹内任何文件。

## 工作流的自进化

用户在日常使用中对 `brain/rules.md` 的调整若**具有通用性**（非项目专属细节），AI 应主动提议将其反向同步回本 skill——更新本文件与 [references/rules-template.md](references/rules-template.md)，并递增 frontmatter `metadata.version`。经用户确认后执行。否则 skill 会随时间退化为过时文档。

## 最简上下文原则

- **AGENTS.md / CLAUDE.md 只放指针**，不复制工作流细节；细节全部收敛在 `brain/rules.md`。
- **rules.md 只放规则、不放决策**：所有拍板一律进 `decisions.md`，rules.md 不设「已定与待定」之类的决策记录节。
- **rules.md 不留僵尸条款**：规则删除或修改时同步检查全文，不保留无实现对应的死规则。
- **归档是冷存储**：archive/ 中的文件不参与日常上下文，AI 默不阅读；历史决策膨胀时按阈值迁出。
- **brain/ 纳入 git**：所有协作痕迹可追溯、可撤回（公有仓库需先做隐私确认）。
