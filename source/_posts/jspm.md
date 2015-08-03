title: jspm
date: 2015-08-03 21:50:33
tags: jspm
---

文章参考 https://github.com/jspm/jspm-cli/wiki/Getting-Started

## jspm 是什么

- jspm 是一个 SystemJS 通用模块加载器的包管理器，建立在动态 ES6 的模块加载器
- 可以平行的加载任意 Registry（比如 npm 和 github ）中的任意形式（ES6，AMD，CommonJS）的模块
- 对于开发环境来说，可以在浏览器中以独立的文件的形式加载模块， 并把 ES6 和插件编译好。
- 对于生产环境（开发环境也是这样）来说，可以优化成一个 bundle 或者 分层的 bundles 或者一个通过一条命令自运行的bundle
 
## 用 jspm 之前的准备 

1. 安装 CLI

```
 npm install jspm -g
``` 

2. 初始化项目

```
 cd my-project
 jspm init
```

初始化之后项目的目录结构为

````
  my-project
    |__config.js
    |__package.json
    |__jspm_packages
````
3. 安装任意的包，来源可以是 jspm Registry 或者 Github 或者 npm

所有的安装都会保存在 package.json 中，你只需要使用 ‘jspm install’ 就可以安装其中的包。
```
  jspm install npm:lodash-node
  jspm install github:components/jquery
  jspm install jquery
  jspm install myname=npm:underscore
```

## 怎么用

### 简单的例子

1. 例子中需要在安装一下4个包
```
    jspm install npm:lodash-node
    jspm install github:components/jquery
    jspm install jquery
    jspm install myname=npm:underscore
```


2. 例子的文件目录结构

````
    my-project
      |__config.js
      |__package.json
      |__jspm_packages
      |__lib
          |__bootstrap.js
          |__main.js
      |__index.html
````

```JavaScript
    lib/bootstrap.js
  
    import _ from 'lodash-node/modern/lang/isEqual';
    import $ from 'jquery';
    import underscore from 'myname';
    
    export function bootstrap() {
      console.log("Hello Linne");
    }
```

````JavaScript
    lib/main.js
  
    import {bootstrap} from './bootstrap';
    bootstrap();
````

```html
  index.html
  
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
    
    <h1>Hello, Linne O(∩_∩)O~</h1>
    
    <script src="jspm_packages/system.js"></script>
    <script src="config.js"></script>
    <script>
        System.import('lib/main');
    </script>
    </body>
    </html>
```

在浏览器中打开 index.html，可以看到 console 中有输出。

3. Bundle for production

执行下面命令
```
    jspm bundle lib/main --inject
```
或下面命令
````
    jspm bundle-sfx lib/main
````
然后在 **index.html** 中就可以只引用一个js文件


```html
  index.html
  
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
    
    <h1>Hello, Linne O(∩_∩)O~</h1>
    
    <script src="build.js"></script>
    </body>
    </html>
```