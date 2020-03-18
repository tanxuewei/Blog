# babel

编译器：把es2015+ 的代码编译成浏览器中能够运行的代码
code -> parse -> ast -> transform -> ast -> Generator -> code
---   babel.babylon --- babel.traverse --- babel.genarator

1. parse 解析：词法解析（生成tokens数组）+语法解析，生成AST
2. transform 转换: 深度遍历， Visitor对象：ArrowFunction/ifstatement/Identifier
3. generator 生成代码: 深度优先遍历

```js
{
  "type": "Program",
  "body": [
    {
      "type": "VariableDeclaration", // 变量声明
      "declarations": [ // 具体声明
        {
          "type": "VariableDeclarator", // 变量声明
          "id": {
            "type": "Identifier", // 标识符（最基础的）
            "name": "add" // 函数名
          },
          "init": {
            "type": "ArrowFunctionExpression", // 箭头函数
            "id": null,
            "expression": true,
            "generator": false,
            "params": [ // 参数
              {
                "type": "Identifier",
                "name": "a"
              },
              {
                "type": "Identifier",
                "name": "b"
              }
            ],
            "body": { // 函数体
              "type": "BinaryExpression", // 二项式
              "left": { // 二项式左边
                "type": "Identifier",
                "name": "a"
              },
              "operator": "+", // 二项式运算符
              "right": { // 二项式右边
                "type": "Identifier",
                "name": "b"
              }
            }
          }
        }
      ],
      "kind": "const"
    }
  ],
  "sourceType": "module"
}
```
