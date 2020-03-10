# Js 知识备忘录

内容整合自[阮一峰 JavaScript 教程](https://wangdoc.com/javascript/)、[阮一峰 ECMAScript 6 教程](https://es6.ruanyifeng.com/)

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
- isNaN 注意非 number 类型传入
- 特殊值 NaN 和 Infinity
- parseInt + Number 实现任意进制的转换

### 字符串

### 对象

- 键名为字符串（不是调用 String 转换）
- in (继承的，enumable 属性

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

- 加法运算符产生重载，转换优先级 String > Number > Boolean， 其他类型会转换为原始类型再相加(先 valueOf 再 toString，但 Date 相反)
- 其他运算符当遇到非数值类型，先转为数值类型再运算
- 自右向左的指数运算符（相当于 Math.pow())

# 未完待续
