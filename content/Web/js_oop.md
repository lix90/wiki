---
title: "Object Oriented Programming in JavaScript"
author: lixiang
date: 2017-04-24 19:11
tag: JavaScript
---

class, super, delete, new, this, get, set, extends
constructor,

# constructor

构建“类”

``` javascript
function Obj() {
    // code
}

class Obj() {
    // code
}

let obj1 = new Obj();
```

检查对象是否为某类的实例

``` javascript
obj1 instanceof Obj

obj1.constructor == Obj;
```

> Although checking constructor property can be used to check the type of an instance, it is recommended to only use the instanceof operator for this purpose, because the constructor property might be overwritten, so it cannot be a reliable method for checking the type of an instance.

constructor可能被复写，所以最好是使用instanceof运算符进行类的检查。

