嗨学网前端开发规范
===

> 2017-03-18

> **Golden Rule:**
> *“ Every line of code should appear to be written by a single person, no matter the number of contributors. ”*

## HTML

#### 一丶语法

* 用两个空格来代替制表符（tab）
* 嵌套元素应当缩进一次（即两个空格）
* 对于属性的定义，确保全部使用双引号，不要使用单引号
* 不要在自闭合（self-closing）元素的尾部添加斜线 （例如，`<br>`或 `<img>`）
* 不要省略可选的结束标签（closing tag）（例如，`</li> `或 `</body>`）

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>
```

#### 二丶注释

* 不要使用模块结束注释
* 注释的缩进应当与其含括的代码一致

```html
<!-- 新闻列表模块 -->
<div class="news">
...
<!-- /新闻列表模块 -->
<!-- 不要使用结束模块的注释，既丑陋，又加重文件负荷。 -->

<!-- TODO: 待办事项 -->
...
```

#### 三丶文档

**HTML5 DOCTYPE**

在每个 HTML 页面开头使用 `DOCTYPE` 来启用标准模式，使每个浏览器尽可能一致地展现。文档类型声明之前，不允许出现任何非空字符。虽然 DOCTYPE 不区分大小写，但是按照惯例，DOCTYPE 大写。

```html
<!DOCTYPE html>
```

**语言属性**

根据 HTML5 规范，强烈建议为 `<html>` 根元素指定 lang 属性，从而为文档设置正确的语言。这将有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等。

```html
<html lang="zh-CN">
  <!-- ... -->
</html>
```

**IE 兼容模式**

IE 支持通过特定的 `<meta>` 标签来确定绘制当前页面所应该采用的 IE 版本。除非有强烈的特殊需求，否则最好是设置为 edge mode，从而通知 IE 采用其所支持的最新的模式。

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

**字符编码**

通过声明一个明确的字符编码，让浏览器轻松、快速地确定适合网页内容的渲染方式。

```html
<meta charset="UTF-8">
```

**引入 CSS 和 JavaScript**

根据 HTML5 规范，在引入 CSS 和 JavaScript 文件时一般不需要指定 `type` 属性，因为 `text/css` 和 `text/javascript` 分别是它们的默认值。尽量避免内部样式表。尽量将 js 文件放在尾部加载。可以使用IE条件注释的方式兼容IE。

```html
<!-- External CSS -->
<link rel="stylesheet" href="code-guide.css">

<!-- In-document CSS -->
<style>
  /* ... */
</style>

<!-- JavaScript -->
<script src="code-guide.js"></script>
```

#### 四丶标签

**语义化标签**

比如标题根据重要性用 h*（同一页面只能有一个 `h1`）, 段落标记用 `p`, 列表用 `ul`, 内联元素中不可嵌套块级元素等

**避免冗余**

编写 HTML 代码时，尽量避免多余的父元素。很多时候，这需要迭代和重构来实现。

**js 生成的标签**

通过 js 生成的标签让内容变得不易查找、编辑，并且降低性能。能避免时尽量避免。

#### 五丶属性

**属性顺序**

* id
* class
* name
* data-*
* src, for, type, href
* title, alt
* aria-*, role

```html
<a id="..." class="..." data-modal="toggle" href="#"> Example link </a>
<input class="form-control" type="text">
<img src="..." alt="...">
```

**布尔属性**

根据 HTML5 规范，布尔型属性可以在声明时不赋值。即元素的布尔型属性如果有值，就是 true，如果没有值，就是 false。

```html
<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

**其他规则**

* 属性值使用双引号
* 省略 url 类属性资源协议头，即去掉 "http://" 或者 "https://"。
* 多媒体元素添加替代属性，即添加 alt 属性。
* `<label>` 使用 for 属性绑定 `<input>`。

---

## CSS

#### 一丶语法

* 用两个空格来代替制表符（tab）。
* 每个声明块的左花括号前添加一个空格，右花括号应当单独成行。
* 每条声明语句的冒号之前不加空格，之后应该插入一个空格。
* 为选择器中的属性添加双引号。
* 为选择器分组时，将单独的选择器单独放在一行。
* 为了获得更准确的错误报告，每条声明都应该独占一行。
* 只包含一条声明的样式，建议将语句放在同一行。
* 避免为 0 值指定单位，如 0px 写为 0 即可。
* CSS 声明中的小数值，不必省略其前面的 0。
* 十六进制值应该全部小写，尽量使用简写形式的十六进制值。
* 对于以逗号分隔的属性值，每个逗号后面都应该插入一个空格。
* 不要在 rgb()、rgba()、hsl()、hsla() 或 rect() 值的内部的逗号后面插入空格。
* 除了重置浏览器默认样式外，禁止直接为html tag添加 css 样式设置;
* 所有声明语句都应当以分号结尾。

#### 二、注释

**注释方式**

```css
/* this is a short comment*/

/*
 * this is comment line 1.
 * this is comment line 2.
 */
```

**文件顶部注释（必需）**

```css
/*
 * @description: 中文说明
 * @author: name (不建议写作者署名，增加维护成本，且本应该每个模块共同可维护)
 * @todo: ...
 */
```

#### 三、代码组织

* 以组件为单位组织代码段，并且具备一致的注释规范。
* 使用一致的空白符将代码分隔成块，这样利于扫描较大的文档。
* 如果使用了多个 CSS 文件，将其按照组件而非页面的形式分拆。

#### 四、选择器

* 使用 classes 而不是通用元素标签来优化渲染性能。
* 避免在经常出现的组件中使用一些属性选择器 (例如，[name="..."])。
* 减少选择器的长度，每个组合选择器选择器的条目应该尽量控制在 3 个以内。
* 只在必要的情况下使用后代选择器 (例如，没有使用带前缀 class 的情况)。

#### 五、命名规范

使用有意义的或通用的 id 和 class 命名：id 和 class 的命名应反映该元素的功能或使用通用名称，而不要用抽象的晦涩的命名。反映元素的使用目的是首选；使用通用名称代表该元素不表特定意义，与其同级元素无异，通常是用于辅助命名；使用功能性或通用的名称可以更适用于文档或模版变化的情况。

* class 名称中只能出现小写字符和破折号（dashe）（不是下划线，也不是驼峰命名法）。破折号应当用于相关 class 的命名（类似于命名空间）（例如，.btn 和 .btn-danger）。
* 避免过度任意的简写。.btn 代表 button，但是 .s 不能表达任何意思。
* class 名称应当尽可能简短，但要足够表达涵义。
* 使用有意义的名称。使用有组织的或目的明确的名称，不要使用表现形式的名称。
* 基于最近的父 class 或基本（base） class 作为新 class 的前缀。能使用前缀则尽量避免嵌套。

#### 六、声明顺序

相关的属性声明应当归为一组，并按照下面的顺序排列：

1. Positioning
2. Box model
3. Typographic
4. Visual

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

```css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```

#### 七、属性简写

在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

* `padding`
* `margin`
* `font`
* `background`
* `border`
* `border-radius`

大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

```css
/* Not so great */
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

/* Better */
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```
