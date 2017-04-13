---
title: "ES6/ES2015"
author: lixiang
date: 2017-03-28 15:09
tag: ecmascript, javascript
---

[TOC]

# 块级作用域变量

**let/const** vs. **var**

var 进行变量声明时会泄露到其它代码块，如 for 循环或者是 if 块。

var 提升：
- var 是在函数作用域中的：即使在声明前，它在整个函数内均可用；
- 声明被提升了：变量在声明前就可以使用了；
- 初始化没有被提升：如果使用 var，一定要在顶部声明变量。

let 提升与 temporal dead zone：
- 在 ES6 中，let 会将变量提升到块顶部，而非如 ES5 提升至函数顶部；
- 在变量声明前引用变量会造成 ReferenceError；
- let 是块级作用域的，不可以在声明前使用；
- temporal dead zone 是块开始到变量被声明的这段区域。

声明常量可以使用 const。

# 立即执行函数表达式（IIFE）

为了防止变量的泄露，避免污染全局环境，需要使用 IIFE 将代码包起来。在 ES6 中，不再需要使用 IIFE，只要用块和 let 便可。

# 文本模版

需要文本模版，ES6 不需要使用嵌套连接，该用反引号 (`) 和字符串插值 ${}。

多行字符串则不需要再连接 n 字符串了。

# 解构赋值

- 获取数组元素
- 调换值
- 返回多个值的解构
- 参数匹配解构
- 深度匹配

对于多返回值的情况，不要用数组解构，用对象解构。

# 类和对象

在 ES5 中利用构造函数实现以面向对象编程的方式创建对象。ES6 则提供了语法糖，可以用 class、constructor 等新的关键字、更少的样板代码实现相同的效果。

- 最好使用 class 语法，避免直接操作 prototype，这样使得代码更佳简明易懂；
- 避免出现空的构造器：如果没有指明，类会有默认的构造器的。

# 继承

ES6 提供了新的关键字 extends 和 super，其原型继承方式比 ES5 简洁了许多。

# 原生 Promise

promise 中可以用 then 在某个函数完成后执行新的代码，而不必再嵌套函数。

# 箭头函数

在ES5 中，函数内需要用临时变量指向 this 或者使用 bind 绑定。ES6 中可以使用箭头函数解决 this 指向问题。箭头函数会捕捉其所在上下文的 this 值，作为自己的 this 值。

箭头函数的引入有两个方面的影响：
- 更简短的函数书写；
- 对 this 的词法解析。

# 使用 for...of 迭代

for --> forEach --> for...of

# 参数

默认参数：ES6 中可以指定 default parameters 的值。
剩余参数：ES6 中可以用展开操作符 ... 实现剩余参数



---

参考资料：

- http://web.jobbole.com/88910/
- ECMAScript 6 入门 http://es6.ruanyifeng.com/
