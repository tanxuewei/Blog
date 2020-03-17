# Vue 相关问题

## 生命周期

events &lifecycle

beforeCreate

initState() -> data,props

created (组件未挂载)

beforeMount: 开始创建 VDOM，最后执行 mounted 钩子，并将 VDOM 渲染为真实 DOM 并且渲染数据

mounted 后可以访问组件

## 组件通信

父子通信: props

兄弟通信：this.$parent.$children

跨层级通信：provide / inject，虽然文档中不推荐直接使用在业务中，但是如果用得好的话还是很有用的。

任意组件
这种方式可以通过 Vuex 或者 Event Bus 解决，另外如果你不怕麻烦的话，可以使用这种方式解决上述所有的通信情况

eventbus: 事件总线 $on,$emit

```js
// 极简版eventbus
const eventBus = {
  obj: {},
  $on (type, fn) {
    this.obj[type] = fn
  },

  $emit (type) {
    let args = [...arguments].slice(1)
    this.obj[type](...args)
  }
}

eventBus.$on('change', function (a) {
  console.log(a)
  console.log(arguments)
})

eventBus.$emit('change', 1, 2)
```
