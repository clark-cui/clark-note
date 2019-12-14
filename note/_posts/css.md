---
title: css笔记
date:  2019/3/13 20:46:25
tags: 

- css
---

# css

- #### 盒子超出问题


 出现盒子超出，要不就box-sizing:border-box; 不行就再把margin换成padding 或者留着margin width 100%改为auto 即可。 或者用margin 然后把height减去margin。 或者用padding border-box,然后height加上padding。 

- #### 在html中style里写有连接符的属性用驼峰转译



- #### 去掉ios横向滚动条

   3级dom.

  第一级overflowhidden,

  第二级overflow-x:scroll,y:hidden，并加padding-bottom。

  第三级里面放循环元素，宽度max-content.

- #### 权重问题

   同时设置属性无效，是因为伪类得权重没有正常得权重大（当只有1个元素时，伪类失效，就是nth-child(1)失效）

  ```javascript
             p{
                  font-size: px(28);
                  color: #666666;
                  text-align: left;
                  padding: px(10) px(40) 0 px(40);
                  margin: 0;
              }
              p:first-child{
                  padding: px(30) px(40) 0 px(40);
              }
  ```

  

- #### p标签自带margin

  用通配符消除

- #### 透明度

   background-color 设置透明度

   方法一：

   opacity: 0.1; 

  background: #FFFFFF; 

   opacity会让子元素带上同样的透明度

  方法二（推荐）  

   background-color: rgba(255,255,255,0.1);   

  这种方式只会设置该元素背景透明度，不会影响到子元素。 

- #### 吸顶

   避免使用fixed 

  方法一：首先让不动的div 和要动的div竖直排列，flex-direction:column; 设置需要滚动栏：overflow:scroll； 设置不动栏：positon:absolute，滚动时和下文会重叠。不设则不会重叠。需要三级dom 
  
  
  
  方法二（推荐）：flex grow:1,overflow:scroll. 需要二级dom

- #### 组件样式

  /deep/

  !important

- #### 图片属性

  ```css
  object-fit
  ```

  

