# 论文写作全能助手 — Skill 整合包

一套完整的论文写作辅助 Skill 体系，包含 **论文写作指导**、**独立盲审**、**配图绘制**、**文献分析**、**论文管理** 五大模块，可无缝接入 Trae IDE。

---

## 目录结构

```
lunwenzhidao-skill-pack/
├── .trae/
│   ├── skill-config.json          ← 技能配置（默认全部启用）
│   └── skills/
│       ├── lunwenzhidao/          ← 主调度器：论文写作导师
│       │   ├── SKILL.md
│       │   ├── CONTEXT.md
│       │   ├── 施工文档_v3.md
│       │   └── stages/            ← 子技能：8个阶段 + 3个拓展
│       │       ├── stage-0-initialize/
│       │       ├── stage-1-methodology/
│       │       ├── stage-2-results/
│       │       ├── stage-3-conclusion/
│       │       ├── stage-4-introduction/
│       │       ├── stage-5-frontmatter/
│       │       ├── stage-6-finalize/
│       │       ├── stage-7-final-check/
│       │       ├── stage-ext-reviewer/     ← 审稿修回
│       │       └── stage-ext-literature/  ← 文献分析
│       ├── paper-manager/         ← 论文管家（后台管理 Agent）
│       │   └── SKILL.md
│       ├── lunwenreview-skill/    ← 独立盲审
│       │   ├── SKILL.md
│       │   ├── refs/
│       │   └── stages/
│       └── lunwenfigure-skill/    ← 配图绘制
│           ├── SKILL.md
│           ├── refs/
│           └── stages/
├── 论文指导/
│   └── workspace/                 ← 论文数据（运行时生成）
└── README.md
```

---

## 安装步骤

### 方式一：复制到已有 Trae 项目

1. 将 `.trae/` 目录复制到你现有 Trae 项目的根目录：

   ```bash
   # 假设你的项目在 /path/to/your-project
   cp -r lunwenzhidao-skill-pack/.trae /path/to/your-project/.trae
   ```

2. 可选：如果你有 `论文指导/` 目录的需求，复制 `论文指导/`：

   ```bash
   cp -r lunwenzhidao-skill-pack/论文指导 /path/to/your-project/论文指导
   ```

### 方式二：全新项目

1. 将整个整合包内容作为项目根目录：

   ```bash
   cp -r lunwenzhidao-skill-pack/* /path/to/new-project/
   ```

---

## 使用说明

在 Trae IDE 中输入以下关键词触发对应功能：

| 你说 | 触发功能 |
|------|---------|
| "写论文" / "论文写作" / "需要论文指导" | 启动 **lunwenzhidao** 主调度器 |
| "审稿" / "审稿意见" | 进入 **独立盲审** 模式 |
| "画图" / "配图" / "流程图" / "数据图" / "示意图" | 进入 **配图绘制** 模式 |
| "分析这篇论文" / "分析文献" / "帮我读一下" | 进入 **文献分析** 模式 |

### 工作流程

主调度器（lunwenzhidao）自动按阶段引导论文写作：

```
阶段0（下定决心）→ 阶段1（方法论）→ 阶段2（结果与讨论）
→ 阶段3（结论）→ 阶段4（引言）→ 阶段5（摘要/标题/关键词）
→ 阶段6（致谢/参考文献）→ 阶段7（终极检查）
                ↘ 审稿修回（随时触发）
                ↘ 文献分析（随时触发）
                ↘ 配图绘制（随时触发）
```

中间随时可以暂停进入其他模式，完成后自动回到原进度。

---

## 数据文件

论文数据存储在 `论文指导/workspace/` 目录下，包括：
- `progress.md` — 写作进度
- `papers-library.json` — 已读论文数据库（由文献分析自动填充）
- `operations-log.json` — 操作记录备份
- `progress-track.json` — 阶段状态追踪
- `drafts/` — 协作草稿

---

## 注意事项

1. **不要修改 `.trae/skills/` 下的 SKILL.md 文件**，除非你清楚自己在做什么
2. 如果需要自定义触发词，修改对应 SKILL.md 的 `description` 字段（frontmatter）
3. 论文数据库（`papers-library.json`）是增量累积的，迁移项目时复制该文件即可保留已读论文记录
4. 所有 Skill 遵循"协作草稿制"——AI 产出草稿，最终决定权始终在用户手中