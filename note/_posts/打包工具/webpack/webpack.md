# webpack

###### 是一种构建工具，静态模块打包器

从入口文件，根据依赖图引入模块，形成chunk，在用loader翻译，用plugin处理，形成bundle,输出在出口文件。

开发模式只是本地开发调试的版本。生产模式是上线的版本，对性能有更多要求，对应的plugin也更多。