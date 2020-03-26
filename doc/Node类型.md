## Node类型
### 介绍
在JavaScript中所有节点类型都继承自Node类型，所以这些节点类型都拥有着Node类型定义的属性和方法。

所有节点类型都拥有**nodeType**属性，用于表明该节点的类型。节点类型由在 Node 类型中定义的下列 12 个数值常量来表示，任何节点类型必然是其中一种

| Node类型                           | 数值常量 | 描述                                        |
| ---------------------------------- | -------- | ------------------------------------------- |
| `Node.ELEMENT_NODE`                | 1        | 元素，例如 `<div>`                          |
| `Node.ATTRIBUTE_NODE`              | 2        | 属性                                        |
| `Node.TEXT_NODE`                   | 3        | 文本节点                                    |
| `Node.CDATA_SECTION_NODE`          | 4        | 文档中的 CDATA 部（不会由解析器解析的文本） |
| `Node.ENTITY_REFERENCE_NODE`       | 5        | 实体引用                                    |
| `Node.ENTITY_NODE`                 | 6        | 实体                                        |
| `Node.PROCESSING_INSTRUCTION_NODE` | 7        | 处理指令                                    |
| `Node.COMMENT_NODE`                | 8        | 注释                                        |
| `Node.DOCUMENT_NODE`               | 9        | 整个文档                                    |
| `Node.DOCUMENT_TYPE_NODE`          | 10       | 向为文档定义的实体提供接口                  |
| `Node.DOCUMENT_FRAGMENT_NODE`      | 11       | 轻量级的 Document 对象（文档的某个部分）    |
| `Node.NOTATION_NODE`               | 12       | DTD 中声明的符号                            |

在IE中使用`Node.ELEMENT_NODE`等这样是失效的，所以要判断节点类型的兼容写法应如下：

```JavaScript
if (someNode.nodeType === 1) {
    console.log('This is ELEMENT_NODE');
}
```

### 节点间的关系

节点与节点之间存在各种各样的关系，如`<body>`为`<html>`的子节点，`<body>`与`<head>`为兄弟节点······

![](https://user-gold-cdn.xitu.io/2020/1/17/16fb2db28194f278?w=1242&h=858&f=png&s=72610)

每一个节点都有一个**childNodes**属性，它保存着当前节点的直接字节点。childNodes属性的值为一个NodeList，这是一种类数组，但不是Array的实例，因此不能使用forEach、map等方法。

若要获取其中一个子节点可采用`[]`或者`item()`这样的方式。

若想取得该列表的第一个子节点，可访问**firstChild**属性。

若想取得该列表的最后一个子节点，可访问**lastChild**属性。

```JavaScript
var nodeList = someNode.childNodes;
nodeList[0] === nodeList.item(0); // true
nodeList[0] === someNode.firstChild; // true
nodeList[nodeList.length - 1] === someNode.lastChild; // true
```

每个节点都有一个**parentNode**属性，该属性指向文档树中的父节点。通过使用列表中每个节点的 **previousSibling**和**nextSibling**属性，可以访问同一childNodes属性列表中的其他节点。

下图反应了各个节点的关系和对应的属性：

![](https://user-gold-cdn.xitu.io/2020/1/17/16fb2e843b0889c3?w=1258&h=616&f=png&s=112582)

### 操作节点

DOM提供了一些操作节点的方法，如基本的增加和修改：

#### appendChild

`appendChild()`用于将节点插入childNodes列表的末尾，并返回新增的节点。

```JavaScript
var returnedNode = someNode.appendChild(newNode);
console.log(returnedNode === newNode); // true
console.log(someNode.lastChild === newNode); // true
```

#### insertBefore

`insertBefore()`用于将节点插入childNodes列表中某个特定的位置上，并返回新增的节点。

```JavaScript
// 将newNode插入在someNode的子节点中的最前面
var returnedNode = someNode.insertBefore(newNode, someNode.childeNodes[0]);
console.log(returnedNode === newNode); // true
console.log(someNode.firstChild === newNode); // true
```

#### replaceChild

`replaceChild`用于替换childNodes列表中某个特定的节点，并返回被移除的节点。

```JavaScript
//移除第一个子节点
var formerFirstChild = someNode.removeChild(someNode.firstChild);
//移除最后一个子节点
var formerLastChild = someNode.removeChild(someNode.lastChild);
```