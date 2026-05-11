# 上游来源说明：PPT Master

## 来源

- 上游仓库：<https://github.com/hugohe3/ppt-master>
- 上游作者：Hugo He
- 上游许可证：MIT License
- 上游 README 显示版本：v2.6.0
- 上游技能路径：`skills/ppt-master/`
- 上游 marketplace 配置：`.claude-plugin/marketplace.json`

## 上游说明摘要

根据上游 README，PPT Master 的定位是：

> 从 PDF、DOCX、URL 或 Markdown 生成原生可编辑 PowerPoint，而不是图片式 PPT。

其主流程大致为：

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

核心依赖包括：

- Python 3.10+
- `skills/ppt-master/scripts/` 下的转换、生成、检查、导出脚本
- `skills/ppt-master/references/` 下的执行规范
- `skills/ppt-master/templates/` 下的版式、图表、图标资源
- `requirements.txt`

## 为什么本仓库没有直接搬运完整项目

完整 `ppt-master` 仓库体积较大，包含大量模板、图标、脚本和示例。如果只复制 `SKILL.md`，实际运行时会缺少脚本和模板；如果直接复制整个仓库，又会让个人技能库迅速变得很大。

因此本次采用“入口提取 + 上游引用”方式：

- 保留可阅读、可复用的技能入口；
- 明确说明完整运行需要上游工具链；
- 保留许可证和来源信息；
- 后续如确实高频使用，再决定是否完整 vendor。

## 完整安装方式

上游 README 提供了几种方式。

### 方式 A：直接克隆完整仓库

```bash
git clone https://github.com/hugohe3/ppt-master.git
cd ppt-master
pip install -r requirements.txt
```

### 方式 B：使用技能安装方式

上游 README 中提到：

```bash
npx skills add hugohe3/ppt-master
```

或在 Claude Code 中：

```bash
/plugin marketplace add hugohe3/ppt-master
/plugin install ppt-master@ppt-master
```

注意：这种方式通常只安装技能文件，仍需要根据上游说明安装 Python 依赖。

## 同步建议

如果后续要更新本目录内容：

1. 查看上游 `skills/ppt-master/SKILL.md` 是否更新；
2. 查看上游 `.claude-plugin/marketplace.json` 的版本号；
3. 如果主流程变化明显，同步更新本目录 `SKILL.md` 和 `README.md`；
4. 如果要完整运行，优先使用完整上游仓库，而不是只依赖本目录。
