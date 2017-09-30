hx-antd
===

> 2017-09-30 发布，最后更新于 2017-09-30

项目中在按需加载 [ant-design](https://github.com/ant-design/ant-design)（MIT License）组件时发现 **引入组件的同时会连带引入 Ant Design 核心样式模块中的一些全局样式（[源码-核心样式入口](https://github.com/ant-design/ant-design/blob/master/components/style/core/index.less)）。**因此会对我们项目本身设定的一些浏览器重置样式及全局公有样式存在覆盖，导致一些样式、交互表现异常。

为解决底层样式冲突问题，我们 fork 了 Ant Design v2.13.4，对源码做了部分更改（删除了部分 CSS Reset），并在 [NPM](https://www.npmjs.com/) 上发布了 [hx-antd](https://www.npmjs.com/package/hx-antd)。后续遇到类似自定制问题可以 clone 该项目修改代码后重新发布到 NPM。

## 本地开发 hx-ant-design 流程

1. clone 项目后，根目录下 `npm i --registry https://r.cnpmjs.org/` 安装依赖 node 包
2. 主体功能及样式代码位于 `/components` 下
3. 功能代码修改后更新 `package.json` 版本号
4. `npm run pub` 进行发布 NPM 前的 Less、JS 预编译，会生成 `/es`, `/lib`, `/dist` 目录用于后续正式发布
5. `npm login` 登录 NPM
6. `npm publish` 正式发布 NPM 包

## 关注更新信息

详见 [GitHub hx-ant-design](https://github.com/highso-fe/hx-ant-design) 及 [NPM hx-antd](https://www.npmjs.com/package/hx-antd) 关注更新信息

## 关于 NPM 发布

* 如何发布 NPM 包：[Publishing npm packages](https://docs.npmjs.com/getting-started/publishing-npm-packages)
* NPM-Developers 指南：[npm-developers](https://docs.npmjs.com/misc/developers)
* 请注意版本号如何更新，遵守行业原则：[Semantic versioning and npm](https://docs.npmjs.com/getting-started/semantic-versioning)
