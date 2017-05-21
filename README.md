# Webpack Revolution

@(Coding)

[TOC]
## 前言

该代码示例描述了一个普通的前端项目进化到使用Webpack + Gulp 管理构建流的过程.

提供了一个现代化JavaScript工程化项目的模板与思路.


[代码下载](https://github.com/Aquariuslt/Webpack-Revolution)

![Project-Structure](https://ooo.0o0.ooo/2017/05/21/59210e605f1c3.png)

示例项目里面包含了若干个子项目,以上图红圈内的几个项目文件夹为示例:
从上往下依次是: 

1.最原始的AngularJS项目
2.使用Webpack构建的,以CommonJS方式编写的JS项目
3.结合1,2的项目,使用Webpack,以CommonJS编写的AngularJS项目
5.在3的基础上,使用Gulp任务流进行Webpack构建的一个AngularJS项目
4.在5的基础上,将原来的AngularJS项目拆分成模块化,并添加CSS构建等模块


> P.S.为什么上面的顺序5和4会对调?因为在Github的网页上面显示的顺序不太对,按照字典序的排序 应该 `webpack-gulp-angularjs` 会在 `webpack-gulp-angularjs-boilerplate` 之前


接下来请跟着文档的步骤,下载项目自己动手运行.

预备知识:
一些基础的AngularJS知识
一些`angular-ui-router`的知识

运行需求环境:
git >=3
npm >=3
node >=6


## Getting Start

### 把项目下载到本地
```bash
git clone https://github.com/Aquariuslt/Webpack-Revolution.git
cd Webpack-Revolution
```

### Pure-AngularJS-Project

#### 安装项目依赖
```
cd pure-angularjs-project
npm install
```

#### 项目说明
项目的文件夹目录大概如下
```
Macbook:pure-angularjs-project Aquariuslt$ tree
.
├── README.md
├── package.json
├── server.js
├── static
│   ├── favicon.ico
│   ├── index.html
│   └── js
│       ├── app
│       │   ├── app.js
│       │   └── routes.js
│       └── vendor
│           ├── angular-ui-router.js
│           └── angular.js

```

这是一个很原始的JavaScript项目,通过手动在`static/index.html`中添加JS,CSS文件的引用,接着使用`express`将`static`这个文件夹下的内容当成静态的前端资源文件提供出来.

#### 运行项目

运行`npm start` 之后,我们可以在浏览器的[http://127.0.0.1:3000](http://127.0.0.1:3000) 看到效果

![pure-angularjs-project-runtime-min.gif](https://ooo.0o0.ooo/2017/05/21/592143245b71e.gif)

#### 代码说明
1.static/index.html
```html
<!DOCTYPE html>
<html lang="en" ng-app="ita-app">
<head>
  <title>Pure AngularJS Application</title>
  <base href="/#!/">
  <meta charset="UTF-8">
  <link rel="icon" href="favicon.ico" type="image/x-icon">
</head>
<body>
<!-- Header Area -->
<h2>Pure AngularJS Application</h2>
<a ui-sref="home">Home</a>
<a ui-sref="about">About</a>
<!-- Router View Area -->
<ui-view></ui-view>


<!-- Vendor JS Files -->
<script type="text/javascript" src="js/vendor/angular.js"></script>
<script type="text/javascript" src="js/vendor/angular-ui-router.js"></script>

<!-- Own Application JS Files -->
<script type="text/javascript" src="js/app/app.js"></script>
<script type="text/javascript" src="js/app/routes.js"></script>

</body>
</html>
```

负责引入`angular.js`,`angular-ui-router.js`
以及项目开发者自行编写的`app.js`与`routes.js`

2.static/app/app.js
```javascript
(function () {
  angular.module('ita-app',
    ['ui.router']
  )
})();
```

此处注册一个angular的module,叫做`ita-app`

3.static/app/routes.js
```javascript
(function () {
  angular.module('ita-app')
    .config(function ($stateProvider) {
      $stateProvider
        .state({
          name: 'default',
          url: '',
          template: ' <h3>Hello ITA</h3>'
        })
        .state({
          name: 'home',
          url: '/',
          template: ' <h3>Hello ITA</h3>'
        })
        .state({
          name: 'about',
          url: '/about',
          template: '<h3>About: This is an ITA Application</h3>'
        });
    });
})();
```

此处声明`ui-router`的三个路由的url:
分别是`/`, `/about`

4.server.js
```javascript
var express = require('express');

var app = express();

app.use('/', express.static('static'));

app.listen(3000);
```
此处表示使用express 监听3000端口,并以项目文件夹下的`static`作为静态资源的文件来提供服务.

#### 总结
如同上面的运行时的GIF所示.
在不同的路由情况下,页面展现的内容不一样.

相信这个内容,在接触了Node.js的`express.js`
与`angular.js` 基本知识之后都能很容易的理解,简直是小菜一碟!



