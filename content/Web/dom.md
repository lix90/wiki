---
title: "DOM"
author: lixiang
date: 2017-04-01 14:17
tag: dom
---

[TOC]

# 什么是 DOM？

- DOM, document object model, 对 web 页面或者 html/xml 文档的完全的面向对象描述；
- DOM 将文档解析为一个由节点和对象（包含属性和方法的对象）组成的结构集合；
- DOM 将web页面和脚本或程序语言连接起来。

[W3C DOM](http://www.w3.org/DOM/) 与 [WHATWG DOM](https://dom.spec.whatwg.org/)

注意：文档可能会在多种浏览器上使用不同的DOM来访问。

所有操作和创建web页面的属性，方法和事件都会被组织成对象的形式

**API (web 或 XML 页面) = DOM + JS (脚本语言)**

重要的数据类型：document, element, nodeList, attribute, nameNodeMap

对象 vs 接口

# 事件与DOM
