第三方库 选型对比
===

> 2017-05-31 发布，最后更新于 2017-05-31

## 前端模板引擎

#### Handlebars.js

* [GitHub](https://github.com/wycats/handlebars.js)
* [Official Handlebars docs site](http://handlebarsjs.com/)
* [Live demo](http://tryhandlebarsjs.com/)
* [Release Notes](https://github.com/wycats/handlebars.js/blob/master/release-notes.md)

Handlebars provides the power necessary to let you build semantic templates effectively with no frustration. Handlebars is largely compatible with Mustache templates. In most cases it is possible to swap out Mustache with Handlebars and continue using your current templates.

###### 兼容性:

* Node.js
* Chrome
* Firefox
* Safari 5+
* Opera 11+
* IE 6+

###### 体积:

[handlebars-4.0.10.min.js](https://cdnjs.cloudflare.com/ajax/libs/handlebars.js/4.0.10/handlebars.min.js): 78kb

#### art-template

* [GitHub](https://github.com/aui/art-template)
* [Docs](https://aui.github.io/art-template/)
* [art-template@4 新特性介绍](https://github.com/aui/art-template/issues/369)

art-template 是一个渲染性能出众模板引擎，无论在 NodeJS 还是在浏览器中都可以运行。

###### 兼容性:

* Node.js 1+
* IE8+ (IE8 需要 [es5-shim](https://github.com/es-shims/es5-shim))

###### 功能点:

* 调试友好：语法、运行时错误日志精确到模板所在行；支持支持在模板文件上打断点（Webpack Loader）
* 支持压缩输出页面中的 HTML、CSS、JS 代码
* 支持 Express、Koa、Webpack
* 支持模板继承与子模板
* 兼容 EJS、Underscore、LoDash 模板语法
* 模板编译后的代码支持在严格模式下运行
* 支持 JavaScript 语句与模板语法混合书写
* 支持自定义模板的语法解析规则

###### 体积:

[art-template-4.9.1.min.js](https://raw.githubusercontent.com/aui/art-template/master/lib/template-web.js): 16kb

#### 对比

|Lib|兼容性|渲染性能|功能性|文件体积|社区成熟度|
|:----:|----|----|----|----|----|
|handlebars-4.0.10|IE6+|★★★★|★★★|78kb|Star 12k|
|art-template-4.9.1|IE8+|★★★★★|★★★★★|16kb|Star 5k|
