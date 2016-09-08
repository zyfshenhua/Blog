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

　　AngularJS有着诸多特性，比如模块化、双向数据绑定、语义化标签、依赖注入等。它与我们之前学习的jQuery是有一定的区别的，jQuery更准确来说只一个类库（类库指的是一系列函数的集合）以DOM做为驱动（核心），而AngularJS则一个框架（诸多类库的集合）以数据做为驱动（核心）。
　　框架对开发的流程和模式做了约束，开发者遵照约束进行开发，更注重实际业务逻辑，与之类似的框架还有BackBone、KnockoutJS、Vue、React等。

<!--more-->

### 下载

1. 通过[AngularJS](https://code.angularjs.org/)官方下载
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

　　下图展示了AngularJS基本结构

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
　　
　　**注：应用（App）其本质也是一个模块**

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
　　
　　通过控制器（Controller）将模型（Model）数据展示到对应的视图（View）上，每个视图（View）都可以对应1个或多个控制器（Controller），通过为HTML标签添加`ng-controller`属性并赋值相应的控制器（Controller）的名称，就确立了关联关系。

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

　　HTML在构建应用（App）时存在诸多不足之处，AngularJS通过扩展一系列的HTML属性或标签来弥补这些缺陷，所谓指令就是AngularJS自定义的HTML属性或标签，AngularJS自身负责解析这些自定义的属性或标签，AngularJS指令都是以`ng-`做为前缀的，例如`ng-app`、`ng-controller`、`ng-repeat`等。

### 内置指令

待定

### 自定义指令

　　AngularJS允许根据实际业务需要自定义指令，通过模块实例对象下的`directive`方法定义。

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

![单向数据绑定](/uploads/one-way.png "单向数据绑定")

　　如上图所示，只能模型（Model）数据向视图（View）传递。

### 双向绑定

　　双向绑定则可以实现模型（Model）数据和视图（View）模板的双向传递，如下图所示

![单向数据绑定](/uploads/two-way.png "单向数据绑定")

### 相关指令

　　在AngularJS通过`\{\{\}\}`和ng-bind指令来实现模型（Model）数据向视图模板（View）的绑定，模型数据通过一个内置服务`$scope`来提供，这个`$scope`是一个对象，通过为这个对象添加属性或者方法便可以在相应的视图（View）模板里访问得到。
　　注：`\{\{\}\}`是ng-bind的简写形式，其区别在于通过`\{\{\}\}`绑定数据时会有“闪烁”现象，添加`ng-cloak`也可以解决“闪烁”现象，通过`ng-bind-template`可以绑定多个数据。

```html
    somecode
```
　　
　　通过为表单元素添加`ng-model`指令实现视图（View）模板向模型（Model）数据的绑定。

```html
    somecode
```

　　通过`ng-init`可以初始化模型（Model）也就是`$scope`。

```html
    somecode
```

　　AngularJS对事件也进行了扩展，无需显式的获取DOM元素便可以添加事件，易用性变得更强。在原有事件名称基础上添加`ng-`做为前缀，然后以属性的形式添加到相应的HTML标签上即可。如`ng-click`、`ng-dblclick`、`ng-blur`等。

```html
    somecode
```

　　通过`ng-repeat`可以将数组或对象数据迭代到视图模板中，`ng-switch`、`on`、`ng-switch-when`可以对数据进行筛选。

　　通过`ng-options`创建下拉选择框，相对比较复杂。

```html
    somecode
```


## 作用域

　　通常AngularJS中应用（App）是由若干个视图（View）组合成而成的，而视图（View）又都是HTML元素，并且HTML元素是可以互相嵌套的，另一方面视图都隶属于某个控制器（Controller），进而控制器之间也必然会产生嵌套关系。
　　每个控制器（Controller）又都对应一个模型（Model）也就是$scope对象，不同层级控制器（Controller）下的$scope便产生了作用域。

### 根作用域

　　一个AngularJS的应用（App）在启动时会自动创建一个根作用域$rootScope，这个根作用域在整个应用范围（ng-app所在标签以内）都是可以被访问到的。

### 子作用域

　　通过ng-controller指令可以创建一个子作用域，新建的作用域可以访问其父作用域的数据。

## 过滤器

　　在AngularJS中使用过滤器格式化展示数据，在中使用“|”来调用过滤器，使用“:”传递参数。

### 内置过滤器

待定

### 自定义过滤器

　　除了使用AngularJS内建过滤器外，还可以根业务需要自定义过滤器，通过模块对象实例提供的filter方法自定义过滤器。

## 依赖注入

　　AngularJS采用模块化的方式组织代码，将一些通用逻辑封装成一个对象或函数，实现最大程度的复用，这导致了使用者和被使用者之间存在依赖关系。
　　所谓依赖注入是指在运行时自动查找依赖关系，然后将查找到依赖传递给使用者的一种机制。
　　常见的AngularJS内置服务有$http、$location、$timeout、$rootScope等

### 推断式注入

　　没有明确声明依赖，AngularJS会将函数参数名称当成是依赖的名称。
　　这种方式会带来一个问题，当代码经过压缩后函数的参数被压缩，这样便会造成依赖无法找到。

### 行内注入

　　以数组形式明确声明依赖，数组元素都是包含依赖名称的字符串，数组最后一个元素是依赖注入的目标函数。
　　**推荐使用这种方式声明依赖**

## 服务

　　服务是一个对象或函数，对外提供特定的功能。

### 内置服务

- $location
- $timeout&interval
- $filter
- $log
- $http

### 自定义服务

　　通过上面例子得知，所谓服务是将一些通用性的功能逻辑进行封装方便使用，AngularJS允许将自定义服务。

- factory
- service
- value

　　在介绍服务时曾提到服务本质就是一个对象或函数，所以自定义服务就是要返回一个对象或函数以供使用。

## 模块加载

AngularJS模块可以在被加载和执行之前对其自身进行配置。我们可以在应用的加载阶段配置不同的逻辑。

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





