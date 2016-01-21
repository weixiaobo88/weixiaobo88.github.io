title: Monad 
date: 2016-01-18 20:18:14
tags: functional-programming
---

参考: 
- [图解 Monad](http://www.ruanyifeng.com/blog/2015/07/monad.html?utm_source=tuicool)
- [Monad Wiki](https://en.wikipedia.org/wiki/Monad_%28functional_programming%29)

软件的基本结构就是数据+过程

数据: 数据类型
过程: 顺序, 分支, 循环

值函数: 处理值的函数

## Monad 是什么

Monad 是一个描绘了一系列计算步骤的结构, 其中这个结构的 type 定义了如何把操作链起来, 或者把那个 type 的函数嵌套起来
表示将一个运算过程，通过函数拆解成互相连接的多个步骤。
你只要提供下一步运算所需的函数，整个运算就会自动进行下去。

## 为什么会有 Monad, 它的出现解决了什么问题

## Monad 有什么用

## Monad 如何用起来
