Web 前端分享 第二期
===

> 2017-07-26 发布，最后更新于 2017-07-26

## （一）那些重要却总被忽视的 HTML 招式

#### 1. DOCTYPE 声明

###### 我们经常会遇到不同的 DOCTYPE 声明方式，Eg:

HTML 5:

        <!DOCTYPE html>

HTML 4.01 Strict:

        <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

HTML 4.01 Transitional:

        <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

...

###### 什么是 DOCTYPE 声明？它影响什么？

DOCTYPE 告知浏览器当前的 HTML (或 XML) 文档是哪一个版本，它是一条声明, 而不是一个标签; 也可以把它叫做 "文档类型声明", 或简称为 "DTD（document type declaration）".

不同文档类型对应的识别标签范围不同，详见: [HTML 元素和有效的 DTD](http://www.w3school.com.cn/tags/html_ref_dtd.asp)

DOCTYPE 也会影响浏览器渲染模式（Q: 混杂模式, A: 近标准模式, S: 标准模式），应设置成 `<!DOCTYPE html>`，确保 IE8+ / Opera9+ / Firefox10+ / Chrome10+ / Safari10+ 为标准模式，另外此时 IE6、IE7 会解析为近标准模式

#### 2. 元数据

元数据是描述数据的数据，使用 [<meta> 元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta) 来为文档添加元数据。

`<meta>` 包含 `name` 和 `content` 属性:

* `name` 指定 meta 元素类型; 说明该元素包含了什么类型的信息。
* `content` 指定元数据内容

Eg:

指定文档字符编码：

        <meta charset="UTF-8">

设定视口属性：

        <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

渲染内核设置，使用 meta 标签来强制 IE8 使用最新的内核渲染页面，避免 IE8 使用“兼容性视图”功能：

        <meta http-equiv="X-UA-Compatible" content="IE=edge, chrome=1">

引导360浏览器（双核）使用 webkit 内核渲染网页：

        <meta name="renderer" content="webkit">

网页 TDK 设置：

        <meta name="keywords" content="嗨学网,嗨学,一级建造师,二级建造师,司法考试,注册会计师,执业药师,一级注册消防工程师,互动,课堂,智能,题库,问答,系统,移动,嗨学,嗨学网登录,王玮老师,李四德老师,杨海军老师,盛英会老师,王霞老师,张千老师,嗨学网视频,嗨学网招聘,嗨学网师资,嗨学网课程">

浏览器辅助功能开关：

        <meta name="format-detection" content="telephone=no" />

#### 3. 块级元素和内联元素

* 块级元素在页面中以块的形式展现 —— 相对于其前面的内容它会出现在新的一行，其后的内容也会被挤到下一行展现。块级元素通常用于展示页面上结构化的内容，类似于段落、列表、导航菜单、页脚等等。一个以 block 形式展现的块级元素不会被嵌套进内联元素中，但可以嵌套在其它块级元素中。
* 内联元素通常出现在块级元素中并被一些其它文本所包围，而不是一整个段落或者一组内容。内联元素不会导致文本换行：它通常出现在一堆文字之间例如超链接元素 `<a>` 或者强调元素 `<em>` 和 `<strong>`
* [块级元素列表](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Block-level_elements)
* [行内元素列表](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Inline_elemente)

嵌套规则：

1. 块元素可以包含内联元素或某些块元素，但内联元素却不能包含块元素，它只能包含其它的内联元素
2. 块级元素不能放在 `<p>` 里面
3. 有几个特殊的块级元素只能包含内嵌元素，不能再包含块级元素，这几个特殊的标签是: h1~6、p、[dt](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/dt)

#### 4. IE Hack

* lt: 小于
* gt: 大于
* lte: 小于等于
* gte: 大于等于
* !: 不等于

Eg:

        <!--[if IE]>
            IE 浏览器生效
        <![endif]-->

        <!--[if IE 8]>
            仅在 IE8 下生效
        <![endif]-->

        <!--[if gte IE 8]>
            在大于等于 IE8 版本的浏览器下生效
        <![endif]-->

        <!--[if !IE 10]>
            非 IE10 的浏览器下生效
        <![endif]-->

#### 6. 特殊字符的实体引用

常用：

|Literal character|Character reference equivalent|
|----|----|
|<|`&lt;`|
|>|`&gt;`|
|"|`&quot;`|
|'|`&apos;`|
|&|`&amp;`|
|不间断空格|`&nbsp;`|
|全角空格|`&emsp;`|
|半角空格|`&ensp;`|
|©|`&copy;`|

[HTML特殊字符编码对照表](http://www.jb51.net/onlineread/htmlchar.htm)

## （二）CSS 基础

#### 1. CSS 规则

![CSS 规则](../img/11/01.png)

[CSS 属性速查](http://www.css88.com/book/css/quicksearch.htm)

#### 2. 不同种类的 CSS 选择器

###### 简单选择器

简单选择器基于元素的类型（或其 class 或 id）直接匹配文档的一个或多个元素

```css
/* 元素选择器 */
ul, ol, dl {
  margin: 0;
  padding: 0;
  list-style: none;
}


/* 类选择器 */
.mt10 {
    margin-top: 10px;
}

.live-pptCtrl--btn {
    display: inline-block;
    width: 25px;
    height: 25px;
    ...
}

/* id 选择器 */
#percentCvs {
    width: 42px;
    height: 42px;
    ...
}

/* 通用选择器 */
* {
    padding: 5px;
    border: 1px solid black;
    background: rgba(255,0,0,0.25);
}
```

###### 属性选择器

`E[att] { sRules }` 选择具有 `att` 属性的 `E` 元素，Eg:
```css
img[alt] {
    margin: 10px;
}
```

`E[att="val"] { sRules }` 选择具有 `att` 属性且属性值等于 `val` 的 `E` 元素
`E[att~="val"] { sRules }` 选择具有 `att` 属性且属性值中有 `val` 的 `E` 元素
`E[att^="val"] { sRules }` 选择具有 `att` 属性且属性值为以 `val` 开头的 `E` 元素
`E[att$="val"] { sRules }` 选择具有 `att` 属性且属性值为以 `val` 结尾的 `E` 元素
`E[att*="val"] { sRules }` 选择具有 `att` 属性且属性值字符串包含 `val` 的 `E` 元素
`E[att|="val"] { sRules }` 选择具有 `att` 属性且属性值为以 `val` 开头并用连接符 "-" 分隔的字符串的 `E` 元素，如果属性值仅为 `val` ，也将被选择

###### 伪类

一个 CSS 伪类是一个以冒号(:)作为前缀的关键字，当你希望样式在特定状态下才被呈现到指定的元素时，你可以往元素的选择器后面加上对应的伪类

![css 伪类](../img/11/02.png)

Eg:

```css
a:hover,
a:active,
a:focus {
    color: darkred;
    text-decoration: none;
}
```

###### 伪元素

就像 pseudo classes (伪类)一样， 伪元素添加到选择器，但不是描述特殊状态，它们允许您为元素的某些部分设置样式。 例如， `::first-line` 伪元素只定位由选择器指定的元素的第一行

* `::after`
* `::before`
* `::first-letter`
* `::first-line`
* `::selection`

Eg.清除浮动:

```css
.clearfix {
  zoom: 1;
}
.clearfix:after {
  content: "";
  display: block;
  height: 0;
  visibility: hidden;
  clear: both;
}
```

###### 关系选择器

|Combinators|Select|
|----|----|
|A B|匹配任意元素，满足条件：B是A的后代结点（B是A的子节点，或者A的子节点的子节点）|
|A>B|匹配任意元素，满足条件：B是A的直接子节点|
|A+B|匹配任意元素，满足条件：B是A的下一个兄弟节点（AB有相同的父结点，并且B紧跟在A的后面）|
|A~B|匹配任意元素，满足条件：B是A之后的兄弟节点中的任意一个（AB有相同的父节点，B在A之后，但不一定是紧挨着A）|

注意 IE 兼容性：

IE8 支持 [兄弟选择符(E~F)](http://www.css88.com/book/css/selectors/relationship/e-brother-f.htm) 和属性选择符: [E[att^="val"]](http://www.css88.com/book/css/selectors/attribute/att4.htm)、[E[att$="val"]](http://www.css88.com/book/css/selectors/attribute/att5.htm)、[E[att*="val"]](http://www.css88.com/book/css/selectors/attribute/att6.htm)

IE8 不支持 [E:root](http://www.css88.com/book/css/selectors/pseudo-classes/root.htm)、[E:nth-child(n)](http://www.css88.com/book/css/selectors/pseudo-classes/nth-child(n).htm)、[E:nth-last-child(n)](http://www.css88.com/book/css/selectors/pseudo-classes/nth-last-child(n).htm)、[E:nth-of-type(n)](http://www.css88.com/book/css/selectors/pseudo-classes/nth-of-type(n).htm)、[E:nth-last-of-type(n)](http://www.css88.com/book/css/selectors/pseudo-classes/nth-last-of-type(n).htm)、[E:last-child](http://www.css88.com/book/css/selectors/pseudo-classes/last-child.htm)、[E:first-of-type](http://www.css88.com/book/css/selectors/pseudo-classes/first-of-type.htm)、[E:last-of-type](http://www.css88.com/book/css/selectors/pseudo-classes/last-of-type.htm)、[E:only-child](http://www.css88.com/book/css/selectors/pseudo-classes/only-child.htm)、[E:only-of-type](http://www.css88.com/book/css/selectors/pseudo-classes/only-of-type.htm)、[E:empty](http://www.css88.com/book/css/selectors/pseudo-classes/empty.htm)、[E:target](http://www.css88.com/book/css/selectors/pseudo-classes/target.htm)、[E:enabled](http://www.css88.com/book/css/selectors/pseudo-classes/enabled.htm)、[E:disabled](http://www.css88.com/book/css/selectors/pseudo-classes/disabled.htm)、[E:checked](http://www.css88.com/book/css/selectors/pseudo-classes/checked.htm)、[E:not(s)](http://www.css88.com/book/css/selectors/pseudo-classes/not(s).htm)

以上 CSS3 选择器 IE9+ 均支持，[兼容性参考](http://caniuse.com/#search=CSS3%20selectors)

#### 3. 盒模型

###### 概念

在写 CSS 时你会发现大部分都是关于盒模型的——设置它们的尺寸，颜色，位置等等。CSS 布局就是基于盒模型的。每个占据页面空间的块级元素都有相似的属性：

* 内边距（padding）, 围绕着内容的空间（比如围绕段落的空间）
* 边框（border）, 紧接着内边距的实体线段
* 外边距(margin), 围绕元素外部的空间

![CSS 盒模型](../img/11/03.png)

margin -> border -> padding -> content

![Chrome 调试盒模型](../img/11/04.png)

盒子的大小：content + padding + border

###### 2种盒模型

盒模型分为2种，IE8+ 浏览器通过 `box-sizing` 来设置：

* 标准盒模型（默认）：`box-sizing: content-box`，`width/height` = content 区域
* 怪异盒模型：`box-sizing: border-box`，`width/height` = content + padding + border

###### 定位

`position` 有4个值：

* static: 对象遵循常规流。此时4个定位偏移属性（top, right, bottom, left）不会被应用
* relative: 对象遵循常规流，并且参照自身在常规流中的位置通过定位偏移属性进行偏移时不会影响常规流中的任何元素
* absolute: 对象脱离常规流，此时偏移属性参照的是离自身最近的定位祖先元素，如果没有定位的祖先元素，则一直回溯到 body 元素。盒子的偏移位置不影响常规流中的任何元素，其 margin 不与其他任何 margin 折叠
* fixed: 与 absolute 一致，但偏移定位是以窗口为参考。当出现滚动条时，对象不会随着滚动

类比一下：static（活人），relative（没火华的尸体），absolute（灵魂出窍），fixed（阴魂不散）

`z-index`

设置对象的层叠顺序，适用于定义了 `position` 为非 `static` 的元素

#### 4. 浏览器渲染过程

![webkit 浏览器渲染过程](../img/11/05.jpg)
