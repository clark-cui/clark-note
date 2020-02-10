### hasOwnProperty

JavaScript 并没有保护 `hasOwnProperty` 这个属性名，因此，当某个对象可能自有一个占用该属性名的属性是，就需要使用外部的 `hasOwnProperty` 获得正确的结果：

```js
var foo = {
  hasOwnProperty: function() {
    return false;
  },
  bar: 'Here be dragons'
};

foo.hasOwnProperty('bar'); // 始终返回 false

// 如果担心这种情况，
// 可以直接使用原型链上真正的 hasOwnProperty 方法
({}).hasOwnProperty.call(foo, 'bar'); // true

// 也可以使用 Object 原型上的 hasOwnProperty 属性
Object.prototype.hasOwnProperty.call(foo, 'bar'); // true
Object.prototype.hasOwnProperty.call(foo, 'hasOwnProperty'); // undefined,因为hasOwnProperty不能判断函数属性
```

注意，只有在最后一种情况下，才不会新建任何对象。

