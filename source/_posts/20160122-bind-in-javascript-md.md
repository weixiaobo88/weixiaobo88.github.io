title: Bind in JavaScript
date: 2016-01-22 22:19:32
tags: 
- JavaScript 
- bind
---

参考 
[Bind MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_objects/Function/bind)
[StackOverflow](http://stackoverflow.com/questions/15455009/javascript-call-apply-vs-bind)
[blog](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/)
[gitbook](https://drboolean.gitbooks.io/mostly-adequate-guide/content/) 

## bind 函数语法

`fun.bind(thisArg[, arg1[, arg2[, ...]]])`

其中:
 
 - fun 是已存在的函数
 - bind 是关键字
 - thisArg 是你想绑定的 target
 - arg1, arg2 ... 是绑定到 thisArg 上的 fun 方法的参数


## bind 函数是什么

bind() 函数会创建一个新函数（称为绑定函数），新函数与被调函数（绑定函数的目标函数）具有相同的函数体。
当目标函数被调用时 this 值绑定到 bind() 的第一个参数，该参数不能被重写。
绑定函数被调用时，bind() 也接受预设的参数提供给原函数。

## bind 函数和 call 有什么区别

bind 函数和 call 都是将 this 绑定到函数或对象上, 不同之处在于函数的调用上.

call 将 this 绑定到函数上, 并立即执行这个函数.

```
var person = {  
	name: "James Smith",
	hello: function(thing) {
		console.log(this.name + " says hello " + thing);
	}
}

person.hello.call(person, "world"); // output: James Smith says hello world
```

bind 将 this 绑定到函数上, 需要单独调用:

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

或者这样:

```    
var helloFunc = person.hello.bind(person, "world");
helloFunc();  // output: James Smith says hello world
```


## bind 函数在什么情况下用

- 借一个函数或复制一个函数
- 设置 this 的值
- 可以把方法赋值给一个变量, 当函数使用
- currying 函数
  * 函数柯里化, 也是偏函数应用, 一个函数会返回一个新的函数, 并预设了一些参数.

```javascript
var person = {
              name: 'li', 
              say: function(hello){ 
                     console.log(this.name + ' say ' + hello)
                   }
             }; 							
var cat = {name: 'cat'};
var catSay = person.say.bind(cat);
catSay('miao~');  //cat say miao~

var catSayHi = person.say.bind(cat, 'hi');
catSayHi(); //cat say hi	    
```


## apply 和 call在什么情况下用

两种情况:

- 借一个函数
- 设置 this 的值

### apply 函数还可以应用于可变参数函数

#### 什么是可变参数函数?

Math.max() 就是一个可变参数函数, 你可以传任意多个参数给它.

```
console.log(Math.max(2, 3, 1, 5, 8));
```

但是我们不能给 Math.max() 传一个数组作为参数, 但是 apply 可以帮我们做到.
 
```
console.log(Math.max.apply(null, [2, 3, 1, 5, 8]));
```

