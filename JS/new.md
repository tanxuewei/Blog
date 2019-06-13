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

```js
function
```

## 实现过程

1. 
2. 
3. 
4. 