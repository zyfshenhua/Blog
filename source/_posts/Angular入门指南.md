---
title: Angular入门指南
date: 2016-09-05 16:12:53
tags:
    - AngularJS
    - MVC
categories: 'Javascript'
---
## 介绍
　　AngularJS是一款由Google公司开发维护的前端MVC框架，其克服了HTML在构建应用上的诸多不足，从而降低了开发成本提升了开发效率。

### 特点
　　AngularJS有着诸多特性，最为核心的是：模块化、双向数据绑定、语义化标签、依赖注入等。与我们之前学习的jQuery是有一定的区别的，jQuery更准确来说只一个类库（类库指的是一系列函数的集合）以DOM做为驱动（核心），而AngularJS则一个框架（诸多类库的集合）以数据和逻辑做为驱动（核心）。
　　框架对开发的流程和模式做了约束，开发者遵照约束进行开发，更注重的实际的业务逻辑，与之类似的框架还有BackBone、KnockoutJS、Vue、React等。

<!--more-->

### 下载
1. 通过AngularJS官网下载，不过由于国内特殊的国情，需要翻墙才能访问。
2. 通过npm下载，npm install angular
3. 通过bower下载，bower install angular

### 体验
``` html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>AngularJS 入门指南</title>
    </head>
    <body ng-app>
        <input type="text" ng-model="name">
        <span>hello {{name}}</span>
        <!-- 引入AngularJS框架 -->
        <script src="./libs/angular.min.js"></script>
    </body>
    </html>
```

## MVC
　　MVC是一种开发模式，由模型（Model）、视图（View）、控制器（Controller）3部分构成，采用这种开发模式为合理组织代码提供了方便、降低了代码间的耦合度、功能结构清晰可见。

- 模型（Model）一般用来处理数据（读取/设置），比如数据库操作
- 视图（View）一般用来展示数据，比如通过HTML展示
- 控制器（Controller）一般用做连接模型和视图的桥梁

![MVC](/uploads/mvc.gif "MVC示意图")

　　MVC更多应用在后端开发程序里，后被引入到前端开发中，由于受到前端技术的限制便有了一些细节的调整，进而出现了很多MVC的衍生版（子集）如MVVM、MVW、MVP、MV*等。

## 模块化
　　通过AngularJS构建应用（App）时是以模块化（Module）的方式组织的，即将整个应用划分成若干模块，每个模块都有各自的职责，最终组合成一个整体。
　　采用模块化的组织方式，可以最大程度的实现代码的复用，可以像搭积木一样进行开发。

![积木](/uploads/积木.jpg "搭积木一样开发")

## 基本结构

　　下图展示了AngularJS基本结构，学习AngularJS会围绕下图的结构展开。

![AngularJS的结构](/uploads/AngularJS结构.jpg "AngularJS的结构")

### 应用(App)
　　通过为任一HTML标签添加`ng-app`属性，可以指定一个应用（App），此标签所包裹的内容都属于应用（App）的一部分。

``` html
    <!DOCTYPE html>
    <!-- 将整个文档做为应用 -->
    <html lang="en" ng-app="App">
    <head>
        <meta charset="UTF-8">
        <title>AngularJS 入门指南</title>
    </head>
    <body>
        
        <script src="./libs/angular.min.js"></script>
    </body>
    </html>
```
或者

``` html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>AngularJS 入门指南</title>
    </head>
    <body>
        <div class="box" ng-app="App">
            <!-- 将此盒子包裹内容作为应用 -->
        </div>

        <script src="./libs/angular.min.js"></script>
    </body>
    </html>
```
### 模块(Module)
　　AngularJS提供了一个全局对象`angular`，在此全局对象下存在若干个方法，其中`angular.module`方法用来定义一个模块（Module）。

```javascript
    // 第1个参数代表模块名称
    // 第2个参数代表依赖其它的模块
    var App = angular.module('App', []);
```
　　**注：应用（App）其本质也是一个模块（一个比较大的模块）**

### 控制器(Controller)
　　控制器（Controller）作为连接模型（Model）和视图（View）的桥梁存在，通过模块实例对象方法`controller`来定义。

```javascript
    // App是上述的应用实例
    // 通过这个应用实例可以创建控制器
    // 第1个参数代表控制器名称
    // 第2个参数代表声明依赖并注入
    App.controller('DemoController', ['$scope', function ($scope) {
        // $scope便是模型（Model）
        $scope.somedata = 'Study AngularJS by myself!';
    }]);
```
　　通过控制器（Controller）将模型（Model）数据展示到对应的视图（View）上，所以需要将控制器（Controller）关联到视图（View）上，通过为HTML标签添加`ng-controller`属性并赋值相应的控制器（Controller）的名称，就确立了关联关系。

```html
    <!-- ng-controller值为控制器的名称 -->
    <div class="box" ng-controller="DemoController">
        <!-- 这里可以访问得到$scope（模型）的数据 -->
        {{ somedata }}
    </div>
```
完整示例

```html
    <!DOCTYPE html>
    <html lang="en" ng-app="App">
    <head>
        <meta charset="UTF-8">
        <title>AngularJS 入门指南</title>
    </head>
    <body>
        <div class="box" ng-controller="DemoController">
            {{ somedata }}
        </div>
      <script src="./libs/angular.min.js"></script>
      <script>
          var App = angular.module('App', []);
          App.controller('DemoController', ['$scope', function($scope) {
              $scope.somedata = 'Study AngularJS by myself!';
          }])
      </script>
    </body>
    </html>
```

## 指令
　　HTML在构建应用（App）时存在诸多不足之处，AngularJS通过扩展一系列的HTML属性或标签来弥补这些缺陷，所谓指令就是AngularJS自定义的HTML属性或标签，这些指令都是以`ng-`做为前缀的，例如`ng-app`、`ng-controller`、`ng-repeat`等。

### 内置指令

### 自定义指令
　　AngularJS允许根据实际业务需要自定义指令，通过模块实例对象下的`directive`方法实现。

```javascript
    // 定义模块
    var App = angular.module('App', []);
    // 自定义指令
    // 第1个参数代表指令名称
    // 第2个参数配置指令参数
    App.directive('myDirective', function () {
        return {
            // 自定义指令的类型
            restrict: 'EAC',
            // 自定义指令模板
            template: '<h1>Hello AngularJS!</h1>',
            // 是否替换原始标签
            replace: true
            // .... 还有其它参数
        }
    });
```
使用

```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>AngularJS 入门指南</title>
    </head>
    <body>
        <!-- 使用自定义指令 -->
        <div my-directive></div>

        <script src="./libs/angular.min.js"></script>
        <script>
            // 定义模块
            var App = angular.module('App', []);
            // 自定义指令
            // 第1个参数代表指令名称
            // 第2个参数配置指令参数
            App.directive('myDirective', function () {
                return {
                    // 自定义指令的类型
                    restrict: 'EAC',
                    // 自定义指令模板
                    template: '<h1>Hello AngularJS!</h1>',
                    // 是否替换原始标签
                    replace: true
                    // .... 还有其它参数
                }
            });
        </script>
    </body>
    </html>
```

## 数据绑定
　　AngularJS是以数据做为驱动的MVC框架，所有模型（Model）里的数据经过控制器（Controller）展示到视图（View）中。
　　所谓数据绑定指的就是将模型（Model）中的数据与相应的视图（View）进行关联，分别有单向绑定和双向绑定两种方式。

### 单向绑定
　　单向数据绑定是指将模型（Model）数据，按着写好的视图（View）模板生成HTML标签，然后追加到DOM中显示，如之前所学的artTemplate 模板引擎的工作方式。
　　如下图所示，只能模型（Model）数据向视图（View）传递。

<!-- ![单向数据绑定](/uploads/) -->

### 双向绑定
　　双向绑定则可以实现模型（Model）数据和视图（View）模板的双向传递，如下图所示。

### 相关指令

## 作用域

### 根作用域

### 子作用域

## 过滤器

### 内置过滤器

### 自定义过滤器

## 依赖注入

### 推断式注入

### 行内注入

## 服务

### 内置服务

### 自定义服务

## 模块加载

### 配置块

### 运行块

## 路由

### SPA

### 路由

#### 配置

#### 参数

## 其它

### jQuery

### bower





