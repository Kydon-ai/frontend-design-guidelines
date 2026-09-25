# 企业级产品设计文档

一套面向企业级产品的中文设计规范与页面模式文档，内容围绕 Ant Design 的设计价值观、设计原则、全局规则、基础视觉和典型页面展开。

## 项目简介

本项目用于集中整理和检索企业级产品设计资料，帮助设计师、产品经理和前端开发者：

- 快速理解企业级产品的通用设计方法；
- 在表单、列表、导航、反馈、数据展示等场景中复用成熟模式；
- 统一色彩、字体、图标、布局、阴影和动效等基础规范；
- 通过页面模板和探索专题降低重复设计成本。

项目当前为纯 Markdown 文档仓库，不包含运行时程序或构建脚本。

## 快速开始

从[文档索引](./index.md)开始，根据目标选择阅读路径：

1. 了解体系背景：阅读[介绍](./introduce.zh-CN.md)和[设计价值观](./values.zh-CN.md)。
2. 理解设计方法：阅读[设计模式概览](./overview.zh-CN.md)，再查看具体原则和全局规则。
3. 搭建视觉基础：参考[色彩](./colors.zh-CN.md)、[字体](./font.zh-CN.md)、[布局](./layout.zh-CN.md)和[图标](./icon.zh-CN.md)。
4. 设计业务页面：根据场景查看[表单页](./research-form.zh-CN.md)、[列表页](./research-list.zh-CN.md)、[详情页](./detail-page.zh-CN.md)或[数据可视化页](./visualization-page.zh-CN.md)。
5. 处理异常和反馈：参考[反馈](./feedback.zh-CN.md)、[空状态](./research-empty.zh-CN.md)、[异常页](./research-exception.zh-CN.md)和[结果页](./research-result.zh-CN.md)。

## 文档内容

### Ant Design 基础

- [介绍](./introduce.zh-CN.md)：项目背景、设计资源、前端实现、使用者与贡献方式。
- [设计价值观](./values.zh-CN.md)：自然、确定性、意义感和生长性。
- [实践案例](./cases.zh-CN.md)：多个企业级产品的设计实践案例。

### 设计模式

- [设计模式概览](./overview.zh-CN.md)：设计模式的定位、作用和使用方式。
- 设计原则：亲密性、对齐、对比、重复、直截了当、足不出户、简化交互、提供邀请、巧用过渡、即时反应。
- 全局规则：反馈、导航、数据录入、数据展示、数据格式、数据列表、按钮和文案。
- 页面模板：详情页和数据可视化页。

### 基础视觉与交互

- [色彩](./colors.zh-CN.md)与[暗黑模式](./dark.zh-CN.md)：系统级、产品级和暗色主题的色彩规范。
- [字体](./font.zh-CN.md)、[图标](./icon.zh-CN.md)与[图形化](./illustration.zh-CN.md)：文字和图形资产规范。
- [布局](./layout.zh-CN.md)与[阴影](./shadow.zh-CN.md)：空间、网格、高度和层次关系。
- [动效](./motion.zh-CN.md)、[可视化](./visual.zh-CN.md)：动效原则和数据图表设计方法。

### 探索专题

探索专题记录持续研究和完善中的页面模式，包括：

- [探索概览](./research-overview.zh-CN.md)
- [导航](./research-navigation.zh-CN.md)
- [表单页](./research-form.zh-CN.md)
- [工作台](./research-workbench.zh-CN.md)
- [消息与反馈](./research-message-and-feedback.zh-CN.md)
- [列表页](./research-list.zh-CN.md)
- [空状态](./research-empty.zh-CN.md)
- [结果页](./research-result.zh-CN.md)
- [异常页](./research-exception.zh-CN.md)

## 目录结构

```text
.
├── README.md                  # 项目说明
├── index.md                   # 全部文档索引与快速查找入口
├── introduce.zh-CN.md         # Ant Design 介绍
├── values.zh-CN.md            # 设计价值观
├── overview.zh-CN.md          # 设计模式概览
├── research-*.zh-CN.md        # 探索专题与页面模板
└── *.zh-CN.md                 # 设计原则、全局规则和基础视觉文档
```

## 使用方式

本项目不需要安装依赖。可以直接在 GitHub、支持 Markdown 的编辑器或本地 Markdown 阅读器中阅读文档。文档中的图片和部分参考链接来自外部资源，离线阅读时可能无法加载。

完整的文件级导航、主题分类和任务导向入口请查看[index.md](./index.md)。

## 贡献指南

欢迎补充案例、修正文案、完善页面模式或增加新的设计规范。建议遵循以下流程：

1. 从独立分支开始修改，保持主题范围清晰；
2. 使用现有的 Markdown 结构和中文命名方式；
3. 新增或移动文档时同步更新[index.md](./index.md)和本 README；
4. 提交前检查相对链接、图片链接、标题层级和 Markdown 渲染效果；
5. 使用能够说明变更内容的 Git 提交信息。

## 项目状态

当前仓库是文档型项目，已整理 42 份设计文档，并通过[index.md](./index.md)提供统一入口。部分“探索”专题属于持续演进内容，使用时应结合具体业务场景进行判断。

## 许可说明

当前仓库未包含独立的 `LICENSE` 文件。对文档进行复制、修改或再分发前，请先确认项目所有者的授权范围。
