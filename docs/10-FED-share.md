Web 前端分享 第一期
===

> 2017-06-16 发布，最后更新于 2017-06-16

## （一）前端领域包括什么？涉及哪些知识点？

* [可视化前端技能树](http://html5ify.com/fks/fks_chart/)
* [GitHub fks](https://github.com/JacksonTian/fks)

## （二）前端发展里程碑

1. 浏览器厂商大战，兼容性问题；设计糟糕的原生 DOM API；HTML Table 布局
2. JQuery 的横空出世：爽快的 DOM 操作、简洁的语法、华丽的链式 API、解决各种兼容性问题
3. 前端需要应用架构，光有 DOM 操作还不够，Backbone 出现，把 MVX 概念引入前端领域
4. Backbone 的视图层依然要手动侦听 model 的变化来做各种 DOM 操作，数据到视图的映射依然频繁。于是开始推崇 MVVM 数据绑定，Angular 火了（同时间段 ES6）
5. 自动化构建工具 Grunt、Gulp，打包工具：Webpack、模块化 Sea.js、Require.js
6. React 技术栈、Vue.js；函数式编程思想、数据流管理等等

对比到嗨学网前端所处的历史历程

## （三）前端编码意识

在思考如何规范且高效地具体编码前，我们往往先去思考“为什么这样编码，编码时应秉承什么原则”。

#### 1. 合理的目录结构及文件命名

我们往往需要为以下几点选择适用项目的目录结构：

* 与 NPM (Node 包管理工具) 的配合使用（package.json, node_modules）
* 与自动化构建工具的配合使用（gulpfile.js / webpack.config.js 等启动文件, .jshintrc / .eslintrc 等构建插件配置文件, src / dist / sprite 等文件预编译 IO 目录）
* 便于构建插件做路径处理（eg. spritesmith, CSS Modules）
* 与 Git 的集成（.gitignore, README.md）
* 与框架的整合（适用于 MV* 框架的构建目录, eg.React /component, /page, /action /reducer 等）
* 项目公有文件：组件、请求的控制汇总、路由汇总、公有样式相关、静态常量配置、可重用模板、公有函数封装、第三方库、移动 Web 端各种兼容适配方案（Rem、Retina适配）等

#### 2. HTML 标签语义化

###### 标签的语义

通过标签判断内容语义，例如根据 `<h1>` 判断出内容是标题，根据 `<p>` 判断内容是段落、`<input>` 是输入框等。H5语义化标签（业界没有形成统一使用规范、需要为了兼容引入 shim、区分 `<article>` 和 `<section>` 是个脑力活儿，所以暂不推荐）

###### 判断是否语义化

去掉样式，只看 HTML，网站依然有很强的可读性和良好的结构。

###### 为什么标签要语义化

1. 搜索引擎友好，SEO
2. 更容易让屏幕阅读器读出网页内容（可访问性）
3. 样式丢失时能让页面呈现清晰的结构（可访问性）
4. 便于开发团队的维护（可维护性）

ps: 推荐阅读 [《编写高质量代码》](https://book.douban.com/subject/4881987/)

> 本书的核心内容是围绕 Web 前端开发的三大技术要素 — HTML、CSS 和 JavaScript 来深入地探讨编写高质量代码的方法、技巧、规范和最佳实践，从而为编写易于维护的 Web 前端代码打下坚实的基础。

#### 3. 高效渲染且高可维护的 CSS

###### 高可维护

* 通过 class 前后缀避免命名冲突（[BEM](https://en.bem.info/)思想，Block 块、Element 元素、Modifier 修饰符，Eg. `live-chatItem--hover`），当然，还可以借助构建工具实现 CSS In JS，CSS 模块化(Eg. Webpack css loader)
* 功能性布局 和 面向属性的 CSS (Eg. [style.css](http://git.highso.com.cn:81/fe/official/blob/master/src/css/common/style.css))

###### 高效渲染

* 浏览器重置（Eg. [normalize.css](http://git.highso.com.cn:81/fe/official/blob/master/src/css/common/normalize.css)）
* 避免嵌套和无意义 Class (Eg. `.main ul li span input#address {...}`)

ps: 其他细节见 [嗨学网前端开发规范](https://github.com/highso-fe/highso-fe-blog/issues/3)

#### 4. 树立浏览器兼容、适配意识

###### 有哪些需要兼容？

* 对语言标准 API 的兼容，包括 HTML 标签，CSS 2/3，[Web API](https://developer.mozilla.org/zh-CN/docs/Web/API) - SVG Canvas 本地存储 DOM节点控制等, JS API 等。措施：往往需要引入兼容库或更换实现方案
* 对特定浏览器的兼容方案，Eg. 360安全浏览器、移动端微信 X5 浏览器、Safari 300ms click 等
* PC Web、移动 Web 甚至 Web 跨平台（React Native / PhoneGap）对不同设备屏幕展示宽度、高度尺寸的适配
* Retina 适配，2倍、3倍图
* 响应式布局适配（CSS Media Query）
