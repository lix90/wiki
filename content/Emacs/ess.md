---
title: "ESS"
author: Lixiang
date: 2017-03-18 22:02:16
tag: ess, r
collection: Emacs/Packages
---

# 补全

## 对象名称的补全

- 在 ess-mode 中，<kbd>TAB</kbd> 先尝试缩进，如果不能缩紧那么补全对象名。
- 在 inferior-ess-mode 中，<kbd>TAB</kbd> 补全光标前的对象名。补全的模式类似于 tcsh，只不过是对象名的补全，而不是文件名。`ess-list-object-completions`或者`M-?` 可以列出所有可供补全的对象名。

变量 `ess-first-tab-never-complete` 可以控制第一次 <kbd>TAB</kbd> 键是否进行补全。如果为 `non-nil` 表示第一次 <kbd>TAB</kbd> 不进行补全。

ESS 提供了列表对象和环境对象的补全，例如 `$` `::` `:::`。

`M-x ess-resynch` 可以刷新所有的对象缓存。

## 对函数参数的补全

在函数调用时即 `(` 之后 <kbd>TAB</kbd> 可以提供函数参数的补全项。

## minibuffer 补全

ESS 使用 ido 包来提供 minibuffer 补全支持。

## 与自动补全包的集成

ESS 可以与 auto-complete 包集成，在 ESS 中默认自动激活 auto-complete。

# 其他

ESS 允许可以开启多个 ESS 进程。通过 `M-x ess-request-a-process` 可切换到 ESS 进程。

ESS 提供了 R 解释器的前端，在 inferior buffer 中运行 R 进程。

在 ESS 中`transcript`指 iESS 中输出的结果的文本。

