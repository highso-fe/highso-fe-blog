FED-share03
===

> 2017-10-10 发布，最后更新于 2017-10-10

为解决服务端同学对于jq代码了解 [api](http://jquery.cuishifeng.cn/) 但不会使用，或者特殊情况不知道怎么处理的情况。我们整理了一些常用的实例，希望能够提高服务端同学在工作中处理前端代码的能力。

## （一） $.ajax及延迟对象的使用

#### 1. ajax api

    $.ajax({
        url: '/path/to/file',
        type: 'default GET (Other values: POST)',
        headers: {'Content-Type': 'text/plain; charset=utf-8'}
        async: 'default: true(Other values: false)'
        dataType: 'default: Intelligent Guess (Other values: xml, json, script, html, jsonp, or text)',
        data: {param1: 'value1'},
        success: function(res) {
            console.log(res);
        },
        error: function(e) {
            console.log(e);
        },
        complete: function() {
            console.log('complete');
        }
    })

###### headers(Object): 

默认:{}。用于设置 ajax 请求头，常用配置项：

"Access-Token": 验证用户登录。

"Content-Type": 告诉服务器传输的数据是什么格式，字符编码可不带，对大小写不敏感，但建议都保持小写。可用值：

1. text: 'text/plain; charset=utf-8' (默认值)
2. json: 'application/json; charset=utf-8'
3. html: 'text/html; charset=utf-8'
4. form: 'application/x-www-form-urlencoded; charset=utf-8'

###### async(Boolean):

默认设置下，所有请求均为异步请求(true)。如果需要发送同步请求，请将此选项设置为 false。注意，同步请求将锁住浏览器，用户其它操作必须等待请求完成才可以执行。

###### dataType(string):

预期服务器返回的数据类型。如果不指定，jQuery 将自动根据 HTTP 包 MIME 信息来智能判断，比如XML MIME类型就被识别为XML。在1.4中，JSON就会生成一个JavaScript对象，而script则会执行这个脚本。随后服务器端返回的数据会根据这个值解析后，传递给回调函数。可用值:

1. "xml": 返回 XML 文档，可用 jQuery 处理。(设置 processData 选项为 false，防止自动转换数据格式。)
2. "html": 返回纯文本 HTML 信息；包含的script标签会在插入dom时执行。
3. "script": 返回纯文本 JavaScript 代码。不会自动缓存结果。除非设置了"cache"参数。'''注意：'''在远程请求时(不在同一个域下)，所有POST请求都将转为GET请求。(因为将使用DOM的script标签来加载)
4. "json": 返回 JSON 数据 。
5. "jsonp": JSONP 格式。使用 JSONP 形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数。
6. "text": 返回纯文本字符串

#### 2. 延迟对象

#### 3. 使用延迟对象的 ajax 请求

    $.ajax({
        url: '/path/to/file',
        type: 'default GET (Other values: POST)',
        dataType: 'default: Intelligent Guess (Other values: xml, json, script, html, jsonp, or text)',
        data: {param1: 'value1'}
    })
    .done(function(res) {
        console.log("success");
    })
    .fail(function(e) {
        console.log("error");
    })
    .always(function() {
        console.log("complete");
    });

## （二） 事件委派

## （三） 模块化