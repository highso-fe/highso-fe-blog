移动 Web 前端基础解决方案汇总
===

> 2017-04-01 发布，最后更新于 2017-04-01

## 对 HTML 的设置

* `<!DOCTYPE html>` 设置正确的浏览器渲染模式
* `<html lang="zh-cmn-Hans">` 设置页面内容的语言为简体中文；`<html lang="zh-cmn-Hant">` 为繁体中文；`<html lang="en">` 为英文。[这么写的原因](https://www.zhihu.com/question/20797118)
* `<meta charset="UTF-8">` 设置编码格式为 UTF-8
* `<meta name="format-detection" content="telephone=no" />` 当该 HTML 页面在手机上浏览时，该标签用于指定是否将网页内容中的手机号码显示为拨号的超链接，iPhone 上默认 `telephone` 设置为 yes
* `<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">` 详情使用参考 [MDN-在移动浏览器中使用 viewport 元标签控制布局](https://developer.mozilla.org/zh-CN/docs/Mobile/Viewport_meta_tag)
* `<link rel="icon" href="**/*.*" />` 设置 icon

## 浏览器重置样式设置

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
          font-weight: 
        }
        ...
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

**3.遮罩层样式**

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

**4.人民币符号**

```css
        .rmb:before {
          content: '￥';
          font-family: Arial;
          vertical-align: baseline;
        }
```
