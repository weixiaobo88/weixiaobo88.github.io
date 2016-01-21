title: 20160121-npm-package-file.md
date: 2016-01-21 21:41:04
tags: npm, package.json
---

## `package.json`文件

这个文件必须是 JSON 文件.


### `main` field

`main`是程序的主要入口点, 是一个 module 的 ID. 

- 默认情况下是相对于包所在文件夹的根目录.
- 也有可能是作为 main script.

举个例子, 如果你的包名为 `foo`, 当用户安装这个包之后, 可以使用 `require('foo')`.

