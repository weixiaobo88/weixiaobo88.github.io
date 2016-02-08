title: 20160130-touring-on-freecodecamp
date: 2016-01-30 17:09:51
tags: touring
---

http://www.freecodecamp.com/

一个不错的网站, 我只想赶紧通过学习, 有机会能在开源项目上贡献自己的力量.

- HTML
- CSS
- jQuery
- JavaScript
 

margin 是一个元素的边框和周围其他元素的距离, 如果 margin 是负数, 那么这个元素会扩大.


## Bootstrap

- Fluid 流式布局
- Grid System

## Font Awesome

Font Awesome 是一个 icon 库, 这些 icon 都是矢量图形, 以 `.svg` 为文件名后缀. 这些 icon 可以像 font 一样使用, 比如用 px 来设定 size.

```
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.5.0/css/font-awesome.min.css"/>
```

## Form

如何让 radio 的文本可点?

两种方式:

- 在 `input` 上加 id, 在 `label` 上加 for
```
<label for='btn-like'> Like </label>
<input type='radio' id='btn-like'/>
```
- 将 `input` 包在 `label` 中
```
<label><input type="radio">like</label>
```


## jQuery

```
$(selector).addClass();
$(selector).removeClass();
$(selector).css();
$(selector).props();
```