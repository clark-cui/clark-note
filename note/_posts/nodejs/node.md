---
title: node笔记
date:  2019/11/01 20:46:25
tags: 

- node
---

# node

#### 版本控制

```
npm cache clean -f //先清除缓存 -f是force
```



###### 方法一 n(支持mac/linux,windows好像不行，百度查查新版本可以了吗)

```
# 全局安装n
$ npm install -g n   //报错可用npm i -g n --force
# 升级到最新稳定版
$ n stable 
# 升级到最新版
$ n latest
# 升级到定制版
$ n v7.10.0
# 切换使用版本
$ n 7.10.0 (ENTER)

$ n rm 7.10.0 //删除某个版本
$ n use 7.10.0 some.js //使用某个版本执行js
```



###### 方法二 nvm

```
官网下载安装，配置环境变量
https://blog.csdn.net/fengshi_fengshi/article/details/80670585

$ nvm --version
# 升级到到定制版
$ nvm install 7.10.0
# 升级到最新版
$ nvm install lastest
# 升级到稳定版
$ nvm install stable
$nvm use 7.10.0 切换版本
```



#### referenceError

 在node环境中会报错ReferenceError: Image is not defined。因为Node中没有图片对象 。除此之外，node中也没有很多浏览器才有的对象接口。

vscode中的 run插件只是模拟了Node环境，却并不是浏览器，故用其做很多调试运算也不能，可以选择在chrome中进行调试

#### export

module.exports={} //后面可以接key-value对象，也可以是数组或者别的

exports={}//后面只可以接key-value对象

综上，统一使用module.exports