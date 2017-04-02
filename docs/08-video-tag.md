`<video>` 技术调研
===

> 2017-04-02 发布，最后更新于 2017-04-02

HTML `<video>` 元素 用于在 HTML 或者 XHTML 文档中嵌入视频内容。具体参考 [MDN - video](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/video#Attributes)

## 重要属性

* `src`: 要嵌到页面的视频的 URL
* `width` 与 `height`: 视频显示区域的宽度，单位是 CSS 像素
* `controls`: 对视频控制条的显隐控制
* `autoplay`: 是否自动开始播放，不会停下来等着数据载入结束
* `preload`: 属性值设置为 `auto`，提示浏览器用户需要这个视频优先加载；换句话说就是提示如果需要的话，可以下载整个视频，即使用户并不一定会用它。规范没有强制浏览器去遵循该属性的值；这仅仅是个提示
* `poster`: 一个海报帧的 URL，用于在用户播放或者跳帧之前展示。如果属性未指定，那么在第一帧可用之前什么都不会展示；之后第一帧就像海报帧一样展示。

## 重要事件

* `canplay`: 在媒体数据已经有足够的数据（至少播放数帧）可供播放时触发。这个事件对应 CAN_PLAY 的 readyState
* `canplaythrough`: 在媒体的 readyState 变为 CAN_PLAY_THROUGH 时触发，表明媒体可以在保持当前的下载速度的情况下不被中断地播放完毕
* `ended`: 播放结束时触发
* `error`: 在发生错误时触发。元素的 error 属性会包含更多信息
* `pause`: 播放暂停时触发
* `play`: 在媒体回放被暂停后再次开始时触发。即，在一次暂停事件后恢复媒体回放
* `playing`: 在媒体开始播放时触发（不论是初次播放、在暂停后恢复、或是在结束后重新开始）
* `progress`: 告知媒体相关部分的下载进度时周期性地触发。有关媒体当前已下载总计的信息可以在元素的 buffered 属性中获取到

详细信息参考 [MDN - 媒体相关事件](https://developer.mozilla.org/zh-CN/docs/Web/Guide/Events/Media_events)

## 兼容性

**视频预加载**

这里有两个概念：

* preload: 当前视频播放器中将要播放但还未播放的视频，可进行预加载设置，提前缓冲
* prefetch: 当页面加载完成后，让浏览器在空闲时提前请求并且缓存资源以供后续使用

对于 preload，IOS Safari 不支持，部分 Android 浏览器支持；在视频开始播放前，大部分浏览器会将当前待播放的视频缓冲一部分，确保后续可以流畅播放，而不是将整个视频进行缓冲。

对于 prefetch，IOS Safari 不支持，具体浏览器支持情况参考 [Can I use - prefetch](http://caniuse.com/#search=prefetch)，也可以用浏览器访问 [Prefetch Information](http://browserspy.dk/prefetch.php) 来检测是否支持 prefetch。即使浏览器支持 prefetch 资源，但由于视频格式资源在 prefetch 后无法被缓存，因此目前无法实现播放第一段视频的时候预下载第二段视频。

PS: 关于 prefetch，我在支持 prefetch 的 chrome 浏览器下作了测试，播放第一段视频的时候确实会请求第二段视频的整个资源，但在接下来播放第二段视频的时候之前预加载的资源没有被缓存。测试 Demo 代码可在 [这里](https://github.com/AnHongpeng/mobile-web-case/tree/master/video) 下载，测试时请将网速调整至 Regular 2G 以模拟低网速情况

**封面图片**

可以使用 poster 属性来设置视频封面图片（海报帧），IOS Safari 支持，但加载速度明显比在 `<img>` 中显示要慢，而 Android 浏览器部分支持。因此推荐使用 `<img>` 的方式设置视频的封面图片

**自动播放**

IOS Safari 中不支持，但在 webview 中可能被开启；iOS 开发文档明确说明蜂窝网络下不允许 autoplay；Android 浏览器部分支持

## 最佳实践

**设置 width 和 height**

使用 `<video>` 标签时推荐明确设置 `width` 和 `height` 属性且不能为0，否则在 IOS Safari 下可能会导致布局 Bug

**设置封面图片**

直接将 `<video>` 显示在页面中，视频播放的初始效果会因内置浏览器而存在差异。建议先将视频设置为 1px x 1px 大小并放置于边缘处，并使用图片和样式模拟视频封面图，但需要提供视频封面图片。

另一种方案是先隐藏视频播放控件（controls），在上面布一层半透明带播放按钮的图片，当点击该图片时触发视频的播放事件
