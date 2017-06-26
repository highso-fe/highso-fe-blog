Web 前端分享 第一期
===

> 2017-06-16 发布，最后更新于 2017-06-26

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

###### 有哪些需要兼容、适配？

* 对语言标准 API 的兼容，包括 HTML 标签，CSS 2/3，[Web API](https://developer.mozilla.org/zh-CN/docs/Web/API) - SVG Canvas 本地存储 DOM节点控制等, JS API 等。措施：往往需要引入兼容库或更换实现方案
* 对特定浏览器的兼容方案，Eg. 360安全浏览器、移动端微信 X5 浏览器、Safari 300ms click 等
* PC Web、移动 Web 甚至 Web 跨平台（React Native / PhoneGap）对不同设备屏幕展示宽度、高度尺寸的适配
* Retina 适配，2倍、3倍图
* 响应式布局适配（CSS Media Query）

###### 如何兼容、适配？

* 查询相关 API 在不同设备浏览器的兼容情况，并合理使用
* 使用兼容性良好的解决方案，或适度引入一些兼容库
* 去浏览器厂商提供的官网、论坛、技术支持板块、浏览器最新公告等处寻求信息
* 协同产品、设计沟通设备适配方案，帮助他们用代码实现的角度去观察问题
* 对各浏览器、设备的未来生产趋势做了解

#### 5. 谨慎地使用第三方库

###### 引入原则

* 实现功能不要产生依赖第三方库的心理，一些复杂功能通过分析，往往是可以简洁高效解决的
* 评判第三方库是否适用，更多的是对比我们项目本身，而不是他的名气
* 当解决一个实际技术问题时，与其应用一整套技术栈，不如仅引入技术栈中的核心库；与其引入一个库，不如引入核心代码块；这样我们项目的编码会更加可控，遇问题时也可以快速定位。当我们的项目与某个技术栈或库绝大面积契合的时候，我们才推荐使用他们
* 第三方库之间会存在依赖关系，这时往往要注意依赖版本的区分

###### 如何评审一个第三方库的项目适用性

* 文件体积
* 浏览器兼容性
* 社区活跃度
* API 文档是否齐全
* 学习曲线陡峭性：语言标准、设计概念、编程思想、API、是否中文文档
* 对于项目的功能覆盖率
* 引入后对于其他库的兼容
* 是否存在断崖式升级（Eg.Angular）
* 未来开发趋势（Eg.Swiper2与3）

#### 6.边界情况的考虑

Eg：

* 图文排版 不同内容量、内容类型时的展现情况
* 设备屏幕宽度、高度缩放后界面的呈现
* 接口异常的客户端处理
* 表单验证客户端处理
* DOM 操作大幅增加后的渲染效率
* 图片、Canvas、Flash 或其他 Web API 等无法使用时的处理

解决思路：找到边界限制点，逐一突破

## （四）优秀的开发辅助工具

相比大而全的 IDE，个人更倾向于使用多个小巧灵活、专职负责某个方面的工具进行配合。前端涉及的开发工具很多，编辑器、命令行、设计工具、不同浏览器、版本控制客户端、各种工具网站等 都会使用用到

#### 文本编辑器

###### Sublime Text 3

[http://www.sublimetext.com/](http://www.sublimetext.com/)

界面简洁清新，拥有丰富的前端编码辅助集成插件，高度定制化，运行速度优秀

[Sublime Text 3 配置推荐](https://github.com/highso-fe/highso-fe-blog/issues/4)

###### ATOM

[https://atom.io/](https://atom.io/)

ATOM 与 Sublime Text 功能覆盖很相似，选择 ATOM，往往是因为有这个狂拽富帅吊炸天的插件：[Activate Power Mode](https://github.com/JoelBesada/activate-power-mode)

###### WebStorm

[https://www.jetbrains.com/webstorm/](https://www.jetbrains.com/webstorm/)

Powerful IDE for the modern JavaScript development。WebStorm 为前端而生，专门为 JS 开发做了很多优化，有许多令前端工程师眼前一亮的地方

优势功能：

* 图片宽高提示
* HTML、CSS、JS 重构：HTML标签的快速替换、快捷地更改文件引用、变量引用
* 对业界最新技术的支持：Sass、NodeJS、CoffeScript、Jade、Emmet，甚至可以管理 NPM 包！
* 高度定制化的代码格式规则
* 本地版本控制
* 与 Redmine / Trello / Jira 等集成
* 文件结构分析

缺点：

* 常驻内存
* 启动慢，启动时间与项目大小相关（某人说 IDE 的正确打开方式是上班启动之，下班关闭之。更有甚者说是入职启动之，辞职关闭之。你们感受一下）

#### 其他工具

* 浏览器调试工具
* Git、SVN 客户端
* 取色工具
* 雪碧图生成工具（gulp spritesmith）
* 本地服务（MAMP，Webpack-dev-server，NodeJS）
* 命令行工具（Iterm）
* 图片压缩导出（PS、[tinypng](https://tinypng.com/)）
* 正则匹配（[regexr.com](http://regexr.com/)）
* [jsfiddle](https://jsfiddle.net/)
* [babel 在线实验](http://babeljs.cn/repl/)
* 翻墙 Google

##（五）优秀的线上资源

#### 语言标准

* [w3c standards](https://www.w3.org/standards/)
* [HTML standard](https://html.spec.whatwg.org/multipage/)
* [CSS current work](https://www.w3.org/Style/CSS/current-work)
* [ECMAScript® 2016 Language Specification](http://ecma-international.org/ecma-262/7.0/#sec-ecmascript-language-lexical-grammar)

#### API 查询

* [Mozilla developer network](https://developer.mozilla.org/zh-CN/)
* [CSS 参考手册](http://www.css88.com/book/css/)
* [jQuery API 参考文档](http://jquery.cuishifeng.cn/index.html)

#### 兼容性查询

* [caniuse](http://caniuse.com/#)
* [statcounter.com](http://gs.statcounter.com/)
* [html5test](https://html5test.com/)

#### 寻找优秀的开源库

* [Github](https://github.com/)
* [npm](https://www.npmjs.com/)
* [gulp plugins](http://gulpjs.com/plugins/)
* [grunt plugins](http://www.gruntjs.net/plugins)

#### QA 社区

* [StackOverflow](https://stackoverflow.com/questions/41612918/can-react-native-navigator-deal-with-this-condition)
* [segmentfault](https://segmentfault.com/)

#### 嗨学网前端 Blog

[Highso-FE](https://github.com/highso-fe)
