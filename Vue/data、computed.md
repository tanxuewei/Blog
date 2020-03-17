# 生命周期

events &lifec

beforeCreate

initState() -> data,props

created (组件未挂载)

beforeMount: 开始创建 VDOM，最后执行 mounted 钩子，并将 VDOM 渲染为真实 DOM 并且渲染数据

mounted 后可以访问组件