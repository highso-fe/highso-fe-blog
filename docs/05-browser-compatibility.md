浏览器兼容解决方案汇总
===

> 2017-03-21

## 浏览器对常用特性的支持情况

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
