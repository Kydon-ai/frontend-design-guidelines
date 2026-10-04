# Ant Design 适配

Ant Design 的组件分类适合直接对应页面模块：通用、布局、导航、数据录入、数据展示和反馈。实现时先按语义角色选组件，再用 `ConfigProvider`、主题 token 和项目 `.design-spec/` 统一颜色、尺寸、圆角、字体与间距。

## 常见模块映射

| 页面模块 | 优先组件 | 组合建议 |
| --- | --- | --- |
| 页面框架 | `Layout`、`Flex`、`Space` | 用 `Layout` 表达区域层级，用 `Flex`/`Space` 控制局部排列和间距。 |
| 顶部/侧边导航 | `Menu`、`Breadcrumb`、`Tabs` | 根据层级导航、当前位置和同级切换分别选择，不要用 Tabs 替代全局导航。 |
| 查询与表单 | `Form`、`Input`、`Select`、`DatePicker`、`Upload` | 查询条件和提交表单分开组织；复杂筛选可配合 `Collapse` 或 `Drawer`。 |
| 列表与表格 | `Table`、`List`、`Pagination`、`Tag` | 列表负责内容浏览，表格负责字段对齐和批量操作；状态用 `Tag` 或 `Badge`。 |
| 详情与指标 | `Descriptions`、`Card`、`Statistic`、`Timeline` | 先分组信息，再用 `Card` 或 `Divider` 建立层级，避免每个字段都做成卡片。 |
| 反馈与异常 | `Alert`、`Message`、`Notification`、`Modal`、`Result`、`Empty`、`Spin` | 根据是否阻断当前任务决定使用浮层、页面内反馈或结果页。 |

## Agent 实现检查

- 明确主操作和次操作，按钮顺序与页面阅读顺序一致。
- 表格、表单和弹窗的 loading、disabled、校验失败、空数据状态必须一并设计。
- 组件默认样式只作为实现起点，最终以项目 token 和 `.design-spec/` 为准。
- 需要跨端复用时，输出语义角色和状态说明，不要把 Ant Design API 当成业务契约。

官方组件总览：[Ant Design Components](https://ant.design/components/overview-cn/)。
