title: 20160313-lazy-loading-images
date: 2016-03-13 16:15:19
tags: 

- performance
- images 
- lazy-loading

---

http://pinggod.com/2016/Lazy-loading-images-on-the-web/


## 问题是什么

图片在页面上的占有大小越来越大, 页面性能受到影响。

相关资料显示, 在 2015 年 5 月, web page 平均大小已经超过 2 MB, 这是 3 年前的 2 倍。


## 如何解决这个问题

解决方法: lazy load images

## 如何来实现 lazy load

本质上是通过 JavaScript 来判断 viewport 中能看到的图片。

- HTML 文件中的 src 标签上使用 data attribute

```
<img data-src="images/Robin.jpg" alt="" />
```

- 改变 viewport 或者 scroll 看哪些图片会出现或者即将出现
- 交换 src 和 data-src 的值

### 使用 PLAIN JAVASCRIPT 来实现

- 先判断元素是不是在 viewport 中
- 监听引起 viewport 的事件, `DOMContentLoaded` `load` `resize` `scroll` 

```
function isElementInViewport (el) {

    var rect = el.getBoundingClientRect();

    return (
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) && /*or $(window).height() */
        rect.right <= (window.innerWidth || document.documentElement.clientWidth) /*or $(window).width() */
    );
}

//these handlers will be removed once the images have loaded
window.addEventListener("DOMContentLoaded", lazyLoadImages);
window.addEventListener("load", lazyLoadImages);
window.addEventListener("resize", lazyLoadImages);
window.addEventListener("scroll", lazyLoadImages);

function lazyLoadImages() {
  var images = document.querySelectorAll("#main-wrapper img[data-src]"),
      item;
  // load images that have entered the viewport
  [].forEach.call(images, function (item) {
    if (isElementInViewport(item)) {
      item.setAttribute("src",item.getAttribute("data-src"));
      item.removeAttribute("data-src")
    }
  })
  // if all the images are loaded, stop calling the handler
  if (images.length == 0) {
    window.removeEventListener("DOMContentLoaded", lazyLoadImages);
    window.removeEventListener("load", lazyLoadImages);
    window.removeEventListener("resize", lazyLoadImages);
    window.removeEventListener("scroll", lazyLoadImages);
  }
}
```

### 使用 JQUERY

```
$(window).on('DOMContentLoaded load resize scroll', function () {;
  var images = $("#main-wrapper img[data-src]");
  // load images that have entered the viewport
  $(images).each(function (index) {
    if (isElementInViewport(this)) {
      $(this).attr("src",$(this).attr("data-src"));
            $(this).removeAttr("data-src");
    }
  })
  // if all the images are loaded, stop calling the handler
  if (images.length == 0) {
    $(window).off('DOMContentLoaded load resize scroll')
  }
})

// source: http://stackoverflow.com/questions/123999/how-to-tell-if-a-dom-element-is-visible-in-the-current-viewport/7557433#7557433
function isElementInViewport (el) {
    var rect = el.getBoundingClientRect();

    return (
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <= $(window).height() &&
        rect.right <= $(window).width()
    );
}
```

## 这两种解决方案的问题

- 成功和错误处理
- responsive images 的 srcset 和 picture
- 图片没有全部下周完的处理
- 图片出现时的动画或者变化

有很多库实现了这些:

- [Lazy Load Plugin for jQuery](http://www.appelsiini.net/projects/lazyload)
- [bLazy](http://dinbror.dk/blazy/) 不需要 jQuery
- [Unveil](http://luis-almeida.github.io/unveil/) 需要 jQuery
- [Lazy Load XT](https://github.com/ressio/lazy-load-xt)
- [Telerik Platform – Responsive Images Service](http://docs.telerik.com/platform/backend-services/javascript/responsive-images/introduction)

