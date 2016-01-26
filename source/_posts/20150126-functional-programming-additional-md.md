title: 20150126-functional-programming-additional.md
date: 2016-01-26 20:09:53
tags: functional-programming
---


## Pure Function

### 概念
```
纯函数是指输入相同, 输出相同的函数, 而且没有任何副作用.
副作用指: 改变文件系统, 插入数据到数据库, http调用, 值的改变, 打印, 获取用户输入, 查询DOM, 访问系统状态等. 
```

### 纯函数有什么优势 

- **Cacheable**
  * 纯函数可以根据输入进行缓存, 这通常叫做memoization
- **Portable / Self-Documenting**
  * 需要依赖的东西会在参数中显示出来, 可移植性比较好 
- **Testable**
- **Reasonable**
  * referential transparency
- **Parallel Code**


### 面向对象语言的问题
    
> The problem with object-oriented languages is they’ve got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana... and the entire jungle    

