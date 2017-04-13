---
title: "base"
date: 2017-03-22
tag: rpackage, rbase
collection: R包
---

[TOC]

# base #

**Sys.**
- `Sys.getenv()` 获取环境变量内容
- `Sys.setenv()` 设置环境变量
- `Sys.unsetenv()` 移除环境变量
- `Sys.time()` `Sys.Date()` 获取当前日期和时间

# Startup #

步骤
1. **设置环境变量**：通过 site 和 user 文件
2. site file 由环境变量 `R_ENVIRON` 指定；如果没有指定，那么使用系统默认 site file，`R_HOME/etc/Renviron.site`。
3. user file 由环境变量 `R_ENVIRON_USER` 指定；如果没有指定，那么搜索当前工作路径或者用户的主路径（HOME directory）中的 `.Renviron` 文件。
  此时 base package 被加载
2. 搜索 profile file，由`R_PROFILE`环境变量指定，若不存在，则使用 `R_HOME/etc/Rprofile.site`。
3. 搜索 user profile，有 `R_PROFILE_USER` 环境变量指定，如果不存在，调用 `.Rprofile`，source 到 workspace 中。
4. 如果存在 `.RData`，则加载
5. 如果存在 `.First` 函数，则执行，然后，`base::.First.sys()` 执行。`.First.sys()` 调用 `require` 加载默认的包。默认的 R 包由 `options("defaultPackages")` 指定。如果默认包中包含 methods package，那么通过函数 `.OptRequireMethods()` 先加载 methods 包。`.First()` 可以在 `.Rprofile` 和 `Profile.site` 中定义，也可以存储在 `.RData` 中。

在 R 启动时，需要两种文件，设置环境变量的文件和包含 R 代码的 profile 文件。

