
两个部分的结果被拼接并返回。当你将这两部分代码组合在一起时如下所示：

```javascript
return (n < 16 ? '0' : '') + n.toString(16)
```

## 如何使用

要将十进制数转换为十六进制，将其传递给 `Dec()` 插件，如下：

```javascript
alert('The decimal number 173 in hexadecimal is ' + Dec(173))
```

## 第 3 章：核心插件 71

此语句显示的值为 'ad'，在 JavaScript 中作为颜色的一部分时，这是一个可以接受的十六进制数，因此通常不需要将其转换为大写或为其添加任何前缀。

到此，你已经完成了基础 JavaScript 工具箱的基础知识，而且本质上，它是书中最长的一个章节之一。在下一章中，我们将开始添加插件来提供位置和定位功能，然后好戏就真正开始了。

## 插件

```javascript
function DecHex(n)
{
  return (n < 16 ? '0' : '') + n.toString(16)
}
```

# 第 4 章

## 位置与尺寸

## JavaScript 插件：100 种解决方案

上一章侧重于提供核心功能的子集。这一章也做了同样的事情，但现在集合中已经有了足够的插件，我们可以开始创建一些有趣的效果，包括调整对象的大小和重新定位。

### 19 ResizeWidth()

在创建动态网页页面时，你经常需要更改对象的尺寸。你可能想通过放大某个部分来强调它，可能允许用户重新排列页面的内容，或者你希望打开像表单或灯箱（light boxes）之类的元素等。

通过此插件，你可以调整任何具有 `width` 属性对象的宽度，如图 4-1 所示的示例 `div`，其宽度被调整为 300 像素。

#### 关于插件

此插件更改对象的宽度。它需要以下参数：

- `id`: 对象的 ID 或对象本身。你也可以传递对象数组和/或对象 ID。
- `width`: 对象的新宽度。如果 `id` 是数组，则引用的所有对象都将设置为此宽度。

#### 变量、数组和函数

| `j` | 本地整数循环 |
| :--- | :--- |
| `overflow` | 对象的 `style.overflow` 属性 |
| `width` | 对象的 `style.width` 属性 |
| `HID` | 值为 'hidden' 的全局字符串变量 |
| `Px()` | 添加后缀 'px' 的插件 |

此插件还提供了 `o()` 和 `s()` 插件的多功能性，其中你可以传递对象的 ID 或对象本身，你甚至可以传递一组 ID 数组/或同时更改它们。

![](img/95e4c43b430487125c342550cc090977_92_0.png)

图 4-1 调整对象的宽度

## 第 4 章：位置与尺寸 75

它的实现利用了 fact：`S()` 插件已经设置好用于处理对象 ID、对象或对象数组和/或对象 ID。因此，只需要调用两次 `S()`：一次将对象或对象数组的 `style.overflow` 属性设置为 'hidden'，然后将 `style.width` 属性设置为 `width` 中的宽度。变量 `HID` 是由 `Initialize()` 插件创建的全局变量，其值为 'hidden'。对象的 `style.overflow` 属性被设置为此值，允许对象缩小或放大，当缩小合，，本会溢出的文本将被忽略。

#### 如何使用

使用此插件时，传递一个对象和一个宽度，如下所示：

```javascript
ResizeWidth('mydiv', 200)
```

或者你可以传递一个对象数组，如下：

```javascript
ids = Array('objone', 'objtwo', 'objthree')
ResizeWidth(ids, 480)
```

这里有一个你可以尝试的示例，它将 `div` 的宽度重置为 300 像素。它还更改了文本和背景颜色，以便你可以看到变化：

```html
<div id='example'>Example div</div>
<script>
window.onload = function() {
  S('example').backgroundColor = 'blue'
  S('example').color = 'yellow'
  ResizeWidth('example', 300)
}
</script>
```

#### 插件

```javascript
function ResizeWidth(id, width) {
  S(id, 'overflow', HID)
  S(id, 'width', Px(width))
}
```

### ResizeHeight()

正如你可能需要调整对象的宽度一样，这里有一个调整其高度的插件。图 4-2 显示了上一个插件创建的 `div` 现在高度增加到 100 像素。

## JavaScript 插件：100 种解决方案

![](img/95e4c43b430487125c342550cc090977_94_0.png)

**图 4-2** 调整对象的高度

#### 关于插件

此插件更改对象的高度。它需要以下参数：

- **id**: 对象的 ID 或对象本身。你也可以传递对象数组和/或对象 ID。
- **height**: 对象的新高度。如果 id 是数组，则引用的所有对象都将设置为此高度。

#### 变量、数组和函数

| `j` | 本地整数循环 |
| :--- | :--- |
| `overflow` | 对象的 `style.overflow` 属性 |
| `height` | 对象的 `style.height` 属性 |
| `HID` | 值为 'hidden' 的全局字符串变量 |
| `Px()` | 添加后缀 'px' 的插件 |

#### 如何工作

这是 `Resize()` 的伴侣插件，它的工作方式与之前的完全相同，唯一的区别是修改的是对象的 `style.height` 而不是 `style.width`。通过 `Resize()`，你可以传递 ID 或对象。有关此插件如何运作的更多细节，请参阅 `Resize()` 插件。

#### 如何使用

使用此插件时，向它传递一个对象和一个高度，如下所示：

```javascript
ResizeHeight('mydiv', 100)
```

## 第 4 章：位置与尺寸 77

或者你可以传递一个对象数组，如下：

```javascript
ids = Array('objone', 'objtwo', 'objthree')
ResizeHeight(ids, 240)
```

这里有一个你可以尝试的示例，它修改了上一个插件中的示例，将 `div` 调整大小为 100 像素：

```html
<div id='example'>Example div</div>
<script>
window.onload = function() {
  S('example').backgroundColor = 'blue'
  S('example').color = 'yellow'
  ResizeWidth('example', 300)
}
</script>
```

#### 插件

```javascript
function ResizeHeight(id, height) {
  S(id, 'overflow', HID)
  S(id, 'height', Px(height))
}
```

### 21 Resize()

此插件将之前的两个合并为一个函数，以节省代码量并使代码更紧凑，如图 4-3 所示。

![](img/95e4c43b30487125c342550cc090977_95_0.png)

图 4-3 调整对象的宽度和高度

## 78 JavaScript 插件：100 种解决方案

#### 关于插件

此插件更改对象的宽度和高度。它需要以下参数：

- **id**: 对象的 ID 或对象本身。你也可以传递对象数组和/或对象 ID。
- **width**: 对象的新宽度。如果 id 是数组，则引用的所有对象都将设置为此宽度。
- **height**: 对象的新高度。如果 id 是数组，则引用的所有对象都将设置为此高度。

#### 变量、数组和函数

| `ResizeWidth()` | 更改宽度的插件 |
| :--- | :--- |
| `ResizeHeight()` | 更改高度的插件 |

#### 如何工作

此插件简单地调用 `ResizeWidth()` 然后调用 `ResizeHeight()`。

#### 如何使用

使用此插件时，向它传递一个对象以及宽度和高度，如下：

```javascript
Resize('mydiv', 100, 100)
```

你可以传递一个对象数组，如下：

```javascript
ids = Array('obj1', 'obj2', 'obj3')
Resize(ids, 128, 128)
```

这里有一个你可以尝试的示例，它改进了上一个插件中的示例，通过一次调用将 `div` 调整大小为 100 像素：

```html
<div id='example'>Example div</div>
<script>
window.onload = function() {
  S('example').backgroundColor = 'red'
  S('example').color = 'white'
  Resize('example', 300, 300)
}
</script>
```

#### 插件

```javascript
function Resize(id, width, height) {
  ResizeWidth(id, width)
  ResizeHeight(id, height)
}
```

## 第 4 章：位置与尺寸 79

### 22 Position()

此插件设置对象的 CSS `position` 属性。当你想要控制对象相对于父级位置的偏移，甚至完全移动到任何绝对位置时，这非常有用。图 4-4 显示了一个相对于之前位置水平偏移了 100 像素的 `div`。

#### 关于插件

此插件设置对象的 `style.position` 属性。它需要以下参数：

- `id`: 对象、对象 ID 或对象数组和/或对象 ID
- `type`: 要赋值的 `style.position` 属性类型，可选 'absolute'、'fixed'、'relative'、'static' 或 'inherit'。你也可以使用更短的全局变量（由 `Initialize()` 插件创建）`ABS`、`FIX`、`REL`、`STA` 和 `INH`。

#### 变量、数组和函数

| `position` | 对象的位置属性 |

#### 如何工作

此函数使用了 `S()` 函数的功能，它可以接收对象、对象 ID 甚至是对象数组和/或对象 ID。因此，它只需将 `id` 和 `type` 中的值直接传递给 `S()` 插件。

#### 如何使用

使用此插件设置对象的 `style.position` 属性，可以如下调用：

```javascript
Position('myobject', ABS)
```

![](img/95e4c43b430487125c342550cc090977_97_0.png)

## 80 JavaScript 插件：100 个强大的解决方案

例如，要将对象设置为具有“绝对（absolute）”位置（使用 `Initialize()` 插件创建的较短全局变量 `ABS`）并移动它，你可以使用如下代码：

```html
<div id='moveme'>移动我</div>
<script>
window.onload = function() {
  S('moveme').backgroundColor = 'red'
  S('moveme').color = 'white'
  Position('moveme', REL = Px(100))
}
</script>
```

此示例创建了一个名为 'moveme' 的 div，将其设置为红色背景上的白色文字，然后使用 `Position()` 插件赋予它一个“相对（relative）”位置。最后，使用 `Px()` 插件设置其 `style.left`，这使其相对于父对象水平向偏移了 100 像素。

> 注意：由于使用“绝对”和“相对”样式定位的 div 之间位置变化存在差异，你还需要考虑这一点：使用“绝对”样式定位的 div 会自动收缩以适应其内容，而使用“相对”样式定位的 div 将保留其之前的宽度，默认情况下，它会延伸到容器对象的右边缘。如果你使用 `span`，它将始终收缩以适应其内容，无论位于何处或如何定位。

#### 插件

```javascript
function Position(id, type)
{
  S(id, 'position')
}
```

### Goto()

如果一个对象已经从页面中释放（例如通过之前的插件 `Position()`），那么你可以通过更改它的 `style.left` 和 `style.top` 属性将其移动到另一个位置，此插件通过提供单一函数使这一操作更快、更简单。在图 4-5 中，一个 div 向右移动了 200 像素，向下移动了 25 像素。

## 第 4 章：位置与尺寸

![](img/95e4c43b430487125c342550cc090977_99_0.png)

图 4-5 GoTo() 插件移动对象。

#### 关于插件

此插件将对象（如果它是可移动的）移动到新位置。它接受以下参数：

- 一个对象、一个对象 ID 或对象和/或对象 ID 数组
- 从父对象左边缘开始水平偏移量，对象将移动到此处（如果对象的 `style.position` 属性为 'fixed' 或 'absolute'，则从浏览器边缘计算）
- 从父对象顶部的垂直偏移量，对象将移动到此处（如果对象的 `style.position` 属性为 'fixed' 或 'absolute'，则从浏览器顶部计算）

#### 变量、数组与函数

| 变量 | 说明 |
| :--- | :--- |
| `left` | 对象的 `style.left` 属性 |
| `top` | 对象的 `style.top` 属性 |
| `Px()` | 添加后缀 'px' 的插件 |

#### 工作原理

此插件还利用了 `S()` 插件管理对象和/或对象 ID 数组、单个对象或对象 ID 的能力。它仅进行了两次调用：一次是将对象的 `style.left` 属性设置为带有 'px' 后缀的 x 值（这是 CSS 规则的要求），另一次是对 `style.top` 属性执行相同的操作，但使用的是 y 值。

#### 如何使用

要使用此插件，请通过通过发布类似如下的命令确保对象是可移动的（使用包含字符串 'relative' 的全局变量 `REL`）：

```javascript
Position('advertdiv', REL)
```

## JavaScript 插件：100 个强大的解决方案

以下示例为 div 赋予了“绝对（absolute）”位置（使用全局变量 `ABS`）并对其进行移动：

```html
<div id='moveme'>移动我</div>
<script>
window.onload = function() {
  S('moveme').backgroundColor = 'green'
  S('moveme').color = 'cyan'
  Position('moveme', ABS)
  Goto('moveme', 200, 25)
}
</script>
```

#### 插件

```javascript
function Goto(id, x, y) {
  S(id, 'left', Px(x))
  S(id, 'top', Px(y))
}
```
