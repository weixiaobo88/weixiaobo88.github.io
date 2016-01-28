title: 20160127-atomic-css.md
date: 2016-01-27 18:24:56
tags: css
---

参考 [OOCSS, ACSS, BEM, SMACSS: what are they? What should I use?](http://clubmate.fi/oocss-acss-bem-smacss-what-are-they-what-should-i-use/)


## 什么是OOCSS

OOCSS 是 Object Oriented CSS

- structure 和  skin 分开: 定义一个 'gradient', 然后在其他地方 extend 这个 gradient
- container 和 content 分开: 不要级联选择器, 直接写在一个class中, 然后引用这个 class

更多资料:

- [Official OCSS documentation on GitHub](http://github.com/stubbornella/oocss/wiki)
- [Nice read about OCSS in Smashing Magazine](http://coding.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss) 


## 什么是Atomic Approach
Atomic Approach, 出自 [Atomic Design](http://bradfrost.com/blog/post/atomic-web-design/), 因为文章[Challenging CSS Best Practices](http://www.smashingmagazine.com/2013/10/21/challenging-css-best-practices-atomic-approach/)而得到普及. 

同时 Atomic Approach 可以用来组织项目的文件, 参考 [The “Other” Interface: Atomic Design With Sass](http://coding.smashingmagazine.com/2013/08/02/other-interface-atomic-design-sass/)

Atomic Design :

- Atoms
- Molecules
- Organisms
- Templates
- Pages


## 什么是ACSS

每个选择器就定义一次, 然后在 markup 里引入对应的 class name

``` css
.large {
  font-size: 20px;
}  
```
``` html
<span class='large'> Lorem Ipsum </span>  
```

缺点:

- 不能用 media queries, 因为现在样式写在了 markup 上, 不能通过 media queries 来改变

## Atomic Design VS ACSS


## 什么是BEM

## 什么是SMACSS


适合什么样的项目, 有什么优势劣势


