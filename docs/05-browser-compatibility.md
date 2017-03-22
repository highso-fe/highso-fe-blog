浏览器兼容解决方案汇总
===

> 2017-03-21

## 浏览器对常用特性的支持情况

#### HTML

###### 1.语义化标签

[New semantic elements](http://caniuse.com/#search=html5): IE9+ 支持，包括 `<section>`、`<article>`、`aside`、`header`、`footer`、`nav`、`figure`、`figcaption`、`time`、`mark`、`main`

#### CSS 特性

###### 1.CSS3 Media Queries

IE9+ 支持，但不支持嵌套 media queries

[兼容性参考](http://caniuse.com/#search=media)

###### 2.其他特性

* [CSS3 Border images](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image): IE11+ 支持，且需要打 -moz, -webkit, -o 标签, [兼容性参考](http://caniuse.com/#search=border-image)
* [CSS3 Border-radius](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-radius): IE9+ 支持，且需要打 -moz, -webkit 标签, [兼容性参考](http://caniuse.com/#search=border-radius)
* [CSS3 Box-shadow](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow): IE9+ 支持，且需要打 -moz, -webkit 标签, [兼容性参考](http://caniuse.com/#search=box-shadow)
* [Multiple background images](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-image): IE9+ 支持
* [CSS3 Background-image options](http://caniuse.com/#search=CSS3%20Background-image%20options): `background-clip`, `background-origin` 和 `background-size` IE9+ 支持
* [CSS Gradients](http://caniuse.com/#search=CSS%20Gradients): IE10+ 支持, 且需要打 -moz, -webkit, -o 标签, [兼容性参考](http://caniuse.com/#search=CSS%20Gradients)

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

#### 编码层面

###### DOCTYPE 声明

DOCTYPE 会影响浏览器渲染模式（Q: 混杂模式, A: 近标准模式, S: 标准模式），应设置成 `<!DOCTYPE html>`，确保 IE8+ / Opera9+ / Firefox10+ / Chrome10+ / Safari10+ 为标准模式，另外此时 IE6、IE7 会解析为近标准模式

###### 渲染内核控制

使用 `meta` 标签来强制 IE8 使用最新的内核渲染页面，避免 IE8 使用“兼容性视图”功能:

        <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">

引导360浏览器（双核）使用 webkit 内核渲染网页:

        <meta name="renderer" content="webkit">

#### 兼容库

* [Respond.js](https://github.com/scottjehl/Respond) - IE6-8 及其他浏览器兼容 min/max-width CSS3 Media Queries
* [html5shiv](https://github.com/aFarkas/html5shiv) - 支持 IE6-9、Safari 4.x 和 FF 3.x、iPhone 3.x 下对 HTML5 语义化标签的使用
