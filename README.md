# 企业级前端ToB产品设计文档参照

一套面向企业级产品的中文设计规范与页面模式文档，内容基于 Ant Design 的设计价值观、设计原则、全局规则、基础视觉和典型页面展开。用于给AI提供基础的组件开发认知参考，版权所属归属源项目。

## 项目简介

本项目用于集中整理和检索企业级产品设计资料，帮助设计师、产品经理和前端开发者：

- 快速理解企业级产品的通用设计方法；
- 在表单、列表、导航、反馈、数据展示等场景中复用成熟模式；
- 统一色彩、字体、图标、布局、阴影和动效等基础规范；
- 通过页面模板和探索专题降低重复设计成本。


## 快速开始

从[文档索引](./index.md)开始，根据目标选择阅读路径：

1. 了解体系背景：阅读[介绍](./src/00-context/introduce.zh-CN.md)和[设计价值观](./src/00-context/values.zh-CN.md)。
2. 理解设计方法：阅读[设计模式概览](./src/00-context/overview.zh-CN.md)，再查看具体原则和全局规则。
3. 搭建视觉基础：参考[色彩](./src/02-foundation/colors.zh-CN.md)、[字体](./src/02-foundation/font.zh-CN.md)、[布局](./src/02-foundation/layout.zh-CN.md)和[图标](./src/02-foundation/icon.zh-CN.md)。
4. 设计业务页面：根据场景查看[表单页](./src/05-scenarios/research-form.zh-CN.md)、[列表页](./src/05-scenarios/research-list.zh-CN.md)、[详情页](./src/04-page-templates/detail-page.zh-CN.md)或[数据可视化页](./src/04-page-templates/visualization-page.zh-CN.md)。
5. 处理异常和反馈：参考[反馈](./src/03-ui-rules/feedback.zh-CN.md)、[空状态](./src/05-scenarios/research-empty.zh-CN.md)、[异常页](./src/05-scenarios/research-exception.zh-CN.md)和[结果页](./src/05-scenarios/research-result.zh-CN.md)。

## 文档内容

### Ant Design 基础

- [介绍](./src/00-context/introduce.zh-CN.md)：项目背景、设计资源、前端实现、使用者与贡献方式。
- [设计价值观](./src/00-context/values.zh-CN.md)：自然、确定性、意义感和生长性。
- [实践案例](./src/00-context/cases.zh-CN.md)：多个企业级产品的设计实践案例。

### 设计模式

- [设计模式概览](./src/00-context/overview.zh-CN.md)：设计模式的定位、作用和使用方式。
- 设计原则：亲密性、对齐、对比、重复、直截了当、足不出户、简化交互、提供邀请、巧用过渡、即时反应。
- 全局规则：反馈、导航、数据录入、数据展示、数据格式、数据列表、按钮和文案。
- 页面模板：详情页和数据可视化页。

### 基础视觉与交互

- [色彩](./src/02-foundation/colors.zh-CN.md)与[暗黑模式](./src/02-foundation/dark.zh-CN.md)：系统级、产品级和暗色主题的色彩规范。
- [字体](./src/02-foundation/font.zh-CN.md)、[图标](./src/02-foundation/icon.zh-CN.md)与[图形化](./src/02-foundation/illustration.zh-CN.md)：文字和图形资产规范。
- [布局](./src/02-foundation/layout.zh-CN.md)与[阴影](./src/02-foundation/shadow.zh-CN.md)：空间、网格、高度和层次关系。
- [动效](./src/02-foundation/motion.zh-CN.md)、[可视化](./src/02-foundation/visual.zh-CN.md)：动效原则和数据图表设计方法。

### 探索专题

探索专题记录持续研究和完善中的页面模式，包括：

- [探索概览](./src/05-scenarios/research-overview.zh-CN.md)
- [导航](./src/05-scenarios/research-navigation.zh-CN.md)
- [表单页](./src/05-scenarios/research-form.zh-CN.md)
- [工作台](./src/05-scenarios/research-workbench.zh-CN.md)
- [消息与反馈](./src/05-scenarios/research-message-and-feedback.zh-CN.md)
- [列表页](./src/05-scenarios/research-list.zh-CN.md)
- [空状态](./src/05-scenarios/research-empty.zh-CN.md)
- [结果页](./src/05-scenarios/research-result.zh-CN.md)
- [异常页](./src/05-scenarios/research-exception.zh-CN.md)

### 组件库适配

- [组件语义角色映射](./src/06-adapters/component-role-map.md)：先按页面模块和语义角色选型，再映射到具体组件库。
- [Ant Design 适配](./src/06-adapters/ant-design.md)
- [Element UI 适配](./src/06-adapters/element-ui.md)
- [Element Plus 适配](./src/06-adapters/element-plus.md)
- [Flutter Material 适配](./src/06-adapters/flutter-material.md)

## 目录结构

```text
.
├── SKILL.md                   # Agent 触发条件、执行流程和交互协议
├── README.md                  # 项目说明与使用方式
├── index.md                   # 全部文档索引与任务导向入口
└── src/
    ├── manifest.yaml          # 文档分类、阅读顺序和检索关键词
    ├── 00-context/            # 项目背景、设计价值观、概览和实践案例
    ├── 01-principles/         # 设计原则与交互方法
    ├── 02-foundation/         # 色彩、字体、布局、图标、动效等基础规范
    ├── 03-ui-rules/           # 按钮、表单、列表、导航、反馈等 UI 规则
    ├── 04-page-templates/     # 详情页、数据可视化页等页面模板
    ├── 05-scenarios/          # 探索专题与具体业务场景
    └── 06-adapters/           # 语义角色到 Ant Design、Element、Flutter 的映射
```

## 使用方式

当前仓库是文档型项目，已整理 42 份设计文档，完整的文件级导航、主题分类和任务导向入口请查看[index.md](./index.md)。

如果将本项目作为 Agent Skill 使用，先读取根目录的[SKILL.md](./SKILL.md)，再按任务从[src/manifest.yaml](./src/manifest.yaml)定位需要加载的资料。Agent 应先判断页面类型和模块，再读取对应的基础规范、UI 规则、页面模板及组件库适配说明，避免一次性加载全部文档。

可以通过如下方式使用本项目：
```
请拉取`https://github.com/Kydon-ai/frontend-design-guidelines` 这个项目，参照其index.md文档的索引，查看项目基础色彩搭配和布局规范。结合我目前的项目，确定基础基调。
```

## 项目参考来源

请跳转到：[ant-design](https://github.com/ant-design/ant-design/tree/master/docs/spec)
