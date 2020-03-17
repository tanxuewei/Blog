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

1. class的内部定义的所有方法都是不可枚举的,ES5是可枚举的（object.keys）
2. class必须使用new调用，不用new，会报错
3. class 的属性名可以使用表达式 (ES5也可以使用)
4. 严格模式
5. 不存在变量提升
6. 不要单独提取出来方法使用（解构那种用法），this指向会有问题
  解决：绑定this、箭头函数、proxy
7. class 有静态方法，只能直接调用，不能被实例所继承
8. class 实例属性可以写在顶部
9. class 静态属性，是指class本身
10. new.target 区分被谁调用

## demo

```js
class Person {
  constructor (name) {
    this.name = name
  }

  getName () {
    return this.name
  }
}

class Child extends Person {
  constructor (name, age) {
    super(name)
    this.age = age
  }
}

let child = new Child('shirley', 19)
console.log(child)
```

## 其他

proxy: 拦截，外界对这个对象的访问都会到这里
reflect
