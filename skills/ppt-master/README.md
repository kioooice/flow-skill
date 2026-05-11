# PPT Master 技能

来源仓库：<https://github.com/hugohe3/ppt-master>

原作者：Hugo He  
许可证：MIT License  
提取日期：2026-05-11  
上游版本：README 显示为 v2.6.0

## 这个技能做什么

`ppt-master` 是一个用于让 AI 从 PDF、DOCX、URL、Markdown 或直接粘贴内容生成可编辑 PowerPoint 的工作流技能。

它的目标不是生成一张张图片式幻灯片，而是生成可以在 PowerPoint 中逐个元素编辑的 `.pptx`：文本框、图形、图表、动画等尽量保持为原生对象。

## 放入本仓库的方式

本目录当前保存的是“技能入口提取版”：

- `SKILL.md`：面向你个人技能库整理后的技能入口说明；
- `UPSTREAM.md`：上游来源、安装方式、同步方式；
- `LICENSE.upstream`：上游 MIT 许可证。

注意：`ppt-master` 的完整可运行版本非常大，除 `SKILL.md` 外还依赖大量 Python 脚本、模板、图标库和参考文档。为了避免把一个残缺的大项目假装成完整技能，本目录没有直接搬运完整仓库。

如果要真正运行它，建议在本地或项目环境中安装完整上游仓库，或者使用上游提供的 skill/plugin 安装方式。

## 推荐用法

当你想做 PPT 时，可以先使用本目录的 `SKILL.md` 作为工作流入口，明确：

1. 输入材料是什么；
2. 目标页数是多少；
3. 受众是谁；
4. 风格方向是什么；
5. 是否需要图片生成、网页图片搜索、动画或旁白；
6. 是否要使用完整上游工具链导出 `.pptx`。

## 后续可做

如果你后面决定把完整 `ppt-master` 工具链也纳入自己的技能库，可以再做一次完整 vendor：

```bash
git clone https://github.com/hugohe3/ppt-master.git
```

然后把上游 `skills/ppt-master/`、`requirements.txt`、必要 `docs/` 与脚本目录按许可证要求完整迁入。