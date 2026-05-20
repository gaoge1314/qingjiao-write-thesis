# 青椒论文写作助手 — qingjiao-write-thesis

> 苏格拉底式论文写作协作导师 — 基于 Trae AI IDE 的 Skill 体系

一套完整的论文写作辅助 Skill 包，包含 **论文写作指导**、**独立盲审**、**配图绘制**、**文献分析**、**论文管理** 五大模块，可无缝接入 Trae IDE。

---

## 🎯 能做什么

| 你说 | 触发功能 |
|------|---------|
| "写论文" / "需要论文指导" | 启动 lunwenzhidao 主调度器，按阶段引导写作 |
| "审稿" / "审稿意见" | 进入独立盲审模式，四分类回复审稿意见 |
| "画图" / "配图" / "流程图" / "示意图" / "数据图" | 进入配图绘制模式（Mermaid/Python/SVG/PS） |
| "分析这篇论文" / "分析文献" / "帮我读一下" | 进入文献分析模式（基于当前阶段确定分析重点） |

## 📦 包含的模块

- **lunwenzhidao** — 主调度器：8阶段顺序引导 + 3个随时触发的拓展
- **paper-manager** — 论文管家：后台管理论文库/操作备份/进度追踪
- **lunwenreview-skill** — 独立盲审：8个子技能覆盖全文审稿
- **lunwenfigure-skill** — 配图绘制：流程图→数据图→示意图→实验图→美化

## 🚀 安装

```bash
# 复制到你的 Trae 项目根目录
cp -r .trae /path/to/your-project/
```

在 Trae IDE 中直接说"写论文"即可开始使用。

## 📂 目录结构

```
.trae/
├── skill-config.json
└── skills/
    ├── lunwenzhidao/          ← 主调度器（10个子技能）
    ├── paper-manager/         ← 论文管家
    ├── lunwenreview-skill/    ← 独立盲审（8个子技能）
    └── lunwenfigure-skill/    ← 配图绘制（5个子技能）
```

## 📝 数据文件

论文数据存储在 `论文指导/workspace/` 目录：
- `papers-library.json` — 已读论文数据库
- `operations-log.json` — 操作记录备份
- `progress-track.json` — 阶段状态追踪

## ⚠️ 注意事项

- 遵循"协作草稿制"——AI 产出草稿，最终决定权在用户手中
- 不编造研究内容、数据或结论
- 中间可随时暂停进入配图/审稿/文献分析模式，完成后退回原进度

---

**基于 Trae AI IDE 构建 · 苏格拉底式启发写作**