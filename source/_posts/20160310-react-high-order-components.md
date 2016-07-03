title: 20160310-react-high-order-components
date: 2016-03-10 15:30:47
tags: react
-----------

参考
http://jamesknelson.com/structuring-react-applications-higher-order-components/
https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750#.aioi9e57j


## 问题是什么

为了复用 React 的组件, 原有组件会改成的很长而难以维护.
在 ES6 不再支持 mixins 的情况下, 该如何来解决这个问题?
 
- 给子节点传一些未知的 props
- 写很长的 css 名字
- 合并在 props 上指定的内部回调


## 解决方案是什么

解决方案是 Higher-Order components (HOCs).

HOCs 是在已有的 component 上加一些其他功能的 JavaScript Functions.

```
是否存在已有概念能帮助我理解 Higher-Order components?

是的. 

- React component 可以给你的 app 增加功能, HOCs 可以给你的 component 增加功能.
- HOCs 可以帮你自动生成代码.(在 ruby 中叫做 元编程)
```

### 看代码

```
// See https://www.npmjs.com/package/except
import except from 'except';

function passthrough(component) {
    const passthroughProps = Object.keys(component.propTypes);

    return class extends component {
        render() {
            super.render(except(this.props, passthroughProps))
        }
    }
}
```

### HOCs 如何帮助我 Structure app

HOCs 帮助你的app实现关注点分离.


## 如何设计有用的 HOCs 

你可以尝试回答以下问题?

- 使用 HOC 会让 component 的代码更清楚吗?
- 使用 HOC 会让 application 更容易维护吗? 修改成本更低
- HOC 有依赖吗?
- HOC 可以在其他 application 中复用吗?

你可能会发现好的 HOC 能减少代码量, 但并不总是这样.
好的设计和少的代码量并不是等同的.

### 例子

```
function render() {
    const className = `app-Paper app-Paper-${this.props.shape} ${this.props.className || ''}`;

    return (
        <div className={className}>
          <div className="app-Paper-inner">
            ...
          </div>
        </div>
    );
}
```
```
function c(appPrefix) {
    return function(component) {
        const prefix = `${appPrefix}-${component.name}`;

        component.prototype.cPrefix = function(name) {
            return `${prefix}-${name}`;
        };

        component.prototype.cRoot = function(name) {
            return `${prefix} ${name ? prefix+'-'+name : ''} ${this.props.className || ''}` ;
        };
    }
}
```





