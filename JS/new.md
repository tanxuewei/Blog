# new

> new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象类型之一

举个例子

```js
function Otaku (name, age) {
  this.name = name
  this.age = age

  this.habits = 'Games'
}

Otaku.prototype.strength = 60

Otaku.prototype.sayYourName = function () {
  console.log('I am ' + this.name)
}

var person = new Otaku('kevin', 18)

console.log(person.name)

person.sayYourName()  // I am Kevin
```

从这个例子中我们可以看到，实例 person 可以：

1. 访问到 Otaku 构造函数里的属性
2. 访问到 Otaku.prototype 中的属性

## 实现

> 如果构造函数返回值是对象，那么就返回这个对象，如果没有，那么就当没有返回值处理

```js
function objectFactory () {
  var obj = {}
  Constructor = [].shift.call(arguments)
  obj.__proto__ = Constructor.prototype
  var ret = Constructor.apply(obj, arguments)

  return typeof ret === 'object' ? ret : obj
}
```

## 实现过程

1. 新建一个对象 obj
2. 取出第一个参数，就是我们要传入的构造函数。此外，因为 shift 会修改原数组，所以 arguments 会被去除第一个参数
3. 将 obj 的原型指向构造函数，这样 obj 就可以访问到构造函数原型中的属性
4. 使用 apply，改变构造函数 this 的指向到新建的对象，这样 obj 就可以访问到构造函数中的属性
5. 返回 obj （如果构造函数返回值是对象就返回这个对象，如果不是返回 obj）
