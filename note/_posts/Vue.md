---
title: Vue笔记
date:  2019/11/01 20:46:25
tags: 
- Vue
---

### 虚拟dom

> 就是一个属性描述的Js对象

[virtual Dom](https://juejin.im/post/5d31c6c35188252d1d5f9c98)

[virtual Dom](https://juejin.im/post/5d36cc575188257aea108a74)

##### 笔记（待补充，这一部分涉及到源码，很多没看懂，等下次突击完再补充）

vue中的virtual Dom就是VNode。Vue中调用creatElement方法生成VNode,数据更新触发update方法视图更新，update方法中调用了path函数，patch函数用diff算法，比较新Vnode与旧的VNode，之后再生成dom。

> 原本没有虚拟dom的情况下，对比dom极其困难，最好的做法是重新生成一棵树来进行替换，但这样做性能极差，尤其是dom节点过多的情况下。为了解决这个问题，在dom上方放了层只含有部分必要信息的虚拟dom。当发生变动时，可精确匹配需要更新的dom、attributes、event listener…，然后再精确的更新到真实dom上，减少受影响的dom。但既然有了虚拟层，自然就有了跨平台的副产物，比如像RN。
>
> 但事实上，虚拟dom并非那么高效。尤其是dom节点足够小的情况下、或者确实需要整个替换的情况下，直接生成一棵树比diff后再生成要明显高效很多。但虚拟dom的好处是提供了多数场景下的一种通用处理方法。

### watch中this的指向

 vue的watch中如果用箭头函数写回调，所以this会取上下文，而不是组件里面的this了，故需要用普通函数。

同理不能在methods用箭头写方法

#### 用vuex进行状态管理

避免使用路由。路由仅支持单页面传值，当2个以上页面回退在进入就会丢失参数。

#### mounted activated

 调用接口写在mounted，activated仅仅放回退时需要重新刷新的内容，比如设置标题。 

#### deactivated destroyed

加了router-view的单页面组件可以用activated与destroyed钩子，deactivated与destroyed都是页面销毁，执行那个自己看。

#### data中的 ||

```javascript
 time:this.$store.state.time||time()  
```

  如果缓存了time就用time,否则就调用time方法，time()是export function。 

#### 用三元代替if else

#### 用if return 代替无交集处理的if else

#### v-bind

 方式一： :class="has ? 'bg':'bgNone'"  :class="index === lists.length-1 ? 'cardLast': 'card'"  （注意外面双引号，内部单引号）

 方式二： :class="{timeItem:a.status,noTime:!a.status}" 这是官方示例的写法 

方式三： :class="[isActive ? activeClass : '', errorClass]" 数组的写法，第二项为固定class 

#### 点击变色

方式一（自用）：

点击时候触发方法传递Index，在方法中改变某个变量的值。该变量决定了这个dom的class，通过切换class实现变换。

方式二（看到的，不好）:

  :style="{backgroundColor:click[index]? 'white':'#f8f8f8'}" 

此处的click是一个数组，index是这个dom的顺序，点击时候触发方法，在方法中添加该数组的Index项目为true



#### dom渲染完后的函数

 vue等待渲染完执行的函数 

```javascript
vm.$nextTick(function({console.log(...)})) 
```

#### 不能直接改变prop

> [Vue warn]: Avoid mutating a prop directly since the value will be overwritten whenever the parent component re-renders. Instead, use a data or computed property based on the prop's value. Prop being mutated: "indexE" 

不能直接修改prop,应该emit在父组件中修改 

#### vue的v-html样式

 vue的v-html只能在里面写样式，在@import里的scss无效 

#### mounted

 mounted表示渲染完执行，但是并不代表里面的异步操作也在渲染完的时候就执行完 

#### ref

```vue
<div class="home" ref="productionBox">
this.screenWidth = this.$refs.productionBox.clientWidth;
 this.screenHeight = this.$refs.productionBox.clientHeight;
```

