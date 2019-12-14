---
title: 阮一峰es6读书笔记
date:  2019/5/01 09:46:25
tags: 
- es6
---

# 阮一峰es6读书笔记

### 语句、表达式、return

##### 原生模拟iterator

```javascript
var it = makeIterator(['a', 'b']);

it.next() // { value: "a", done: false }
it.next() // { value: "b", done: false }
it.next() // { value: undefined, done: true }

function makeIterator(array) {
  var nextIndex = 0;
  return {
    next: function() {
      return nextIndex < array.length ?
        {value: array[nextIndex++], done: false} :
        {value: undefined, done: true};
    }
  };
}
```

##### 

##### 补充函数声明的3种方式

| 函数声明                              |                  |
| ------------------------------------- | ---------------- |
| `function print (...args){}`          | function命令     |
| `var print =function(...args){}`      | 函数表达式       |
| `var print =new Function(...args,{})` | Function构造函数 |

##### 方法的两种写法

| 方法                        |                                                |
| --------------------------- | ---------------------------------------------- |
| `print(...args){}`          | 缩写                                           |
| `print:function(...args){}` | 一般写法（也算是表达式类的写法类似a:3或者1+3） |

##### 解析

###### 表达式、语句

> 此处附上阮一峰es5中关于语句与表达式的描述
>
> 语句（statement）是为了完成某种任务而进行的操作，比如下面就是一行赋值语句。
>
> `1 + 3`叫做表达式（expression），指一个为了得到返回值的计算式。
>
> 语句和表达式的区别在于，前者主要为了进行某种操作，一般情况下不需要返回值；后者则是为了得到返回值，一定会返回一个值。表达式一般放在函数的return里面。或者一些api，比如vue的几个钩子，data里面的return，methods里面，放的都是表达式。

此处代码，定义了makeIterrator函数，其中返回一个方法next

这里为什么要把next放到return里面,为什么要在next方法里面也return

```javascript
//如果直接这么写，不要第一个return，会报错
function makeIterator(array) {
  var nextIndex = 0;
    next: function() {                  //这里也可以next(){}
      return nextIndex < array.length ?
        {value: array[nextIndex++], done: false} :
        {value: undefined, done: true};
    }
}
//因为这么写，相当于a:3，这么写肯定是错的啊，只有值，没有对应的赋值操作。要不就这么写let next=function(){},这样语法是对的，但你在一个函数里再声明一个函数有啥用嘞。
//故需要借助return,把这个方法给返回出来，当你调用这个函数的时候，就返回一个数据结构，内部有一个可以调用的next方法。
//next方法内的return，同理， {value: array[nextIndex++], done: false}，这个东西只是一个值，你需要赋值操作或者return出来。赋值没意义， 要把这个值给renturn出来，不然虽然你处理了这个值，但不return的话，外面取不到这个值，也没啥用。
//此处用var it = makeIterator(['a', 'b']);是因为，需要把这个返回的数据结构赋值给一个变量。不然你直接this. makeIterator(['a', 'b']);虽然语法不会报错，但没有意义，的确生成了一个数据结构，但你没有把他赋值给任何变量，从而你访问不到这个数据结构。
```

###### return的区分

```javascript
return index <(x.length)? {value:x[index++],done:false}:{value:undefined,done:true} //正确
return{index <(x.length)? {value:x[index++],done:false}:{value:undefined,done:true}}//错误
```

return 一个值，比如return 0;

return一个对象 ，比如vue中的data，return{x:1,y:2};

此处明显是return一个已经有括号的对象出来，就不要加括号了，此处的括号不是代码块的意思，也不能在外面包一个括号表示代码块，因为return后面肯定是跟一个值的，就不会是语句，所以不要用代码块{}，尽管代码不会报错，但某些检查工具会提示错误，这样写也没意义。

###### 函数传递参数

```javascript
function makeGenerator(x) {
    var index =0;
    return{
        next(){
            return index <(x.length)? {value:x[index++],done:false}:         {value:undefined,done:true}
        }
    }
}
//next里的x用的是makeGenerator（x）传进来的x
```

```javascript
function makeGenerator(x) {
    var index =0;
    return{
        next(x){
            return index <(x.length)? {value:x[index++],done:false}:{value:undefined,done:true}
        }
    }
}
let a= makeGenerator(x);
a.next(x);
//此处 makeGenerator(x)传进去的x并没有使用，next里面的x,是在调用next方法时传禁区的x（优先匹配上一级）
```

###### index++ 与++index

通用的一种数据结构处理的写法，算是表达式的一种，会改变Index的值。前者先用，用完再加。后者先加，加完再用。此处这么写可以简化少写一句index+=1;

###### index+=1

此处补充一点c语言/java中的小数计算。

JS中，当他们都是Number都为整数的时候，a=a+1与a+=1是一样的。(String也会被转换Number)

但在java/c中，两者不一定相等。

```java
//java中
public class Test{
   public static void main(String[] args){
       short a=1;
       a+=1;   //a=2
       short b=1;
       b=b+1;  //报错，因为b是short,1是init
   }
}
```



```c
//c中
int a = 2;
a += 1.2;    // 不报错，最终 a = 3
a = a + 1.2; // 报错，a是init,1.2不是init
```



### Iterator遍历器

> 遍历器（Iterator）一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作。Iterator 的作用可以是提供一个访问接口来顺序遍历数据结构（他并不能直接遍历，他只是一个接口，需要外部去访问调用他），主要供for..of消费。
>
> 本质上来说遍历器对象就是一个指针对象，通过next()来改变指向。



### Set与Map

#### set

##### 遍历操作

> 这里提到了`Set.prototype.values()/keys()/entries()`均返回**遍历器**。遍历器不要直接输出，输出的结果不太好。只能通过循环或者用`generator`中的`next`进行挨个输出。

###### 例如直接输出set结构与分别输出不一样

```javascript
const b=new Set([1,2,3,4,5,5]);
console.log(b.entries())
for (let i of b.entries())
{ console.log(i)}
/**
[Set Iterator] { 1, 2, 3, 4, 5 }
[ 1, 1 ]
[ 2, 2 ]
[ 3, 3 ]
[ 4, 4 ]
[ 5, 5 ]
*/
```

###### mdn中关于Set.prototype.entries()用next输出

```javascript
var mySet = new Set();
mySet.add("foobar");
mySet.add(1);
mySet.add("baz");

var setIter = mySet.entries();
/**
console.log(setIter.next().value); // ["foobar", "foobar"]
console.log(setIter.next().value); // [1, 1]
console.log(setIter.next().value); // ["baz", "baz"]
*/
```

