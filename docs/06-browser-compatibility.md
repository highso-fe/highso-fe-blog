PC 端浏览器兼容解决方案汇总
===

> 2017-03-25

## 浏览器对常用特性的支持情况

#### HTML

###### 1.语义化标签

[New semantic elements](http://caniuse.com/#search=html5): IE9+ 支持，包括 `<section>`、`<article>`、`<aside>`、`<header>`、`<footer>`、`<nav>`、`<figure>`、`<figcaption>`、`<time>`、`<mark>`、`<main>`

###### 2.placeholder

[input placeholder attribute](http://caniuse.com/#search=placeholder): IE10+ 支持

#### CSS 特性

###### 1.CSS3 Media Queries

IE9+ 支持，但不支持嵌套 media queries

[兼容性参考](http://caniuse.com/#search=media)

###### 2.CSS3 selectors

IE8 支持 [兄弟选择符(E~F)](http://www.css88.com/book/css/selectors/relationship/e-brother-f.htm) 和属性选择符: [E[att^="val"]](http://www.css88.com/book/css/selectors/attribute/att4.htm)、[E[att$="val"]](http://www.css88.com/book/css/selectors/attribute/att5.htm)、[E[att*="val"]](http://www.css88.com/book/css/selectors/attribute/att6.htm)

IE8 不支持 [E:root](http://www.css88.com/book/css/selectors/pseudo-classes/root.htm)、[E:nth-child(n)](http://www.css88.com/book/css/selectors/pseudo-classes/nth-child(n).htm)、[E:nth-last-child(n)](http://www.css88.com/book/css/selectors/pseudo-classes/nth-last-child(n).htm)、[E:nth-of-type(n)](http://www.css88.com/book/css/selectors/pseudo-classes/nth-of-type(n).htm)、[E:nth-last-of-type(n)](http://www.css88.com/book/css/selectors/pseudo-classes/nth-last-of-type(n).htm)、[E:last-child](http://www.css88.com/book/css/selectors/pseudo-classes/last-child.htm)、[E:first-of-type](http://www.css88.com/book/css/selectors/pseudo-classes/first-of-type.htm)、[E:last-of-type](http://www.css88.com/book/css/selectors/pseudo-classes/last-of-type.htm)、[E:only-child](http://www.css88.com/book/css/selectors/pseudo-classes/only-child.htm)、[E:only-of-type](http://www.css88.com/book/css/selectors/pseudo-classes/only-of-type.htm)、[E:empty](http://www.css88.com/book/css/selectors/pseudo-classes/empty.htm)、[E:target](http://www.css88.com/book/css/selectors/pseudo-classes/target.htm)、[E:enabled](http://www.css88.com/book/css/selectors/pseudo-classes/enabled.htm)、[E:disabled](http://www.css88.com/book/css/selectors/pseudo-classes/disabled.htm)、[E:checked](http://www.css88.com/book/css/selectors/pseudo-classes/checked.htm)、[E:not(s)](http://www.css88.com/book/css/selectors/pseudo-classes/not(s).htm)

以上 CSS3 选择器 IE9+ 均支持，[兼容性参考](http://caniuse.com/#search=CSS3%20selectors)

###### 3.Flexible Box Layout Module

Flex Box 布局 IE10+ 部分兼容并存在大量 Bug，[兼容性参考](http://caniuse.com/#search=Flexible%20Box%20Layout%20Module)

###### 4.CSS3 Colors

`hsl()` 以及在 `hsl()` 和 `rgba()` 中的 alpha-透明度 IE9+ 支持

###### 5.其他特性

* [CSS3 Border images](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image): IE11+ 支持，且需要打 -moz, -webkit, -o 标签, [兼容性参考](http://caniuse.com/#search=border-image)
* [CSS3 Border-radius](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-radius): IE9+ 支持，且需要打 -moz, -webkit 标签, [兼容性参考](http://caniuse.com/#search=border-radius)
* [CSS3 Box-shadow](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow): IE9+ 支持，且需要打 -moz, -webkit 标签, [兼容性参考](http://caniuse.com/#search=box-shadow)
* [Multiple background images](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-image): IE9+ 支持
* [CSS3 Background-image options](http://caniuse.com/#search=CSS3%20Background-image%20options): `background-clip`, `background-origin` 和 `background-size` IE9+ 支持
* [CSS Gradients](http://caniuse.com/#search=CSS%20Gradients): IE10+ 支持, 且需要打 -moz, -webkit, -o 标签, [兼容性参考](http://caniuse.com/#search=CSS%20Gradients)
* [CSS filter](https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter): IE 浏览器不支持且该属性是一个实验中的功能

#### Web API 接口

###### 1.EventTarget.addEventListener() 等事件监听 API

* Basic support: IE9+ 支持
* useCapture made optional: IE9+ 支持事件捕获技术，IE8 不具有任何替代 useCapture 的方法，仅支持时间冒泡阶段

对于 IE，IE9 之前必须使用 [attachEvent](http://msdn.microsoft.com/en-us/library/ms536343(VS.85).aspx) 而不是标准的 addEventListener，使用 attachEvent 方法有个缺点，this 的值会变成 window 对象的引用而不是触发事件的元素。

[兼容性参考](http://caniuse.com/#search=addEventListener)

同样的，[removeEventListener](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/removeEventListener)、[dispatchEvent](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/dispatchEvent) IE8 也不支持

###### 2.DOM Event 模型

* [eventTarget](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget)
* [event.timeStamp](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/timeStamp)
* [event.cancelable](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/cancelable)
* [event.bubbles](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/bubbles)
* [event.currentTarget](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/currentTarget)
* [event.preventDefault()](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)
* [event.stopPropagation()](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/stopPropagation)
* [event.stopImmediatePropagation()](https://developer.mozilla.org/zh-CN/docs/Web/API/Event/stopImmediatePropagation)

以上 API IE8 均不支持

###### 3.Node 接口

* [Node.textContent](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/textContent)
* [Element.firstElementChild](https://developer.mozilla.org/zh-CN/docs/Web/API/ParentNode/firstElementChild)
* [Element.lastElementChild](https://developer.mozilla.org/zh-CN/docs/Web/API/ParentNode/lastElementChild)
* [NonDocumentTypeChildNode.previousElementSibling](https://developer.mozilla.org/zh-CN/docs/Web/API/NonDocumentTypeChildNode/previousElementSibling)
* [NonDocumentTypeChildNode.nextElementSibling](https://developer.mozilla.org/zh-CN/docs/Web/API/NonDocumentTypeChildNode/nextElementSibling)

以上 API IE9+ 支持

###### 4.document 与 window 对象

* [document.defaultView](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/defaultView)
* [window.getComputedStyle()](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/getComputedStyle)

以上 API IE9+ 支持

## 兼容解决方案

#### 了解浏览器渲染内核并控制其渲染模式

###### 嗨学 PC 端兼容标准

* Chrome 57.0
* Safari
* Firefox
* IE8+
* 360 安全浏览器 8.1+
* UC 浏览器 6.1
* QQ 浏览器

###### 浏览器渲染内核

* [Chrome](https://zh.wikipedia.org/wiki/%E7%BD%91%E9%A1%B5%E6%B5%8F%E8%A7%88%E5%99%A8%E5%88%97%E8%A1%A8#.E5.9F.BA.E6.96.BCTrident.E6.8E.92.E7.89.88.E5.BC.95.E6.93.8E): 从28版本开始使用 Blink 内核
* [Firefox](https://zh.wikipedia.org/wiki/Firefox): [Gecko 内核](https://zh.wikipedia.org/wiki/Gecko)
* [Safari](https://zh.wikipedia.org/wiki/Safari): [WebKit 内核](https://zh.wikipedia.org/wiki/WebKit)
* IE8: Trident 4.0 内核
* IE9: Trident 5.0 内核，首次支持 HTML5、SVG、CSS3 及采用新的 JScript 引擎。另外，首次加入利用 DirectX 中的硬件加速改善网络应用程序的性能
* IE10: Trident 6.0 内核: 支持 CSS3 多栏式排版、格子对齐、浮动式区块排版、渐变以及 ECMA5 严格模式
* IE11: Trident 6.0 内核: 支持 WebGL 和 SPDY。增强对 HTML5 标准的支持和性能提升
* [QQ 浏览器](https://zh.wikipedia.org/wiki/QQ%E6%B5%8F%E8%A7%88%E5%99%A8): WebKit 内核 / Trident 内核
* 360 安全浏览器 8.1: Chromium 45 内核 / Trident 内核，2016年7月发布
* 360 安全浏览器 9.1: chrome 55 内核 / Trident 内核，2017年3月发布
* UC 浏览器 6.1: Chromium 50 内核 / Trident 内核，2017年3月发布
* [搜狗高速浏览器](https://zh.wikipedia.org/wiki/%E6%90%9C%E7%8B%97%E9%AB%98%E9%80%9F%E7%80%8F%E8%A6%BD%E5%99%A8): WebKit 内核 / Trident 内核
* [傲游浏览器](https://zh.wikipedia.org/wiki/%E5%82%B2%E6%B8%B8%E4%BA%91%E6%B5%8F%E8%A7%88%E5%99%A8): Blink 内核 / Trident 内核
* [Opera](https://zh.wikipedia.org/wiki/Opera%E9%9B%BB%E8%85%A6%E7%80%8F%E8%A6%BD%E5%99%A8): [Blink 内核](https://zh.wikipedia.org/wiki/Blink)(WebKit 中 WebCore 组件的一个分支)
* [Chromium](https://zh.wikipedia.org/wiki/Chromium): Blink 内核

###### DOCTYPE 声明

DOCTYPE 会影响浏览器渲染模式（Q: 混杂模式, A: 近标准模式, S: 标准模式），应设置成 `<!DOCTYPE html>`，确保 IE8+ / Opera9+ / Firefox10+ / Chrome10+ / Safari10+ 为标准模式，另外此时 IE6、IE7 会解析为近标准模式

###### 渲染内核控制

使用 `meta` 标签来强制 IE8 使用最新的内核渲染页面，避免 IE8 使用“兼容性视图”功能:

        <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">

引导360浏览器（双核）使用 webkit 内核渲染网页:

        <meta name="renderer" content="webkit">

#### 支持常用特性

###### background-size

该属性用来设置背景图片大小，语法:

        background-size：<bg-size> [ , <bg-size> ]*
        <bg-size> = [ <length> | <percentage> | auto ]{1,2} | cover | contain

* IE8 不支持 `background-size`
* auto: 背景图像的真实大小
* cover: 将背景图像等比缩放到完全覆盖容器，背景图像有可能超出容器
* contain: 将背景图像等比缩放到宽度或高度与容器的宽度或高度相等，背景图像始终被包含在容器内

尽管 IE8 不支持该属性，我们还是可以通过非标准的 `-ms-filter` 函数模仿该功能:

        -ms-filter: "progid:DXImageTransform.Microsoft.AlphaImageLoader(src='path_relative_to_the_HTML_file', sizingMethod='scale')";

该代码用来模仿 `cover` 效果

另外，如果用渐变作为背景并且对它使用了 `background-size` ，最好不要只用一个auto， 或者只指定一个宽度值 (例如 background-size: 50%)。对这两种情况 Firefox 8有所改变， 并且目前各浏览器表现不一致。应将 background-size 的宽度值和高度值写全，eg:

        width: 50px; height: 100px;
        background-image: gradient(...);
        background-size: 25px 50px; /* 推荐 */
        background-size: 50% 50%; /* 推荐 */

###### FlexBox 布局

IE 几乎不支持 FlexBox 布局，但我们可以在一些很适合 Flex 布局的场景下，使用 `display: inline-block` / `display: table` / `display: inline` 来实现部分兼容。

* [Almost complete guide to flexbox (without flexbox)](https://kyusuf.com/post/almost-complete-guide-to-flexbox-without-flexbox) 介绍模拟实现 FlexBox 布局的技术
* [Flexbox Patterns](http://www.flexboxpatterns.com/site-header) 介绍利用 FlexBox 实现常用布局的例子

###### hsl() 和 rgba() 中的透明度

IE8 不支持 hsl() 和 rgba() 中的透明度设置，我们可以用带透明度的 png 图片来兼容 IE8

#### 兼容库

* [Respond.js](https://github.com/scottjehl/Respond): IE6-8 及其他浏览器兼容 min/max-width CSS3 Media Queries
* [html5shiv](https://github.com/aFarkas/html5shiv): 支持 IE6-9、Safari 4.x 和 FF 3.x、iPhone 3.x 下对 HTML5 语义化标签的使用
* [css3pie](https://github.com/lojjic/PIE): 使 IE 支持 `border-radius`、`box-shadow`、`border-image`、`multiple background images`、`linear-gradient as background image`
* [placeholder.js](https://github.com/NV/placeholder.js): 支持 IE6-8、Safari 4-5、FF 3.5、Chrome 3-6、Opera 9.5-10.6 下对 placeholder 属性的使用
* [html5media](https://github.com/etianen/html5media): 使主流浏览器支持 `<video>` 和 `audio` 标签
* [selectivizr](https://github.com/keithclark/selectivizr): 模仿实现 IE6-8 下 CSS3 伪元素和属性选择器

#### 查询线上资源

* [MDN](https://developer.mozilla.org/zh-CN/)
* [Can I use](http://caniuse.com/#)
* [360安全浏览器社区](http://bbs.360.cn/forum-141-1.html)
* [W3C](https://www.w3.org/)
* [Safari CSS Reference](https://developer.apple.com/library/content/documentation/AppleApplications/Reference/SafariCSSRef/Introduction.html)
* [CSS current work](https://www.w3.org/Style/CSS/current-work)

#### 寻求社区力量

浏览器对各种 Web 标准的实现有所差异，一些不断迭代的前端库及框架存在宿主环境兼容性问题也很正常，当我们遇到无法解决的问题时，寻求社区帮助也是一个很高效的解决方式。我们一般会在以下社区中寻求帮助或寻找问题相关解决线索:

* [Stack Overflow](http://stackoverflow.com/): 高效且专业的全球 IT 技术问答网站，即使问题得不到完美解决，外国友人也会为你提供思路
* [SegmentFault](https://segmentfault.com/): 国内技术社区，有些论坛化，不过还是卧虎藏龙的
* [知乎](https://www.zhihu.com/): 技术高管们装X的地方，顺便兜售知识
