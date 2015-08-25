<img src="http://angular-meteor.com/images/logo-large.png" width="60" height="60" />  [angular-meteor-学习笔记]()
======================================================

> The power of Meteor and the simplicity and eco-system of AngularJS

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [快速开始](#%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)
    - [Meteor 项目](#meteor-%E9%A1%B9%E7%9B%AE)
    - [Meteor 客户端 - 通过Bower安装](#meteor-%E5%AE%A2%E6%88%B7%E7%AB%AF---%E9%80%9A%E8%BF%87bower%E5%AE%89%E8%A3%85)
  - [Resources](#resources)
  - [用法](#%E7%94%A8%E6%B3%95)
    - [内容目录](#%E5%86%85%E5%AE%B9%E7%9B%AE%E5%BD%95)
    - [应用初始化](#%E5%BA%94%E7%94%A8%E5%88%9D%E5%A7%8B%E5%8C%96)
    - [模板化](#%E6%A8%A1%E6%9D%BF%E5%8C%96)
- [Hello {{yourName}}!](#hello-yourname)
    - [Meteor Collections（集合）数据绑定](#meteor-collections%EF%BC%88%E9%9B%86%E5%90%88%EF%BC%89%E6%95%B0%E6%8D%AE%E7%BB%91%E5%AE%9A)
    - [订阅数据Subscribe](#%E8%AE%A2%E9%98%85%E6%95%B0%E6%8D%AEsubscribe)
    - [路由](#%E8%B7%AF%E7%94%B1)
    - [&lt;meteor-include&gt;](#&ltmeteor-include&gt)
    - [用户鉴定](#%E7%94%A8%E6%88%B7%E9%89%B4%E5%AE%9A)
    - [Meteor 的 promises方法](#meteor-%E7%9A%84-promises%E6%96%B9%E6%B3%95)
    - [绑定 Meteor session](#%E7%BB%91%E5%AE%9A-meteor-session)
    - [额外的 packages](#%E9%A2%9D%E5%A4%96%E7%9A%84-packages)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 快速开始

### Meteor 项目
1. 通过 `$ curl https://install.meteor.com | /bin/sh` 安装 [Meteor](http://docs.meteor.com/#quickstart) 
2. 通过 `$ meteor create myapp` 创建一个新的Meteor应用， 或者cd 到已存在应用的根目录
3. 通过 `$ meteor add urigo:angular` 安装 urigo:angular

### Meteor 客户端 - 通过Bower安装
> 在非Meteor的angular应用中使用Meteor作为一个service

1. 安装 [meteor-客户端](https://github.com/idanwe/meteor-client-side) `$ bower install meteor-client-side`
2. 安装 angular-meteor `$ bower install angular-meteor`

## Resources
- [Getting started tutorial](https://angular-meteor.com/tutorial)
- [Example application](https://github.com/Urigo/meteor-angular-socially) (Final version of the tutorial)
- [angular-meteor University](https://github.com/Urigo/meteor-angular-socially#angular-meteor-university-)
- Questions and help - [stack-overflow `angular-meteor` tag](http://stackoverflow.com/questions/tagged/angular-meteor)
- Discussions - [Angular category on the Meteor Forum](https://forums.meteor.com/c/angular) and [![Join the chat at https://gitter.im/Urigo/angular-meteor](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/Urigo/angular-meteor?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
- [Report issues](https://github.com/Urigo/angular-meteor/issues)
- [Change Log, updates and breaking changes](https://github.com/Urigo/angular-meteor/releases)
- [Roadmap - Trello board](https://trello.com/b/Wj9U0ulk/angular-meteor)
- [angular-meteor Blog](https://medium.com/angular-meteor)
- Starters - [angular-meteor Yeoman generator](https://github.com/ndxbxrme/generator-angular-meteor), [Angular-Meteor-Boilerplate with TypeScript](https://github.com/ShMcK/Angular-Meteor-Boilerplate)
- [Meteor package - urigo:angular](https://atmospherejs.com/urigo/angular)
- [Angular-Meteor Platform](https://github.com/planet-training/angular-meteor-platform) - No Blaze, plain HTML
- [Awesome Meteor](https://github.com/Urigo/awesome-meteor) - A curated, community driven list of awesome Meteor packages, libraries, resources and shiny thing

## 用法
### 内容目录
- [应用初始化](#app-initialization)
- [模板化](#templating)
- [Meteor集合的数据绑定](#binding-to-meteor-collections)
- [路由](#routing)
- [用户鉴定](#user)
- [Meteor promises方法](#meteor-methods-with-promises)
- [绑定Meteor session](#bind-meteor-session)

### 应用初始化

在应用中注册 `angular-meteor` 模块：

```js
angular
  .module('myModule', ['angular-meteor']);
```

### 模板化

你必须在`.ng.html`文件中写Angular模板标签，因为Meteor不会将这些文件当成Spacebars模板(注：Meteor自带的Blaze)
将HTML和`.ng.html`文件组合在一起很容易，我们可以使用Angular的`ng-include`指令

请注意这些Angular模板的名字将是他们在Meteor中的URL。
**因此每一个模板URL是相对路径（相对于Meteor项目的根目录），包含正斜线。**当使用`ng-include`来包含模板的时候要特别注意。

`client/index.html`:

```html
<head>
    <title>Angular and Meteor</title>
</head>

<body ng-app="myModule">
    <ng-include src="'client/views/user.ng.html'"></ng-include>
    <ng-include src="'client/views/settings.ng.html'"></ng-include>
</body>
```

`client/views/user.ng.html`:

```html
<div>
    <label>Name:</label>
    <input type="text" ng-model="yourName" placeholder="Enter a name here">

    <h1>Hello {{yourName}}!</h1>
</div>
```


### Meteor Collections（集合）数据绑定

[angular-meteor](http://angular-meteor.com/) 提供了 (view-client-server) 三方 数据绑定 ， 将 Meteor collection 赋值给 Angular model.
具体查看 API [$meteor.collection](http://angular-meteor.com/api/meteorCollection).

```js
$scope.todos = $meteor.collection(Todos);
```

### 订阅数据Subscribe

[$meteor.subscribe](http://angular-meteor.com/api/subscribe) 是 `Meteor.subscribe`（返回promise）的封装。

这是一个绑定Meteor collection到表单中Angular model的例子：

```js
$meteor.subscribe('Todos').then(function () {
    $scope.todos = $meteor.collection(Todos);
});
```

### 路由

使用官方 AngularUI ui-router Meteor package - [angularui:angular-ui-router](https://atmospherejs.com/angularui/angular-ui-router)

### &lt;meteor-include&gt;

你可以通过[meteor-include](http://angular-meteor.com/api/meteor-include) 指令来引入Meteor的原生模板.


```html
<template name="todoList">
    A couple of todos
</template>

<meteor-include src='todoList'></meteor-include>
```

Read more on meteor-include, using parameters and binding Meteor templates to Angular's scope in the [API docs](http://angular-meteor.com/api/meteor-include).

### 用户鉴定

angular-meteor 提供了对 [Meteor accounts system](http://docs.meteor.com/#/full/accounts_api)的完全支持。 查看API -  [Documentation](http://angular-meteor.com/api/user).

[More in step 8 of the tutorial](http://angular-meteor.com/tutorial/step_08)

### Meteor 的 promises方法

[$meteor.call](http://angular-meteor.com/api/methods) calls a [Meteor method](http://docs.meteor.com/#/full/meteor_methods) and returns a promise.

```js
$meteor.call('addUser', username).then(function (data) {
    console.log('User added', data);
});
```

### 绑定 Meteor session

[$meteor.session](http://angular-meteor.com/api/session) 绑定Angular 作用域上的变量到Meteor Session的变量。

```js
$meteor.session('counter').bind($scope, 'counter');
```

### 额外的 packages
如下是Meteor包中Angular库的不完全列表：

- [Meteor packages for Angular 3rd party libraries](https://trello.com/c/EGCdgHAk/47-official-meteor-packages-to)
- [civilframe:angular-jade](https://github.com/civilframe/meteor-angular-jade) enables the usage of JADE files in place of HTML files. Files ending in *.ng.jade and will be compiled to *.html.
- [pbastowski:angular-babel](https://github.com/pbastowski/angular-meteor-babel/) empowers angular-meteor with Babel and ng-annotate all in the one package. Files ending in .es6 will first be transpiled by Babel and then annotated with ng-annotate.

尽情创造更多的Angular包，并添加到此列表中。
