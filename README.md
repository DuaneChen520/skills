# skills

Agent Skills 集合（作者：**DuaneChen520**），遵循 [Agent Skills 规范](https://agentskills.io/specification)。

## skills/brain-workflow

初始化并维护 `brain/` 文件夹的「想法 → 决策 → 计划 → 开发 → 归档」人机协作工作流。

```
thoughts/（想法，每想法一个 md）
   │ 用户拍板
   ▼
decisions.md（一行一句，锚点唯一对应，状态唯一权威源）
   │ 方案展开
   ▼
plans/（计划文档，与 thoughts 同一时间戳命名）
   │ 按计划开发
   ▼
用户确认完成 → thoughts/plans 双份归档至 archive/
```

## 安装

**推荐**（自动检测本机已安装的 agent，支持 Claude Code / Codex / Cursor / OpenCode 等 75+）：

```bash
npx skills add DuaneChen520/skills
```

**手动**：clone 仓库后，将 `skills/brain-workflow` 复制到所用 agent 的 skills 目录：

| Agent | 用户级（跨项目可用） | 项目级（仅当前仓库） |
| --- | --- | --- |
| Trae | `~/.agents/skills/` | 项目根 `.agents/skills/` 或 `.trae/skills/` |
| Claude Code | `~/.claude/skills/` | 项目根 `.claude/skills/` |
| 其他 | 见所用 agent 文档中的 skills 目录约定 | — |

安装后重启会话生效。新项目中对 AI 说「初始化 brain」即可触发；日常说「记录想法 / 拍板 / 展开计划 / 归档」。

