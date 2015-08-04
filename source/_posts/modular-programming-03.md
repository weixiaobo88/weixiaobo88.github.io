title: 模块化编程 Modular Programming 03 —— require.js 的用法
date: 2015-08-04 14:33:11
tags: modular programming
---

## 为什么要用 require.js

最早的时候，所有Javascript代码都写在一个文件里面，只要加载这一个文件就够了。后来，代码越来越多，一个文件不够了，必须分成多个文件，依次加载。

    ```
        <script src="1.js"></script>
        <script src="2.js"></script>
        <script src="3.js"></script>
        <script src="4.js"></script>
        <script src="5.js"></script>
        <script src="6.js"></script>
    ```
    
这样的写法的缺点：
    
    - 加载文件过多，网页失去响应的时间就会越长
    - 由于js文件之间存在依赖关系，因此必须严格保证加载顺序（比如上例的1.js要在2.js的前面），依赖性最大的模块一定要放到最后加载，当依赖关系很复杂的时候，代码的编写和维护都会变得困难
    
require.js的诞生，就是为了解决这两个问题：
    
    - 实现js文件的异步加载，避免网页失去响应；
    - 管理模块之间的依赖性，便于代码的编写和维护。
    