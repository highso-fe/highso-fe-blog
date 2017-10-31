FED-share03
===

> 2017-10-10 发布，最后更新于 2017-10-12

虽然我们公司已经启动了前后端分离的进程，但在后台页面，以及部分前台重要旧页面的维护中，服务端同学难免需要写一些前端代码。所以为解决服务端同学对于jq代码 [了解 api](http://jquery.cuishifeng.cn/) 但不会使用，或者特殊情况不知道怎么处理的情况。我们整理了一些常用的实例，希望能够提高服务端同学在工作中处理前端代码的能力，也希望前端同学温故而知新 ^ ^。

## （一） $.ajax及延迟对象的使用

#### 1. ajax api

    $.ajax({
        url: '/path/to/file',
        type: 'default GET (Other values: POST)',
        timeout: 10000, 
        beforeSend: function(xhr) {
            xhr.setRequestHeader('Access-Token');
        },
        headers: {
            'Access-Token': $.cookie('access_token'),
            'Content-Type': 'text/plain; charset=utf-8'
        },
        async: 'default: true(Other values: false)',
        // processData: false,
        dataType: 'default: Intelligent Guess (Other values: xml, json, script, html, jsonp, or text)',
        data: {param1: 'value1'},
        success: function(res) {
            console.log(res);
        },
        error: function(xhr, statusText) {
            console.log(xhr, statusText);
        },
        complete: function() {
            console.log('complete');
        }
    })

###### timeout(Number):

单位为毫秒。默认为0，代表不会超时。当超时请求时会进入 error 函数，并在 statusText 里注明 'timeout'。

###### beforeSend(Function):

在发送请求之前调用，并且传入一个XMLHttpRequest作为参数。可进行 xhr 的配置。

###### headers(Object): 

默认:{}。用于设置 ajax 请求头，常用配置项：

1. "Access-Token": 验证用户登录。

2. "Content-Type": 告诉服务器传输的数据是什么格式，字符编码可不带，对大小写不敏感，但建议都保持小写。可用值：

    1. text: 'text/plain; charset=utf-8' (默认值)
    2. json: 'application/json; charset=utf-8'
    3. html: 'text/html; charset=utf-8'
    4. form: 'application/x-www-form-urlencoded; charset=utf-8'

###### async(Boolean):

默认设置下，所有请求均为异步请求(true)。如果需要发送同步请求，请将此选项设置为 false。注意，同步请求将锁住浏览器，用户其它操作必须等待请求完成才可以执行。

###### dataType(String):

预期服务器返回的数据类型。如果不指定，jQuery 将自动根据 HTTP 包 MIME 信息来智能判断，比如XML MIME类型就被识别为XML。在1.4中，JSON就会生成一个JavaScript对象，而script则会执行这个脚本。随后服务器端返回的数据会根据这个值解析后，传递给回调函数。可用值:

1. "xml": 返回 XML 文档，可用 jQuery 处理。(设置 processData 选项为 false，防止自动转换数据格式。)
2. "html": 返回纯文本 HTML 信息；包含的script标签会在插入dom时执行。
3. "script": 返回纯文本 JavaScript 代码。不会自动缓存结果。除非设置了"cache"参数。'''注意：'''在远程请求时(不在同一个域下)，所有POST请求都将转为GET请求。(因为将使用DOM的script标签来加载)
4. "json": 返回 JSON 数据 。
5. "jsonp": JSONP 格式。使用 JSONP 形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数。
6. "text": 返回纯文本字符串。

#### 2. 延迟对象

###### 延迟对象是什么：

延迟对象，在jquery1.5被引入，是调用jQuery.Deferred()方法生成的一个链式功用对象。它可以注册多个回调到回调队列，提取回调队列，传递任何异步或同步函数的成功或失败状态。

**简单说，deferred对象就是jQuery的回调函数解决方案。**在英语中，defer的意思是"延迟"，所以deferred对象的含义就是"延迟"到未来某个点再执行。

它解决了如何处理耗时操作的问题，对那些操作提供了更好的控制，以及统一的编程接口。

###### 为什么要引入延迟对象：

    // 回调地狱    
    $.ajax({
        url: 'some.do',
        type: 'GET',
        dataType: 'json',
        success: function(res) {
            $.ajax({
                url: 'someOther.do',
                type: 'POST',
                dataType: 'json',
                data: {name: res.name},
                success: function(res) {
                    $.ajax({
                        url: 'someEles.do',
                        type: 'POST',
                        dataType: 'json',
                        data: {age: res.age},
                        success: function(res) {
                            ...
                        }
                    });
                }
            });
        }
    });

由于回调函数是异步的，在上面的代码中每一层的回调函数都需要依赖上一层的回调执行完，所以形成了层层嵌套的关系最终形成类似上面的回调地狱，但代码以此种形式展现时无疑是不利于我们阅读与维护的，此时就要想办法改进这种代码形式。

初次改进：

     
    function postAge(data) {
        $.ajax({
            url: 'someEles.do',
            type: 'POST',
            dataType: 'json',
            data: {age: data.age},
            success: function(res) {
                ...
            },
            error: function(xhr) {
                console.log(xhr);
            }
        });
    }  
    
    function postName(data) {
        $.ajax({
            url: 'someOther.do',
            type: 'POST',
            dataType: 'json',
            data: {name: data.name},
            success: function(res) {
                postAge(res);
            },
            error: function(xhr) {
                console.log(xhr);
            }
        });
    }    
    
    $.ajax({
        url: 'some.do',
        type: 'GET',
        dataType: 'json',
        success: function(res) {
            postName(res);
        },
        error: function(xhr) {
            console.log(xhr);
        }
    });

通过 *将匿名函数命名* 写成如上形式，这样看上去就要比第一次的代码优雅清晰很多。

但这种改写方式也有缺点：

1. 命名函数太多，挤占命名空间。
2. 当代码量较多时，不易阅读当前命名函数是由哪一个请求触发的。
3. 错误处理函数多次书写，没有进行复用。

那有没有一种既能像写同步代码一样写异步代码，同时又能体现代码之间相互关系的写法呢？ jq 在这里为我们引入了 [deferred 对象](http://jquery.cuishifeng.cn/deferred.done.html)。（ES6 使用了 promise）

###### 延迟对象常用 api ：

1. def.done()：延迟成功时调用，对应 success 函数。
2. def.fail()：延迟失败时调用，对应 error 函数。
3. def.always()：不论成功失败均调用，对应 complete 函数。

###### 自定义延迟对象：

    var dtd = $.Deferred(); // 新建一个deferred对象
    
    var wait = function(def){ 
        setTimeout(function(){
            console.log("执行完毕！");  
            def.resolve(); // 改变deferred对象的执行状态
        }, 5000); 
        return def;
    };
    
    wait(dtd)
        .done(function(){ console.log("成功"); })  
        .fail(function(){ console.log("失败"); });  

以上代码执行之后，定时器中的回调函数会先打印，5s 之后再打印成功/失败。

#### 3. 使用延迟对象的 ajax 请求

    $.ajax({
        url: 'some.do',
        type: 'GET',
        dataType: 'json'
    })
    .done(function(res) {
        return $.ajax({
            url: 'someOther.do',
            type: 'POST',
            dataType: 'json',
            data: {name: res.name}
        });
    })
    .done(function(res) {
        return $.ajax({
            url: 'someElse.do',
            type: 'POST',
            dataType: 'json',
            data: {age: res.age}
        });
    })
    
    ...
    
    .fail(function(xhr) {
        console.log(xhr);
    })
    .always(function() { // always 函数会在所有异步完成后，或出现错误时触发
        console.log("complete");
    });

通过延迟对象，我们做到了：

1. 将异步代码写成了同步代码的格式，避免了多个回调嵌套。
2. 复用了错误处理函数。
3. 代码结构更加清晰，阅读性更高。

## （二） 事件委派

在后台管理页面，通常会出现这样一种业务逻辑：

1. 进入页面或翻页后获取当前页面列表条目数据。
2. 生成列表条目 dom 节点。
3. 对列表 dom 进行一些事件绑定，实现对当前条目的修改。

#### 1. 事件绑定误区
    
    $.ajax({
        url: 'getList.do',
        type: 'GET',
        dataType: 'json'
    })
    .done(function(res) {
    
        // 使用模板引擎生成 html 字符串
        var listHtml = template('list', res); 
    
        // 将字符串放到目标列表中
        $('.targetList').html(listHtml); 
    })
    .fail(function(xhr) {
        console.log(xhr);
    });
    
     // 为列表每一项绑定事件
    $('.targetListItem').on('click', function(event) {
        // do something ...
    });   

这种绑定事件的方式是不会生效的。由于 ajax 是异步代码，所以当请求发出后，代码会暂时挂起，等待同步代码执行完毕后，再来检查响应、执行回调。反映到我们上面的代码就是事件的绑定先于 dom 节点的生成，自然我们绑定的事件就不会生效了。

#### 2. 传统的事件绑定

    $.ajax({
        url: 'getList.do',
        type: 'GET',
        dataType: 'json'
    })
    .done(function(res) {
    
        // 使用模板引擎生成 html 字符串
        var listHtml = template('list', res); 
    
        // 将字符串放到目标列表中
        $('.targetList').html(listHtml); 
    
        // 为列表每一项绑定事件
        $('.targetListItem').on('click', function(event) {
            // do something ...
        });
    })
    .fail(function(xhr) {
        console.log(xhr);
    });

传统事件绑定的劣势：

1. 每次绑定均需要查询 dom。
2. 查询出的 dom 需要再次循环来绑定事件。
3. 每次翻页后需要再次执行以上两步，有大量的 dom 操作，消耗性能。

#### 3. 事件委派

###### 事件模型 （[详细介绍](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events)）：

事件冒泡（ Event Bubbling）：IE 的事件流叫做事件冒泡，即事件开始时由最具体的元素接收，然后逐级向上传播到较为不具体的节点。

事件捕获（ Event Capturing）：事件捕获的思想是不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件。

jQuery 使用冒泡系统。如果想要设置捕获，则可以调用 target.addEventListener(type, listener, useCapture Optional );

其中：

1. type：字符串，表示监听的事件类型
2. listener：监听器对象（JavaScript函数），在指定事件发生时可以收到通知
3. useCapture：布尔值，是否注册到捕获阶段

###### 什么是事件委派：

利用 事件冒泡 原理，将事件触发绑定在父级元素上，根据事件对象event.target获取到事件源，这就是事件委派。通俗的说就是：将每一个下级都要办的事交给了一个统一的上司去办。（例：采购办公用品）

###### 事件委派的优势：

1. 不需要多次查询 dom 节点。
2. 只需要绑定一次事件给父元素。
3. 翻页后只需要更新 dom，不需要再次查询并绑定，减少 dom 操作，节省大量性能。

###### 怎么使用事件委派：

方式 1：(推荐)
    
    // 为列表父元素绑定事件    
    $('.targetList').on('click', '.targetListItem', function(event){
        // do something ...
    });    
        
    $.ajax({
        url: 'getList.do',
        type: 'GET',
        dataType: 'json'
    })
    .done(function(res) {
    
        // 使用模板引擎生成 html 字符串
        var listHtml = template('list', res); 
    
        // 将字符串放到目标列表中
        $('.targetList').html(listHtml); 
    })
    .fail(function(xhr) {
        console.log(xhr);
    });

方式 2：(低版本 jq 可选方式)

使用 jq 提供的 [事件委派 api](http://jquery.cuishifeng.cn)。

## （三） 模块化

#### 1. 什么是模块化

模块化是指解决一个复杂问题时自顶向下逐层把系统划分成若干模块的过程，有多种属性，分别反映其内部特性。

#### 2. 为什么要采用模块化

随着网站逐渐变成"互联网应用程序"，嵌入网页的 Javascript 代码越来越庞大，越来越复杂。前端迫切需要一种能够实现代码管理的开发方式，于是，模块化开发就被引入到了前端中。

#### 3. 怎么使用模块化

虽然概念早就已经有了，但是 Javascript 不是一种模块化编程语言，它不支持其他语言的"类"（class），更遑论"模块"（module）了。（ECMAScript标准第六版已经正式支持"类"和"模块"了。）

Javascript 社区做了很多努力，在现有的运行环境中，实现了"模块"的效果。

###### 原始写法：

    function module1() {
        //...
    }
    
    function module2() {
        //...
    }

模块就是实现特定功能的一组方法。

只要把不同的函数（以及记录状态的变量）简单地放在一起，就算是一个模块。

###### 对象写法：

    var module1 = new Object({
        _count : 0,
        m1 : function (){
    　　　　//...
    　　},
    　　m2 : function (){
    　　　　//...
    　　}
    });

上面的函数m1()和m2(），都封装在module1对象里。使用的时候，就是调用这个对象的属性。

    module1.m1()    

但是，这样的写法会暴露所有模块成员，内部状态可以被外部改写。比如，外部代码可以直接改变内部计数器的值。

    module1._count = 7;   

###### 立即执行函数写法：

    var module1 = (function(){
    
    　　function m1() {
    　　　　//...
    　　};
    
    　　function m2() {
    　　　　//...
    　　};
    
    　　var _count = 0;
    
    　　return {
    　　　　m1 : m1,
    　　　　m2 : m2
    　　};
    })();

使用上面的写法，外部代码无法读取内部的_count变量。这种方式也是 js 模块化的基本方式。

###### 扩展模式：

    // 实现模块之间的扩展继承    
    var module1 = (function(mod){
    
    　　mod.m3 = function() {
            // ...
        }
    
    　　return mod;
    })(module1);

通过上面的代码，为 module1 添加了一个 m3 方法，并返回新的 module1 模块。

    // 加入容错机制    
    var module1 = (function(mod){
    
    　　mod.m3 = function() {
            // ...
        }
    
    　　return mod;
    })(window.module1 || {});

因为在浏览器环境中，模块各个部分通常都是从网上获取的，有时无法知道哪个部分会先加载。所以需要加入一些容错机制，形成“宽放大”。

    // 输入全局变量   
    var module1 = (function($){
    
        // ...
        
    })(jQuery);

独立性是模块的重要特点，模块内部最好不与程序的其他部分直接交互。为了在模块内部调用全局变量，必须显式地将其他变量输入模块。同时也体现了模块间的依赖关系。

###### 管理模块命名空间：

    // 常规定义
    window.module1 = (function(){
        // ...
    })();

通过显式声明模块名的方式，我们得到了一个 window 对象下的 module1。但是这种方式有可能产生命名冲突，覆盖了其他模块。

    // 集中管理
    window.live.module1 = (function(){
        // ...
    })();
    
    window.static.module1 = (function(){
        // ...
    })();

使用在模块名前加入模块分类名的方式，我们避免了不同类下同名模块之间的冲突。
 
    // 定义嵌套命名空间
    function namespace(name) {
        var parts = name.split('.'),
            crt = window,
            i;
    
        for (i = 0; i < parts.length; i++) {
            if (!crt[parts[i]]) {
                crt[parts[i]] = {};
            }
            crt = crt[parts[i]];
        }
    }
    
    namespace('static.sensitive'); // window.static.sensitive = {};

通过以上代码，我们实现了对模块命名空间的管理。

#### 4. CommonJS、AMD 规范：

###### CommonJS：

2009年，美国程序员Ryan Dahl创造了node.js项目，将javascript语言用于服务器端编程。

这标志"Javascript模块化编程"正式诞生。因为老实说，在浏览器环境下，没有模块也不是特别大的问题，毕竟网页程序的复杂性有限；但是在服务器端，一定要有模块，与操作系统和其他应用程序互动，否则根本没法编程。

node.js的模块系统，就是参照CommonJS规范实现的。在CommonJS中，有一个全局性方法require()，用于加载模块。假定有一个数学模块math.js，就可以像下面这样加载。

    var math = require('math');
    
    math.add(2, 3);

但是这种加载方式在浏览器环境有一个重大的缺陷，即当同步代码加载模块时会卡住浏览器，当网络不好时，会产生一种浏览器假死现象。因此，浏览器端的模块，不能采用"同步加载"（synchronous），只能采用"异步加载"（asynchronous）。这就是AMD规范诞生的背景。

###### AMD：

AMD是"Asynchronous Module Definition"的缩写，意思就是"异步模块定义"。它采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。

AMD也采用require()语句加载模块，但是不同于CommonJS，它要求两个参数：

    require([module], callback);

第一个参数[module]，是一个数组，里面的成员就是要加载的模块；第二个参数callback，则是加载成功之后的回调函数。如果将前面的代码改写成AMD形式，就是下面这样：

    require(['math'], function(math) {
        math.add(2, 3)
    });

math.add()与math模块加载不是同步的，浏览器不会发生假死。所以很显然，AMD比较适合浏览器环境。
目前，主要有两个Javascript库实现了AMD规范：require.js和curl.js。


