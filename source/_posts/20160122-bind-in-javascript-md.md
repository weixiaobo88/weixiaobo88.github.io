title: Bind in JavaScript
date: 2016-01-22 22:19:32
tags: bind
---

参考 
[Bind MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind)
[StackOverflow](http://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind) 

## bind 函数语法

`fun.bind(thisArg[, arg1[, arg2[, ...]]])`

其中:
 
 - fun 是;
 - bind 是关键字
 - thisArg 是你想绑定的 target
 - arg1, arg2 ... 是绑定到 thisArg 上的 fun 方法的参数


## bind 函数是什么

bind() 函数会创建一个新函数（称为绑定函数），新函数与被调函数（绑定函数的目标函数）具有相同的函数体。
当目标函数被调用时 this 值绑定到 bind() 的第一个参数，该参数不能被重写。
绑定函数被调用时，bind() 也接受预设的参数提供给原函数。

## bind 函数和 call 有什么区别

They all attach this into function (or object) and the difference is in the function invocation (see below).

call attaches this into function and executes the function immediately:

```
var person = {  
  name: "James Smith",
  hello: function(thing) {
    console.log(this.name + " says hello " + thing);
  }
}

person.hello.call(person, "world"); // output: James Smith says hello world
```

bind attaches this into function and it needs to be invoked separately like this:

```
var person = {  
  name: "James Smith",
  hello: function(thing) {
    console.log(this.name + " says hello " + thing);
  }
}

var helloFunc = person.hello.bind(person);
helloFunc("world");  // output: James Smith says hello world
```

or like this:

```    
var helloFunc = person.hello.bind(person, "world");
helloFunc();  // output: James Smith says hello world
```

## bind 函数在什么情况下用

- 设定某个函数调用的 this  值
- 预设初始参数
- callback 中传递 this
- 快捷调用

