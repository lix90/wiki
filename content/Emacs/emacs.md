---
title: "Learn Emacs"
author: lixiang
date: 2017-03-22 19:26
tag:
---

## 快捷键设置

四种类型的快捷键设置：
- 全局快捷键：`(global-set-key (kbd "A") 'your-command')`
- 全局映射键：`(define-key key-translation-map (kbd "A") (kbd "B"))`
- 基于 Major-Mode 的局部快捷键：`(local-set-key (kbd "A") 'your-command)`
- 基于 Minor-Mode 的局部快捷键：`(define-key your-minor-mode-map (kbd "A") 'your-command)`

删除或禁用键：`(global/local-unset-key (kbd "A"))` `(global/local-set-key (kbd "A") 'ignore/nil)`

解决键冲突

- 暴力映射：`define-key key-translation-map`
- 映射到新的 prefix 键上，再全局或者局部设置键。

宏与函数的区别：函数的参数是在传入时 eval，而宏则是传入并展开后再 eval。
快捷键的优先级：`key-translation-map > minor-mode-map > local-set-key > global-set-key`
在设置局部键时，需写出相应的代理映射键（prefix）。

说明：整理自Emacs（微信公众号）文章《那就从妖艳酷炫的快捷键开始吧！（一）》

## : & 符号

- `:foo` 在 Emacs Lisp 中是 `keyword symbol`
- 在 `use-package` 中被用作 `keyword arguments`
- `&optional` 指定的形参是可选的，如果没有指定，则当作 `nil`
- `&rest` 指定的形参是可变

> 宏的实参不会在宏被求值的时候立刻求值，而是会被当做数据直接传递给宏。因此宏可以自己决定那些代码在什么时候被求值。

参考 emacs-china 社区[问答](https://emacs-china.org/t/emacslisp/1566)
