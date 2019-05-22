---
title: interview-js
date: 2019-05-22 16:38:02
tags:
  - javascript
  - 技术
  - 面试
  - 笔记
categories: 笔记
type: 'categories'
---

> imooc 的 javascript 笔记

<!--more-->

# 原型规则和示例

- 所有的引用类型（数组、对象、函数），都具有对象特性，即可自由扩展属性（除了“null”以外）
- 所有的引用类型（数组、对象、函数），都有一个 ** proto ** (隐式原型)属性，属性值是一个普通的对象
- 所有的函数，都有一个 prototype(显示原型)属性，属性值也是一个普通对象
- 所有的引用类型（数组、对象、函数），** proto ** (隐式原型)属性值指向它的构造函数的“prototype”(显示类型)属性值 **obj. ** porto ** === Object.prototype**
- 当试图得到一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的 ** proto **(即它的构造函数的 prototype)中寻找

# 作用域和闭包

执行上下文

this

作用域

作用域链

闭包

## 执行上下文

范围：一段 < script > 或者一个函数

全局：变量定义、函数声明

函数：变量定义、函数声明、this、arguments

Ps：函数声明 和 函数表达式 的区别

## this

this 要执行时才能确认值，定义时无法确认

```javascript
var a = {
  name: 'A',
  fn: function() {
    console.log(this.name)
  }
}
a.fn() // this === a
a.fn.call({ name: 'B' }) // this === {name: 'B'}
var fn1 = a.fn
fn1() // this === window
```

- 作为构造函数执行
- 作为对象属性执行
- 作为普通函数执行
- call apply bind

```javascript
function Foo(name) {
  this.name = name
}
var f = new Foo('zhangsan')
```

```javascript
var obj = {
  name: 'A',
  printName: function() {
    console.log(this.name)
  }
}
obj.printName() // this === obj
```

```javascript
function fn() {
  console.log(this) // this === window
}
fn()
```

```javascript
// call apply bind
function fn1(name, age) {
  alert(name)
  console.log(this)
}
fn1.call({ x: 100 }, 'zhangsan', 20) // this === {x:100}
fn1.apply({ x: 100 }, ['zhangsan', 20])

var fn2 = function(name, age) {
  alert(name)
  console.log(this)
}.bind({ y: 200 })
fn2('zhangsan', 20)
```

作用域

- 没有块级作用域

- 只有函数和全局作用域

  ​

```javascript
// 无块级作用域
if (true) {
  var name = 'zhangsan'
}
console.log(name)

// 函数和全局作用域
var a = 100
function fn() {
  var a = 200
  console.log('fn', a)
}
console.log('global', a)
fn()
```

作用域链

```javascript
var a = 100
function fn() {
  var b = 200

  // 当前作用域没有定义的变量，即“自由变量”
  console.log(a)
  console.log(b)
}
fn()
```

```javascript
var a = 100
function F1() {
  var b = 200
  function F2() {
    var c = 300
    console.log(a) // a是自由变量
    console.log(b) // b是自由变量
    console.log(c)
  }
  F2()
}
F1()
```

## 闭包的使用场景

- 函数作为返回值
- 函数作为参数传递

```javascript
function F1() {
  var a = 100
  // 返回一个函数(函数作为返回值)
  return function() {
    console.log(a) // 自由变量，父级作用域寻找
  }
}
// f1 得到一个函数
var f1 = F1()
var a = 200
f1()

// 1.函数作为返回值 ↑
// 2.函数作为参数来传递 ↓
function F1() {
  var a = 100
  return function() {
    console.log(a)
  }
}
var f1 = F1()
function F2(fn) {
  var a = 200
  fn()
}
F2(f1)
```

### 创建 10 个<a>标签，点击的时候弹出对应的序号

```javascript
var i
for (i = 0; i < 10; i++) {
  ;(function(i) {
    var a = document.createElement('a')
    a.innerHTML = i + '<br>'
    a.addEventListener('click', function(e) {
      e.preventDefault()
      alert(i)
    })
    document.body.appendChild(a)
  })(i)
}
```

### 闭包的应用

```javascript
// 闭包实际开发中主要用于封装变量，收敛权限
function isFirstLoad() {
  var _list = []
  return function(id) {
    if (_list.indexOf(id) >= 0) {
      return false
    } else {
      _list.push(id)
      return true
    }
  }
}
// 使用  判断是否第一次
var firstLoad = isFirstLoad()
firstLoad(10) // true
firstLoad(10) // false
firstLoad(20) // true
```

# 异步和单线程

## 同步和异步的区别是什么

同步会阻塞代码执行，而异步不会

alert 是同步，setTimeout 是异步

## 前端使用异步的场景有哪些

定时任务：setTimeout、setInterval

网络请求：ajax 请求，动态<img>加载

事件绑定

# 日期

```javascript
Date.now() // 获取当前时间毫秒数
var dt = new Date()
dt.getTime() // 获取毫秒数
dt.getFullYear() // 年
dt.getMonth() // 月(0-11)
dt.getDate() // 日(1-31)
dt.getHours() // 小时(0-23)
dt.getMinutes() // 分钟(0-59)
dt.getSeconds() // 秒(0-59)
```

# 数组 API

## forEach

```javascript
var arr = [1, 2, 3]
arr.forEach(function(item, index) {
  //  遍历数组的所有元素
  console.log(index, item)
})
```

## every

```javascript
var arr = [1, 2, 3]
var result = arr.every(function(item, index) {
  // 用来判断所有的数组元素，都满足一个条件
  if (item < 4) {
    return true
  }
})
console.log(result)
```

## some

```javascript
var arr = [1, 2, 3]
var result = arr.some(function(item, index) {
  // 用来判断只要有一个数组元素满足条件
  if (item < 1) {
    return true
  }
})
console.log(result)
```

## sort

```javascript
var arr = [1, 3, 2, 3, 5]
var arr2 = arr.sort(function(a, b) {
  // 从小到大排序
  return a - b
  // 从大到小排序
  // return b - a
})
console.log(arr)
console.log(arr2)
```

## map

```javascript
var arr = [1, 2, 3, 4]
var arr2 = arr.map(function(item, index) {
  // 将元素重新组装，并返回
  return '<b>' + item + '</b>'
})
console.log(arr2)
```

## filter

```javascript
var arr = [1, 2, 3]
var arr2 = arr.filter(function(item, index) {
  // 通过某一个条件过滤数组
  if (item >= 2) {
    return true
  }
})
console.log(arr2)
```

# 对象 API

```javascript
var obj = {
  x: 100,
  y: 200,
  z: 300
}
var key
for (key in obj) {
  if (obj.hasOwnProperty(key)) {
    console.log(key, obj[key])
  }
}
```

**获取随机数，要求是长度一致的字符串格式**

```javascript
var random = Math.random()
var random = random + '0000000000' // 后面加上10个零
var random = random.slice(0, 10)
console.log(random)
```

**一个能遍历对象和数组的 forEach 函数**

```javascript
// 自定义forEach
function forEach(obj, fn) {
  var key
  if (obj instanceof Array) {
    obj.forEach(function(item, index) {
      fn(index, item)
    })
  } else {
    for (key in obj) {
      if (obj.hasOwnProperty(key)) {
        fn(key, obj[key])
      }
    }
  }
}
// 使用forEach
// 遍历数组
var arr = [1, 2, 3]
// 注意,这里参数的位置顺序换了，为了和对象遍历格式一致
forEach(arr, function(index, item) {
  console.log(index, item)
})
// 遍历对象
var obj = { x: 100, y: 200 }
forEach(obj, function(key, value) {
  console.log(key, value)
})
```

# DOM

## 获取 DOM 节点

```javascript
var div1 = document.getElementById('div1') //元素
var divList = document.getElementsByTagName('div') // 集合

var containerList = document.getElementByClassName('.container') // 集合
var pList = document.querySelectorAll('p') // 集合
```

## property

```javascript
var obj = { x: 100, y: 200 }
console.log(obj.x) // 100

var p = document.getElementsByTagName('p')[0]
console.log(p.nodeName) // P
```

## Attribute

```javascript
var pList = document.querySelectorAll('p')
var p = pList[0]
p.getAttribute('data-name')
p.setAttribute('data-name', 'imooc')
p.getAttribute('style')
p.setAttribute('style', 'font-size:30px')
```

property 只是一个 js 对象的属性的修改

Attribute 是对 HTML 标签属性的修改

## 新增节点

```javascript
var div1 = document.getElementById('div1')
// 添加新节点
var p1 = document.createElement('p')
p1.innerHTML = 'this is p1'
div1.appendChild(p1) // 添加新创建的元素
// 移动已有节点
var p2 = document.getElementById('p2')
div1.appendChild(p2)
```

## 获取父元素和子元素

```javascript
var div1 = document.getElementById('div1')
var parent = div1.parentElement

var child = div1.childNodes
```

## 删除节点

```javascript
var div1 = document.getElementById('div1')
var child = div1.childNodes
div1.removeChild(child[0])
```

# BOM

## navigator & screen

```javascript
// navigator
var ua = navigator.userAgent
var isChrome = ua.indexOf('Chrome')
console.log(isChrome)

// screen
console.log(screen.width)
console.log(screen.height)
```

## location & history

```javascript
// location
console.log(location.href)
console.log(location.protocol) // 'http:' 'https:'
console.log(location.host) //  域名
console.log(location.pathname) // '/learn/199'
console.log(location.search) // '?a=xxx'
console.log(location.hash) // '#...'

// history
history.back()
history.forward()
```

# 事件

## 通用事件绑定

```javascript
var btn = document.getElementById('btn1')
btn.addEventListener('click', function(event) {
  console.log('clicked')
})

function bindEvent(elem, type, fn) {
  elem.addEventListener(type, fn)
}
var a = document.getElementById('link1')
bindEvent(a, 'click', function(e) {
  e.preventDefault() //阻止默认行为
  alert('clicked')
})
```

关于 IE 低版本的兼容性

IE 低版本使用 attachEvent 绑定事件，和 W3C 标准不一样

IE 低版本使用量已非常少，很多网站都早已不支持

## 代理

```html
<div id="div1">
  <a href="#">a1</a>
  <a href="#">a2</a>
  <a href="#">a3</a>
  <!-- 会随时新增更多a标签 -->
</div>

<script>
  var div1 = document.getElementById('div1')
  div1.addEventListener('click', function(e) {
    var target = e.target
    if (target.nodeName === 'A') {
      alert(target.innerHTML)
    }
  })
</script>
```

## 完善通用绑定事件的函数

```javascript
function bindEvent(elem, type, selector, fn) {
  if (fn == null) {
    fn = selector
    selector = null
  }
  elem.addEventListener(type, function(e) {
    var target
    // 代理
    if (selector) {
      target = e.target
      if (target.matches(selector)) {
        fn.call(target, e)
      }
    } else {
      // 不是代理
      fn(e)
    }
  })
}

// 使用代理
var div1 = document.getElementById('div1')
bindEvent(div1, 'click', 'a', function(e) {
  console.log(this.innerHTML)
})

// 不使用代理
var a = document.getElementById('a1')
bindEvent(div1, 'click', function(e) {
  console.log(a.innerHTML)
})
```

# Ajax

## XMLHttpRequest

```javascript
var xhr = new XMLHttpRequest()
Xhr.open('GET', '/api', false) // false指异步
Xhr.onreadystatechange = function() {
  // 这里的函数异步执行
  if (xhr.readyState == 4) {
    if (xhr.status == 200) {
      console.log(xhr.responseText)
    }
  }
}
xhr.send(null)
```

IE 低版本使用 ActiveXObject

## readyState

0 - (未初始化) 还没用调用 send()方法

1 - (载入) 已调用 send()方法，正在发送请求

2 - (载入完成) send()方法执行完成，已经接收到全部响应内容

3 - (交互) 正在解析响应内容

4 - (完成) 响应内容解析完成，可以在客户端调用了

## status

2xx - 表示成功处理请求。 如 200

3xx - 需要重定向，浏览器直接跳转

4xx - 客户端请求错误，如 404

5xx - 服务端错误

# 跨域

浏览器有同源策略，不允许 ajax 访问其他域接口

跨域条件：协议、域名、端口，有一个不同就算跨域

## 允许跨域的三个标签

img

link

script

<img> 用于打点统计，统计网站可能是其他域

<link><script> 可以使用CDN,CDN的也是其他域

<script>可以用于JSONP



## 跨域注意事项

所有的跨域请求都必须经过信息提供方允许

如果未经允许即可获取，那是浏览器同源策略出现漏洞



## JSONP实现原理

加载http://coding.m.imooc.com/classindex.html

不一定服务器端存在一个classindex.html文件

服务器跨域根据请求，动态生成一个文件，返回

同理于 <script src="http://coding.m.imooc.com/api.js">



例如你的网站要跨域访问慕课网的一个接口

慕课给你一个地址http://coding.m.imooc.com/api.js

返回内容格式如 callback({x:100,y:200}) (可动态生成)

```javascript
window.callback = function(data) {
    // 这是我们跨域得到的信息
  	console.log(data)
}
<script src="http://coding.m.imooc.com/api.js"></script>
<!-- 以上将返回 callback({x:100,y:200}) -->

````



# 存储

描述一下cookie,sessionStorage和localStorage的区别

## cookie

本身用于客户端和服务器端通信

但是它有本地存储的功能，于是就被“借用”

使用document.cookie = … 获取和修改



**cookie用于存储的缺点**

存储量太小，只有4KB

所有http请求都带有，会影响获取资源的效率

API简单，需要封装才能用 document.cookie = ...



## sessionStorage和localStorage的

HTML5专门为存储而设计，最大容量5M

API简答易用

localStorage.setItem(key, value); localStorage.getItem(key)







# 页面加载

## 加载一个资源的过程

浏览器根据DNS服务器得到域名的IP地址

向这个IP的机器发送http(或https)请求

服务器收到、处理并返回http(或https)请求

浏览器得到返回内容

## 浏览器渲染页面的过程

根据HTML结果生成DOM Tree

根据CSS生成CSSOM

将DOM和CSSOM整合成RenderTree

根据RenderTree开始渲染和展示

遇到<script>时，会执行并阻塞渲染



## window.onload 和 DOMContentLoaded

```javascript
window.addEventListener('load',function () {
    // 页面的全部资源加载完才会执行，包括图片、视频等
})
document.addEventListener('DOMContentLoaded', function () {
    // DOM渲染完即可执行，此时图片、视频还可能没有加载完
})
````

# 性能优化

**原则**

多使用内存、缓存或者其他方法

减少 CPU 计算、减少网络请求

**从哪里入手**

加载页面和静态资源

页面渲染

**加载资源优化**

静态资源的压缩合并

静态资源缓存

使用 CDN 让资源加载更快

使用 SSR 后端渲染，数据直接输出到 HTML 中

**渲染优化**

CSS 放前面、JS 放后面

懒加载(图片懒加载、下拉加载更多)

减少 DOM 查询，对 DOM 查询做缓存

减少 DOM 操作，多个操作尽量合并在一起执行

事件节流

尽早执行操作（如 DOMContentLoaded）

## 缓存 DOM 查询

```javascript
// 未缓存DOM查询
var i
for (i = 0; i < document.getElementByTagName('p').length; i++) {
  // todo
}

// 缓存了DOM查询
var pList = document.getElementByTagName('p')
var i
for (i = 0; i < pList.length; i++) {
  //todo
}
```

## 合并 DOM 插入

```javascript
var listNode = document.getElementById('list')

// 要插入 10 个 li 标签
var frag = document.createDocumentFragment()
var x, li
for (x = 0; x < 10; x++) {
  li = document.createElement('li')
  li.innerHTML = 'List item' + x
  frag.appendChild(li)
}
listNode.appendChild(frag)
```

## 事件节流

```javascript
var textarea = document.getElementById('text')
var timeoutId
textarea.addEventListener('keyup', function() {
  if (timeoutId) {
    clearTimeout(timeoutId)
  }
  timeoutId = setTimeout(function() {
    // 触发 change 事件
  }, 100)
})
```

## 尽早操作

```javascript
window.addEventListener('load', function() {
  // 页面的全部资源加载完才会执行，包括图片、视频等
})
document.addEventListener('DOMContentLoaded', function() {
  // DOM渲染完即可执行，此时图片、视频还可能没有加载完
})
```

# 安全性

XSS 跨站请求攻击

XSRF 跨站请求伪造
