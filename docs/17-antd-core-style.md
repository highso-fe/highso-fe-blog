Ant Design 基础样式（Base less）
===

> 2017-10-11 发布，最后更新于 2017-10-11

## 重要

1. 通配符全标签范围使用 CSS怪异盒模型（`border-box`）
2. 各元素行高是它本身字号大小的 1.5 倍
3. 基础布局使用 `em` 作单位，允许弹性伸缩布局的设定，基准字号12px
4. 字体使用 `"Helvetica Neue For Number", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", "Helvetica Neue", Helvetica, Arial, sans-serif`
5. 文字颜色 `rgba(0, 0, 0, 0.65)`
6. 标题 h1~5 加粗，`font-weight: 500`
7. 超链接（`a 标签`）颜色 `108ee9`；点击时 0.3S 渐隐渐现动画；获取焦点状态存在下划线；`hover` 状态颜色 `#49a9ee`；`active` 状态颜色 `#0e77ca`
8. 使用的 CSS Normalize v7

## 其他

1. 数字字体做了自定制，使用 Helvetica Neue For Number。http://stackoverflow.com/a/13611748/3040605
2. 当用户点击 IOS 的 Safari 中的链接或 JavaScript 的可点击的元素时，覆盖显示的高亮颜色
3. 表单元素可语义化标签的样式重置

附：Ant 协助进行页面级整体布局：https://ant.design/components/layout-cn/
