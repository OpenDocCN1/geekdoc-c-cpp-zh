

# 第 3 章：核心插件 31

## 插件

```javascript
function O(id, property, value)
{
  if (id instanceof Array)
  {
    var tmp = []
    for (var j = 0; j < id.length; ++j)
      tmp.push(O(id[j]), property, value)
    return tmp
  }

  if (typeof property != UNDEF && typeof value != UNDEF)
  {
    if (typeof value == "'" + value + "'")
      return eval("O(\ + id + "")" + property + " = " + value)")
  }
}
```

```javascript
if (typeof id == 'object') return id
else
{
  try { return document.getElementById(id) }
  catch(e) { alert("PJ - Unknown ID: ' + id) }
}
```

## 2 S()

JavaScript 最常见的用途可能是修改 HTML 文档中的 CSS 属性。这些包括颜色、尺寸、位置、透明度等。通常，这是通过使用下面的代码来实现的，它更改了 div 的前景色：

```javascript
document.getElementById('element').style.color = 'red'
```

或者，使用之前的插件，可以将其缩短为：

```javascript
O('element').style.color = 'red'
```

这是一个常见的操作，我为 O() 创建了一个配套插件称为 S（代表 Style，即样式），用于处理对象的 style 子对象。使用它，前面的命令可以简化为以下内容：

```javascript
S('element').color = 'red'
```

图 3-2 显示了如何使用该插件更改三个 div 的背景颜色。尽管该图不是彩色的，但你可以通过它们的深浅看出这些 div 的颜色是不同的。

## 32 插件 JavaScript：100 种强大解决方案

3-2
使用 s() 更改某些 div 的背景颜色

![](img/95e4c43b430487125c342550cc090977_51_0.png)

### 关于插件
S() 与 O() 类似，区别在于它不是引用对象，而是访问对象的 style 子对象。此外，由于它不使用事件，因此没有必要检查此函数。它接受以下参数：

- id：可以是一个包含对象 ID 的字符串，甚至是一个包含多个对象和/或 ID 的数组。如果没有提供其他可选参数，则该函数将返回 id 所代表的对象（或对象）的 style 子对象。如果有可选参数，函数的目的将变为将值赋值给 id 中对象（或对象）style 子对象中的 property 属性。
- property：此可选的字符串参数可以包含 id 中对象（或对象）style 子对象中需要修改的属性名。
- value：如果设置了此可选参数，它代表要赋值给 id 中对象（或对象）style 子对象中 property 属性的值。property 和 value 参数都必须有值，否则 S() 将仅仅返回 id 中对象（或对象）的 style 子对象。

## 变量、数组和函数

| | |
|---|---|
| tmp[] | 存储 id 数组处理结果的数组 |
| j | 用于索引 id 的整数型值变量 |
| style | style 子对象 |
| push() | 向数组推入一个值的函数 |
| try() | 运行函数并将任何错误传递给匹配的 catch() 语句的函数 |
| catch() | 当 try() 语句失败时调用的函数 |
| O() | 插件 1，主“对象”函数。O() 或 S() 几乎被所有插件使用，这是它们最后一次出现在“变量、数组和函数”章节中 |

# 第 3 章：核心插件 33

## 工作原理

现在你已经理解了 O() 插件的工作原理，你就会对这个插件如何运作有一个了解。因为它们相似，我将只概述基本知识。

与 O() 一样，这个函数有三个主要部分。第一部分处理 id 恰好是数组的情况。它通过递归调用自身来处理数组中的每个元素，以便单独处理每一个元素。它执行的代码如下，最后一行返回处理过程中返回的所有值的数组：

```javascript
if (id instanceof Array)
{
  var tmp = []
  for (var j = 0 ; j < id.length ; ++j)
    tmp.push(S(id[j], property, value))
  return tmp
}
```

第二部分处理当你以属性赋值模式使用插件的情况。它通过检查是否同时具有 property 和 value 属性来确定这一点。如果是，则将 value 赋值给 id 所代表对象的 style 子对象中的 property 属性。

否则，进入对象获取模式，并在 try() 语句中返回 id 的子对象，任何错误都可以被捕获并通过调用 alert() 显示，这使用了匹配的 catch() 语句：

```javascript
if (typeof property != UNDEF && typeof value != UNDEF)
  try { return O(id).style[property] = value }
  catch(e) { alert('PJ - Unknown ID: ' + id) }
else if (typeof id == 'object') return id.style
else
{
  try { return O(id).style }
  catch(e) { alert('PJ - Unknown ID: ' + id) }
```

在开发过程中，你会发现这种错误捕获非常有用，写错 ID 名称或在声明之前访问它们是常见的错误。

> 注意：我指的是 style 子对象，也可以称之为 style 属性，因为两者兼顾：它既是一个格式良好的样式，而样式 本身是一个具有属性的对象。因此，我倾向于将也是对象的属性称为子对象。

## 如何使用

你使用插件的方式与使用 O() 函数非常相似。通过它，你可以获取对象的 style 子对象，或者修改对象的某个 style 属性。这里是你可以使用插件首先获取后使用对象 style 子对象的方法：

```javascript
var _styleobject = S('mydiv')
styleobject.color = 'red'
```

或者，你可以直接访问样式，如下：

```javascript
S('mydiv').color = 'red'
```

如果你愿意，你也可以这样设置属性值：

```javascript
S('mydiv', 'color', 'red')
```

在这种情况下，数组中的所有对象的 innerHTML 都将被设置为：

```javascript
ids = Array('div1', 'div2', 'div3')
S(ids, 'innerHTML', 'red')
```

## 34 插件 JavaScript：100 种强大解决方案

首先，div 是在 HTML 中被创建的，然后：

```html
<div id="div1">First</div>
<div id="div2">Second</div>
<div id="div3">Third</div>
```

在接下来的章节中，你将看到 S() 被用于许多语境，我发现以后你将永远不想以其他方式访问样式了。

## Initialize()

为了设置插件的使用，你必须在 Web 页面的开头调用一个较小的插件。如前提到的，我建议你始终在每个页面的开头包含以下两行代码：

```html
<script src="PJ.js"></script>
<script>Initialize()</script>
```

或者如果你使用的是压缩版的插件 Pjssmall.js，则你应该使用该文件代替 Pjs。

这个插件是由该代码调用的 Initialize() 函数，它准备了你可以调用的广泛功能，如图 3-3 所示，在此处检测浏览器类型。

### 关于插件
此插件不需要任何参数，也不返回任何值。然而，请参考下一节的变量、数组和函数表，因为它设置了非常重要的全局变量。

图 3-3
调用此插件后显示 BROWSER 变量

![](img/95e4c43b430487125c342550cc090977_54_0.png)

