---
title: NPM自用整理
date:  2019/03/22 20:46:25
tags: 
- npm
---

# NPM自用整理

设置淘宝源

```c
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

[npm中文文档](https://www.npmjs.cn/)

| 命令                       | 作用                     |
| -------------------------- | ------------------------ |
| `npm init`                 | 初始化 生成package.json  |
| `ctrl +c`                  | 撤销                     |
| `npm i`                    | 下载依赖                 |
| `npm i --save`             | 下载依赖并存到生产依赖中 |
| `npm i --save dev`         | 下载依赖并存到开发依赖中 |
| `npm uninstall -g`         | 全局删除包               |
| `npm uninstall`            | 删除包                   |
| `npm uninstall --save`     | 生产依赖卸载包           |
| `npm uninstall --save dev` | 开发依赖卸载包           |
| `npm undate`               | 更新包                   |
| `npm outdated`             | 是否有包过期             |

升级Npm

```
npm install npm@latest -g
```

升级包

```
npm update -g
```

升级了Node后，老项目需要重构node-sass

```
npm rebuild node-sass
```



`npm i` 报错的时候，有可能是npm缓存机制问题。执行下列命令删除缓存，重置淘宝源

```
npm cache clean –force
npm install –registry=https://registry.npm.taobao.org
npm install -g 
cnpm –registry=https://registry.npm.taobao.org
```