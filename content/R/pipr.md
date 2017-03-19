---
title: "pipeR"
author: Lixiang
date: 2017-03-18 17:29:29
tag: piper, pipeline, rpackage
description: "流程化"
collection: R包
---

[TOC]

# Overview

[pipeR](https://github.com/renkun-ken/pipeR) 是由国内开发者 [renkun-ken](https://github.com/renkun-ken) 开发的一个强大的流程化代码的包，并且编写了详细的教程 [pipeR-tutorial](http://renkun.me/pipeR-tutorial)。该包提供四种流程化代码的风格：

- 运算符形式：`%>>%`
- 对象形式: `Pipe()`
- 参数形式：`pipeline()`
- 表达式形式：`pipeline({})`

``` r
devtools::install_github("renkun-ken/pipeR")
```

# 使用记录

目前全部将`[magrittr](https://github.com/tidyverse/magrittr)`包中的`%>%`全部用`%>>%`替代，还未尝试使用其他三种风格。

什么时候省略函数的 `()`？当函数只需传入一个参数时，并且不使用 `::` 指定包。
利用副作用在同一个流程的代码中将结果赋值到新的变量：例如`(~ filter(., x == 1) -> var)`

