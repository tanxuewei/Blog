# DOMContentLoaded、load、defer、async介绍

## 什么是DOMContentLoaded

当HTML文档被加载和解析完成后，DOMContentLoaded事件就会被触发。不需要等待图片或其他资源加载完成。（**相当于jQuery中的ready**）

## load

DOM树构建完并且网页所依赖的所有资源都加载完成（**相当于jQuery中的load**）

## 异步脚本

我们都知道html在解析时遇到js就会马上执行，等js执行完再构建DOM，会阻塞DOM加载，因此出现了异步脚本

**defer**：DOM、CSSOM构建完毕，开始执行defer，会按照顺序在DOMContentLoaded前依次执行

**async**：异步下载，下载完就执行，肯定在load之前，但是不一定在DOMContentLoaded前后

如果 script 无 src 属性，则 defer, async 会被忽略。

动态添加的 script 标签隐含 async 属性。
