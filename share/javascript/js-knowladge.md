# Js 知识备忘录

内容整合自[阮一峰 JavaScript 教程](https://wangdoc.com/javascript/)、[阮一峰 ECMAScript 6 教程](https://es6.ruanyifeng.com/)，部分来源于 [你不知道的 JavaScript](https://github.com/getify/You-Dont-Know-JS)

🧓 会了，🧓 现在就去和面试官对线

## 数据类型篇

### 概述

- 八种基本类型(BigInt)
- 各个类型的 typeof
- Object.prototype.toString.call()

### null 和 undefined

- null 和 undefined 的 typeof
- null 和 undefined 转 Number
- 六种转为 false 的值

### 数值

- parseInt 工作流程
- isNaN 注意非 number 类型传入(NaN 参与的任何比较都是 false)
- 特殊值 NaN 和 Infinity
- parseInt + Number.prototype.toString 实现任意进制的转换

### 字符串

### 对象

- 键名为字符串（不是调用 String 转换）
- in (继承的，enumerable 属性

### 函数

- 函数也是对象（Function 的实例）
- 函数可多次声明
- 函数声明提升，表达式不提升，提升优先级高于变量声明
- 函数作用域（LHS 和 RHS）
- arguments 对象（类数组对象和转为数组的方法、修改不影响实际参数，arguments.length 和 函数名.length 区别）
- 普通函数和箭头函数的区别（this 绑定、arguments 有无、可否再次绑定）
- 闭包：可以记住内部运行环境的函数
- IIFE（括号防止解释为函数定义、防止污染作用域）
- eval（影响当前作用域，严格模式下形成一个作用域，但别名调用 eval 为全局作用域，包括严格模式下）(可能用在 JSON.parse 的内部源码中)

### 数组

- 数组也是对象（Array 实例）typeof === 'object'
- in 遍历数组会遍历非数字键
- 空位产生原因（设置 length、delete 某一位、new Array）
- 跳过空位的方法（for in、forEach、Object.keys、
- 类数组对象（具有 length 且 key 为数字）转为数组（Array.of(), Array.from(), Array.prototype.slice.call())

## 运算符

### 算术运算符

- 加法运算符产生重载，转换优先级 String > Number，其他类型会转换为原始类型再相加(先 valueOf 再 toString，但 Date 相反)
- 其他运算符当遇到非数值类型，先转为数值类型再运算
- 自右向左的指数运算符（相当于 Math.pow())

### 比较运算符

- `==` 原始类型转为 Number 后比较，对象转为原始类型比较

### 布尔运算符

- Boolean(bool) 与 !!bool 效果相同

## 数据类型转换

- Number() 工作流程，遇到对象先 valueOf，若还为对象 toString，还为对象抛出 TypeError，String() 转换流程相反
- 自动转换： 预期需要什么值，自动强制转换为那个值

## 错误处理机制

- 六大原生错误类型：SyntaxError、ReferenceError、RangeError、TypeError、URIError、EvalError
- catch 自带作用域

## 标准库

### Object

- Object.keys(): enumerable 的自身属性，Object.geetOwnPropertyNames() 自身属性, in enumerable 的所有属性，Object.prototype.propertyIsEnumerable(attr) 对自身的可遍历属性返回 true

### 属性描述对象

- 使用 Object.defineProperty 时，enumerable、writable、configurable 为 false
- 如果设置了 get / set，就无法将 writable 设置为 false
- enumerable 为 false 情况下，in / Object.keys() / JSON.stringfy 都无法取该属性
- 当 configurable 为 false 情况下，仍然可以将 writable 改为 false
- 无法 delete 一个 configurable 为 false 的属性
- 对象深拷贝（Object.getOwnPropertyNames，遍历并使用 Object.defineProperty 拷贝，如果拷贝值为对象，递归）
- 冻结对象： preventExtensions（无法新增） < seal（无法删除、新增 - configurable 为 false） < freeze（无法删除、新增、修改）

### 数组

- Array 的构造函数：单数值参数 - 长度为数组的空位数组、单非数值参数和多参数 - 一个成员为参数列表的数组
- 判断是否为数组：instanceof 、Object.prototype.toString.call、Array.isArray
- 改变数组的方法：push pop shift unshift reverse splice(删除数组一部分，并返回删除部分) sort
- 不改变数组的方法：join concat slice forEach map filter some every
- 跳过空位的方法：map forEach for...in
- [使用 reduce 找出字符串长度最长的成员](https://wangdoc.com/javascript/stdlib/array.html#reduce%EF%BC%8Creduceright)

### 包装对象

- 原始类型的值会自动当做包装对象使用
- new Boolean(false) === true

### Boolean 对象

### Number

- parseInt + Number.prototype.toString 转换任意进制到任意进制

### String 对象

- 将字符串转数组： for、split、Array.prototype.slice.call
- [slice、substring 和 substr 的区别](https://wangdoc.com/javascript/stdlib/string.html#stringprototypeslice)

### Math

感觉没啥写的，就常用的几个数学方法

### RegExp

- lastIndex 只对同一个正则表达式，且带有 g 有效
- RegExp.prototype.exec 和 String.prototype.match 的区别
- 匹配规则
- 在正则中使用 \ 转义时，如果从字符串生成 RegExp，则需要两个斜杠

### JSON

- JSON.stringify()
- Object.prototype.toJSON
- JSON.parse() 实现深拷贝无法解析 null undefined RegExp

## 面对对象编程

### 实例对象与 new 命令

- new 的全过程，构造函数 this 指向和返回值情况（不是对象、不是 this）
- new.target 、 instanceOf、this === window 防止不使用 new 直接调用构造函数

### this 关键字

- 推荐 你不知道的 JavaScript 四种 this 绑定方法
- 多层嵌套的 this、回调函数的 this
- call（参数列表）/ apply（参数数组） / bind（参数列表）
- Function.prototype.call.bind

### 对象的继承

- 原型对象 prototype（实例属性继承 prototype 属性）
- 原型链（先找自身属性，否则沿着原型链向上找，直到找到 null）
- instance 根据 prototype.constructor 进行工作
- Object.create() 以某个对象为原型创造对象
- 多种设置 prototype 的优缺点 - 1.new 对象：会继承对象本身属性方法 2.指向某个 prototype：修改自身 prototype 会导致上游 prototype 一同修改 3. Object.create(某个 prototype) 保证不修改上游 prototype 比较好
- 对构造函数的 prototype 赋值后一定要修改 constructor 属性重新指向构造函数
- 通过 Object.assign 混入（mixin）多个 prototype 实现多重继承

### Object 对象的相关方法

- 使用 call + setPrototypeOf 模拟一个 new
- [手写一个 Object.create](https://wangdoc.com/javascript/oop/object.html#objectcreate)

### [严格模式](https://wangdoc.com/javascript/oop/strict.html)

- 模块默认严格模式

## 异步操作

### 概述

- 任务队列和事件循环

### 定时器

- 使用闭包 + setTimeout 实现防抖和节流

## DOM

### Node 接口

- 七种类型节点（Node）：Document、DocumentFragment、Doctype、Element、Attribute、Text、Comment
- 常用属性 ：nextSibling、 previousSibling、firstChild、lastChild、parentNode、parentElement、childNodes（NodeList）
- 常用方法： appendChild、cloneNode（拷贝子节点 true）、insertBefore（实现在某一节点前后插入节点）、contains、isEqualNode 和 isSameNode 的区别

### NodeList 和 HTMLCollection

- 区别：NodeList 只有 childNodes 是动态集合，HTMLCollection 都是动态集合

### ParentNode 和 ChildNode

- 当为父节点和子节点时分别混入（Mixin）对应方法
- ParentNode.children 和 Node.childNodes(前者为 HTMLCollection，后者为 NodeList)
- append 和 appendChild 和 innerHTML：appendChild 只能添加节点对象，append 可以添加节点和文档节点字符串，innerHTML 只能添加 HTML 字符串
- 在某一节点后插入节点的方法：insertBefore + nextSibling / ChildNode.prototype.before()

## let 和 const

- var / let 的区别（作用域、重复声明、window 挂载、死区）

## 解构赋值

- 解构可对可迭代对象进行局部取值来进行赋值
- [对象解构赋值的重命名](https://es6.ruanyifeng.com/#docs/destructuring#%E7%AE%80%E4%BB%8B)（尤其是嵌套版）
- 函数参数的默认值解构 - 先赋值再解构

## 字符串的扩展

- 字符串为可迭代对象
- 模板字符串
- codePointAt 和 charCodeAt 的区别（UTF-16 编码和 ASCii 码）

## 正则扩展

- y 修饰符 （sticky）
- 具名组匹配 (?<组名>)

## 函数扩展

- 函数默认值：生成作用域、length 属性失真、不允许重名、位置要求、不能显式严格模式
- rest 参数作为数组(和 arguments 的区别)
- 箭头函数和普通函数的区别（this 默认绑定、arguments 对象，不可作构造函数，不可作为 generator）
- 尾调用优化（最后一句调用函数，如果不引用函数内部变量，则不会保留上一个调用栈），主要用于递归

## 数组的扩展

- 扩展运算符实现数组扁平化、拷贝、可迭代对象转换为数组
- find / findIndex 和 indexOf 的区别（传入比较函数 、NaN）

## 对象的扩展

- 在对象中 super 指向原型对象
- 链判断运算符和 Null 判断作用符
- Object.is 解决 NaN

## Symbol

- Symbol 不能和其他值运算，但能强制转换为 String
- Symbol.prototype.description 在转为 String 时提示
- Symbol 在对象中使用需要用到方括号
- Symbol 消除魔术字符串
- Symbol 做键名，只能被 Reflect.ownKeys 和 Object.getOwnPropertySymbol 取到
- Symbol.for (全局) 和 Symbol.keyFor
- Symbol 实现 Singleton 模式

## Set 和 Map

- Set 实现交并补
- 数组去重的方法（Set、Hash、遍历）
- Weak 不会增加引用计数使得可被垃圾回收，且只接受对象

## Proxy 和 Reflect

- Proxy 和 Reflect 的 13 种拦截方法 / 静态方法
- Proxy 代理对象，对象内部属性 this 指向 Proxy 对象
- get / set / has / deleteProperty / construct / getPrototypeOf / setPrototypeOf / apply / defineProperty
  / getOwnPropertyDescriptor / isExtensible / preventExtensions / ownKeys(所有属性)

## Promise

- 手写一个 Promise
- resolve 和 reject 不会终止 Promise 函数运行，直到函数结束，才执行 then(事件循环原理)
- then 返回新 Promise 实例
- Promise 产生的异常会一路冒泡直至 catch，如果没 catch，只会打印异常但不会被 catch 块捕获
- Promise.all / Promise.race
- Promise.allSettled
- [Promise 的 then 是微任务，追加在本轮时间循环后执行](https://wangdoc.com/javascript/async/promise.html#%E5%BE%AE%E4%BB%BB%E5%8A%A1)
- Promise.resolve()

# 未完待续

憋去，他们问题多
