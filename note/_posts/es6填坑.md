---
title: es6填坑
date:  2019/4/21 20:46:25
tags: 
- es6
- javascript
---

# es6填坑

### 数组的扩展运算符

> 扩展运算符（spread）是三个点（`...`）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。该运算符主要用于函数调用。

```javascript
let arrAll=[];
let arr=[true,true,true,true,true,true,true];
// arrAll.push(...arr);  //输出[true,true,true,true,true,true,true]
arrAll.push(arr);        //输出[[true,true,true,true,true,true,true]]
console.log(arrAll);  
```

### call aplly bind 箭头与this

`call` 和 `apply` 都是为了解决改变 `this` 的指向。作用都是相同的，只是传参的方式不同。

除了第一个参数外，`call` 可以接收一个参数列表，`apply` 只接受一个参数数组。

`bind` 和其他两个方法作用也是一致的，只是该方法会返回一个函数。并且我们可以通过 `bind` 实现柯里化。

箭头函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。不能用call apply bind去改变箭头函数的this指向，因为其指向在定义时就已经固定。

```javascript
let a = {
    value: 1
}
function getValue(name, age) {
    console.log(name)
    console.log(age)
    console.log(this.value)
}
getValue.call(a, 'yck', '24')
getValue.apply(a, ['yck', '24'])
```

###### 不适合用箭头的场合

第一个场合是定义对象的方法，且该方法内部包括`this`。若用箭头，则this就会指向window，当调用这个方法的时候，this就没法指向调用时的外围实例，从而导致取不到内部的this。

第二个场合是需要动态`this`的时候，也不应使用箭头函数。

```javascript
var button = document.getElementById('press');
button.addEventListener('click', () => {
  this.classList.toggle('on');
});
```

### set map weakset weakmap

[垃圾回收](https://zh.javascript.info/garbage-collection)

[垃圾回收机制与weakmap](https://javascript.info/map-set-weakmap-weakset)

[阮一峰](http://es6.ruanyifeng.com/#docs/set-map#WeakSet)

#### resolve() reject()

 promise中，resolve(),reject()，不会跳出函数，他只会传递值出去,他后面的代码仍然会执行。 

#### 图片懒加载封装promise

```javascript
function loadImageAsync(url) {
    return new Promise(function(resolve, reject) {
      const image = new Image();
 
      image.onload = function() {
        resolve(image);
        console.log(11111)
      };
  
      image.onerror = function() {
        reject(new Error('Could not load image at ' + url));
        console.log(2222)
      };
  
      image.src = "http://a.hiphotos.baidu.com/image/h%3D300/sign=a62e824376d98d1069d40a31113eb807/838ba61ea8d3fd1fc9c7b6853a4e251f94ca5f46.jpg";
    });
  }

```

#### 由毫秒生成时间戳

```javascript
 let date = new Date(this.question.createTime);
            let year = date.getFullYear();
            let monthX = date.getMonth();
            //检查隔年
            if (monthX < 11) {
                this.month = monthX + 1;
            } else {
                year++;
                this.month = 1;
            }

            this.month = this.month < 10 ? '0' + this.month : this.month
            let day = date.getDate() < 10 ? '0' + date.getDate() : date.getDate();
            let hour = date.getHours() < 10 ? '0' + date.getHours() : date.getHours();
            let minute = date.getMinutes() < 10 ? '0' + date.getMinutes() : date.getMinutes();
            let seconds = date.getSeconds() < 10 ? '0' + date.getSeconds() : date.getSeconds();
            this.timeStamp = `${year}-${this.month}-${day} ${hour}:${minute}:${seconds}`
            console.log("icityRes", this.timeStamp)
```

#### 防止图片缓存

```javascript
imgObj.src = imgUrl+ '?vxh=' + Math.random(); //方法一防止图片缓存
       
imgObj.src = imgUrl+ '?time=' + new Date().valueOf(); //方法二防止图片缓存
```

#### await

await sb.data是错误的

因为sb返回的是promise。不能直接.

赋值以后 let res=await sb。 res.data可以。

只有1个接口可以直接 await sb.then().catch();

