第三方库 选型对比
===

> 2017-05-31 发布，最后更新于 2017-06-01

## (一) 模板引擎

推荐使用兼容 IE8+、体积更小、功能覆盖广、渲染性能更加优越的 aui/art-template

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

[在线速度测试](https://aui.github.io/art-template/rendering-test/)

## （二）滚动与轮播插件

推荐 PC Web 端使用 fullPage.js 实现全屏滚动效果，移动 Web 端使用 Swiper3 实现全屏滚动及其他触摸滑动效果

#### fullPage.js

* [GitHub](https://github.com/alvarotrigo/fullPage.js)

A simple and easy to use libary to create fullscreen scrolling websites (also known as single page websites or onepage sites). It allows the creation of fullscreen scrolling websites, as well as adding some landscape sliders inside the sections of the site.

###### 兼容性

* IE8+
* Opera
* Safari
* Firefox
* Chrome

###### 依赖

* jQuery library. (1.6.0 minimum)
* jquery.fullPage.js
* jquery.fullPage.css

###### 功能点

* 全屏滚动封装
* 手机端、平板电脑、触摸屏设备上的浏览器的触摸操作
* 懒加载图片、音频视频文件
* 自动播放嵌入式媒体

#### Swiper3

* [GitHub](https://github.com/nolimits4web/Swiper)

Swiper - is the free and most modern mobile touch slider with hardware accelerated transitions and amazing native behavior. It is intended to be used in mobile websites, mobile web apps, and mobile native/hybrid apps. Designed mostly for iOS, but also works great on latest Android, Windows Phone 8 and modern Desktop browsers.

###### 兼容性

* Swiper 从 3.0 开始不再全面支持 PC 端。因此，如需在 PC 上兼容更多的浏览器，可以选择 [Swiper2.x](http://2.swiper.com.cn/)
* Swiper2 支持移动端的 Safari，Android 2.1+，windows Phone8, 以及 PC 端的 Chrome，Firefox，IE7-10 和 Opera

###### 依赖

* 可单独使用，也可以结合 jQuery, jQuery Mobile, Zepto 等

###### 功能点

* 定位：移动端触摸滑动插件
* progress，更细粒度控制切换特效
* 提供封装了的动画 API
* Flexbox 布局
* 硬件加速过渡（如果该设备支持的话）
