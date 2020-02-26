# 数组的扩展

## 扩展运算符 spread (...)

### 含义

扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，**将一个数组转为用逗号分隔的参数序列**。

```js
console.log(...[1, 2, 3]); // 1, 2, 3
console.log(1, ...[2, 3, 4], 5)
[...[2,3,4]]
```

该运算符主要用于函数调用

```js
function push (array, ...items) {
  array.push(...items)
}

function add (x, y) {
  return x + y
}

const numbers = [4, 38]
add(...numbers) // 42
```

扩展运算符后面还可以放置表达式。

```js
const arr = [
  ...(x > 0 ? ['a'] : []), //如果...后面是空数组，则不产生任何效果
  'b'
]
```

注意，只有函数调用时，扩展运算符才可以放在圆括号中，否则会报错。

### 替代函数的 apply 方法

调用apply 方法时可以传一个数组，所以这里可以直接取代

另一个例子是通过push函数，将一个数组添加到另一个数组的尾部。

```js
// ES5的 写法
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
Array.prototype.push.apply(arr1, arr2);

// ES6 的写法
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];
arr1.push(...arr2);
```

上面代码的 ES5 写法中，push方法的参数不能是数组，所以只好通过apply方法变通使用push方法。有了扩展运算符，就可以直接将数组传入push方法。

### 扩展运算符的应用

1、复制数组
数组是复合的数据类型，直接赋值的话，只是复制了指向底层数据结构的指针，而不是克隆一个全新的数组。

```js
// 引用
const a1 = [1, 2]
const a2 = a1

a2[0] = 2
a1 // [2, 2]

// ------ ES5 变通方法 ----
const a1 = [1, 2]
const a2 = a1.concat()

a2[0] = 2
a1 // [1, 2]

// ----- ES6 ------
const a1 = [1, 2]
const a2 = [...a1]
// 或
const [...a2] = a1
```

注意：ES6 的写法只是浅克隆哈，如果里面还有数组，还是会影响到新数组

2、合并数组

```js
let arr1 = [1, 2, 3]
let arr2 = [4, 5, 6]
arr1.push(...arr2)
arr1 // [1, 2, 3, 4, 5, 6]
arr2 // [4, 5, 6]
// 或者
let arr3 = [...arr1, ...arr2]
```

3、与解构赋值结合

4、字符串

字符串转数组

```js
[...'hello']
// [ "h", "e", "l", "l", "o" ]
```

## Array.form

Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）。

Array.from(friends, ({name}) => name)
Array.form 第二个参数为函数，类似于map方法
