title: React-Bootstrap-Introduction
date: 2016-01-12 20:21:38
tags: react bootstrap
---

# 介绍 —— 使用React重建最受欢迎的前端框架

React-Bootstrap 是一个可重用的前端组件库。用 Facebook 的 React.js
框架，你能构建一个和 Twitter Bootstrap 类似的库，但是代码会更整洁。

如果你想要一个小的 button ，button 上显示 “Something”，并能触发 someCallback
函数。如果你是在写一个原生的 app，你可能会像下面这样写：

```
button(size=SMALL, color=GREEN, text="Something", onClick=someCallback)
```

如果用 Twitter Bootstrap，你会写下面的 HTML：

```html
<button id="something-btn" type="button" class="btn btn-success btn-sm">
  Something
</button>
```

然后会在 JavaScript 中写一些类似这样的代码：
`$('#something-btn').click(someCallback);`

从 web 的标准来看，这挺好，只是还有些不好。 React-Bootstrap 可以让你写成这样：

```
<Button bsStyle="success" bsSize="small" onClick={someCallback}>
  Something
</Button>
```

具体的 HTML/CSS
实现细节已经进行了抽象，提供给你的接口可以让你像其他编程语言一样来写。


## 使用 React.js 的 Bootstrap API

Bootstrap 的代码重复的很多，因为 HTML 和 CSS
不支持组件库的抽象。这也是为什么你需要在一个元素 `button` 中写 三次`btn`。

React.js 解决这个问题的方式就是直接写在 JavaScript 中。 React
接管了渲染页面的整个任务。你只需要把 JavaScript
对象树传给它即可，并且把状态告诉它。

举例来说，我们想让 React 渲染一个页面，只显示一个 button，并用 Bootstrap CSS
来给它加样式：

```
var button = React.DOM.button({
  className: 'btn btn-lg btn-success',
  children: 'Register'
});

React.render(button, mountNode);
```

但是现在在 JavaScript 中，我们可以包裹 HTML/CSS，然后提供一个更好的 API：

```
var button = ReactBootstrap.Button({
  bsStyle: 'success',
  bsSize: 'large',
  children: 'Register'
});

React.render(button, mountNode);
```

React-Bootstrap 就是类似这样的组件库，你可以很容易的扩展和加强你的功能。


## JSX 语法

每个 React 组件就是一个 JavaScript 对象，写成树形结构也会很烦。React 鼓励使用 JSX
的语法糖，你可以和像 HTML 的语法一些样来写：

```
var buttongGroupInstance = (
  <ButtonGroup>
    <DropdownButton bsStyle='success' title='Dropdown'>
      <MenuItem key='1'>Dropdown link</MenuItem>
      <MenuItem key='2'>Dropdown link</MenuItem>
    </DropdownButton>
    <Button bsStyle='info'>Middle</Button>
    <Button bsStyle='info'>Right</Button>
  </ButtonGroup>
);

React.render(buttonGroupInstance, mountNode);
```

有些人对 React.js 的第一印象就是混合 JavaScript 和 HTML
会让代码看起来很混乱。然而，比较在这个例子中要添加一个 dropdown button 在
Bootstrap JavaScript 和 Component 文件中，Component
文件需要分成两个，因为你需要在代码中两个地方来实现这个组件：首先必须添加
HTML/CSS 元素，然后必须调用 JavaScript 把这两个组件写到一起。

React-Bootstrap 的组件希望遵循 React.js 的哲理，单独的功能需要放在单独的地方。
在 [组件页面](http://react-bootstrap.github.io/components.html) 查看当前的 React-Bootstrap 库。






