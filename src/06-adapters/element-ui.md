# Element UI 适配

Element UI 主要服务于 Vue 2 项目。若项目已经使用 Element UI，应沿用项目现有版本和封装层；不要在同一个页面无理由混用 Element Plus 或另一套组件库。

## 常见模块映射

| 页面模块 | 优先组件 | 组合建议 |
| --- | --- | --- |
| 页面框架 | `el-container`、`el-header`、`el-aside`、`el-main`、`el-row`、`el-col` | 先确定页面级容器，再用栅格表达列关系，间距由设计变量统一控制。 |
| 导航 | `el-menu`、`el-breadcrumb`、`el-tabs`、`el-steps`、`el-pagination` | 全局、局部、步骤和分页保持角色区分。 |
| 表单 | `el-form`、`el-input`、`el-select`、`el-date-picker`、`el-upload` | 使用 `el-form-item` 表达标签、控件和校验信息，不要用占位符代替标签。 |
| 数据展示 | `el-table`、`el-card`、`el-descriptions`、`el-tag`、`el-tree` | 表格操作列保持克制；详情字段按业务组分组。 |
| 反馈 | `el-alert`、`this.$message`、`this.$notify`、`el-dialog`、`el-drawer`、`el-loading`、`el-empty` | 区分页面内提示、全局提示、阻断确认和加载遮罩。 |

## 迁移注意

Element UI 与 Element Plus 的组件名相近，但安装方式、事件写法、类型和部分 API 不完全相同。Agent 应先确认项目是 Vue 2 + Element UI，还是 Vue 3 + Element Plus，再读取对应适配文档。

官方组件文档：[Element UI](https://element.eleme.cn/#/zh-CN/component/installation)。
