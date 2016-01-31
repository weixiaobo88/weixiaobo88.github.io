title: 20160129-css-design
date: 2016-01-29 21:36:24
tags: css
---

参考 
[csszengarden](http://www.csszengarden.com/)
[10 BEST CSS PRACTICES TO IMPROVE YOUR CODE](http://www.webdesignerdepot.com/2009/05/10-best-css-practices-to-improve-your-code/)

- 如何设计 CSS
- 项目初期有哪些是预先需要敲定的


?scss 写 placeholder 还是 include??

基本样式, 包括 网站的颜色, 网站的字体, 网站的字号, 间距, 圆角, 布局


- reset 样式 
  * reset styles
  * box-sizing: border-box
- 网站基本设计样式  
  * 颜色表, 网站的颜色只能从这个表中选取
  * 字体表
  * 字号表
  * 间距表
  * 圆角表
  * 布局表, 几种布局的实现, 比如 two-column
  * 比如: body, h1-h5, link:active/visited/hover
- 文件组织结构
  * 按照 feature
  * browser-specific CSS 以单独文件存在
- 命名
   * 文件命名
   * class 的命名
   * 不要使用具体的比如颜色来命名 class
- 编码习惯
   * DON’T REPEAT YOURSELF, 用逗号将共用的样式 group 起来
- 上线前压缩   






