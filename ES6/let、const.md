# let/const

## 问题1：let/const声明的变量，是否还会变量提升

```js
console.log(a); // Uncaught ReferenceError: a is not defined

/* --------- */
console.log(a); // Uncaught ReferenceError: Cannot access 'a' before initialization
let a = 20;
```

**不能在初始化之前访问 a。**

这个报错说明了什么问题呢？变量定义了，但是没有初始化。

所以在这里我们就可以得出结论：let/const声明的变量，仍然会提前被收集到变量对象中，但和var不同的是，let/const定义的变量，不会在这个时候给他赋值undefined。

因为完全没有赋值，即使变量提升了，我们也不能在赋值之前调用他。这就是我们常说的**暂时性死区**。
