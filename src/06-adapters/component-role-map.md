# 组件语义角色映射

组件库的名称和 API 可以不同，但页面中承担的语义角色相对稳定。Agent 不应先从组件名出发，而应先确认“用户要完成什么动作、理解什么信息、获得什么反馈”，再选择对应库的组件。

## 角色层

| 语义角色 | 典型职责 | 常见页面模块 |
| --- | --- | --- |
| Layout | 组织页面区域、列、行、间距和响应式关系 | 页面框架、工作台、仪表盘 |
| Navigation | 在层级、页面、步骤或分页之间移动 | 顶部导航、侧边栏、面包屑、标签页 |
| Action | 触发提交、保存、删除、刷新或次要操作 | 工具栏、表单底部、卡片操作区 |
| Input | 采集、选择、筛选和上传信息 | 查询区、表单、设置页 |
| Display | 展示文本、状态、统计、记录和结构化数据 | 卡片、详情、列表、表格、图表 |
| Overlay | 在当前上下文中临时承载确认、补充信息或编辑 | 对话框、抽屉、气泡、浮层 |
| Feedback | 告知系统状态、操作结果、进度和异常 | 加载、成功、失败、警告、空状态 |

## 选择规则

1. 先按页面类型确定模块，再在模块内确定语义角色。
2. 同一个角色优先保持同一种组件表达；不要仅因为视觉偏好替换语义。
3. 需要用户确认时使用阻断式 Overlay；只需告知结果时使用非阻断式 Feedback。
4. 组件库没有一对一组件时，组合基础组件，并保留相同的角色、状态和键盘/触控行为。
5. 组件名、尺寸和颜色都要服从项目的 `.design-spec/`，不能直接照搬库的默认主题。

## 跨库速查

| 角色 | Ant Design | Element UI / Element Plus | Flutter Material |
| --- | --- | --- | --- |
| Layout | `Layout`、`Row`、`Col`、`Space`、`Flex` | `el-container`、`el-row`、`el-col`、`el-space` | `Scaffold`、`Row`、`Column`、`Wrap`、`Expanded`、`Padding` |
| Navigation | `Menu`、`Breadcrumb`、`Tabs`、`Steps`、`Pagination` | `el-menu`、`el-breadcrumb`、`el-tabs`、`el-steps`、`el-pagination` | `NavigationBar`、`NavigationRail`、`TabBar`/`TabBarView`、`Stepper` |
| Action | `Button`、`Dropdown`、`Popconfirm` | `el-button`、`el-dropdown`、`el-popconfirm` | `FilledButton`、`OutlinedButton`、`TextButton`、`IconButton` |
| Input | `Form`、`Input`、`Select`、`DatePicker`、`Upload` | `el-form`、`el-input`、`el-select`、`el-date-picker`、`el-upload` | `Form`、`TextFormField`、`DropdownButton`、`showDatePicker` |
| Display | `Card`、`Table`、`Descriptions`、`Statistic`、`Tag`、`Empty` | `el-card`、`el-table`、`el-descriptions`、`el-statistic`、`el-tag`、`el-empty` | `Card`、`DataTable`、`ListTile`、`Chip`、`Badge`、`DataTable` |
| Overlay | `Modal`、`Drawer`、`Popover`、`Tooltip` | `el-dialog`、`el-drawer`、`el-popover`、`el-tooltip` | `AlertDialog`、`Dialog`、`showModalBottomSheet`、`Tooltip` |
| Feedback | `Alert`、`Message`、`Notification`、`Progress`、`Spin`、`Result` | `el-alert`、`ElMessage`、`ElNotification`、`el-progress`、`v-loading`、`el-result` | `SnackBar`、`MaterialBanner`、`CircularProgressIndicator`、`LinearProgressIndicator` |

具体属性、插槽、事件和版本差异，继续读取对应库的适配文档；本表只用于第一轮角色判断。
