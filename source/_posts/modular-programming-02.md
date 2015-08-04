title: 模块化编程 Modular Programming 02 —— AMD 规范
date: 2015-08-04 12:46:39
tags: modular programming
---

参考资料： http://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html

讨论：如何在浏览器环境组织不同的模块、管理模块之间的依赖性

## 为什么要有模块

因为有了模块，我们就可以更方便地使用别人的代码，想要什么功能，就加载什么模块。

但是，这样做有一个前提，那就是大家必须以同样的方式编写模块，否则你有你的写法，我有我的写法，岂不是乱了套！

目前，通行的 JavaScript 模块规范共有两种：CommonJS 和 AMD。我主要介绍 AMD，但是要先从 CommonJS 讲起。

## CommonJS

2009 年 node.js 项目诞生， JavaScript 也开始用于服务器端编程。在浏览器环境下，没有模块也不是特别大的问题，毕竟网页程序的复杂性有限；但是在服务器端，一定要有模块，与操作系统和其他应用程序互动，否则根本没法编程。 

node.js 的模块系统就是参照 CommonJS 规范实现的。

在 CommonJS 中，有一个全局方法 require()，用于加载模块。

### 浏览器环境

有了服务器端的模块以后，大家就像要客户端模块。而且最好两者能够兼容，一个模块不用修改，在服务器和浏览器都可以运行。

但是，由于一个重大的局限，使得CommonJS规范不适用于浏览器环境。
    ```
        
        >原因是，在服务器端模块都在本地硬盘，可以同步加载完成，等待时间就是硬盘的读取时间。
        但是，对于浏览器，这却是一个大问题，因为模块都放在服务器端，等待时间取决于网速的快慢，可能要等很长时间，浏览器处于"假死"状态。
        
        var math = require('math');
    　　 math.add(2, 3);
    
    ```
对于浏览器端来说，只能采用“异步加载”，这也是 AMD 规范诞生的背景。


## AMD 

AMD是"Asynchronous Module Definition"的缩写，意思就是"异步模块定义"。它采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。

AMD也采用require()语句加载模块，但是不同于CommonJS，它要求两个参数：
    ```
        require([module], callback);
    ```
    第一个参数[module]，是一个数组，里面的成员就是要加载的模块；第二个参数callback，则是加载成功之后的回调函数。
    如果将前面的代码改写成AMD形式，就是下面这样：
    ````
        require(['math'], function (math) {
        　　　　math.add(2, 3);
        　　});
    ````
    math.add()与math模块加载不是同步的，浏览器不会发生假死。

目前，主要有两个JavaScript库实现了AMD规范：require.js和curl.js。


    




