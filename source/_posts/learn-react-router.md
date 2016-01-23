title: learn-react-router
date: 2016-01-11 20:35:47
tags: 
- react
- react router
---

参考资料： https://github.com/rackt/react-router/blob/0.13.x/doc/06%20Mixins/State.md

翻译： React Router 0.13.x 中的 State

State 是 components 的一个 mixin, 它需要知道 active params, query 和 routes. 任何拥有动态 segments 的路由处理器都想拥有 State.

## 实例方法

### `getPath()`

返回当前 URL 路径, 包含 query 字符串

### `getPathname()`

返回当前 URL 路径, 不包含 query 字符串

### `getParams()`

返回当前活跃的 URL 参数的哈希

### `getQuery()`

返回当前活跃的 query 参数的哈希

### `isActive(routeName, params, query)`

当一个路由, 参数, query 是活跃的就返回 true, 反之返回 false

### `getRoutes()`

以嵌套的形式返回当前活跃路由的数组


## 示例

通常你只想获得参数(params) 和 query:

    
```js

// route
<Route name="user" path="user/:name" handler={User} />

// handler
var User = React.createClass({
 mixins: [ Router.State ],

 render: function () {
   var name = this.getParams().name;
   return (
     <div>
       <h1>{name}</h1>
     </div>
   );
 }
});
```

如果你用 bootstrap 并且想得到 Tabs 上 li 标签中活跃的元素:

```js
var Link = require('react-router').Link;
var State = require('react-router').State;

var Tab = React.createClass({

  mixins: [ State ],

  render: function () {
    var isActive = this.isActive(this.props.to, this.props.params, this.props.query);
    var className = isActive ? 'active' : '';
    var link = (
      <Link {...this.props} />
    );
    return <li className={className}>{link}</li>;
  }

});

// use it just like <Link/>, and you'll get an anchor wrapped in an `li`
// with an automatic `active` class on both.
<Tab to="foo">Foo</Tab>
    
```