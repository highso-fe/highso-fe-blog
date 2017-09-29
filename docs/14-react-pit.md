React技术栈 踩坑贴
===

> 2017-09-29 发布，最后更新于 2017-09-29

记录技术实施过程中的一些神坑。

#### 预编译时 CSS 模块化将第三方包排除

使用 `babel-plugin-import` 按需加载 `Ant Design` 组件，因为我们配置使用了 CSS 模块化，它会将 Ant 的样式模块化前缀及哈希化处理，因此建议 CSS 模块化配置将 node_modules 目录文件 exclude 掉，不要让它们走 CSS Modules

可参考:

* [Stack overflow: CSS Modules: How do I disable local scope for a file?](https://stackoverflow.com/questions/35398733/css-modules-how-do-i-disable-local-scope-for-a-file)
* [GitHub Issues: ant-design 样式无法显示](https://github.com/ant-design/ant-design/issues/3442)
* [babel-plugin-import](https://github.com/ant-design/babel-plugin-import)
