---
name: ppt-master
description: >
  AI-driven presentation generation workflow. Use when the user asks to create PPT,
  make presentation, 生成PPT, 做PPT, 制作演示文稿, or mentions ppt-master.
upstream: https://github.com/hugohe3/ppt-master
license: MIT
extraction_note: >
  This is a personal skill-library entry extracted from the upstream PPT Master project.
  Full runtime requires the upstream scripts, templates, references and Python dependencies.
---

# PPT Master Skill：可编辑 PPT 生成工作流

> 来源：<https://github.com/hugohe3/ppt-master>  
> 原作者：Hugo He  
> 许可证：MIT  
> 本文件是个人技能库中的“入口提取版”，不是完整可运行发行版。

## 0. 适用场景

当用户提出以下需求时使用本技能：

- 创建 PPT；
- 从 PDF / DOCX / URL / Markdown 生成演示文稿；
- 把一段材料整理成幻灯片；
- 生成 PowerPoint；
- 制作可编辑的 PPTX；
- 需要从资料到大纲、视觉风格、页面设计、导出文件的一整套流程。

本技能目标是生成**原生可编辑 PPTX**，而不是把每页做成一张图片塞进 PPT。

---

## 1. 核心原则

1. **先确认设计方向，再生成页面**  
   不要一上来直接做 PPT。先确认页数、受众、风格、颜色、字体、图片方式等。

2. **串行流程**  
   按顺序执行：资料处理 → 项目初始化 → 设计确认 → 内容规划 → 图片获取 → 页面生成 → 质量检查 → 导出。

3. **不要把 PPT 当普通文章总结**  
   PPT 需要页面节奏、视觉层级、标题结构、图表/图片策略、演讲备注。

4. **输出应尽量可编辑**  
   使用文本框、形状、图表、SVG/OOXML 等可编辑元素，而不是整页截图。

5. **完整运行依赖上游工具链**  
   如果需要真正执行脚本导出 `.pptx`，应安装完整上游仓库或上游 skill/plugin。

---

## 2. 上游完整流程摘要

上游 PPT Master 的主流程可概括为：

```text
Source Document
→ Create Project
→ Template Option
→ Strategist
→ Image Acquisition
→ Executor
→ Post-processing
→ Export PPTX
```

对应角色：

- **Source Processor**：把 PDF、DOCX、网页、Excel、PPTX 等转为 Markdown 或可分析材料；
- **Project Manager**：初始化项目目录；
- **Strategist**：确认设计规格，输出内容结构与执行锁定；
- **Image Generator / Searcher**：按需生成或搜索图片；
- **Executor**：逐页生成 SVG 页面；
- **Post Processor**：检查 SVG、拆分备注、处理图片/图标/文本，导出 PPTX。

---

## 3. 用户输入处理

用户可能提供：

- PDF；
- Word / DOCX；
- Excel；
- PPTX；
- Markdown；
- URL；
- 直接粘贴的一段文字；
- 只给一个主题。

处理规则：

1. 有源文件：先读取或转换成可分析文本；
2. 有 URL：抓取网页内容并整理；
3. 只有主题：先做资料收集或让用户补充关键材料；
4. 有明确风格要求：纳入设计确认；
5. 有页数要求：优先遵守；
6. 无页数要求：根据材料复杂度推荐范围。

---

## 4. 设计确认：必须先问/确认的 8 项

在正式生成 PPT 之前，必须给用户一个推荐方案，并等待用户确认或修改。

推荐确认项：

1. **画布格式**：16:9、4:3、小红书、竖版、故事版等；
2. **页数范围**：例如 8–10 页、12–15 页；
3. **目标受众**：老板、客户、面试官、老师、投资人、普通读者等；
4. **风格目标**：商务、学术、科技、极简、咨询风、发布会、杂志风等；
5. **色彩方案**：主色、辅助色、背景色；
6. **图标策略**：少量线性图标、实心图标、不用图标等；
7. **字体策略**：标题字体、正文字体、字号层级；
8. **图片策略**：用户提供、AI 生成、网页搜索、占位图、不用图。

输出给用户时不要太长，格式可以是：

```text
我建议这样做：
1. 格式：PPT 16:9
2. 页数：10 页左右
3. 受众：……
4. 风格：……
5. 颜色：……
6. 图标：……
7. 字体：……
8. 图片：……
确认后我再进入生成。
```

---

## 5. 内容规划

确认后，先生成 PPT 结构，而不是直接画页面。

每页至少明确：

- 页码；
- 页面标题；
- 核心信息；
- 视觉形式；
- 是否需要图表；
- 是否需要图片；
- 演讲备注要点。

示例：

```text
第 1 页：封面
作用：建立主题和视觉基调
内容：标题、副标题、作者/日期
视觉：大标题 + 背景图/抽象图形

第 2 页：问题背景
作用：说明为什么要看这个主题
内容：3 个背景事实
视觉：三栏卡片或时间线
```

---

## 6. 页面生成原则

1. 每页只表达一个核心观点；
2. 标题要像结论，不要只是章节名；
3. 避免整页堆文字；
4. 尽量使用卡片、时间线、流程图、对比表、指标卡、矩阵图；
5. 图片必须服务于观点；
6. 图表必须能读懂，不能只是装饰；
7. 保持统一的色彩、字体、间距、圆角、阴影、图标风格；
8. 长材料要分章节，章节页可作为节奏点。

---

## 7. 质量检查

生成后检查：

- 每页是否有清晰标题；
- 是否存在信息过载；
- 字号是否过小；
- 对齐是否混乱；
- 颜色是否过多；
- 图表是否与数据对应；
- 图片是否低清、跑题或侵权风险明显；
- 页面之间是否风格统一；
- 是否真的满足用户目标。

如果使用上游完整工具链，应运行其 SVG 质量检查和导出脚本。

---

## 8. 完整上游工具链提示

本目录不是完整工具链。真正运行 `ppt-master` 需要完整上游仓库中的：

- `skills/ppt-master/scripts/`
- `skills/ppt-master/references/`
- `skills/ppt-master/templates/`
- `skills/ppt-master/requirements.txt`
- 其他必要资源与 Python 依赖

上游安装方式示例：

```bash
git clone https://github.com/hugohe3/ppt-master.git
cd ppt-master
pip install -r requirements.txt
```

或使用上游 README 提到的 skill/plugin 安装方式：

```bash
npx skills add hugohe3/ppt-master
```

---

## 9. 禁止事项

执行本技能时避免：

1. 用户刚说“做个 PPT”就直接生成最终文件；
2. 不确认受众和风格；
3. 把长文直接切成很多页；
4. 每页只放标题 + 大段文字；
5. 生成不可编辑的整页图片式 PPT；
6. 忽略图表和图片版权/来源问题；
7. 把上游缺失脚本的入口文件误当成完整可运行环境；
8. 未说明依赖条件就承诺能本地完整导出。

---

## 10. 本技能库中的使用建议

如果只是让 ChatGPT 帮你规划 PPT：

- 直接使用本文件即可；
- 输出结构、大纲、页面说明、风格建议。

如果要真正自动生成可编辑 PPTX：

- 使用完整上游 `ppt-master`；
- 或把完整上游项目 clone 到本地；
- 再让 AI 按上游 `skills/ppt-master/SKILL.md` 执行。

如果你后续高频使用这个技能，可以把上游完整 `skills/ppt-master/` vendor 到本仓库，但要保留 MIT License 和来源说明。
