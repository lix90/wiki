---
title: "Reading Books"
author: lixiang
date: 2017-03-22 20:11
tag: r
---

# Test R Code by Richard Cotton

## 为什么进行测试？

- 大量的复杂的数据处理：自己就很容易犯错
- 代码将供其他用户使用：我不犯错不代表别人不犯错

## 两类测试

> The point of development-time testing is to make sure that you haven’t done something stupid. By contrast, the point of run-time testing is to make sure that the user hasn’t done something stupid.

1. 开发时测试：development-time testing，阻止开发者犯错，`testthat`
2. 运行时测试：run-time testing，阻止用户犯错，`assertive`

# R for Data Science by Hadley Wickham, Garrett Grolemund #

> Rule of thumb: never copy and paste more than twice.

## 如何减少重复代码？

1. 使用函数 functions
2. 使用迭代 iteration
3. 使用 imperative programming
4. 使用 functional programming
