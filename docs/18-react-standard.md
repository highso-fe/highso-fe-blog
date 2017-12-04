嗨学网 react 开发规范
===

> 2017-12-04

## 项目结构

采用Ducks对新的Redux项目结构的提议，它提倡将相关联的reducer、action types和action写到一个文件里。但是我们为了区分action以及reducer，不完全采用这种方式。 以下是基于Ducks提议整理出来适用于嗨学项目的目录结构：
```       
  components/ (应用级别通用组件)
    SiderBar/ (采用大驼峰命名 或者 sider-bar(短横线命名))
      index.css
      index.js

  constants/ (常量)

  containers/  （容器）
    Feature1/  （采用大驼峰命名）
      components/  (功能拆分出的专用组件)
      index.css
      index.js    (feature1对外暴露的接口)

  libs/
    api/   (fetch/) (请求后台数据)
      user.js
      home.js
    utils/ (工具函数)
      func.js

  redux/
    actions/
      user.js
      home.js
    reducers/
      user.js
      home.js
    reducer.js
    store.js

  router/ (路由文件)

  static/ (静态资源)
    css/ (公有样式)
    iconfont/ (放字体图标)
    images/ (图片)
    ...

  index.js (入口文件)
  index.html (html模板)
```

## JSX

#### 一、语法

* 用两个空格来代替制表符（tab）
* 嵌套元素应当缩进一次（即两个空格）
* 对于属性的定义，确保全部使用双引号，不要使用单引号

#### 二、注释

*注释是为了解释当前代码做了什么，而不是怎么做的*

* 函数注释应该指出参数，必要时可指出返回值
* 复杂逻辑应该详细写出每行代码做了什么
* **当代码更新时，注释一定要更新**

#### 三、函数命名
###### 命名能够在语义上体现返回值或者函数操作，如：

* 返回值为 boolean 类型，则命名应有 is、has、should 等
* 返回值为 React Node 则命名应有 render
* 函数进行 fetch 请求，则命名应有 get、post 等

###### 命名能够自注释
```
// bad
const fetchUser = (id) => (
  fetch(buildUri`/users/${id}`) // Get User DTO record from REST API
    .then(convertFormat) // Convert to snakeCase
    .then(validateUser) // Make sure the the user is valid
); 

// better
const fetchUser = (id) => (
  fetch(buildUri`/users/${id}`)
    .then(snakeToCamelCase)
    .then(validateUser)
); 
```

###### 避免命名过分自注释（命名应体现做了什么，而不是怎么做的）如：
```
// bad
const getConfigFromServer = () => {
    ...
};

// better
const getConfig = () => {
    ...
};
```

#### 四、其他细节

* 函数抽离：当一段逻辑重复三次及以上时，应抽离出一个函数去复用这段逻辑（注意不要过分抽离）
* 代码编写应符合嗨学 eslint 规范