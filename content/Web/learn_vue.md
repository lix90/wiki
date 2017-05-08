---
title: "Learn Vuejs"
author: lixiang
date: 2017-04-25 16:25
tag: vuejs
---

[TOC]

# Components 组件

创建模版

```html
<template id="hello">
  <h1>Hello</h1>
</template>

<div>
  <hello-component></hello-component>
</div>
```

注册组件

``` javascript
Vue.component('hellow-component', {
  template: '#hello'
});

new Vue({
  el: '#app'
});
```

在创建组件时，为防止实例共享数据，需要使用匿名函数声明属性。

* `Vue.extend()` 创建组件子类
* `Vue.component()` 注册或获取一个全局组件

``` javascript
const HelloComponent = Vue.component('hello-component', {
  el: function () {
    return '#hello';
  },
  data: function () {
    return {
      msg: 'Hellow'
    }
  }
});
```

组件作用域

组件作用域为组件本地，应用的作用域为全局。但是组件调用全局的数据需要显式地在组件中通过`prop`属性声明，然后使用`v
-bind`与组件实例进行绑定。

组件的嵌套

在嵌套的组件中，单向数据绑定只支持父级传输数据给子组件，而子组件不能改变父级的数据。但是可以通过事件来实现双向绑定。另外，`.sync`或者`.once`也可以实现双向绑定，`:user.sync="user"`。

单文件组件

包含三部分：

* `<script>`
* `<template>`
* `<style>`

样式的作用域需要通过 `scoped` 属性声明。

预处理器：`lang="jade"` `lang="sass"`


# data binding 数据绑定 #

单向绑定

双向绑定

`v-model` 指令

* `<input>`
* `<texterea>`
* `<select>`

`v-bind` 绑定属性：`v-bind:attribute="obj / arr"`

Object, Array

Dynamic Class: `v-bind:class=" "`
Array Syntax: `v-bind:class="[...]"`

绑定行内样式 `v-bind:style="{...}"`

`v-if` & `v-show`：条件化渲染

v-if on <template>

v-if > v-else-if > v-else

# 选项

`el`

* 提供在页面上已存在的DOM元素作为Vue实例的挂载目标
* 可以通过 `vm.$el` 访问

`template`

* 模板，替换挂载元素
* 挂载元素的内容都将被忽略，除非模板内容有分发slot <?>
* 如果选项中包含render函数，template将被忽略

`render`

* 用来替代字符串模板

`data`

* 必须声明为返回一个初始数据对象的函数
* data仅仅为数据

`computed`

* 计算属性将被混入Vue实例中
* 所有getter和setter的this上下文自动绑定为Vue实例
* **不要使用箭头函数定义计算属性函数**
* computed属性函数会立即执行，在用到的数据变更后同样被触发执行

`methods`

* 同样被混入到Vue实例中
* 可通过Vue实例访问，或在指令表达式中使用
* this自动绑定为Vue实例，所以不应该使用箭头函数定义method函数
* methods用来代表事件

`props`

* 用于接收来自父组件的数据
* 可以对其类型进行检测

`directives` 指令

`filters` 过滤器

`components` 组件

`parent` 制定父实例，建立父子关系

# 绑定

## 绑定属性（组件prop）

`v-bind` `:`

## 绑定表单

`v-model`

## 绑定事件

`v-on` & `@`

* 绑定普通元素时，只能监听原生DOM事件
* 绑定自定义元素时，可以监听自定义事件

## 特殊属性

`key` 可用于强制替换元素或组件，而非复用它
`ref` 给元素或组件注册引用信息
`slot` 标记插入子组件内容

# 渲染

`v-text` `v-html`

`v-show` `v-once`

`v-if` `v-else` `v-else-if`

`v-for`

# 组件

## 注册组件

`Vue.component`

## 内置组件

`component` 渲染一个元组件为动态组件，通过 `is` 的值来决定哪个组件被渲染。

`transition` 作为单个元素或组件的过渡效果，不会渲染额外的DOM元素。

`transition-group` 作为多个元素或组件的过渡效果。

`keep-alive` 用于保留组件状态或避免重新渲染。

`slot` 插槽，用于内容分发

# 生命周期
# 工具
## vue-cli
## vue-loader
## vue-devtools
# 插件
## vue-router
## Vuex
### State “状态”

* 单一状态树包含应用所有层级的状态。
* 组件可通过computed属性获取状态值。
* 在根组件中通过store选项注入单一状态树，所有子组件便可以获取（`this.$store`）可用状态值。
* 可以使用 `mapState` 辅助函数在某一组件中多次获取使用状态值和状态计算（getters）方法。

### Getters 计算状态

* 对状态值进行进一步计算的方法
* 所生成的值可供多个组件反复使用
* 使用 `mapGetters` 函数在组件中使用多个getters

### Mutations “事件”

* 个人把mutations理解为事件函数，它包含两部分：type名称，handler代表事件逻辑的匿名函数。
* mutations仅仅是事件的逻辑或者过程，表示被促发后会发生什么。
* mutations需要被“外部”触发（actions便是这一促发的开关）才能产生作用。
* 使用大写变量名来区分mutation，并建议统一管理。
* mutations遵循Vue的相应式规则，需要通过 `Vue.set` 添加新的属性。
* mutations必须是同步式。
* `mapMutations` 可以集体触发mutations。

### Actions “开关”

* 个人把actions比作开关，它与mutations联通，mutations产生作用必须通过actions的“开关”来触发。
* actions可以是异步式。
* 通过 `store.dispatch` 可以分派各种mutations对应的actions。
* 使用 `mapActions`可以同时分派多个actions。
* 可以通过异步编程合并多个actions，构成一连串地事件。

### Modules 模块

* 当状态对象太过复杂，可以将其拆分为多个模块进行管理。
* 模块支持局部状态
* 模块状态默认注册为全局模式，但可以通过 `namespaced: true` 将模块注册为局部状态。
