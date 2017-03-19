---
title: "Lisp"
author: Lixiang
date: 2017-03-18 17:49:54
tag: lisp, emacs-lisp
description: "lisp学习笔记"
---

backquote

``` common-lisp
(setq a "a's value" b "b's value" c "c's value" d '(a b))
'(a  b  c)      ; => (a b c)
`(,a b ,c)      ; => ("a's value" b "c's value")
`(,a b ,c ,@d)  ; => ("a's value" b "b's value" (a b))
```
