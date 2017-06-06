嗨学网前端自动化构建
===

> 发布于 2017-03-17， 最后更新于 2017-06-02

> 使用基于文件流操作的 [gulp](http://www.gulpjs.com.cn/) 作为前端自动化构建工具。

## 核心模块

#### 编译

* [gulp-less](https://github.com/plus3network/gulp-less) - 编译 [less](https://github.com/less/less.js) 为 CSS

#### 压缩

* [gulp-htmlmin](https://github.com/jonschlinkert/gulp-htmlmin) - 压缩 HTML 通过 [HTMLMinifier](https://github.com/kangax/html-minifier)
* [gulp-clean-css](https://github.com/scniro/gulp-clean-css) - 压缩 CSS 通过 [clean-css](https://github.com/jakubpawlowicz/clean-css)
* [gulp-uglify](https://github.com/terinjokes/gulp-uglify) - 压缩 JS 通过 [UglifyJS2](https://github.com/mishoo/UglifyJS2)
* [gulp-imagemin](https://github.com/sindresorhus/gulp-imagemin) - 压缩 PNG, JPEG, GIF and SVG 图片通过 [imagemin](https://github.com/imagemin/imagemin)
* [gulp-sourcemaps](https://github.com/floridoo/gulp-sourcemaps) - 提供 source map 支持

#### 图片处理

* [gulp.spritesmith](https://github.com/twolfson/gulp.spritesmith) - 生成 CSS 雪碧图
* [gulp.spritesmith-multi](https://github.com/reducejs/gulp.spritesmith-multi) - 封装 gulp.spritesmith 生成多个雪碧图及 CSS

#### 静态资源版本修订

* [gulp-rev](https://github.com/sindresorhus/gulp-rev) - 在静态文件名的后面添加hash值来进行版本修订
* [gulp-rev-css-url](https://github.com/galkinrost/gulp-rev-css-url) - 重写经 gulp-rev 哈希校验修订后的 CSS 文件中的 url
* [gulp-rev-delete-original](https://github.com/nib-health-funds/gulp-rev-delete-original) - 删除经 gulp-rev 或 gulp-rev-all 重写的源文件
* [gulp-rev-collector](https://github.com/shonny-ua/gulp-rev-collector) - 从 manifests 中收集版本修订信息，替换模板中的链接

#### 代码质量检测

* [gulp-jshint](https://github.com/spalger/gulp-jshint) - js 代码质量检测通过 [jshint](http://jshint.com/)，配置项见 [JSHint Options](http://jshint.com/docs/options/#enforcing-options)
* [jshint-stylish](https://github.com/sindresorhus/jshint-stylish) - 时髦的 JSHint 报告器

#### 实时加载

* [browser-sync](https://github.com/browsersync/browser-sync) - 保证多个浏览器或设备网页同步显示([recipes](https://github.com/BrowserSync/gulp-browser-sync))，配合 gulp 请参考 [Browsersync + Gulp.js](https://browsersync.io/docs/gulp)

#### 流控制

* [gulp-if](https://github.com/robrich/gulp-if) - 按照条件运行 task
* [run-sequence](https://github.com/OverZealous/run-sequence) - 指定 task 运行顺序
* [merge-stream](https://github.com/grncdr/merge-stream) - 合并多个流到一个插入的流
* [vinyl-buffer ](https://github.com/hughsk/vinyl-buffer) - 缓冲文件流
* [pump](https://github.com/mafintosh/pump) - pipes streams together and destroys all of them if one of them closes.
* [del](https://github.com/sindresorhus/del) - 使用 [globs](https://github.com/isaacs/node-glob) 删除文件/文件夹.

## 其他参考资源

1. [Why Use Pump?](https://github.com/terinjokes/gulp-uglify/blob/master/docs/why-use-pump/README.md#why-use-pump)
