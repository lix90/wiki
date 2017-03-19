---
title: "git-commit message guides"
date: 2017-03-19
tag: git
---

[TOC]

# 动机

接触和使用 git 都是比较偶然而随意的事情。未曾考虑过提交信息中的书写规范问题。然而，总是会在提交更新时挠头忘记有哪些更新。每回更新时也没有相应的进行提交。每回提交时总是伴随着多种类型的修改。代码写得再漂亮，git-commit message 毫无规范，也只能算作是粗制滥造品吧。因为项目的发展是长期的维护，并且大项目和开源项目是需要多人合作的。因此，是时候了解和熟悉 git-commit message 规范了。

# 规范化 git-commit message 作用

- 提供更多的历史信息，方便快速浏览。
- 过滤 commit，便于快速查找。
- 便于生成 Change log。

# git-commit message 的规范

参考阮一峰介绍的 Angular 规范，其 message 格式为：

```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

其中，Header 是必需的，Body 和 Footer 可以省略。

## Header

Header部分只有一行，包括三个字段：type（必需）、scope（可选）和subject（必需）

### type

type 用于说明 commit 的类别，只允许使用下面7个标识。

* feat：新功能（feature）
* fix：修补 bug
* docs：文档（documentation）
* style： 格式（不影响代码运行的变动）
* refactor：重构（即不是新增功能，也不是修改 bug 的代码变动）
* test：增加测试
* chore：构建过程或辅助工具的变动

如果 type 为 feat 和 fix，则该 commit 将肯定出现在 Change log 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。

### scope

scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

### subject

subject 是 commit 目的的简短描述，**不超过50个字符**。

* **以动词开头，使用第一人称现在时**，比如change，而不是 changed 或 changes
* **第一个字母小写**
* **结尾不加句号（.）**

## Body

Body 部分是对本次 commit 的详细描述，可以分成多行，每行限制在72个字符。空行来分隔段落。

有两个注意点:

- 使用第一人称现在时，比如使用change而不是changed或changes。
- 应该说明代码变动的动机，以及与以前行为的对比。

## Footer

Footer 部分只用于两种情况。

（1）不兼容变动

如果当前代码与上一个版本不兼容，则 Footer 部分以 BREAKING CHANGE 开头，后面是对变动的描述、以及变动理由和迁移方法。

BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.

（2）关闭 Issue

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

Closes #234

也可以一次关闭多个 issue 。

Closes #123, #245, #992

## Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以 revert: 开头，后面跟着被撤销 Commit 的 Header。

revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.

Body 部分的格式是固定的，必须写成 This reverts commit <hash>.，其中的 hash 是被撤销 commit 的 SHA 标识符。

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的 Reverts 小标题下面。

# TODO: Emacs/Magit 配置

# 主要参考资料

- [阮一峰：Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/?utm_source=wanqu.co&utm_campaign=Wanqu+Daily&utm_medium=rss)
