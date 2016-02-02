title: 20160201-scrolling-messages
date: 2016-02-01 20:18:28
tags: jquery
---


做一个滚动新闻


```html
<div class="scroll_list">
    <span class="notice">最新消息</span>
    <ul class="scroll_list_contents">
      <li>
        <p class="yscrollfont">
          <a href="#" target="_blank">
            Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium
          </a> 
        </p>
      </li>
      <li>
        <p class="yscrollfont">
          <a href="#" target="_blank">
            totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo
          </a>
        </p>
      </li>
      <li>
        <p class="yscrollfont">
          <a href="#" target="_blank">
            Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit
          </a>
        </p>
      </li>
      <li>
        <p class="yscrollfont">
          <a href="#" target="_blank">
            sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt
          </a>
        </p>
      </li>
      <li>
        <p class="yscrollfont">
          <a href="#" target="_blank">
            Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet
          </a>
        </p>
      </li>
    </ul>
</div>
```
```jquery
$(function(){
  setTimeout(function(){
    var itemHeight = 40;
    var marginTop = 0;
    $($(".scroll_list_contents li ")[0]).clone(true).insertAfter($($(".scroll_list_contents li ")[$(".scroll_list_contents li ").length - 1]));

    function move() {
      marginTop = marginTop - itemHeight;
      if (marginTop >= -($(".scroll_list_contents li ").length - 2) * itemHeight) {
        $(".scroll_list_contents ").animate({
          marginTop: marginTop
        }, 2000);
      } else {
        $(".scroll_list_contents").animate({
          marginTop: marginTop
        }, 2000, function() {
          marginTop = 0;
          $(".scroll_list_contents").css({
            marginTop: 0
          });
        });
      }
    };

    var t = setInterval(move, 4000);
    $(".scroll_list_contents ").hover(function() {
        clearInterval(t);
    }, function() {
        t = setInterval(move, 4000);
    })       
  },500);
});
```
```css
.scroll_list {
  border-bottom: 1px solid #DFDFDF;
  width: 100%;
  overflow: hidden;
}

.scroll_list,
.scroll_list_contents,
.scroll_list_contents > li
{
  height: 40px;
}

.scroll_list_contents {
  margin-left: 200px;
  margin-top: -40px;  
}

.notice,
.scroll_list_contents,
.scroll_list_contents > li,
.yscrollfont,
.yscrolltime {
  display: inline-block;
}

.notice {
  width: 200px;
  text-align: center;
  display: inline-block;
  line-height: 40px;
}

.scroll_list_contents > li {
  line-height: 40px;
  width: 1000px;
}

.yscrolltime {
  margin-left: 40px;
}      
```

