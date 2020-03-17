---
title: node笔记
date:  2019/11/01 20:46:25
tags: 

- node
---

# node

#### referenceError

 在node环境中会报错ReferenceError: Image is not defined。因为Node中没有图片对象 。除此之外，node中也没有很多浏览器才有的对象接口。

vscode中的 run插件只是模拟了Node环境，却并不是浏览器，故用其做很多调试运算也不能，可以选择在chrome中进行调试

