# Object

## Object.defineProperty

Object.defineProperty(obj, prop, descriptor)

* 存取描述符:
configurable: 可否改变描述符，表示对象的属性是否可以被删除，以及除value和writable特性外的其他特性是否可以被修改。(指先设为ture，后改为false)
enumerable: 是否枚举
get
set

* 数据描述符
configurable: 可否改变描述符
enumerable: 是否枚举
value: 默认undefined
writable: 当且仅当该属性的writable为true时，value才能被赋值运算符改变。

两种描述符不能混合使用
