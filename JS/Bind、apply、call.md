# Bind、Apply、Call实现

## bind

> bind方法会创建一个新函数。当这个新函数被调用时，bind()的第一个参数将作为它运行时的this，之后的一序列参数将会在传递的实参前传入作为它的参数。

bind的特点：

* 返回一个函数

* 可以传入参数

bind实现

```js
Function.prototype.MyBind = function (context) {
  var self = this
  var args = [].slice.call(arguments, 1)

  return function () {
    var bindArgs = [].slice.call(arguments)
    return self.apply(context, args.concat(bindArgs))
  }
}

```

// TODO 构造函数相关

## call

> call方法在使用一个指定的this值和若干个指定的参数值的前提下调用某个函数或方法。

eg:

```js
var foo = {
  value: 1
}

function bar () {
  console.log(this.value)
}

bar.call(foo) // 1
```

call的特点：

* 改变了this的指向，指向到foo

* 执行了这个bar函数

### 模拟实现

```js
var foo = {
  value: 1
  bar: function () {
    console.log(this.value)
  }
}

bar.call(foo) // 1
```

实现步骤

1. 将函数设为对象的属性 foo.fn = bar
2. 执行该函数         foo.fn()
3. 删除该函数         delete foo.fn

实现时注意问题：

* 参数个数是不确定的
* 如果this为null，指向window
* 函数时有返回值的

最终实现：

```js
  Function.prototype.MyCall = function (context) {
    var context = context || window
    context.fn = this
    var args = []
    for (var i = 1, len = arguments.length; i < len; i++) {
      args.push('arguments[' + i + ']')
    }
    // 主要是为了传过去对应的参数，个数对应
    var result = eval('context.fn(' + args + ')')
    delete context.fn
    return result
  }
```

ES6实现：
```js
  Function.prototype.MyCall6 = function (context) {
    var context = context || window
    context.fn = this
    var args = []
    for (var i = 1, len = arguments.length; i < len; i++) {
      args.push(arguments[i])
    }
    // 主要是为了传过去对应的参数，个数对应
    var result = context.fn(...args)
    delete context.fn
    return result
  }
```

## apply

apply和call类似，就是apply调用时传入的参数是一个数组

```js
Function.prototype.MyApply = function (context, arr) {
  var context = context || window
  context.fn = this

  var result
  if (!arr) {
    result = context.fn()
  } else {
    var args = []
    for (var i = 0, len = arr.length; i < len; i++) {
      args.push('arr[' + i + ']')
    }
    result = eval('context.fn(' + args + ')')
  }
  delete context.fn
  return result
}
```