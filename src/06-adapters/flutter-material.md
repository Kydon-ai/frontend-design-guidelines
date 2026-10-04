# Flutter Material 适配

Flutter Material 不是 Web 组件库的逐名翻译。Agent 应先把页面拆成 Material 的交互角色，再选择 Widget，并根据设备宽度、触控目标和平台导航习惯调整布局。

## 常见模块映射

| 页面模块 | 优先 Widget | 组合建议 |
| --- | --- | --- |
| 页面框架 | `Scaffold`、`AppBar`、`NavigationBar`、`NavigationRail` | 先确定移动端底部导航还是宽屏侧边导航，再组织内容区。 |
| 布局与间距 | `Row`、`Column`、`Wrap`、`Expanded`、`Flexible`、`Padding`、`LayoutBuilder` | 用约束和响应式断点表达关系，避免固定像素堆叠导致窄屏溢出。 |
| 导航 | `NavigationBar`、`NavigationRail`、`TabBar`、`TabBarView`、`Stepper` | 全局导航、同级切换和分步流程保持语义区分。 |
| 输入 | `Form`、`TextFormField`、`DropdownButtonFormField`、`Checkbox`、`Radio`、`Switch` | 表单状态、校验信息和键盘行为需要一起设计。 |
| 数据展示 | `Card`、`ListView`、`ListTile`、`DataTable`、`Chip`、`Badge` | 列表项提供明确的点击反馈；数据表格要考虑横向滚动和小屏替代方案。 |
| Overlay | `AlertDialog`、`Dialog`、`showModalBottomSheet`、`Tooltip` | 移动端优先考虑底部操作面板和触控面积，慎用悬停语义。 |
| Feedback | `SnackBar`、`MaterialBanner`、`CircularProgressIndicator`、`LinearProgressIndicator`、`showDatePicker` | SnackBar 适合短反馈，Banner 适合持续提示，阻断任务使用 Dialog。 |

## 跨端检查

- 8 基数是间距的起点，不等于每一行必须排列 8 个组件。
- 触控目标、系统返回、键盘遮挡、横竖屏和无障碍语义要纳入页面验收。
- 颜色和字体可以沿用项目设计变量，但 Material 的 elevation、surface 和状态层需要单独校准。

官方组件资料：[Flutter Material component widgets](https://docs.flutter.dev/ui/widgets/material)。
