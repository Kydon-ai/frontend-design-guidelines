# 文档索引

本目录整理了一套面向企业级产品的 Ant Design 中文设计文档，共包含 42 份 Markdown 文档，覆盖设计价值观、设计模式、全局样式、交互原则、通用规则、页面模板和数据可视化等内容。文档已按用途归档到 `src/00-context` 至 `src/05-scenarios`，组件库适配资料位于 `src/06-adapters`，Agent 的按需读取规则见 `src/manifest.yaml`。

## 推荐阅读路径

1. 先阅读[介绍](./src/00-context/introduce.zh-CN.md)，了解 Ant Design 的背景、资源、前端实现和参与方式。
2. 通过[设计价值观](./src/00-context/values.zh-CN.md)理解“自然、确定性、意义感、生长性”四项核心价值。
3. 阅读[设计模式概览](./src/00-context/overview.zh-CN.md)，再按需进入具体的设计原则和全局规则。
4. 进行页面设计时，优先参考“页面模板”和“探索专题”中的对应页面类型。
5. 涉及图表或数据分析时，结合[可视化](./src/02-foundation/visual.zh-CN.md)与[数据可视化页](./src/04-page-templates/visualization-page.zh-CN.md)。

## 一、Ant Design 基础

| 文档 | 内容简介 |
| --- | --- |
| [介绍](./src/00-context/introduce.zh-CN.md) | 介绍 Ant Design 的产生背景、设计资源、前端实现、使用者、社区评价与贡献方式。 |
| [设计价值观](./src/00-context/values.zh-CN.md) | 说明自然、确定性、意义感和生长性四项设计价值观。 |
| [实践案例](./src/00-context/cases.zh-CN.md) | 汇总蚂蚁金融科技、OceanBase、语雀、Ant Design Pro、阿里云流计算等实践案例。 |

## 二、设计模式总览

| 文档 | 内容简介 |
| --- | --- |
| [设计模式概览](./src/00-context/overview.zh-CN.md) | 说明设计模式的定位、作用、使用方式以及相关设计资源。 |

### 2.1 设计原则

| 文档 | 内容简介 |
| --- | --- |
| [亲密性](./src/01-principles/proximity.zh-CN.md) | 通过纵向、横向间距组织信息层级，表达元素之间的关联程度。 |
| [对齐](./src/01-principles/alignment.zh-CN.md) | 规范文案、表单和数字等内容的对齐方式，建立清晰的视觉秩序。 |
| [对比](./src/01-principles/contrast.zh-CN.md) | 通过主次、总分和状态关系的对比突出重点、建立层级。 |
| [重复](./src/01-principles/repetition.zh-CN.md) | 通过重复使用相同的视觉元素降低学习成本，并强化内容关联。 |
| [直截了当](./src/01-principles/direct.zh-CN.md) | 倡导在上下文中直接完成编辑和操作，减少不必要的页面跳转。 |
| [足不出户](./src/01-principles/stay.zh-CN.md) | 尽量在当前页面解决问题，减少刷新和跳转对用户心流的打断。 |
| [简化交互](./src/01-principles/lightweight.zh-CN.md) | 根据需要展示工具，使用实时可见、悬停即现和开关显示等方式降低界面负担。 |
| [提供邀请](./src/01-principles/invitation.zh-CN.md) | 通过可感知的提示和可供性，引导用户发现并执行下一步操作。 |
| [巧用过渡](./src/01-principles/transition.zh-CN.md) | 使用添加、移除和自然过渡等方式保持上下文，并解释界面变化。 |
| [即时反应](./src/01-principles/reaction.zh-CN.md) | 在交互前、交互中和交互后提供及时反馈，帮助用户理解系统状态。 |

### 2.2 全局规则

| 文档 | 内容简介 |
| --- | --- |
| [反馈](./src/03-ui-rules/feedback.zh-CN.md) | 规范提示信息、过程反馈、录入反馈和结果反馈的使用方式。 |
| [导航](./src/03-ui-rules/navigation.zh-CN.md) | 介绍菜单、面包屑、标签页、步骤条和分页器等导航组件。 |
| [数据录入](./src/03-ui-rules/data-entry.zh-CN.md) | 规范文本输入、选择录入、日期选择和文件上传等录入场景。 |
| [数据展示](./src/03-ui-rules/data-display.zh-CN.md) | 介绍表格、折叠面板、卡片、走马灯、树形控件和时间轴等展示方式。 |
| [数据格式](./src/03-ui-rules/data-format.zh-CN.md) | 规范数值、金额、日期时间、脱敏和数据状态等数据表达方式。 |
| [数据列表](./src/03-ui-rules/data-list.zh-CN.md) | 说明列表类型、查询筛选、分页、批量操作、新建、删除和工具栏设计。 |
| [按钮](./src/03-ui-rules/buttons.zh-CN.md) | 介绍按钮类型、强调方式、放置位置、顺序、分组及按钮文案。 |
| [文案](./src/03-ui-rules/copywriting.zh-CN.md) | 规范界面语言、语气、大小写、数字和标点，帮助建立清晰一致的沟通方式。 |

### 2.3 页面模板

| 文档 | 内容简介 |
| --- | --- |
| [详情页](./src/04-page-templates/detail-page.zh-CN.md) | 介绍基础详情、单据详情和复杂详情页的布局、区隔方式与内容组件。 |
| [数据可视化页](./src/04-page-templates/visualization-page.zh-CN.md) | 介绍概览、分析、明细等数据可视化页面类型及其布局和组件选择建议。 |

## 三、全局样式与基础视觉

| 文档 | 内容简介 |
| --- | --- |
| [色彩](./src/02-foundation/colors.zh-CN.md) | 介绍系统级和产品级色彩体系，包括基础色板、中性色、数据可视化色板和功能色。 |
| [暗黑模式](./src/02-foundation/dark.zh-CN.md) | 说明暗黑模式的适用场景、设计原则和色彩处理方式。 |
| [字体](./src/02-foundation/font.zh-CN.md) | 规范字体家族、主字体、字阶与行高、字重和字体颜色。 |
| [图标](./src/02-foundation/icon.zh-CN.md) | 介绍图标的设计原则、规格、分层、轮廓线、构图韵律、平衡与辨识度。 |
| [图形化](./src/02-foundation/illustration.zh-CN.md) | 介绍图形化设计的背景、原则、色板、人物组件、元素组件和设计应用。 |
| [布局](./src/02-foundation/layout.zh-CN.md) | 说明统一画板、响应式适配、网格单位、栅格和常用模度。 |
| [阴影](./src/02-foundation/shadow.zh-CN.md) | 介绍 UI 高度、光源、阴影值和常用阴影设计表。 |

## 四、动效与数据可视化

| 文档 | 内容简介 |
| --- | --- |
| [动效](./src/02-foundation/motion.zh-CN.md) | 说明动效的价值、意义衡量方式，以及自然、高效、克制等设计原则。 |
| [可视化](./src/02-foundation/visual.zh-CN.md) | 介绍图表类型选择、色板、标题与注释、坐标轴、图例、标签、提示信息、布局适应和交互。 |

## 五、探索专题

探索专题聚焦仍在研究、完善或持续演进的企业级页面模式，包含概览、导航、表单、工作台、消息反馈、列表、空状态、结果页和异常页。

| 文档 | 内容简介 |
| --- | --- |
| [探索概览](./src/05-scenarios/research-overview.zh-CN.md) | 说明探索频道的定位、研究内容和反馈方式。 |
| [导航](./src/05-scenarios/research-navigation.zh-CN.md) | 介绍全局导航、子站点导航、页内导航、下钻、返回和联想类导航。 |
| [表单页](./src/05-scenarios/research-form.zh-CN.md) | 介绍普通表单、分步表单、分组表单、设置、登录和注册等页面模板。 |
| [工作台](./src/05-scenarios/research-workbench.zh-CN.md) | 介绍作为应用主页的工作台，以及信息组织、导航方式和异常状态处理。 |
| [消息与反馈](./src/05-scenarios/research-message-and-feedback.zh-CN.md) | 说明成功、失败等场景下的反馈方式，以及留在原地、跳转等行为选择。 |
| [列表页](./src/05-scenarios/research-list.zh-CN.md) | 介绍单列、双栏、查询表格、标准列表、卡片列表、搜索列表和成员管理等模板。 |
| [空状态](./src/05-scenarios/research-empty.zh-CN.md) | 说明新手引导、完成或清空、无数据等空状态的目标、原则和使用场景。 |
| [结果页](./src/05-scenarios/research-result.zh-CN.md) | 介绍操作完成后的结果反馈、基础结果页、复杂结果页和补充信息。 |
| [异常页](./src/05-scenarios/research-exception.zh-CN.md) | 介绍 404、403、500、浏览器不兼容、空状态和加载失败等异常页面。 |

## 六、按任务快速查找

| 如果你要…… | 优先阅读 |
| --- | --- |
| 搭建一套页面的基础视觉规范 | [色彩](./src/02-foundation/colors.zh-CN.md)、[字体](./src/02-foundation/font.zh-CN.md)、[布局](./src/02-foundation/layout.zh-CN.md)、[图标](./src/02-foundation/icon.zh-CN.md)、[阴影](./src/02-foundation/shadow.zh-CN.md) |
| 设计表单或录入流程 | [数据录入](./src/03-ui-rules/data-entry.zh-CN.md)、[表单页](./src/05-scenarios/research-form.zh-CN.md)、[按钮](./src/03-ui-rules/buttons.zh-CN.md)、[反馈](./src/03-ui-rules/feedback.zh-CN.md) |
| 设计列表、表格或数据管理页 | [数据列表](./src/03-ui-rules/data-list.zh-CN.md)、[数据展示](./src/03-ui-rules/data-display.zh-CN.md)、[列表页](./src/05-scenarios/research-list.zh-CN.md)、[导航](./src/03-ui-rules/navigation.zh-CN.md) |
| 设计数据分析或监控页面 | [可视化](./src/02-foundation/visual.zh-CN.md)、[数据可视化页](./src/04-page-templates/visualization-page.zh-CN.md)、[数据格式](./src/03-ui-rules/data-format.zh-CN.md) |
| 处理加载、成功、失败和空数据 | [反馈](./src/03-ui-rules/feedback.zh-CN.md)、[消息与反馈](./src/05-scenarios/research-message-and-feedback.zh-CN.md)、[空状态](./src/05-scenarios/research-empty.zh-CN.md)、[异常页](./src/05-scenarios/research-exception.zh-CN.md)、[结果页](./src/05-scenarios/research-result.zh-CN.md) |
| 优化交互的连贯性和反馈 | [提供邀请](./src/01-principles/invitation.zh-CN.md)、[巧用过渡](./src/01-principles/transition.zh-CN.md)、[即时反应](./src/01-principles/reaction.zh-CN.md)、[足不出户](./src/01-principles/stay.zh-CN.md) |
