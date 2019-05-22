---
title: interview
date: 2019-05-22 16:29:49
tags:
  - javascript
  - 技术
  - 面试
  - 笔记
categories: 笔记
type: 'categories'
---

> imooc 面试笔记

<!--more-->

# DOM 事件

基本概念：DOM 事件级别

DOM 事件级别

DOM 事件流

描述 DOM 事件捕获的具体流程

Event 对象的常用应用

自定义事件

## DOM 事件类 事件级别

DOM0 element.onclick=function(){}

DOM2 element.addEventListener('click',function(){},false)

DOM3 element.addEventListener('keyup',function(){},false)

## DOM 事件模型

事件模型

​ 捕获 ↓ 冒泡 ↑

## DOM 事件流

三阶段

捕获->目标阶段->冒泡

## 描述 DOM 事件捕获的具体流程

window->

​ document->

​ html->

​ body->

​ ….

​ 目标元素

```javascript
var ev = document.getElementById('ev')

window.addEventListener(
  'click',
  function(e) {
    console.log('window captrue')
  },
  true
)

document.addEventListener(
  'click',
  function(e) {
    console.log('document captrue')
  },
  true
)

document.documentElement.addEventListener(
  'click',
  function(e) {
    console.log('html captrue')
  },
  true
)

document.body.addEventListener(
  'click',
  function(e) {
    console.log('body captrue')
  },
  true
)

ev.addEventListener(
  'click',
  function(e) {
    console.log('ev captrue')
  },
  true
)
```

## Event 对象的常用应用

event.preventDefault() //阻止默认行为

Event.stopPropagation() //阻止冒泡行为

Event.stopImmediatePropagation()

​ //同一元素绑定两个点击事件 A 和 B 在事件 A 中使用该事件 Event.stopImmediatePropagation()可以阻止事件 B 的触发

Event.currentTarget //当前绑定的事件

Event.target //当前被点击的元素

## 自定义事件

```Javascript
var eve = new Event('custome');
el.addEventListener('custome',function(){
  console.log('custome');
});
el.dispatchEvent(eve)
```

CustomEvent 可以添加参数

# HTTP 协议类

HTTP 协议的主要特点

HTTP 报文的组成部分

HTTP 方法

POST 和 GET 的区别

HTTP 状态码

什么是持久链接

什么是管线化

## HTTP 协议的主要特点

### 简单快速

​ 每个资源(URI)都是固定的

### 灵活

​ 通过头部分，一个 HTTP 协议可以完成不同数据类型的传输

### 无连接

​ 连接一次，它就会断掉，不会保持连接

### 无状态

​ 单从 HTTP 协议上，是不能区分两次连接者的身份的

## HTTP 报文的组成部分

### 请求报文

​ 请求行

​ http 方法、页面地址、http 协议、版本

​ 请求头

​ 空行

​ 请求体

### 响应报文

​ 状态行

​ 响应头

​ 空行

​ 响应体

## HTTP 协议类

### HTTP 方法

​ GET 获取资源

​ POST 传输资源

​ PUT 更新资源

​ DELETE 删除资源

​ HEAD 获得报文首部

## POST 和 GET 的区别

- GET 在浏览器回退时是无害的，而 POST 会再次提交请求

- GET 产生的 URL 地址可以被收藏，而 POST 不可以

- GET 请求会被浏览器主动缓存，而 POST 不会，除非手动设置

- GET 请求只能进行 url 编码，而 POST 支持多种编码方式

- GET 请求参数会被完整保留在浏览器历史记录里，而 POST 中的参数不会被保留

- GET 请求在 URL 中传送的参数是有长度限制的，而 POST 没有限制

- 对参数的数据类型，GET 只接受 ASCII 字符，而 POST 没有限制

- GET 比 POST 更不安全，因为参数直接暴露在 URL 上，所以不能用来传递敏感信息

- GET 参数通过 URL 传递，POST 放在 Request body 中

## HTTP 状态码

1xx: 指示信息-表示请求已接受，继续处理

2xx: 成功-表示请求已被成功接受

3xx: 重定向-要完成请求必须进行更进一步的操作

4xx: 客户端错误-请求语法错误或请求无法实现

5xx: 服务器错误-服务器未能实现合法的请求

200 OK : 客户端请求成功

206 Partial Content: 客户发送了一个带有 Range 头的 GET 请求，服务器完成了它

301 Moved Permanently: 所请求的页面已经转移至新的 url

302 Found: 所请求的页面已经临时转移至新的 url

304 Not Modified: 客户端有缓存的文档并发出了一个条件性的请求，服务器告诉客户，原来缓存的文档还可以继续使用

400 Bad Request: 客户端请求有语法错误，不能被服务器所理解

401 Unauthorized: 请求未经许可，这个状态码必须和 WWW-Authenticate 报头域一起使用

403 Forbidden: 对被请求页面的访问被禁止

404 Not Found: 请求资源不存在

500 Internal Server Error: 服务器发生不可预测的错误原来缓存的文档还可以继续使用

503 Server Unavailable: 请求未完成，服务器临时过载或当机，一段时间后可能恢复正常

## 持久链接

HTTP 协议采用“请求-应答”模式，当使用普通模式，即非 Keep-Alive 模式时，每个请求/应答客户和服务器都要新建立一个连接，完成之后立即断开连接（HTTP 协议为无连接的协议）

当使用 Keep-Alive 模式(又称持久连接、连接重用)时，Keep-Alive 功能使客户端到服务器端的连接持续有效，当出现对服务器的后继请求时，Keep-Alive 功能避免了建立或重新建立连接

1.1 才支持持久连接

## 管线化

**在使用持久连接的情况下**，某个连接上消息的传递类似于

请求 1->响应 1->请求 2->响应 2->请求 3->响应 3

某个连接上的消息变成了类似这样

请求 1->请求 2->请求 3->响应 1->响应 2->响应 3

- 管线化机制通过持久连接完成，仅 HTTP/1.1 支持此技术
- 只有 GET 和 HEAD 请求可以进行管线化，而 POST 则有所限制
- 初次创建连接时不应启动管线机制，因为对方(服务器)不一定支持 HTTP/1.1 版本的协议
- 管线化不会影响响应到来的顺序，如上面的例子所示，响应返回的顺序并未改变
- HTTP/1.1 要求服务器端支持管线化，但并不要求服务器端也对响应进行管线化处理，只是要求对于管线化的请求不失败即可
- 由于上面提到的服务器端的问题，开启管线化很可能并不会带来大幅度的性能提升，而且很多服务器端和代理 程序对管线化的支持并不好，因此现代浏览器如 Chrome 和 Firefox 默认并未开启管线化支持

# 原型链类

创建对象有几种方法

原型、构造函数、实例、原型链

instanceof 的原理

new 运算符

## 创建对象的几种方法

// 字面量创建对象

var o1 = {name:'o1'}

var o11 = new Object({name:'o11'})

// 显示构造函数创建对象

var M = function(){this.name = 'o2'}

var o2 = new M();

// 通过 Object.create

var P = {name: 'o3'}

var o3 = Object.create(P)

## new 运算符

一个新对象被创建。它继承自 foo.prototype

​ ↓

构造函数 foo 被执行。执行的时候，相应的传参会被传入，同时上下文（this）会被指定为这个新实例。new foo 等同于 new foo(),只能用在不传递任何参数的情况

​ ↓

如果构造函数返回一个“对象”，那么这个对象会取代整个 new 处理的结果。如果构造函数没有返回对象，那么 new 出来的结果为步骤 1 创建的对象。

```javascript
var new2 = function(func) {
  var o = Object.create(func.prototype) //传入一个构造函数的原型对象来创建对象
  var k = func.call(o) //上下文（this）会指定为这个新实例
  if (typeof k === 'object') {
    return k
  } else {
    return o
  }
}
```

# 通信类

什么是同源策略及限制

前后端如何通信

如何创建 Ajax

跨域通信的几种方式

## 什么是同源策略及限制

同源策略限制从一个源加载的文档或脚本如何与来自另一个源的资源进行交互。

这是一个用于隔离潜在恶意文件的关键的安全机制。

- Cookie、LocalStorage 和 IndexDB 无法读取

- DOM 无法获得

- AJAX 请求不能发送

  ​

## 前后端如何通信

Ajax

WebSocket

CORS

## 如何创建 Ajax

XMLHttpRequest 对象的工作流程

兼容性处理

事件的触发条件

事件的触发顺序

## 跨域通信的几种方式

JSONP

Hash

postMessage

WebSocket

CORS

# 安全类

## CSRF

CSRF,通常称为跨站请求伪造，英文名 Cross-site request forgery

## CSRF 防御措施

Token 验证

Referer 验证

隐藏令牌

## XSS

XSS（cross-site scripting）跨域脚本攻击

# 算法类

排序

堆栈、队列、链表

递归

波兰式和逆波兰式

# 渲染机制

## 什么是 DOCTYPE 及作用

DTD(doucument type definition,文档类型定义)是一系列的语法规则，用来定义 XML 或(x)HTML 的文件类型。浏览器会使用它来判断文档类型，决定使用何种协议来解析，以及切换浏览器模式

DOCTYPE 是用来声明文档类型和 DTD 规范的，一个主要的用途便是文件的合法性验证。如果文件代码不合法，那么浏览器解析时便会出一些差错

## 浏览器渲染过程

## 重排 Reflow

**定义**

DOM 结构中的各个元素都有自己的盒子（模型），这些都需要浏览器根据各种样式来计算并根据计算结果将元素放到它该出现的位置，这个过程称之为 reflow

**触发 Reflow**

当你增加、删除、修改 DOM 节点时，会导致 Reflow 或 Repaint

当你移动 DOM 的位置，或是搞个动画的时候

当你修改 CSS 样式的时候

当你 Resize 窗口的时候（移动端没有这个问题），或是滚动的时候

当你修改网页的默认字体时

## 重绘 Repaint

**定义**

当各种盒子的位置、大小以及其他属性，例如颜色、字体大小等确定下来后，浏览器于是便把这些元素都按照各自的特性绘制一遍，于是页面的内容出现了，这个过程称之为 repaint

**触发 Repaint**

DOM 改动

CSS 改动

## 布局 Layout

# JS 运行机制

异步任务

setTimeout 和 setInterval

DOM 事件

ES6 中的 Promise

# 页面性能

提升页面性能的方法有哪些？

1、资源压缩合并，减少 HTTP 请求

2、非核心代码异步加载->异步加载的方式->异步加载的区别

3、利用浏览器缓存->缓存的分类->缓存的原理

4、使用 CDN

5、预解析 DNS

​ <meta http-equiv="x-dns-prefetch-control" content="on"> // https 中 a 链接打开 DNS 预解析

​ <link rel="dns-prefetch" href="//host_name_to_prefetch.com">

**异步加载**

1、异步加载的方式

​ 1）动态脚本加载 2）defer 3）async

2、异步加载的区别

​ 1）defer 是在 HTML 解析完之后才会执行，如果是多个，按照加载的顺序依次执行

​ 2）async 是在加载之后立即执行，如果是多个，执行顺序和加载顺序无关

**浏览器缓存**

1、缓存的分类

​ 1）强缓存

​ Expires Expires:Thu,21 Jan 2017 23:39:02 GMT

​ Cache-Control Cache-Control:max-age=3600

​ 2）协商缓存

​ Last-Modified If-Modified-Since Last-Modified:Wed,26 Jan 2017 00:35:11 GMT

​ Etag If-None-Match

# 错误监控

前端错误的分类

错误的捕获方式

上报错误的基本原理

**即时运行错误的捕获方式**

1）try…catch 2）window.onerror

**资源加载错误**

1）object.onerror 2）performance.getEntries() 3）Error 事件捕获

**延伸：跨域的 js 运行错误跨域捕获吗，错误提示什么，应该怎么处理？**

1、在 script 标签增加 crossorigin 属性

2、设置 js 资源响应头 Access-Control-Allow-Origin:\*

**上报错误的基本原理**

1、采用 Ajax 通信的方式上报

2、利用 Image 对象上报

# 业务能力

我做过什么业务？

负责的业务有什么业绩？

使用了什么技术方案？

突破了什么技术难点？

遇到了什么问题？

最大的收获是什么？

# 事物推动能力

主动描述

# 终面

1、职业竞争力

2、职业规划

## 职业竞争力

1、业务能力

2、思考能力

3、学习能力

4、无上限的付出

# 职业规划

1、目标是什么

​ 在业务上成为专家，在技术上成为行业大牛

2、近阶段的目标

​ 不断的学习积累各方面的经验，以学习为主

3、长期目标

​ 做几件很有价值的事情，如开源作品、技术框架等

4、方式方法

​ 先完成业务上的主要问题，做到极致、然后逐步向目标靠拢

# 面试技巧

1、乐观积极

2、主动沟通

3、逻辑顺畅

4、上进有责任心

5、有主张、做事果断
