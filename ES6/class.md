# class

其实 class 就是对 es5 构造函数的一种语法糖，换了一种写法。然后还有一些差别，下面会讲到。

## 基本写法

```js
class Point {
  // es5 构造函数的方法
  constructor (x, y) {
    this.x = x
    this.y = y
  }

  toString () {

  }
  // 方法之间没有‘，’
}
```

## 和 es5 的差别

1. 类的内部定义的所有方法都是不可枚举的
