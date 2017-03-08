嗨学网重构 PCWeb 端 js 框架选型对比
===

> 2017-03-08

> 本文重点关注不同框架的对比情况，至于某种框架如何优雅实现具体业务场景或功能（如使用 Redux 还是 Mobx 来配合 React 进行状态管理）留作框架选型后深入讨论。

## 业务需求

1. 兼容IE8+
2. 仅 PC 端，非手机 Web 端
3. 用户登录后是个人学习管理操作平台（核心功能模块，包括课程、题目、学习资料等的管理），UI 布局版式固定（顶栏、尾栏、侧边栏等视图框架模式），较多涉及数据过滤后的局部区域重新渲染，无复杂交互，交互后粘带数据实时更新的场景较少，几乎不涉及数据可视化。

## 框架对比

#### 先做排除法：

1. [Angular1](https://angularjs.org/)：双向数据绑定（本项目应用场景较少，且相比单向数据流难以预测数据走向）；脏检查渲染性能较差（独立作用域变化后 watcher 的重新计算），需投入过多精力在避免脏检查循环上；[Angular1.3 后不再兼容 IE8](https://blog.angularjs.org/2013/12/angularjs-13-new-release-approaches.html)。
2. [Ember2.0](https://github.com/emberjs/ember.js)：[Ember2.0不再兼容IE8](http://emberjs.com/blog/2015/04/20/ie8-support-update.html)；社区繁荣度较小；UI层渲染性能一般（字符串模板、双向绑定）；灵活性差；学习成本较高；文件体积庞大。Ember 适合作为不特别在乎体积及渲染性能的前端一体化解决方案，适合频繁创建、修改、查询的复杂表单系统场景，不太适合面向大规模用户、性能要求卓越、灵活性强、自定制组件多（非社区轮子）的场景。

#### 总览

虽然 [vue2.0 不兼容 IE8](https://cn.vuejs.org/v2/guide/installation.html)，但介于 Vue.js 其卓越的渲染性能、官方维护的活跃中文社区、先进的框架理念及相对非陡峭的学习曲线，我还是将它列入框架比较对象中（万一后面要开发仅支持现代浏览器的项目呢 :stuck_out_tongue_winking_eye:）。

另外 React 作为一个 View 层渲染库本身与 Vue 和 Angular 在框架层的可比性就不大，这里更多指的是 React 相关的一整套解决方案。

|框架|兼容IE8|渲染性能|社区繁荣度|学习曲线|开发灵活性|
|----|----|----|----|----|----|
|[React v0.14.8](https://github.com/facebook/react/releases/tag/v0.14.8)|[v15后不再支持](https://facebook.github.io/react/blog/2016/01/12/discontinuing-ie8-support.html)|2nd|1st|较陡|1st|
|[Vue v2.0](https://cn.vuejs.org/v2/guide/index.html)|否(从未支持过)|1st|3rd|一般|2nd|
|[Angular v2.4](https://angular.cn/docs/ts/latest/)|否(1.3后不支持)|3rd|2nd|较陡|3rd|

#### 渲染性能对比

Duration in milliseconds (Slowdown = Duration / Fastest)

| |angular v2.0.0-rc5|react v15.3.1|vue v2.0.0-beta1|
|----|----|----|----|
|create rows|198.06|187.28|171.36|
|replace all rows|178.45|190.16|68.76|
|partial update|11.42|16.40|22.17|
|select row|2.39|5.96|13.30|
|swap rows|50.16|48.25|19.14|
|remove row|64.11|67.07|44.09|
|create many rows|1914.70|1839.96|1712.87|
|append rows to large table|594.38|297.09|420.53|
|clear rows|281.60|371.16|223.87|
|clear rows a 2nd time|265.82|354.71|210.56|
|slowdown geometric mean|1.85|1.82|1.37|

参考 [Results for js web frameworks benchmark - round 4](http://stefankrause.net/js-frameworks-benchmark4/webdriver-ts/table.html)

#### 其他注意点

* Angular v4.0 预计于2017年3月发布，[v4.0.0-rc.2](https://github.com/angular/angular/compare/4.0.0-rc.1...4.0.0-rc.2) 已出，且 Angular 将基于时间的发布周期进行发布，并使用[语义化版本号](http://semver.org/lang/zh-CN/)

* 大型商用性质工程选择谷歌产品还是要慎重，就以往历史来看，Angular 喜欢断崖式升级：v1.08 时兼容 IE6-8，v1.2 时需要打补丁兼容旧浏览器，v1.3时直接不再兼容并删除所有兼容代码，v1.4 不向下支持动画模块，v2.0 不支持 IE6-11、chrome30。且自17年3月份发布4.0后又会以6个月为周期迭代新的大版本...

## 总结

对比 vue v2.0、Angular v2.4、选择 React 技术栈，原因有四：

1. React v0.14.8 是三者中唯一兼容 ie8 的
2. 适合当前业务场景：UI 多可重用组件；不涉及频繁且复杂的表单数据过滤操作；不需要双向数据流，更多是通过用户操作改变视图状态进而获取数据并渲染视图的单向数据流场景
3. 视图渲染性能优秀，且架构轻巧灵活
4. 无断崖式升级，未来升级版本的开发成本较小且社区资源丰富

## 参考资源

1. [Vue.js 对比其他框架](https://cn.vuejs.org/v2/guide/comparison.html#Angular-1)
2. [Angular 2.4 浏览器支持](https://angular.cn/docs/ts/latest/guide/browser-support.html)
3. [Discontinuing IE 8 Support in React DOM](https://facebook.github.io/react/blog/2016/01/12/discontinuing-ie8-support.html)
4. [Igor Minar - Opening Keynote - Version 4 Announcement - NG-BE 2016](https://www.youtube.com/watch?v=aJIMoLgqU_o)
5. [Results for js web frameworks benchmark – round 4](http://stefankrause.net/js-frameworks-benchmark4/webdriver-ts/table.html)
6. [为什么选择 emberjs 开发 dashboard 和 CMS 类系统](https://juejin.im/entry/57567af52e958a006a7d56c3)
