title: 20160204-javascript-listen
date: 2016-02-24 20:19:34
tags:
- JavaScript 
- listen
---


https://www.w3.org/TR/DOM-Level-2-Events/events.html#Events-EventListener

最近看 React - Reflux, 有很多 listen 的方法, 甚是不懂.

翻箱找到 EventListener, 才知道事件处理都和它扯不开.

回答三个问题即可明白:

- `EventListener` 是什么?
- `EventListener` 如何来?
- `EventListener` 如何走?

答案:

- EventListener 是一个处理事件的主要接口方法
- 用户通过 `AddEventListener` 来实现 EventListener 接口并将其注册到 EventTarget 上. 
- 用户通过 `RemoveEventListener` 来移除 EventTarget 上的 EventListener

当 EventListener 上注册的事件发生时, 就会调用 `handleEvent` 方法.

