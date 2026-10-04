---
name: frontend-design-spec
description: 当 Agent 需要在 Web 前端、移动端或桌面客户端中新增、修改或实现页面 UI 时使用。读取或初始化项目级 .design-spec/ 设计配置，判断页面类型和页面模块，并将语义化 UI 角色映射到项目实际使用的组件库，包括 Ant Design、Element UI/Element Plus 和 Flutter Material。仅后端或与 UI 无关的任务不要使用此 Skill。
metadata:
  short-description: 面向项目的 UI 设计与组件映射
---

# 前端设计规范 Skill

## 目标

将本仓库中的企业级 UI 设计方法论转化为可重复执行的页面 UI 改动流程。

每次修改页面前，必须回答以下四个问题：

1. 当前项目使用哪些视觉和布局规则？
2. 正在修改的页面或功能属于什么类型？
3. 这个页面或功能由哪些模块组成？
4. 每个模块应使用什么语义组件，以及项目组件库中的哪个具体组件？

本 Skill 只用于辅助设计决策，不代表可以重做与任务无关的页面。除非用户明确要求，否则应保留现有产品约定和用户已经确认的配置。

## 触发范围

当用户需要在 Web 前端、移动端或桌面客户端中新增、删除、调整、重构、换肤或实现页面 UI 时使用本 Skill。

以下情况不要使用：

- 只修改后端逻辑、数据模型或接口；
- 只修改与 UI 无关的构建配置；
- 只制作视觉资源，且不涉及界面结构和交互决策；
- 与页面 UI 无关的普通代码任务。

## 必须执行的工作流

### 1. 先读取项目设计规范

在做任何 UI 决策前，先检查项目根目录下的 `.design-spec/`。

- 如果 `.design-spec/` 存在，读取其中与当前任务相关的文件，并将已确认的项目配置视为最高优先级。
- 如果存在 `.design-spec/design-spec.yaml`，将它作为规范主文件。
- 如果目录中已有其他明确的规范主文件，先读取它，不要悄悄创建另一份互相竞争的配置。
- 如果某些配置缺失，只询问会影响当前 UI 改动的字段。
- 不要覆盖已有设计规范。如果已有值与本 Skill 默认值冲突，应保留项目值并向用户说明冲突。
- 在给出具体组件建议或代码前，还要检查项目真实使用的框架、组件库、版本、主题 Provider、设计 Token 和业务组件封装。

### 2. 缺少 `.design-spec/` 时初始化

如果项目根目录没有 `.design-spec/`，先用一次集中式问题引导用户完成全局配置，不要让用户逐个配置所有设计 Token。

需要用户选择：

1. 一个必选的主基础色，也可以额外选择辅助基础色；
2. 一个中性色系：黑、白或灰；用户没有偏好时默认使用灰；
3. 布局模式：上下、左右或网格；选择网格时，网格基数固定为 8；
4. 如果无法从项目中可靠识别，则询问组件库。

基础色候选如下：

| 名称 | Hex |
|---|---|
| 薄暮 | `#5c0011` |
| 火山 | `#610b00` |
| 日暮 | `#612500` |
| 金盏花 | `#613400` |
| 日出 | `#614700` |
| 青柠 | `#254000` |
| 极光绿 | `#092b00` |
| 明青 | `#002329` |
| 拂晓蓝 | `#002766` |
| 极客蓝 | `#030852` |
| 酱紫 | `#120338` |
| 法式洋红 | 用户必须补充 Hex 后才能使用 |

除非已有项目配置与默认值冲突，否则不要询问功能色和字体。功能色固定为：

- 成功：`#52c41a`
- 失败：`#ff4d4f`
- 警告：`#faad14`
- 通知：`#1890ff`

默认字体组合为：

```css
-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial,
'Noto Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol',
'Noto Color Emoji'
```

默认间距网格基数为 8。用户选择上下或左右时，仍然使用 8 作为间距基准；用户选择网格时，记录 `layout.mode: grid` 和 `layout.grid.base: 8`，不要擅自替换成其他布局模式。

用户确认后，创建 `.design-spec/design-spec.yaml`，结构如下。保留用户选择的值；项目相关但尚未确认的值使用 `auto-detect`，不要凭空编造。

```yaml
version: 1
source: user-confirmed
component_library:
  name: auto-detect
  version: auto-detect
color:
  base:
    primary_name: 拂晓蓝
    primary_hex: "#002766"
    secondary: []
  neutral_family: gray
  functional:
    success: "#52c41a"
    error: "#ff4d4f"
    warning: "#faad14"
    info: "#1890ff"
typography:
  font_family: "-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji'"
layout:
  mode: vertical
  grid:
    enabled: true
    base: 8
```

创建文件后，向用户展示解析后的配置，再继续处理当前 UI 需求。如果用户尚未确认选择，不要提前创建 `.design-spec/`。

### 3. 维护简洁的决策状态

每个相关配置项都要记录来源：

- `confirmed`：用户或已有项目规范明确确认；
- `inferred`：根据代码库或需求推断，但仍可修改；
- `default`：用户未指定时使用的 Skill 默认值；
- `unknown`：缺失，并且重要到需要询问。

使用以下优先级：

1. 当前用户明确指令；
2. 已有 `.design-spec/` 配置；
3. 代码库和现有业务组件约定；
4. 当前对话中用户此前确认过的值；
5. Skill 默认值；
6. Agent 推断。

在进行较大 UI 改动前，先展示简短的“当前设计配置”，包括已确认值、默认值和会影响结果的未决问题。尽量一次只追问一个重点问题。

## 用户交互协议

不要在开始时一次性询问很长的问卷。先从用户描述和代码库中提取已知信息，再询问高影响配置。

首次确认通常包括：

- 页面或功能类型；
- 主要用户和用户目标；
- 目标平台或视口；
- 无法从项目中识别时的组件库和版本；
- 输出形式：设计方案、组件方案、代码实现或 UI 评审。

确定页面类型后，再根据类型追问：

- 表单：字段数量、校验方式、保存或草稿行为、是否分步、重置和取消行为；
- 列表或表格：数据量、筛选、排序、分页、选择、批量操作、导出、行操作；
- 详情页：只读还是编辑、信息分区、标签页、状态流转、审计记录；
- 数据看板：指标、对比周期、刷新频率、下钻路径、图表库；
- 工作台：导航、固定面板、快捷操作、多任务行为；
- 移动端或客户端：触控区域、安全区、手势、平台导航、离线行为。

用户没有指定风格时，使用项目规范和现有页面的视觉语言。除非会实质影响当前改动，否则不要追问圆角、阴影、图标和动效细节。

## ETC 抽象

Ant Design 的设计模式文档将内容组织为功能范例、页面模板、组件和通用概念。本 Skill 将 ETC 操作化为：

- **E — Example / 功能范例**：要支持的用户旅程或业务能力；
- **T — Template / 页面模板**：页面级组合，例如列表、表单、详情、看板、工作台、结果、空状态或异常页；
- **C — Component / 组件**：可复用的语义化构建块，包括基础组件和业务模块。

通用概念是贯穿 E、T、C 的横向规则，包括色彩、字体、间距、布局、文案、反馈、动效、无障碍和响应式行为。

不要把 ETC 当成某个组件库的固定 API，也不要假设不同组件库之间存在一对一映射。同一个语义组件在不同组件库中可能名称不同、组合方式不同，交互行为也可能不同。

## 页面分类与模块拆解

先将用户请求归入一个主要页面类型：

- 应用框架或导航页；
- 列表、表格、搜索或管理页；
- 新建、编辑、设置或分步表单；
- 详情页或读写混合页；
- 数据看板、分析或数据可视化页；
- 工作台或任务处理页；
- 结果、成功、空数据、加载或异常页；
- 登录、注册、引导或邀请页；
- 其他类型，必须明确命名。

然后按实际需要拆解页面模块：

| 页面模块 | 需要考虑的语义角色 |
|---|---|
| 应用框架 | 页面布局、顶部栏、侧边栏、顶部导航、内容区、页脚、安全区 |
| 上下文头部 | 页面标题、面包屑、标签页、状态、摘要、主要操作 |
| 查询或筛选区 | 表单、文本输入、选择器、日期范围、分段选择、重置和搜索操作 |
| 操作区 | 主要操作、次要操作、危险操作、下拉操作、批量操作、更多操作 |
| 数据区 | 表格、列表、卡片网格、树、时间线、日历、统计、图表 |
| 详情区 | 描述列表、信息分组、标签页、卡片组、附件、活动记录 |
| 编辑区 | 表单字段、校验、上传、步骤、保存、取消、重置、草稿 |
| 反馈区 | 加载、空数据、错误、成功、警告、无权限、进度 |
| 辅助浮层 | 弹窗、抽屉、气泡、Tooltip、底部弹层、侧边面板 |

对每个使用到的模块，都要说明：

1. 模块目的；
2. 数据和交互；
3. 视觉优先级；
4. 与当前场景相关的正常、加载、空数据、错误、禁用和无权限状态；
5. 需要的语义组件角色；
6. 项目组件库中可以使用的具体组件。

## 跨组件库的组件抽象

先按语义角色选择组件，再映射到具体组件库 API。下表是起始映射，不替代对项目实际依赖和版本的检查。

| 语义角色 | Ant Design | Element UI / Element Plus | Flutter Material |
|---|---|---|---|
| 页面框架与布局 | `Layout`、`Header`、`Sider`、`Content`、`Footer`、`Flex`、`Grid`、`Space` | `el-container`、`el-header`、`el-aside`、`el-main`、`el-footer`、`el-row`、`el-col`；Element Plus 还可使用 `el-space` | `Scaffold`、`AppBar`、`SafeArea`、`Row`、`Column`、`Expanded`、`Flexible`、`Stack`、`Container` |
| 主导航 | `Menu`、`Breadcrumb`、`Tabs`、`Steps`、`Pagination` | `el-menu`、`el-breadcrumb`、`el-tabs`、`el-steps`、`el-pagination` | `NavigationBar`、`NavigationDrawer`、`NavigationRail`、`TabBar`、`Stepper` |
| 操作 | `Button`、`Dropdown`、`FloatButton`、图标包 | `el-button`、`el-dropdown`、`el-link`、图标包 | `ElevatedButton`、`FilledButton`、`OutlinedButton`、`TextButton`、`IconButton`、`FloatingActionButton`、`SegmentedButton` |
| 文本与内容 | `Typography`、`Card`、`List`、`Descriptions`、`Avatar`、`Tag`、`Statistic`、`Image` | `el-card`、`el-descriptions`、`el-avatar`、`el-tag`、`el-image`；Element Plus 还提供 `el-text` 和 `el-statistic` | `Text`、`Card`、`ListTile`、`Chip`、`Badge`、`Image`、`DataTable` |
| 数据录入 | `Form`、`Input`、`InputNumber`、`Select`、`Radio`、`Checkbox`、`Switch`、`DatePicker`、`TimePicker`、`Upload`、`Cascader`、`TreeSelect`、`Transfer`、`Slider` | `el-form`、`el-input`、`el-input-number`、`el-select`、`el-radio`、`el-checkbox`、`el-switch`、`el-date-picker`、`el-time-picker`、`el-upload`、`el-cascader`、`el-tree-select`、`el-transfer`、`el-slider` | `Form`、`TextFormField`、`DropdownMenu`、`Radio`、`Checkbox`、`Switch`、`DatePicker`、`TimePicker`、`Autocomplete`、`Slider`、`RangeSlider`、`ChoiceChip`、`FilterChip` |
| 数据展示 | `Table`、`List`、`Card`、`Tree`、`Calendar`、`Timeline`、`Descriptions`、`Progress`、`Statistic`、`Empty` | `el-table`、`el-card`、`el-tree`、`el-calendar`、`el-timeline`、`el-descriptions`、`el-progress`；Element Plus 还提供 `el-statistic` 和 `el-empty`；没有列表组件时使用项目已有基础组件组合 | `DataTable`、`ListView`、`GridView`、`Card`、`ExpansionTile`、`LinearProgressIndicator`、`CircularProgressIndicator`；Material 没有精确组件时使用项目依赖或自定义 Widget |
| 反馈与状态 | `Alert`、`Message`、`Notification`、`Modal`、`Drawer`、`Popconfirm`、`Result`、`Skeleton`、`Spin`、`Progress`、`Tooltip` | `el-alert`、`el-message`、`el-notification`、`el-dialog`、`el-drawer`、`el-popconfirm`、`el-result`、`el-skeleton`、`el-loading`、`el-progress`、`el-tooltip` | `AlertDialog`、`SnackBar`、`MaterialBanner`、`showModalBottomSheet`、`LinearProgressIndicator`、`CircularProgressIndicator`、`Tooltip`、`Badge` |
| 临时浮层 | `Modal`、`Drawer`、`Popover`、`Tooltip`、`Dropdown` | `el-dialog`、`el-drawer`、`el-popover`、`el-tooltip`、`el-dropdown` | `AlertDialog`、`showDialog`、`BottomSheet`、`PopupMenuButton`、`MenuAnchor`、`Tooltip` |
| 图表与可视化 | 通常使用 AntV、ECharts 或项目已有图表库 | 通常使用 ECharts 或项目已有图表库 | 通常使用项目图表包或自定义绘制；不要虚构 Material 图表组件 |

### 跨库映射规则

- 从 `package.json`、`pubspec.yaml`、import、lockfile 和现有业务组件中识别真实使用的组件库。
- 区分 `element-ui`（Vue 2）和 `element-plus`（Vue 3）。语义相同不代表 API 相同。
- 区分 Flutter 的核心 `widgets` 基础组件和 Material 组件，并检查项目使用的是 Material 2 还是 Material 3。
- 对 Ant Design，区分基础 `antd` 组件与 ProTable、ProForm 或项目自定义业务组件。
- 如果现有业务组件已经封装了 Token、权限、埋点或业务行为，优先复用业务组件，而不是直接使用底层组件。
- 不要因为其他组件库存在某个组件，就虚构当前组件库中的同名组件。如果没有完全对应的组件，应使用最接近的基础组件组合，并说明差异。
- 设计模式映射为组件时，要同时检查状态、无障碍、响应式和交互语义。
- 图表、富文本编辑器、地图或其他专业控件如果不属于核心组件库，应识别项目已经安装的专业包；新增依赖前先询问用户。

## UI 改动决策流程

每次处理 UI 改动时，按以下顺序执行：

1. 读取 `.design-spec/` 和相关项目代码；
2. 提取并确认当前设计配置；
3. 判断页面类型和用户目标；
4. 从本地设计文档中选择最接近的页面模板或设计模式；
5. 拆解受影响的页面模块；
6. 将每个模块映射为语义角色，再映射到具体组件库组件；
7. 应用项目色彩、字体、布局模式和 8 单位网格；
8. 检查主要/次要操作层级、导航连续性，以及加载、空数据、错误、禁用和无权限状态；
9. 在满足需求的前提下做最小范围改动，保持周边页面的一致性；
10. 如果用户要求实现代码，使用项目真实的框架和组件库 API 修改代码，并运行最相关的检查。

## 输出要求

实现前先输出简短的决策摘要，包含：

- 当前生效的 `.design-spec/` 配置；
- 页面类型以及判断理由；
- 受影响的页面模块；
- 语义组件角色；
- 已知版本下可用的具体组件；
- 尚未解决的假设或问题。

如果用户只要求设计方案，输出页面结构、信息层级、组件、状态、交互行为、文案建议和使用到的本地设计文档。

如果用户要求代码，必须使用项目实际存在的组件 API。未验证 API 时，不要输出看起来像真实 API 的伪代码。

## 本地文档读取路由

按任务逐步读取本地文档，不要每次都读取全部文档。完整分类和页面类型关键词见 `src/manifest.yaml`；以下是常用任务的快捷路由。

- 基础视觉：`src/02-foundation/colors.zh-CN.md`、`src/02-foundation/font.zh-CN.md`、`src/02-foundation/layout.zh-CN.md`、`src/02-foundation/icon.zh-CN.md`、`src/02-foundation/shadow.zh-CN.md`、`src/02-foundation/motion.zh-CN.md`
- 设计原则：`src/01-principles/proximity.zh-CN.md`、`src/01-principles/alignment.zh-CN.md`、`src/01-principles/contrast.zh-CN.md`、`src/01-principles/repetition.zh-CN.md`、`src/01-principles/direct.zh-CN.md`、`src/01-principles/lightweight.zh-CN.md`、`src/01-principles/stay.zh-CN.md`、`src/01-principles/invitation.zh-CN.md`、`src/01-principles/transition.zh-CN.md`、`src/01-principles/reaction.zh-CN.md`
- 表单和录入：`src/05-scenarios/research-form.zh-CN.md`、`src/03-ui-rules/data-entry.zh-CN.md`、`src/03-ui-rules/buttons.zh-CN.md`、`src/03-ui-rules/copywriting.zh-CN.md`、`src/03-ui-rules/feedback.zh-CN.md`
- 列表和数据：`src/05-scenarios/research-list.zh-CN.md`、`src/03-ui-rules/data-list.zh-CN.md`、`src/03-ui-rules/data-display.zh-CN.md`、`src/03-ui-rules/data-format.zh-CN.md`、`src/03-ui-rules/navigation.zh-CN.md`
- 详情和结果：`src/04-page-templates/detail-page.zh-CN.md`、`src/05-scenarios/research-result.zh-CN.md`、`src/05-scenarios/research-empty.zh-CN.md`、`src/05-scenarios/research-exception.zh-CN.md`、`src/05-scenarios/research-message-and-feedback.zh-CN.md`
- 看板和可视化：`src/04-page-templates/visualization-page.zh-CN.md`、`src/02-foundation/visual.zh-CN.md`、`src/05-scenarios/research-overview.zh-CN.md`、`src/05-scenarios/research-workbench.zh-CN.md`
- 索引和背景：根目录的 `index.md`、`src/00-context/overview.zh-CN.md`、`src/00-context/values.zh-CN.md`
- 组件库适配：`src/06-adapters/component-role-map.md`，以及对应的 `ant-design.md`、`element-ui.md`、`element-plus.md`、`flutter-material.md`

当本地设计文档与已安装组件库 API 不一致时，使用项目真实代码和版本作为实现依据，同时单独说明设计文档中的规则。

## 官方跨库参考

当组件名称、API、版本或 Material 行为不确定时，优先查阅官方文档：

- Ant Design 设计模式概览：https://ant.design/docs/spec/overview/
- Ant Design 组件概览：https://ant.design/components/overview/
- Element Plus 设计原则：https://element-plus.org/en-US/guide/design.html
- Element Plus 组件概览：https://element-plus.org/en-US/component/overview
- Flutter Material 组件目录：https://docs.flutter.dev/ui/widgets/material
- Flutter Material Dart API：https://api.flutter.dev/flutter/material/index.html

不要因为外部参考文档存在某个组件，就擅自更换项目组件库或新增依赖；这类变化必须获得用户确认。
