# 虚拟DOM习题

## 1、给出如下虚拟dom的数据结构，如何实现简单的虚拟dom，渲染到目标dom树

```js
//样例数据
let demoNode = ({
  tagName: 'ul',
  props: {'class': 'list'},
  children: [
    ({tagName: 'li', children: ['douyin']}),
    ({tagName: 'li', children: ['toutiao']})
  ]
});
```

根据以上数据，构建一个render函数，将demoNode对象渲染为以下dom

```js
<ul class="list">
  <li>douyin</li>
  <li>toutiao</li>
</ul>
```

看到虚拟DOM，是不是感觉很玄乎，但是剥开它华丽的外衣，也就那样:

1. 通过JavaScript来构建虚拟的DOM树结构，并将其呈现到页面中；

2. 当数据改变，引起DOM树结构发生改变，从而生成一颗新的虚拟DOM树，将其与之前的DOM对比，将变化部分应用到真实的DOM树中，即页面中。

通过上面的介绍，下面，我们就来实现一个简单的虚拟DOM，并将其与真实的DOM关联。

### 构建虚拟DOM

虚拟DOM，其实就是用JavaScript对象来构建DOM树，如上ul组件模版，其树形结构如下：

[ul-li-tree](../Images/ul-li-tree.webp)

好了，通过Element我们可以任意地构建虚拟DOM树了。但是有个问题，虚拟的终归是虚拟的，我们得将其呈现到页面中，不然，没卵用。。

怎么呈现呢？

从上面得知，这是一颗树嘛，那我们就通过遍历，逐个节点地创建真实DOM节点:

　　1. createElement;

　　2. createTextNode.

怎么遍历呢？

因为这是一颗树嘛，对于树形结构无外乎两种遍历：

1. 深度优先遍历(DFS)
2. 广度优先遍历(BFS)

针对实际情况，我们得采用DFS，为什么呢？

因为我们得将子节点append到父节点中

好了，那我们采用DFS，就来实现一个render函数吧，如下:

```js
Element.prototype.render = function(){
    var el = document.createElement(this.tagName),
        props = this.props,
        propName,
        propValue;
    for(propName in props){
        propValue = props[propName];
        el.setAttribute(propName, propValue);
    }
    this.children.forEach(function(child){
        var childEl = null;
        if(child instanceof Element){
            childEl = child.render();
        }else{
            childEl = document.createTextNode(child);
        }
        el.appendChild(childEl);
    });
    return el;
};
```

此时，我们就可以轻松地将虚拟DOM呈现到指定真实DOM中啦。假设，我们将上诉ul虚拟DOM呈现到页面body中，如下：

```js
var elem = Element({
    tagName: 'ul',
    props: {'class': 'list'},
    children: [
        Element({tagName: 'li', children: ['item1']}),
        Element({tagName: 'li', children: ['item2']})
    ]
});
document.querySelector('body').appendChild(elem.render());
```

全部代码：

```js
function Element ({ tagName, props, children }) {
  if (!(this instanceof Element)) {
    return new Element({ tagName, props, children })
  }

  this.tagName = tagName
  this.props = props || {}
  this.children = children || []
}

Element.prototype.render = function () {
  var el = document.createElement(this.tagName),
    props = this.props,
    propName,
    propValue;

  for (propName in props) {
    propValue = props[propName]
    el.setAttribute(propName, propValue)
  }

  this.children.forEach((child) => {
    var childEl = null

    if (child instanceof Element) {
      childEl = child.render()
    } else {
      childEl = document.createTextNode(child)
    }

    el.append(childEl)
  })

  return el
}

var elem = Element({
  tagName: 'ul',
  props: { "class": 'list' },
  children: [
    Element({tagName: 'li', children: ['item1']}),
    Element({tagName: 'li', children: ['item2']})
  ]
});

// 渲染到页面中
document.getElementById('app').appendChild(elem.render())
```
