嗨学网前端自动化构构建
===

> 2017-03-14

> 使用 [gulp](http://www.gulpjs.com.cn/) 作为前端自动化构建工具

## 核心模块

#### 压缩

* [gulp-htmlmin](https://github.com/jonschlinkert/gulp-htmlmin) - 压缩 HTML 通过 [HTMLMinifier](https://github.com/kangax/html-minifier)
* [gulp-clean-css](https://github.com/scniro/gulp-clean-css) - 压缩 CSS 通过 [clean-css](https://github.com/jakubpawlowicz/clean-css)
* [gulp-uglify](https://github.com/terinjokes/gulp-uglify) - 压缩 JS 通过 [UglifyJS2](https://github.com/mishoo/UglifyJS2)
* [gulp-imagemin](https://github.com/sindresorhus/gulp-imagemin) - 压缩 PNG, JPEG, GIF and SVG 图片通过 [imagemin](https://github.com/imagemin/imagemin)
* [gulp-rev-collector](https://github.com/shonny-ua/gulp-rev-collector) - 从 manifests 中收集版本修订信息，替换模板中的链接

#### 静态资源版本修订

* [gulp-rev](https://github.com/sindresorhus/gulp-rev) - 在静态文件名的后面添加hash值来进行版本修订
* [gulp-rev-css-url](https://github.com/galkinrost/gulp-rev-css-url) - 重写经 gulp-rev 哈希校验修订后的 CSS 文件中的 url
* [gulp-rev-delete-original](https://github.com/nib-health-funds/gulp-rev-delete-original) - 删除经 gulp-rev 或 gulp-rev-all 重写的源文件

#### 流控制

* [run-sequence](https://github.com/OverZealous/run-sequence) - 指定 task 运行顺序
* [pump](https://github.com/mafintosh/pump) - pipes streams together and destroys all of them if one of them closes.
* [del](https://github.com/sindresorhus/del) - 使用 [globs](https://github.com/isaacs/node-glob) 删除文件/文件夹.

## 其他参考资源

1. [Why Use Pump?](https://github.com/terinjokes/gulp-uglify/blob/master/docs/why-use-pump/README.md#why-use-pump)
