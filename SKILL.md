---
name: frontend-design-spec
description: 当 Web、移动端或桌面客户端的任务涉及页面、组件、布局、样式、交互、响应式或视觉规范时使用。也适用于 OpenSpec apply-change、Spec Kit implement 等实现阶段的 UI 任务。负责读取、创建或更新 .design-spec/，并根据项目真实技术栈完成前端 UI 设计与实现。仅后端或与 UI 无关的任务不要使用。
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

## 三种 SOP 与调用分流

本 Skill 统一通过 `$frontend-design-spec` 调用。调用后先做只读判断，不要直接把所有请求都当成页面开发任务。根据用户意图选择以下一种 SOP：

如果用户只调用 `$frontend-design-spec`，没有附带具体任务，不要扫描后直接写入项目；只询问用户本次要“创建规范、更新规范，还是开发 UI”，然后等待选择。

| 用户意图 | 典型表达 | 执行 SOP |
|---|---|---|
| 创建规范 | “创建 `.design-spec`”“初始化设计规范”“给这个项目配置一套 UI 规范” | SOP A：创建 `.design-spec/` |
| 更新规范 | “把主色改成极客蓝”“布局改成左右”“更新设计 Token”“组件库改成 Element Plus” | SOP B：更新 `.design-spec/` |
| 开发 UI | “开发一个列表页”“修改登录页样式”“新增一个移动端表单页面” | SOP C：根据自然语言需求开发 UI |

如果用户一次需求同时包含多个意图，严格按以下顺序处理：

1. 先执行 SOP A，确保 `.design-spec/` 存在并完成必要的用户确认；
2. 再执行 SOP B，写入用户明确要求更新的配置；
3. 最后执行 SOP C，使用最终配置完成页面设计或代码实现。

不要因为 SOP C 中推断出了某个新颜色、布局或组件库，就自动反向修改 `.design-spec/`。推断值只能标记为 `inferred`，只有用户确认后才能进入 SOP B。

### SOP A：创建 `.design-spec/`

#### 适用条件

- 用户明确要求创建或初始化 `.design-spec/`；
- 执行 SOP C 时发现项目根目录没有 `.design-spec/`；
- 执行 SOP B 时发现没有可更新的规范主文件。

#### 执行步骤

1. 读取项目根目录，确认 `.design-spec/` 是否不存在；同时只读检查 `package.json`、`pnpm-lock.yaml`、`yarn.lock`、`pubspec.yaml`、现有主题文件和组件封装，以便识别框架、组件库和版本。
2. 不创建空目录、不创建默认配置，也不要先开始页面开发。先向用户发送“基础配置填写模板”，并明确要求用户复制、填写后反馈。
3. 等待用户反馈后，逐项校验所有必填项。缺失、格式错误、选项不在候选范围、只写“默认”但未明确接受默认值、或确认项不是“是”，都不能进入创建阶段。
4. 如果反馈不完整或不符合要求，只回复未通过的字段、原因和可直接复制的修正模板；继续等待用户反馈。这个循环可以重复多次，直到所有必填项有效且用户明确确认。
5. 只有在校验通过并收到“我确认以上配置无误，可以创建 `.design-spec/`：是”后，才创建 `.design-spec/` 和 `.design-spec/design-spec.yaml`。目录和主文件必须在同一次操作中创建，不能只创建一个空目录。
6. 写入后重新读取并校验 YAML，向用户回报实际生效配置；如果本次请求还包含页面开发，再继续 SOP C，否则在创建 SOP 完成处停止。

#### SOP A：发给用户的可复制填写模板

首次进入 SOP A 时，读取 `src/templates/design-spec-init.md`，将其 Markdown 内容原样返回给用户，并放在一个 `md` 代码块中，方便用户整体复制。不要只返回文件路径、摘要或改写后的问卷。

可以根据代码库预检测结果预填“组件库”和“版本”，但预填内容必须标记为“待用户确认”，不能当作已确认值。基础色、中性色、字体和布局必须由用户明确填写；候选列表中的“推荐”或“默认”不代表已经选择。

模板文件缺失时，才可以在回复中临时重建同等字段的 Markdown 模板；字段和校验规则必须与本节及 `src/templates/design-spec-init.md` 保持一致。

#### SOP A：反馈校验规则

- 主色必须且只能有一个；必须来自候选列表。选择“法式洋红”时，必须同时提供合法的 Hex 值。
- 辅助色可以为空；如果填写，必须来自候选列表，并记录名称和 Hex。
- 中性色只能是“黑”“白”“灰”。“灰”是推荐默认值，但用户必须明确填写“灰”或“灰（接受默认）”，不能由 Agent 擅自代填。
- 字体必须填写“默认字体组合（接受默认）”或一组非空的自定义字体栈。只写“默认”或留空都视为未确认。
- 布局只能是“上下”“左右”“网格”。内部值分别写为 `vertical`、`horizontal`、`grid`；网格基数固定为 8，不代表一行排列 8 个组件。
- 组件库可以由用户明确指定，也可以明确授权“由 Agent 根据项目检测”；Agent 检测出的名称和版本仍要回显给用户确认。
- 功能色是固定值，不需要用户填写或选择；默认字体组合是候选值，但必须由用户显式接受。
- 最终确认项必须是“是”。填写“否”“待确认”“稍后确认”或缺失确认项，都不能创建目录。

#### SOP A：不合格反馈的固定处理格式

如果用户反馈不合格，使用以下结构，不得继续执行 SOP C：

```text
当前还不能创建 .design-spec/，因为以下字段未通过：
1. <字段>：<缺失或错误原因>
2. <字段>：<缺失或错误原因>

请只修正以下模板后重新发回：
<保留已通过字段，只保留待修正字段和确认项>
```

每轮只追问缺失或不合格字段，已通过字段不得要求用户重复填写。直到全部字段通过且确认项为“是”，才允许写入文件。

#### SOP A 的写入规则

- 不覆盖已存在的 `.design-spec/`；如果目录刚刚被其他流程创建，先重新读取再决定是否继续。
- 未确认的项目特定值只能保留在对话中的待确认状态，不能写入 `design-spec.yaml`；不要用 `auto-detect` 或 Agent 猜测值绕过用户确认。
- 功能色使用本 Skill 规定的固定值；默认字体只能在用户明确填写“接受默认”后写入。
- 创建完成的最低验收条件是：用户填写模板通过校验、确认项为“是”、目录存在、`design-spec.yaml` 存在、YAML 可解析、用户选择被原样保留。

### SOP B：更新 `.design-spec/`

#### 适用条件

- 用户明确要求修改颜色、字体、布局、组件库、网格或其他全局设计变量；
- 用户要求把当前项目规范同步到新的设计决策；
- 用户在开发 UI 前确认了新的全局规则。

#### 执行步骤

1. 读取 `.design-spec/`，优先读取 `design-spec.yaml`；如果主文件不存在但目录内有其他明确规范文件，先读取并沿用，不要悄悄创建第二套主文件。
2. 将用户自然语言转换为字段级变更。例如“主色改成极客蓝”对应 `color.base.primary_name` 和 `color.base.primary_hex`；“使用网格布局”对应 `layout.mode: grid`、`layout.grid.enabled: true`、`layout.grid.base: 8`。
3. 检查变更是否合法：颜色名称和 Hex 是否一致、布局模式是否为 `vertical`/`horizontal`/`grid`、网格基数是否为 8、组件库版本是否能在项目中找到。
4. 先向用户展示“当前值 → 新值”的变更摘要。用户只要求查看或评估时，不写文件；用户明确要求更新时，可以直接执行，但涉及覆盖已有配置或存在歧义时必须先确认。
5. 只修改用户指定的字段，保留其他字段、注释约定和项目已有值；不要把缺失字段批量重置为默认值。
6. 写入 `.design-spec/design-spec.yaml` 后重新读取并校验，回报实际变更和未变更字段。
7. 如果用户同时要求开发页面，更新成功后转入 SOP C；如果只要求更新规范，则在回报变更后停止。

#### SOP B 的安全边界

- 不因某次页面实现中的临时样式而修改全局配置。
- 不把 `inferred` 或 `default` 自动升级为 `confirmed`。
- 不删除用户未提及的色板、字体、布局或组件库配置。
- 如果 YAML 损坏、存在多个冲突主文件或无法确定字段含义，先报告冲突并停止写入。
- 更新完成后必须展示变更前后对比，不能只回复“已更新”。

### SOP C：根据自然语言需求开发 UI

#### 适用条件

- 用户要求新增、修改、重构、换肤或实现页面 UI；
- 用户用页面目标、业务流程或视觉描述提出需求，而没有直接指定组件。

#### 执行步骤

1. 读取 `.design-spec/`。如果不存在，立即转入 SOP A 并暂停页面分析与编码，直到用户填写模板、反馈通过、确认项为“是”且配置创建完成；如果存在但缺少影响当前页面的字段，再执行最小范围的 SOP B 询问。
2. 检查项目真实技术栈：框架、组件库、版本、主题 Provider、设计 Token、现有页面和业务组件封装。不得仅凭用户提到的组件名假设项目依赖。
3. 从自然语言中提取：用户目标、主要任务、目标平台/视口、页面入口、数据来源、操作结果和异常情况。
4. 按 ETC 拆解为：
   - E：用户要完成的业务能力或用户旅程；
   - T：页面类型或页面模板；
   - C：每个页面模块的语义组件角色和项目具体组件。
5. 判断页面类型和模块，按 `src/manifest.yaml` 选择最相关的设计文档、页面模板、UI 规则和组件库适配资料，不要一次性读取全部文档。
6. 在修改代码前输出简短决策摘要，至少包含当前配置、页面类型及理由、受影响模块、语义角色、具体组件、状态覆盖和未决问题。
7. 如果用户要设计方案，只输出结构、层级、组件、状态、交互和文案建议，不修改业务代码。
8. 如果用户要代码实现，按项目现有框架和组件库 API 做最小范围修改；同时补齐正常、加载、空数据、错误、禁用、无权限和响应式状态中与当前需求相关的部分。
9. 运行与本次改动最相关的检查或构建，必要时提供页面验收要点。不要因为视觉改动而顺手重构无关业务逻辑。
10. 如果实现过程中发现需要改变全局色彩、字体、布局或组件库，暂停实现，转入 SOP B 请求用户确认；不要隐式更新 `.design-spec/`。

#### SOP C 的完成条件

- 页面类型、模块和组件选择有明确理由；
- 组件来自项目真实依赖或已有业务封装；
- 当前 `.design-spec/` 规则已被实际应用；
- 相关交互状态和响应式行为已处理；
- 代码检查或构建结果已回报；
- 未将临时推断写入全局设计规范。

## 共享规则与配置基线

### 1. 读取和优先级

在做任何 UI 决策前，先检查项目根目录下的 `.design-spec/`。

- 如果 `.design-spec/` 存在，读取其中与当前任务相关的文件，并将已确认的项目配置视为最高优先级。
- 如果存在 `.design-spec/design-spec.yaml`，将它作为规范主文件。
- 如果目录中已有其他明确的规范主文件，先读取它，不要悄悄创建另一份互相竞争的配置。
- 如果 `.design-spec/` 已存在但某些配置缺失，只询问会影响当前 UI 改动的字段；如果目录不存在，必须完整执行 SOP A，不能用默认值跳过基础配置确认。
- 不要覆盖已有设计规范。如果已有值与本 Skill 默认值冲突，应保留项目值并向用户说明冲突。
- 在给出具体组件建议或代码前，还要检查项目真实使用的框架、组件库、版本、主题 Provider、设计 Token 和业务组件封装。

### 2. SOP A 的配置基线

SOP A 使用一次集中式确认完成全局配置，不要让用户逐个配置所有设计 Token。以下字段是创建主配置时的基线：

需要用户选择：

1. 一个必选的主基础色，也可以额外选择辅助基础色；
2. 一个中性色系：黑、白或灰；灰只是推荐候选，必须由用户明确填写并接受；
3. 字体：明确接受默认字体组合，或提供自定义字体栈；
4. 布局模式：上下、左右或网格；选择网格时，网格基数固定为 8；
5. 组件库：明确指定名称和版本，或明确授权 Agent 根据项目检测。

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

功能色固定，不需要用户选择；字体虽然提供默认组合，但创建时必须让用户明确选择“默认字体组合（接受默认）”或填写自定义字体栈。功能色固定为：

- 成功：`#52c41a`
- 失败：`#ff4d4f`
- 警告：`#faad14`
- 通知：`#1890ff`

可供用户明确接受的默认字体组合为：

```css
-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial,
'Noto Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol',
'Noto Color Emoji'
```

默认间距网格基数为 8。用户选择上下或左右时，仍然使用 8 作为间距基准；用户选择网格时，记录 `layout.mode: grid` 和 `layout.grid.base: 8`，不要擅自替换成其他布局模式。

用户填写模板并确认后，创建 `.design-spec/design-spec.yaml`。下面只是结构模板，不是可以直接写入的默认配置；写入前必须将所有尖括号占位符替换为已通过校验的用户选择。保留用户选择的值；未获用户授权的项目特定值不能写入。

```yaml
version: 1
source: user-confirmed
component_library:
  name: "<用户确认的组件库名称或 auto-detect>"
  version: "<用户确认的版本或 auto-detect>"
color:
  base:
    primary_name: "<用户确认的主色名称>"
    primary_hex: "<用户确认的主色 Hex>"
    secondary: []
  neutral_family: "<black|white|gray>"
  functional:
    success: "#52c41a"
    error: "#ff4d4f"
    warning: "#faad14"
    info: "#1890ff"
typography:
  font_family: "<用户确认的默认字体组合或自定义字体栈>"
layout:
  mode: "<vertical|horizontal|grid>"
  grid:
    enabled: true # 启用 8 基数间距/尺寸约束，不代表一行 8 列
    base: 8
```

创建文件后，向用户展示解析后的配置，再继续处理当前 UI 需求。如果用户尚未完成模板填写或确认选择，不要提前创建 `.design-spec/`。

### 3. 维护简洁的决策状态

每个相关配置项都要记录来源：

- `confirmed`：用户或已有项目规范明确确认；
- `inferred`：根据代码库或需求推断，但仍可修改；
- `default`：Skill 提供的候选默认值，只能在用户明确接受后写入，不能代替用户确认；
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

## SOP C 的 UI 改动决策细则

SOP C 的页面分析和实现阶段，按以下顺序执行：

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

每次执行先明确输出当前模式：`SOP A（创建规范）`、`SOP B（更新规范）` 或 `SOP C（开发 UI）`。

- SOP A：输出待确认配置、字段来源和创建后的实际配置；
- SOP B：输出配置变更前后对比、校验结果和未变更字段；
- SOP C：实现前输出简短的页面决策摘要，包含：

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
