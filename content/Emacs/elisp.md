---
title: "Emacs Lisp"
author: lixiang
date: 2017-03-23 23:02
tag: elisp
---

# Hello world

``` emacs-lisp
(message "Hello world!")
```

# Basics

## 函数与变量

`defun` `setq` `defvar` `defconst` `defcustom` `let` `let*`

### 定义变量 ###

``` emacs-lisp
(setq foo "I'm foo")
(defvar var-name value
  "document string")
```

setq vs defvar

### 局部作用域的变量 ###

``` emacs-lisp
(let (bindings)
  body)
```

let vs let*

### 定义函数 ###

``` emacs-lisp
(defun function-name ()
  "document string."
  body)
```

### lambda 表达式 ###

``` emacs-lisp
(lambda (arguments-list)
  "documentation string."
  body)
```

调用 lambda：

``` emacs-lisp
(funcall (lambda (name)
            (message "Hello, %s!" name)) "Lix")
```

lambda 表达式最常用的是作为参数传递给其它函数

## 控制结构

顺序执行：`(progn A B C ...)`

### 条件判断

`if` `cond` `when` `unless`

``` emacs-lisp
(if condition
    then
  else)
```

``` emacs-lisp
(cond (case1 do-when-case1)
      (case1 do-when-case2)
      ...
      (t do-when-none-meet))
```

when 能省去 if 里的 progn 结构，unless 省去条件为真子句需要的 nil 表达式。

### 循环

`while`

``` emacs-lisp
(while condition
  body)
```

## 逻辑运算

`and` `or` `not`

and 可代替 when，用于设置函数的"省值；or 可代替 unless，用于参数检查。

# 数据类型

内建的 emacs 数据类型称为 primitive types，包括整数、浮点数、cons、符号（symbol）、字符串、向量（vector）、散列表（hash-table）、subr（内建函数，比如 cons, if, and 之类）、byte-code function，和其他特殊类型，例如缓冲区（buffer）。

## 数字

emacs 的数字分为整数和浮点数，无双精度数 double。

### 测试函数 ###

整数类型 integerp，浮点数类型 floatp，数字类型 numberp。

elisp 测试函数一般都是用 p 结尾，p 是 predicate 的第一个字母。

### 数的比较 ###

< > >= <= = /=

`/=` 用来作为不等于的测试
`eql` 不仅用于测试数字的值是否相等，还测试数字类型是否一致

### 数的转换 ###

整数向浮点数转换：float
浮点数转换成整数：
- truncate 转换成靠近 0 的整数；
- floor 转换成最接近的不比本身的整数；
- ceiling 转换成最接近的不比本身小的整数；
- round 四舍五入后的整数

### 数的运算 ###

+ - * /

如果参数都是整数，作除法时数相等返回1，不相等返回0。如果参数中有浮点数，整数会自动转换成浮点数进行运算。

emacs 中没有 ++ 和 --，可以用 1+ 和 1- 使用 setq 赋值来替代 ++ 和 --。Common lisp 中的两个宏 incf 和 decf 可以实现 ++ 和 --。但是在 elisp 中使用这两个宏，需要在文件头写上：`(eval-when-compile (require 'cl))`。

`abs` 取数的绝对值。
两个取整的函数：`%` `mod`；前者第一个参数必须是整数；后者第一个参数既可以是整数也可以是浮点数。另外，即使对相同的参数，两个函数也不一定具有相同的返回值。

三角运算函数：sin, cos, tan, asin, acos, atan
开方函数：sqrt
exp 为 e 以底的指数运算，expt 可以指定底数的指数运算。
log 默认底数为 e，但也可以指定底数。`(log x 10)` -> log10。logb 以 2 为底的对数运算。
random 产生随机数。
