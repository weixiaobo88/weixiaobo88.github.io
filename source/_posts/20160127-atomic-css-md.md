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

总结: ACSS 适应于大的网站, 对小的网站来说并么有明显的优势.


Atomic File Structure
```
mkdir -p atomic-structuring/{utilities,quarks,atoms,molecules} 
```


###Atomic CSS 可能会遇到的问题

如果有两个结构的样式相同, 由于原子样式会写在 markup 上, 所以复用性上就差了点.
另外, 如果这两个样式都想要换的话, 需要改两个地方, 增加了维护成本.

## Atomic Design VS ACSS




## 什么是BEM

BEM 是 Block, Element, Modifier, 是给 class 起名字的方式

比如
```
/* This is the Block */
.block {}

/* This is an element, that helps to form the block as a whole */
.block__element {}

/* This modifies the element or a block*/
.block--modifier {}
```

使用的时候应该注意什么:

- 不要级联元素, 比如不要写成`block__element1__element2`, 而是直接写成 `block__element2`

嵌套的 DOM-tree 和 BEM-tree 的区别:
 
DOM-tree
```
<ul>
  <li>
    <a>
      <span></span>
    </a>
  </li>
</ul>

.ul {}
.ul > li {}
.ul > li > a {}
.ul > li > a > span {}
```

BEM-tree

```
<ul class="menu">
  <li class="menu__item">
    <a class="menu__link">
      <span class="menu__text"></span>
    </a>
  </li>
</ul>

.menu {}
.menu__item {}
.menu__link {}
.menu__text {}
```

更多资料:

- [The BEM site](http://bem.info/method/definitions/)
- [An easy to understand article about BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)
- [Great SO answer by Igor Zenich](http://stackoverflow.com/a/27900589/976972)
 

## 什么是SMACSS

SMACSS 是 Scalable and Modular Architecture for CSS

更多资料:

- [SMACSS website](http://smacss.com/)
- [Smashing Mag article Decoupling HTML from CSS](http://coding.smashingmagazine.com/2012/04/20/decoupling-html-from-css)

## 该如何选择

适合什么样的项目, 有什么优势劣势






