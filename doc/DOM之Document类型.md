## Document类型

### 介绍
在JavaScript中用Document类型表示整个文档。在浏览器中document对象表示整个HTML文档。document对象是HTMLDocument的实例，而HTMLDocument又继承自Document类型。
<br />
**Document类型特点：**
|特点|值
|-|-
|`nodeType`|9
|`nodeName`|#document
|`nodeValue`|null
|`parentNode`|null
|`ownerDocument`|null
|子节点|可能为`DocumentType`（最多一个）、`Element`（最多一个）、`ProcessingInstruction`、`Comment`
<br />

### 文档的子节点
#### documentElement和childNodes属性
虽然Document的子节点可以为`DocumentType`（最多一个）、`Element`（最多一个）、`ProcessingInstruction`、`Comment`，但仍有两个内置的属性可以快速访问其直接子节点：
<br />
- `documentElement`属性，始终指向`<html>`元素；
- `childNodes`属性，文档元素列表。

```HTMl
<html>
  <body>
  </body>
</html>
```
上面这个文档包含一个直接子节点即`<html>`元素，可使用以下方法进行访问：
```JavaScript
var html = document.documentElement; // <html>元素
html === document.childeNodes[0]; // true
html === document.firstChild; // true
```
#### body属性
`document`对象还有一个`body`属性直接指向`<body>`元素。
```JavaScript
var body = document.body; // <body>元素
```
所有浏览器都支持`document.docuemntElement`和`document.body`属性。
#### docType属性
`Document`类型可能还存在另外一个子节点，即`DocumentType`。
```JavaScript
var docType = document.docType; // 取得对<!DOCTYPE>的引用
```
<br/>

### 文档的信息
document对象作为HTMLDocument的一个实例，其还存在一些标准Document类型没有的属性。这些属性提供了document对象所表现的网页信息。
#### title属性
`title`属性显示在浏览器的标题栏或者标签栏上，修改`title`属性可改变网页的title。
```JavaScript
var title = document.title; // 获得原始的title值
document.title = 'new title'; // 为网页设置新的title
```
#### URL属性（只读）
`URL`属性包含页面完整的URL（即地址栏中显示的URL）。
```JavaScript
var url = document.URL; // 取得完整的URL
```
#### domain属性
`domain`属性**只包含**页面的域名。
```JavaScript
var domain = document.domain; // 取得网页的域名
```
>注： `domain`属性只可设置为当前域名的子域名，且遵循“松散紧绷”规则。
#### referrer属性（只读）
`referrer`属性保存着链接到当前页面的那个页面的URL。若在没有来源页面的情况下，`referrer`属性可能为空字符串
```JavaScript
var referrer = document.referrer; // 取得来源网页的URL
```
<br />

### 查找元素
查找元素再进行一些操作，这是DOM最常见的应用。
#### getElementById()方法
`getElementById()`方法只接受一个参数，即要取得元素的ID。如果找到则返回该元素，否则返回`null`。以下面元素为例。
```HTML
<div id="myDiv">text</div>
```
可使用下面代码获取该元素：
```JavaScript
var myDiv = document.getElementById('myDiv'); // 取得<div>元素的引用
```
>注： ID必须与页面元素中的id属性严格匹配，包括大小写。
#### getElementsByTagName()方法
`getElementsByTagName()`方法只接受一个参数，即要取得元素的标签名。返回的则是包含0个或者多个的NodeList。同样以下面元素为例。以下面元素为例。
```HTML
<img src="src" name="myImg" />
```
可使用下面代码获取该元素：
```JavaScript
var allTags = document.getElementsByTagName('*'); // 取得包含文档所有元素的NodeList
var imgs = document.getElementsByTagName('img'); // 取得包含页面所有<img>元素的NodeList
alert(imgs.length); // 输出页面<img>元素的数量
alert(imgs[0]); // 输出页面第一个<img>元素
alert(imgs[0].src); // 输出页面第一个<img>元素的src属性
alert(imgs.item(0).src); // 输出页面第一个<img>元素的src属性
alert(imgs.namedItem('myImg')); // 输出页面<img>元素中包含name属性为“myImg”的NodeList
alert(imgs.['myImg']); // 同namedItem()方法
```
>注： 传入的标签名不区分大小写。

### 特殊集合
出了属性和方法，document对象还有一些特殊集合。这些集合都是HTMLCollection对象。
|集合                 |描述
|---------------------|----------------------------------------------------------------------------------
|`document.anchors`   |包含文档中所有带**name**属性`<a>`元素
|`document.applets`   |包含文档中所有`<applet>`元素，因为不再推荐使用`<applet>`元素，所以这个集合已经不再建议使用了
|`document.forms`     |包含文档中所有的`<form>`元素，与`document.getElementsByTagName('form')`得到的结果相同
|`document.images`    |包含文档中所有的`<img>`元素，与`document.getElementsByTagName('img')`得到的结果相同
|`document.links`     |包含文档中所有带**href**属性的`<a>`元素

### 文档写入
为了将输出流写入网页文档中，document对象提供了4个方法：`write()`、`writeln()`、`open()`、`close()`。
#### write()和writeln()方法
`write()`和`writeln()`方法都接受一个字符串参数，即要写入到输出流中的文本。`write()`会原样写入，而`writeln()`会在字符串末尾加一个换行符`\n`。

```HTML
<html>
  <body></body>
  <script>
    document.write(`this time is ${new Date().toString()}`);
  </script>
</html>
```
上面这个例子中，通过`write()`方法，动态地向文档写入了当前的日期和时间。
<br />
通过`write()`和`writeln()`方法，还可以动态的引入外部资源，例如JavaScript文件等。如下：
```HTML
<html>
  <body></body>
  <script>
    document.write('<script src="index.js">');
  </script>
</html>
```
注意若在文档加载完成后再使用`write()`或`writeln()`方法，那么输出的内容将重写整个页面！
#### open()和close()方法
`open()`和`close()`方法分别用于打开和关闭网页的输出流。

---
***- RZeeY***