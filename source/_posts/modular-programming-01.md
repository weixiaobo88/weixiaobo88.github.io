title: 模块化编程 Modular Programming 01 —— 模块的写法
date: 2015-08-04 09:09:19
tags: 
- JavaScript
- modular programming
---

参考资料： http://www.ruanyifeng.com/blog/2012/10/javascript_module.html

讨论： JavaScript 中模块的几种写法

## 模块的写法

介绍 6 种写法

1. 最原始的写法
    
    ```

        function func1() {
            console.log('This is func1.');
        }
        
        function func2() {
            console.log('This is func2.');
        }
    ```
    上面的函数 func1() 和 func2()，组成一个模块。使用的时候，直接调用就行了。
    这种做法的缺点很明显："污染"了全局变量，无法保证不与其他模块发生变量名冲突，而且模块成员之间看不出直接关系。

2. 对象的写法
    
    ```
    
        var moduleA = new Object({
            _count: 0,
            func1: function () {
                console.log('This is func1 in moduleA');
            },
            func2: function () {
                console.log('This is func1 in moduleA');
            }
        });

    ```
    这样的写法会暴露所有模块成员，内部状态可以被外部改写。

3. 立即执行函数（IIFE）的写法
    ```
    
        var moduleB = (function () {
            var _count = 0;
            var func1 = function () {
                console.log('This is func1 in moduleB');
            };
            var func2 = function () {
                console.log('This is func2 in moduleB');
            };
            return {
                func1: func1,
                func2: func2
            };
        })();

    ```
    可以达到不暴露私有成员的目的。
    
4. 放大模式（augmentation）的写法
    ```
    
        var moduleB = (function (module){
            module.func3 = function () {
                console.log('This is func3 in moduleB from augmentation.js');
            };
            return module;
        })(moduleB);
    ```
    如果一个模块很大，必须分成几个部分，或者一个模块需要继承另一个模块，这时就有必要采用"放大模式"（augmentation）。

5. 宽放大模式（Loose augmentation）的写法
    ```
        
        var moduleB = ( function (module){
            module.func4 = function() {
                console.log('This is func4 in moduleB from looseAugmentation.js');
            };
            return module;
        })(window.moduleB || {});

    ```    
    在浏览器环境中，模块的各个部分通常都是从网上获取的，有时无法知道哪个部分会先加载。如果采用augmentation的写法，第一个执行的部分有可能加载一个不存在空对象，这时就要采用"宽放大模式"。

6. 输入全局变量的写法
    ```
    
        var moduleC = ( function ($){
            console.log('.. This is from globalVariable.js, current url: ', $(location).attr('href'));
        })(jQuery);
    
    ```    
    这样做除了保证模块的独立性，还使得模块之间的依赖关系变得明显。

    