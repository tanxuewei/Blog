# 箭头函数

## 用法

```js
let func = (value, num) => value * num
```

相当于：

```js
let func = function (value, num) {
  return value * num
}
```

## 和普通函数的区别

1. 没有 this，箭头函数中的 this 只取决于包裹箭头函数的第一个普通函数的 this。

2. 没有 arguments
  箭头函数没有自己的 arguments 对象，这不一定是坏事，因为箭头函数可以访问外围函数的 arguments 对象

```js
function constant () {
  return () => arguments[0]
}

var result = constant(1)
console.log(result())  // 1
```

如果需要访问箭头函数的参数，可以通过命名参数或者 rest 参数的形式访问参数

```js
let nums = (...data) => data
```

3. 不能通过 new 关键字调用

JavaScript 函数有两个内部方法：[[Call]] 和 [[Construct]]。

当通过 new 调用函数时，执行 [[Construct]] 方法，创建一个实例对象，然后再执行函数体，将 this 绑定到实例上。

当直接调用时，执行 [[Call]] 方法，直接执行函数体。

箭头函数并没有 [[Construct]] 方法，不能被用作构造函数，如果通过 new 的方式调用，会报错。

```js
var Foo = () => {}
var foo = new Foo() // TypeError: Foo is not a constructor
```

4. 没有 new.target

因为不能使用 new 调用，所以也没有 new.target 值

（如果构造函数不是通过 new 命令或Reflect.construct()调用的，new.target 会返回 undefined）

5. 没有原型

由于不能使用 new 调用箭头函数，所以也没有构建原型的要求，于是箭头函数也不存在 prototype 这个属性。

```js
var Foo = () => {}
console.log(Foo.prototype)
```

6. 没有 super

连原型都没有，自然也不能通过 super 来访问原型的属性，所以箭头函数也是没有 super 的，不过跟 this、arguments、new.target 一样，这些值由外围最近一层非箭头函数决定。

## 作为构造函数时的区别
