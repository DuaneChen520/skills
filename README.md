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

**安装**：将 `skills/brain-workflow` 复制到你的 agent skills 目录（如 `.agents/skills/` 或 `~/.claude/skills/`）。

**使用**：新项目中说"初始化 brain"，AI 会创建目录骨架、询问事实引用源/仓库可见性/工单边界，并生成项目专属的 `brain/rules.md`；之后日常只需说"记录想法 / 拍板 / 展开计划 / 归档"。
