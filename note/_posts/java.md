---
title: java笔记
date:  2019/3/13 20:46:25
tags: 

- java
---

# java

- #### java环境的配置

   java8之前，安装的时候，jdk的路径要和jre的区分开，不然会造成覆盖 java9之后，引入了一种新的Java编程组件，也就是模块，按照Oracle的说法，它是一个可命名的、自描述的代码和数据集合。模块技术的核心目标是减少Java应用和Java核心运行时环境的大小与复杂性。为此，JDK本身进行了模块化，Oracle希望通过这种方式提升性能、安全性和可维护性。    为了支持Java 9的模块，引入一种新的模块化JAR文件形式，按照这种形式会在其根目录中包含一个module-info.class文件。Oracle同时提供了工具，允许我们组合和优化一组模块，形成自定义的运行时镜像（image），这样的镜像不必将整个Java运行时包含进来。模块化所带来的其他变化包括从Java运行时镜像中移除了rt.jar和tools.jar。 更新后，版本带来的变化，模块化后导致不需要或者说将toos.jar和dt.jar文件兼容到其他部分，jdk的lib下面不会再出现这俩文件；也就是说装jdk-9.0.4版本时，配置环境变量时不需要配置classpath变量；    java12只需要配置path变量即可，按照官方文档就ok 
