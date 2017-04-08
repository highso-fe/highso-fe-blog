移动 Web 项目前端脚手架
===

> 2017-04-02 发布，最后更新于 2017-04-05

[脚手架项目](https://github.com/AnHongpeng/mobile-web-case/tree/master/staging)

## 对 HTML 的设置

* `<!DOCTYPE html>` 设置正确的浏览器渲染模式
* `<html lang="zh-cmn-Hans">` 设置页面内容的语言为简体中文；`<html lang="zh-cmn-Hant">` 为繁体中文；`<html lang="en">` 为英文。[这么写的原因](https://www.zhihu.com/question/20797118)
* `<meta charset="UTF-8">` 设置编码格式为 UTF-8
* `<meta name="format-detection" content="telephone=no" />` 当该 HTML 页面在手机上浏览时，该标签用于指定是否将网页内容中的手机号码显示为拨号的超链接，iPhone 上默认 `telephone` 设置为 yes
* `<meta name="format-detection" content="email=no" />` 忽略 Android 平台中对邮箱地址的识别
* `<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">` 详情使用参考 [MDN-在移动浏览器中使用 viewport 元标签控制布局](https://developer.mozilla.org/zh-CN/docs/Mobile/Viewport_meta_tag)
* `<link rel="icon" href="**/*.*" />` 设置 icon

## 浏览器重置样式设置

[reset.css](https://github.com/AnHongpeng/mobile-web-case/blob/master/staging/css/reset.css)

**1.可重置点击链接时出现的高亮颜色及 outline**

```css
        * {
          outline: 0;
          -webkit-tap-highlight-color: transparent;
        }
```

参考 [-webkit-tap-highlight-color](https://developer.mozilla.org/zh-CN/docs/Web/CSS/-webkit-tap-highlight-color)

**2.text-size-adjust**

```css
        html {
          -webkit-text-size-adjust: 100%;
          -moz-text-size-adjust: 100%;
          -ms-text-size-adjust: 100%;
        }
```

参考 [text-size-adjust](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-size-adjust)

**3.大屏幕下 body 水平居中**

```css
        body {
          margin: 0 auto;
          padding: 0;
          max-width: 540px;
        }
```

**4.设置图片无法被选中**

```css
        img {
          -webkit-user-select: none;
          -moz-user-select: none;
          -ms-user-select: none;
        }
```

参考 [user-select](https://developer.mozilla.org/zh-CN/docs/Web/CSS/user-select)

## 公有样式设置

[style.css](https://github.com/AnHongpeng/mobile-web-case/blob/master/staging/css/style.css)

**1.使用面向属性的 CSS**

```css
        .fs12 {
          font-size: 12px;
        }
        .fs14 {
          font-size: 14px;
        }
        .fw200 {
          font-weight: 200;
        }
        .fw600 {
          font-weight: 600;
        }
```

**2.clearfix 清除浮动**

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

**3.0.5px 边框实现**

```css
        .bd0_5 {
          position: relative;
        }
        .bd0_5:before {
          content: '';
          position: absolute;
          top: 0;
          left: 0;
          width: 200%;
          height: 200%;
          box-sizing: border-box;
          border: 1px solid transparent;
          transform-origin: left top;
          transform: scale(0.5);
          z-index: -1;
        }
```

**4.遮罩层样式**

```css
        .shade {
          display: none;
          position: absolute;
          top: 0;
          left: 0;
          min-width: 100%;
          min-height:100%;
          background: rgba(0, 0, 0, 0.7);
          z-index: 800;
        }
```

**5.人民币符号**

```css
        .rmb:before {
          content: '￥';
          vertical-align: baseline;
        }
```

## 集成手淘 rem 方案

* [可伸缩布局方案](https://github.com/amfe/lib-flexible)
* [使用 Flexible 实现手淘 H5 页面的终端适配](https://github.com/amfe/article/issues/17)
* [flexible.js 源码](https://github.com/amfe/lib-flexible/blob/master/src/flexible.js)

阅读源码可以知道，如果我们设置了 viewport 元数据，那么 dpr = 1 / scale；如果手动设置 flexible，则 dpr 取决于设置值；如果两者都不设置，那么 flexible.js 会根据 IOS/Android 平台去动态生成 meta 标签并设置 dpr（此时 dpr 值可能为 1~3）及缩放比例。

建议使用修改源码后的 [rem.js](https://github.com/AnHongpeng/mobile-web-case/blob/master/lib/rem.js)，设置 viewport 视口，在锁定缩放比例的同时，还可以使用 `<html data-dpr="1~3">` 提供的 class 过滤功能。
