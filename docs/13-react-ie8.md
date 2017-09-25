React技术栈IE8的兼容解决方案汇总
===

> 2017-09-25 发布，最后更新于 2017-09-25

## Web特性兼容，如H5、CSS、JS、WebAPI的兼容

### 1.HTML 5

* [html5shiv](https://github.com/aFarkas/html5shiv): 支持 IE6-9、Safari 4.x 和 FF 3.x、iPhone 3.x 下对 HTML5 语义化标签的使用
* [html5media](https://github.com/etianen/html5media): 使主流浏览器支持 `<video>` 和 `audio` 标签
* [placeholder.js](https://github.com/NV/placeholder.js): 支持 IE6-8、Safari 4-5、FF 3.5、Chrome 3-6、Opera 9.5-10.6 下对 placeholder 属性的使用；JQuery placeholder 插件：[jquery-placeholder](https://github.com/mathiasbynens/jquery-placeholder)

### 2.CSS

* [css3pie](https://github.com/lojjic/PIE): 使 IE 支持 `border-radius`、`box-shadow`、`border-image`、`multiple background images`、`linear-gradient as background image`
* [Respond.js](https://github.com/scottjehl/Respond): IE6-8 及其他浏览器兼容 min/max-width CSS3 Media Queries
* [selectivizr](https://github.com/keithclark/selectivizr): 模仿实现 IE6-8 下 CSS3 伪元素和属性选择器
* `react-css-module`在ie8下不支持，用`cssModule`就可以了

### 3.JS、WebAPI

* [es5-shim / es5-sham](https://github.com/es-shims/es5-shim): 使旧版及部分现代浏览器兼容 ES5 标准中的方法（shim与sham区别：shim使ES5 中有些方法，可以在旧 JS 引擎中完美模拟。ES5 中其他无法被完美模拟的方法，就由 sham 承包了。 sham 只承诺你用的时候代码不会崩溃，至于对应的方法是不是起作用它就不保证了，它只是尽力模拟。所以要用的方法在 shim 中都包含了，那么就不需要 sham 。sham 能不引用就不引用。但是如果要用的方法只包含在 sham 中，那要明白 sham 只是保证不崩溃，并不能保证对应方法的功能正确。另外 sham 依赖 shim）
* [es6-shim](https://github.com/paulmillr/es6-shim): 为旧引擎浏览器尽可能地提供 ES6 方法的兼容性垫片
* `console-polyfill`：Browser console polyfill. Makes it safe to do `console.log()`
* [core-js](https://github.com/zloirock/core-js)：Includes polyfills for `ECMAScript 5`, `ECMAScript 6: promises`, `symbols`, `collections`, `iterators`,` typed arrays`,` ECMAScript 7+ proposals`,` setImmediate`。比如修复Object.assign


错误信息 | 原因 | 解决方案 
--- | ---- | --------
`Expected identifier` | 代码中或者第三方模块中使用了保留字，比如 `default` | 使用 [es3ify](https://www.npmjs.com/package/es3ify) 或者 [es3ify-loader](https://github.com/sorrycc/es3ify-loader)
`Exception thrown and not caught` | babel 把 `export * from 'xxx'` 编译成了 `Object.defineProperty`，而 IE8 中不支持 accessor property | 把 `es5-shim` `es5-shim/es5-sham` 插入到入口文件的最上方，并且在代码中不要使用 `export * from 'xxx'` 
`Object expected` | 可能你使用了 `fetch` | 用 `es6-promise` 和 `fetch-ie8` polyfill 
`'Promise' is undefined` | `Promise` 需要 polyfill | 用 `es6-promise` polyfill 
`Object doesn't support this property or method` | 可能你使用了 `Object.assign` | 用 `core-js` polyfill 
`'JSON' is undefined` | 需要使用 IE8 Standards Mode | 添加 `<!DOCTYPE html>` 和 `<meta http-equiv="X-UA-Compatible" content="IE=EDGE"/>` 

注意：
项目代码分为两部分（我们自己写的代码和`node_modules`里面引用的外部代码），按照以上方法，我们只能解决我们自己代码中的兼容性，并不能解决`node_modules`中应用的代码的兼容性！
比如：`Exception thrown and not caught`这个问题，给的解决方法是：把`es5-shim` `es5-shim/es5-sham`插入到入口文件的最上方，并且在代码中不要使用 `export * from 'xxx'`。
这样使用其实可以解决我们代码中的兼容性，但是node_modules里面应用的外部库的兼容并不能解决。
我们把这些编译文件放到`webpack`配置文件中，让webpack打包的时候，也去转义`node_modules`里面的文件！
比如`es5-shim`这个库，我们的引用方式如下面的配置文件，我们的`es3ify`就使用`es3ify-webpack-plugin`来代替，全部都集成到`webpack`配置文件中。

## 核心库兼容选型（react react-dom redux react-router）

### 1.react和react-dom
为了兼容IE8，react选用0.14.8版本。从 React v15 开始，React DOM 将不会再支持 IE8 了。

### 2.redux
选用最新版本。Redux 源文件由 ES2015 编写，但是会预编译到 CommonJS 和 UMD 规范的 ES5，所以它可以支持[任何现代浏览器](https://caniuse.com/#feat=es5)。Redux 是 JavaScript 状态容器，提供可预测化的状态管理。Redux 除了和 React 一起用外，还支持其它界面库。

### 3.react-router
react-router选用2.8.1版本。react使用的是低版本（v0.14.8），所以react-router也只能选用对应的低版本。官方同时维护 2.x 和 4.x 两个版本，所以前者依然可以用在项目中。

## 核心库API兼容（版本15.6.0【后台系统】 0.14.8【前台系统】）

### 1.react14到15版本变更

#### 主要变更

* 加入了`document.createElement`，取消了`data-reactid`
关于与`DOM`的交互方式，发生了重大改动。最显著的改动在于：不再为每个`DOM`节点设置`data-reactid`属性，使react更加轻量级。此外在变更后，在最初的渲染中也能使用`document.createElement`了。随着浏览器的优化，使用`createElement`之后，React速度更快。使用id将事件映射回React组件，代表着尽管存在着大量的缓存数据，每个事件仍要完成一堆的工作。我们都有这样的经历：缓存，尤其是无效缓存很容易导致出错，结果就是这些年来出现了一大堆难以复现的问题。现在，由于对节点有了控制权，在渲染时我们可以构建出直接映射。
注意：在服务器渲染内容中，还会存在`data-reactid`，不过会比以前少得多，自动递增的序号也会更简单。
* 取消额外的`<span>`
在DOM交互中还有一项大变化，就是我们渲染文本模块的方式。之前react在渲染是会加入很多额外的span，现在渲染后纯文本节点与用于界定的注释交错排列。在DOM交互中还有一项大变化，就是我们渲染文本模块的方式。由于依赖所生成标记的用户很少，此项修改的影响面也会很小。不过，如果你在CSS中使用了这些作为对象的话，可能需要做出相应的调整。不过在组件中，你随时可以执行渲染。
* 渲染返回`null`目前改成了`注释节点`
我们也利用注释节点修改了null，这个功能是在`React 0.11`中加入的，通过渲染`<noscript>`元素实现。在改用注释节点渲染后，有些CSS可能会指向错误的对象，特别在使用了`:nth-child`时。在React中，`<noscript>`标记的运用一直被看作是React指向`DOM`方式的实现细节。由于这些细节并没有相关依赖，我们认为可以在这一版中直接作出修改，而无需先发一个版本让大家体验其中细微的差异。此外在很多主要应用中，我们已经看到了这些变化对React的性能带来的提高。
* 函数组件也可返回`null`
在`React 0.14`中，增加了我们增加了对[定义无状态组件为函数](https://facebook.github.io/react/blog/2015/09/10/react-v0.14-rc1.html#stateless-function-components)的支持。然而，在`React 0.14`中我们仍可以在不需扩展`React.Component`或使用`React.createClass()`的情况下，对类组件进行定义，[因此我们无法确定这个组件是类组件还是函数组件](https://github.com/facebook/react/issues/5355)因此我们无法确定这个组件是类组件还是函数组件；并且在`0.14版本`中，类组件是不会返回`null`的。这个问题在React 15中得到了解决，现在可以从任何组件——无论是[类组件或者函数组件](https://github.com/facebook/react/issues/5355)返回`null`了。
* 改进对`svg`的支持
现在React将完全支持所有的`SVG标签`（不常见的SVG标签不会出现在`React.DOM`元素助手中，不过`JSX`和`React.createElement`适用于所有的标签名），并支持浏览器实现的所有`SVG属性`。

#### 关键性变动
* `React.cloneElement()`现在包括`defaultProps`
修复了`React.cloneElement()`中的bug，如果`cloneElement()`接收到的某些`props`是`undefined`，常返回带有未定义值的元素。在React 15中，我们将其修改为与`createElement()`保持一致。现在任何发送给`cloneElement()`的未定义`props`都有相应的组件`defaultProps`了。
* `ReactPerf.getLastMeasurements()`晦涩不明 

#### 删除的内容
* 在v0.14版本中，这些内容已经被标记为将要移除的内容：
从React顶层输出中移除的`API`包括：`findDOMNode`、`render`、`renderToString`、`renderToStaticMarkup`以及`unmountComponentAtNode`。在此提醒，这些API现在在`ReactDOM`和`ReactDOMServer`中可用。
* 移除的插件包括：`batchedUpdates`以及`cloneWithProps`。
* 移除的组件实例方法包括：`setProps`、`replaceProps`以及`getDOMNode`。
* `CommonJSreact`/`addons`入口点也不再使用，在此提醒：可以使用单独的`react-addons-*`软件包来替代，不过只适用于使用`CommonJS`软件包时。
* 将`children`发送给类似`<input>`之类的空元素的做法被取消了，现在改成抛出异常。
* 在`DOMrefs`（例如`this.refs.div.props`）中使用`React-specific`属性的做法也被删除了。

#### 新的警告提醒
* 如果你使用精简后的开发版，`React DOM`会提示你使用速度更快的生产版。

* `React DOM`：在指定没有单位的`CSS`值为字符串时，以后的版本将不会自动添加`px`字样。当前的版本在此类情况下（比如编写style={{width: '300'}}）会发出警告。类似width: 300这样的无单位数据值不会被修改。

* 目前在设置及访问未作适当清除的属性时，合成事件（Synthetic Events）会发出警告，并在事件返回到池中后，在访问时发出提醒。  

* 在尝试从`props`读取`ref`和`key`时，元素现在会发出提示。

* 在构造函数中，若将不同的`props`对象发送给`super()`，React会发出提示。

* 如果在`getChildContext()`中调用`setState()`，则React会发出提示。

* React DOM现在会提示DOM元素事件句柄键入错误，比如`onclick`应该是`onClink`。

* React DOM现在会在style中提示`NaN`值。

* 如果在输入内容中指定了`value和defaultValue`，则React DOM现在会发出提示。

* 如果输入在受约束与不受约束之间切换，则React DOM现在会发出提示。

* 如果指定了`onFocusIn`或`onFocusOut`handler，则React DOM现在会发出提示，因为在React中这两者没有必要出现。

* 如果将无效回调作为`ReactDOM render()`、`this.setState()`或`this.forceUpdate()`的最后一个参数发送过去，则React会输出描述性的错误信息。

* 插件：如果尝试在浅渲染中使用`TestUtils.Simulate()`，则会输出帮助性的消息。

* `PropTypes`：`arrayOf()`与`objectOf()`会为无效参数提供更详尽的错误信息。

#### 其他优化

* React现在使用`loose-envify`来代替`envify`，所以安装的过度依赖较之前更少。

* 浅渲染器暴露`getMountedInstance()`。

* 浅渲染器从`render()`返回渲染输出结果。

* 在以前的环境中，React对于`Object.create`及`Object.freeze`是依赖`ES5 shams`的，现在仍是如此，但在相关环境中需要提供ES5 shams。

* React DOM支持名称以数字开头的react- 属性。

* React DOM为类似[Draft.js](https://draftjs.org/)之类用React管理`contentEditable`子集的组件添加了新的`suppressContentEditableWarning`。

* React改进了`createClass()`在复杂参数中的性能表现。

### 2.React v0.14.8
* 在服务器上渲染时修复内存泄漏(Fixed memory leak when rendering on the server)

### 3.React v15.6.0
* 声明式设计 − 采用声明范式，可以轻松描述应用，无痛创建交互式 UI 。
* 基于组件 − 通过 React 构建组件，使得代码更加容易得到复用，然后组合它们以创建复杂的 UI 。
* 高效易用 − 不对技术堆栈的其余部分做出假设，可以在 React 中开发新功能，而无需重写现有的代码。
* 该版本替换了原来的降级弃用警告(用 `console.warn `取代` console.error `)，添加了 `React.createClass` 的弃用警告，并为 React.DOM 格式助手添加了单独的模块。此外，针对 React DOM ，还在 style 属性中添加对 CSS 变量的支持，以及对 CSS 网格样式属性的支持。


