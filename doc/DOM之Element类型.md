

## Element类型

### 介绍

在DOM中出了Document类型之外，Element类型算是最常用的了。它提供了对元素标签名、子节点以及特性的访问。

| 特征         | 值                                                           |
| ------------ | ------------------------------------------------------------ |
| `nodeType`   | 1                                                            |
| `nodeName`   | 元素的标签名                                                 |
| `nodeValue`  | `null`                                                       |
| `parentNode` | `Document`或`Element`                                        |
| 子节点       | 可能为`Element`、`Text`、`Comment`、`ProcessingInstruction`、`CDATASelection`或`EntityReference` |

### HTML元素

所有元素都由HTMLElement类型表示，不是直接通过这个类型，也是通过它的子类型来表示。HTMLElement类型直接继承自Element类型并添加了一些属性。添加的属性如下：

| 属性名    | 描述                     |
| --------- | ------------------------ |
| id        | 元素在文档中的唯一标识符 |
| title     | 有关元素的附加信息       |
| lang      | 元素内容的语言代码       |
| dir       | 语言的方向，“ltr”或“rtl” |
| className | 元素的css类              |

```HTML
<!DOCTYPE html>
<html lang="en">
  <body>
    <div id="myDiv" class="bd" title="Body text" lang="en" dir="ltr"></div>
  </body>
  <script>
    var div = document.getElementById('myDiv');
    alert(div.id); // myDiv
    alert(div.className); // bd
    alert(div.title); // Body text
    alert(div.lang); // en
    alert(div.dir); // ltr
  </script>
</html>
```

这些属性除了读取操作，也可进行赋值操作，如要将上面div中的id值改为"yourDiv"可使用下面的代码。

```javascript
div.id = 'yourDiv';
```

> 注： 上面有提到不是所有的HTML元素都是由HTMLElement类型表示，又可能会是通过更具体的子类型表示。下面是所有HTML元素和与之关联的类型。

![image-20200308144411141](/Users/rzeey/Library/Application Support/typora-user-images/image-20200308144411141.png)

![image-20200308144518711](/Users/rzeey/Library/Application Support/typora-user-images/image-20200308144518711.png)

### 取得属性

每个元素可能有一个或者多个属性，若想操作这些属性DOM提供了三个方法，分别为：`getAttribute()`、`setAttribute`、`removeAttribute()`。

```html
<!DOCTYPE html>
<html lang="en">
  <body>
    <div id="myDiv" class="bd" title="Body text" lang="en" dir="ltr"></div>
  </body>
  <script>
    var div = document.getElementById('myDiv');
    // 获取title属性
    alert(div.getAttribute('title')); // 'Body text'
    // 设置title属性
    div.setAttribute('title', 'setTitle');
    alert(div.getAttribute('title')); // 'setTitle'
    // 移除title属性
    div.removeAttribute('title');
    alert(div.getAttribute('title')); // null
  </script>
</html>
```

> 注： 属性的名称不区分大小写，即“title”和“TITLE”代表同一个属性。

### attributes属性

Element类型是唯一一个使用attributes属性的DOM节点类型。

---

***- RZeeY***