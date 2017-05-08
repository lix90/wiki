---
title: "Practices"
author: lixiang
date: 2017-03-30 15:32
tag: emacs
---

想写一个emacs lisp函数，用来基于stardict和eshell查单词，即利用stardict命令行，在eshell中查询单词。

1. 在mini buffer输入需查询单词
2. 选择或新建eshell buffer
3. 在eshell中输入执行查询命令

输入单词
``` emacs-lisp
(setq word (read-string "Please enter word:"))
```

检查eshell buffer是否存在，如果存在，切换至eshell；否则新建并切换至eshell。

切换buffer: `switch-to-buffer`

移动point至buffer最末端。

在buffer中插入内容

# 判断一个mode 是否开启？

`boundp` 判断符号的值是否为void
`fboundp` 判断符号的函数定义是否为void

`(boundp 'some-mode)` 判断mode是否为void
`(and (boundp 'some-mode) some-mode)` 若某mode不为void，则启动该mode。
`(bound-or-true-p some-mode)` 等同于上面一句
