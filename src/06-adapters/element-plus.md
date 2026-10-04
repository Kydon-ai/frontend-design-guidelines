# Element Plus 适配

Element Plus 主要服务于 Vue 3 项目。使用时优先采用 `el-*` 组件和项目已有的 composable/二次封装，并把全局色彩、尺寸、圆角和状态变量收敛到主题变量中。

## 常见模块映射

| 页面模块 | 优先组件 | 组合建议 |
| --- | --- | --- |
| 页面框架 | `el-container`、`el-row`、`el-col`、`el-space`、`el-divider` | 结构布局用 Container/Grid，局部节奏用 Space，不要用大量空 `div` 撑间距。 |
| 导航 | `el-menu`、`el-breadcrumb`、`el-tabs`、`el-steps`、`el-pagination` | 根据页面层级选择导航；分页与筛选区保持明确的视觉分组。 |
| 数据录入 | `el-form`、`el-input`、`el-select`、`el-date-picker`、`el-upload` | 长表单考虑分组或步骤；错误信息要在字段附近可见。 |
| 数据展示 | `el-table`、`el-card`、`el-descriptions`、`el-statistic`、`el-tag`、`el-empty` | 统计值突出数值与单位，状态表达使用 Tag/Badge，不要只依赖颜色。 |
| 反馈与浮层 | `el-alert`、`ElMessage`、`ElNotification`、`el-dialog`、`el-drawer`、`el-popover`、`el-tooltip`、`el-progress` | 按阻断程度选择反馈；异步操作同时提供 loading 和结果反馈。 |

## Vue 3 实现检查

- 先确认组件是否已经被项目统一注册，避免重复注册或引入方式不一致。
- 事件、插槽、`v-model` 和类型写法以项目当前 Element Plus 版本为准。
- 不要通过深度覆盖组件内部 DOM 解决设计问题；优先使用主题变量、组件属性和外层布局。
- 对表格、抽屉、弹窗和表单验证补齐空态、加载态、错误态和窄屏行为。

官方组件总览：[Element Plus Components](https://element-plus.org/zh-CN/component/button.html)。
