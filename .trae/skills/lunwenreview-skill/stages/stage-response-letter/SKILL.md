---
name: stage-response-letter
description: 中英文双语回复信生成子技能
---

# stage-response-letter — 中英文双语回复信生成子技能

## 1. 当前目标

读取所有审稿意见缓存和双语答辩缓存，自动生成标准格式的 **Response to Reviewer #1** 中英文双语回复信，写入 workspace 供用户直接使用。

## 2. 主要矛盾

用户在苏格拉底式过招中产出了大量零散的"大白话修改思路"，这些内容虽然逻辑正确但缺乏学术规范表达；同时各章节的 Comments 分散在不同缓存文件中，需要系统性地整合为一份结构完整、格式标准的正式回复信。

## 3. 要素清单

| 要素 | 说明 |
|------|------|
| 数据读取 | 读取 workspace/review-comments/ 下所有审稿意见缓存文件 |
| 答辩提取 | 读取 workspace/review-comments/rebuttal-cache.md 中的双语答辩内容 |
| 评论归类 | 按章节维度将 Comments 归类整理，标注每个 Comment 对应哪个章节 |
| 格式生成 | 生成标准 Response to Reviewer #1 格式：General Comments → Point-by-Point Response |
| 双语输出 | 每个 Comment 包含中文答辩 + English Response |
| 文件写入 | 将完整回复信写入 workspace/drafts/lunwenreview/response-letter.md |

### 读取的缓存文件清单

| 文件 | 内容来源 |
|------|---------|
| methodology-comments.md | 方法论审稿意见 + 用户修改答辩 |
| results-comments.md | 结果与讨论审稿意见 + 用户修改答辩 |
| conclusion-comments.md | 结论审稿意见 + 用户修改答辩 |
| introduction-comments.md | 引言审稿意见 + 用户修改答辩 |
| frontmatter-comments.md | 摘要/标题/关键词审稿意见 + 用户修改答辩 |
| finalize-comments.md | 致谢/参考文献审稿意见 + 用户修改答辩 |
| rebuttal-cache.md | 苏格拉底过招时累积的双语答辩内容 |

## 4. 常见错误

- ❌ 遗漏某个章节的 Comments → 导致回复信不完整
- ❌ 直接将大白话辩护作为 English Response → 缺乏学术规范
- ❌ 中文答辩和英文回复内容不对应 → 严重影响审稿人体验
- ❌ 未标注对应章节来源 → 审稿人无法定位原文修改位置
- ❌ 引用 rebuttal-cache 时断章取义，丢失上下文逻辑链

## 5. 进阶办法

- English Response 部分自动做学术化润色（从大白话升级为学术博弈语体）
- 在回复信中标注每个 Comment 对应的原文修改位置（引用 chapter-split.md 的定位信息）
- 支持多轮审稿回复：第二、三轮回复时追加前缀 "Response to the Second Round of Comments"

## 6. 指导操作

### 步骤 1：读取所有缓存

依次读取以下文件，获取完整的审稿意见和答辩数据：

1. `workspace/review-comments/chapter-split.md` → 确认章节划分
2. `workspace/review-comments/methodology-comments.md`
3. `workspace/review-comments/results-comments.md`
4. `workspace/review-comments/conclusion-comments.md`
5. `workspace/review-comments/introduction-comments.md`
6. `workspace/review-comments/frontmatter-comments.md`
7. `workspace/review-comments/finalize-comments.md`
8. `workspace/review-comments/rebuttal-cache.md`

### 步骤 2：整理 Comments 列表

从各章节缓存中提取所有 Comments，按原始顺序排列，标注每个 Comment 的来源章节：

```
Comment 1（方法论）- Major Issue: 未交代选择实验方法的原因
Comment 2（方法论）- Major Issue: 公式附近AIGC查重高危
Comment 3（方法论）- Minor Issue: 时态混乱  ...
Comment 4（结果与讨论）- Major Issue: 缺乏误差分析
...
```

从 rebuttal-cache.md 中提取对应的中文答辩和 English Response 内容，匹配到每个 Comment。

### 步骤 3：生成回复信

生成标准格式：

```markdown
# Response to Reviewer #1

## General Comments

**中文**
作者非常感谢审稿人建设性的意见。我们已经对全文进行了彻底的重构，特别是深化了机制讨论并补充了误差分析。所有修改内容已在稿件中以修订模式标注。以下是对每条审稿意见的逐条回复。

**English**
The authors highly appreciate the reviewer's constructive and profound comments. We have thoroughly revised the manuscript, especially by deepening the mechanism discussions and incorporating error analysis. All revisions are marked in the revised manuscript. Below is our point-by-point response to each comment.

---

## Point-by-Point Response

### Comment 1: [章节来源] [Comment 标题]

**Reviewer's Comment:**
[引述审稿意见原文]

**中文答辩：**
[从 rebuttal-cache 或对应章节缓存中提取的中文答辩内容]

**English Response:**
[从 rebuttal-cache 或对应章节缓存中提取的英文回复，做学术化规范润色]

---

### Comment 2: [章节来源] [Comment 标题]

**Reviewer's Comment:**
[引述审稿意见原文]

**中文答辩：**
[中文答辩内容]

**English Response:**
[英文回复内容]

---

...
```

### 步骤 4：写入文件

将生成的回复信写入 `workspace/drafts/lunwenreview/response-letter.md`。

### 步骤 5：告知用户

> 中英文双语回复信已生成并保存至 `workspace/drafts/lunwenreview/response-letter.md`。
> 
> 内容包含：
> - General Comments（中英文）
> - 共 N 条 Point-by-Point Response
> 
> 建议你检查 English Response 部分，如有需要可进一步润色学术表达。

## 7. 与其他阶段的关系

| 方向 | 关系 |
|------|------|
| **上游** | 由主技能（lunwenreview-skill）在所有审稿阶段完成后调用 |
| **依赖** | 需要所有 review-comments 缓存文件存在 + rebuttal-cache.md 存在 |
| **输入源** | 读取 7 个缓存文件（6 个章节审稿 + 1 个答辩缓存） |
| **输出** | 写入 `workspace/drafts/lunwenreview/response-letter.md` |
| **顺序** | 必须最后执行：所有 6 个审稿阶段 + 苏格拉底过招全部完成 |

## 8. 环节验收

- ☑️ 所有 7 个缓存文件已成功读取
- ☑️ Comments 已按"章节来源 + 序号"规整排列
- ☑️ General Comments 中英文双语已生成
- ☑️ 每条 Comment 包含：审稿意见引用、中文答辩、English Response
- ☑️ `response-letter.md` 已成功写入 workspace
- ☑️ 用户已被告知生成结果