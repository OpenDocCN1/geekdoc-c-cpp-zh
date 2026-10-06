

## 第 3 章：核心插件 59

这个示例与之前的示例非常相似，在 HTML 部分创建了一个名为 'square' 的 div。不同之处，`alert()` 函数使用 `W()` 和 `H()` 插件显示对象的宽度和高度。

注意：你可能会发现使用所有的 `S()`、`H()` 和 `NoPx()` 插件非常有意思。你已经可以看到这些插件是如何结合在一起让你的编程工作变得简单得多的。如果没有之前的那些构建函数，这些插件的大小可能会是现在的两到三倍，但通过这种方式，它们只需要几个字符，例如 `W ('obj')`。当你继续深入阅读此本书时，你将获得更强大的函数，这些函数从头开始编写需要几十甚至上百行代码。

## 插件

```
function W(id) {
    var width = O(id).offsetWidth +
    NoPx(id).marginLeft +
    NoPx(id).marginRight

    var bord = O(id).borderLeftWidth +
    NoPx(id).borderRightWidth

    if (bord > 0) width = bord
    else if (O(id).border) width = O(id).border *

    return width
}
```

```
function H(id) {
    var height = O(id).offsetHeight +
    NoPx(id).marginTop +
    NoPx(id).marginBottom

    var bord = NoPx(id).borderTopWidth +
    NoPx(id).borderBottomWidth

    if (bord > 0) height = bord
    else if (O(id).border) height = O(id).border *

    return height
}
```

![](img/95e4c43b430487125c342550cc090977_78_0.png)

因为你会经常发现自己需要编写对象的 `innerHTML` 属性，我编写了这个简单的插件来保持代码简洁并提高其可读性，如图 3-12 所示。

## 60 插件 JavaScript：100 个强大的解决方案

图 3-12
此插件可以轻松地读取和写入对象的 HTML 内容。

![](img/95e4c43b430487125c342550cc090977_79_0.png)

## 这是一个子标题

### 关于插件
此插件返回传递给它的对象的 `innerHTML` 属性。你可以用它来读取或写入数组。读取值只需要第一个参数，但写入一个值时两个参数都需要：

- 要访问的具有 `innerHTML` 属性的对象的 Id
- value 要赋值给 `innerHTML` 属性的值

## 变量、数组和函数

| | |
|---|--- |
| innerHTML | 包含对象 HTML 文本的属性 |

### 工作原理
要读取一个值，该插件使用 `O()` 插件来引用 `id` 中的对象并返回其 `innerHTML` 属性。要写入一个值，向插件使用第二个参数 `value`。如果代码检测到传递了此参数，则 `id` 的 `innerHTML` 属性将更改为 `value`。无论哪种情况，都会返回 `innerHTML` 属性。

## 如何使用

你可以读取或写入支持此函数的对象的 `innerHTML` 属性。要写入它，你使用如下语句：

```
Html('mydiv', 'This is some new text')
```

要从属性读取，使用如下语句：

```
var contents = Html('mydiv')
```

这里有一段使用 `alert()` 用的代码，这样你可以看到使用此插件前后的效果：

```html
<div id='heading'><h1>This is a heading</h1></div>
```

```html
<script>
```

## 第 3 章：核心插件

```
window.onload = function() {
    alert (Htl('heading'))
    Htl('heading', '<h2>This is a subheading</h2>')
    alert (Htl('heading'))
}
</script>
```

HTML 的第一部分创建一个带有 `<h1>` 标题的 div。然后 `<script>` 部分立即弹出一个警报框，通过调用 `Htl()` 显示此值。之后，对象的 `innerHTML` 属性值被更改为子标题，同样是使用 `Htl()`，然后第二次调用 JavaScript `alert()` 函数使用 `Htl()` 函数再次显示该属性——每次执行你都会看到内容已经发生了变化。

## 插件

```
function Htl(id, value) {
    if (typeof id != UNDEF) {
        O(id).innerHTML = value
    }
    return O(id).innerHTML
}
```

## SaveState()

在更改对象的属性后，有时你可能想将其恢复到原始状态。此插件允许你备份对象最重要的样式属性。图 3-13 显示了在测试 `SaveState()` 插件之前准备的带有几个值的 div。

### 关于插件
此插件备份了对象的几个最重要的样式属性，如果你以后需要，可以重新检索它们。它接收以下参数：

- **id**: 要备份的对象属性

图 3-13 创建一个用于测试保存和恢复状态的 div

![](img/95e4c43b430487125c342550cc090977_80_0.png)

## 62 插件 JavaScript：100 个强大的解决方案

## 变量、数组和函数

| | |
|---|--- |
| left | 对象的 style.left 属性 |
| top | 对象的 style.top 属性 |
| visibility | 对象的 style.visibility 属性 |
| color | 对象的 style.color 属性 |
| backgroundColor | 对象的 style.backgroundColor 属性 |
| display | 对象的 style.display 属性 |
| opacity | 对象的 style.opacity 属性 |
| MozOpacity | 对象的 style.MozOpacity 属性 |
| KhtmlOpacity | 对象的 style.KhtmlOpacity 属性 |
| filter | 对象的 style.filter 属性 |
| zIndex | 对象的 style.zIndex 属性 |

### 工作原理

## 如何使用
要为对象创建一组备份属性，将其 ID 传递给 `SaveState()` 插件，如下：

```
SaveState('myobject')
```

以下代码显示了对对象的一些样式设置，然后保存了它的状态：

```html
<div id='mydiv'>Example Text</div>

<script>
window.onload = function() {
  S('mydiv').width = Px(200)
  S('mydiv').height = Px(100)
  S('mydiv').backgroundColor = 'green'
  S('mydiv').color = 'white'
  S('mydiv').position = 'absolute'

  SaveState('mydiv')
}
</script>
```

## 第 3 章：插件 63

这创建了一个绿色的、200像素的矩形，带有白色文本，位置是绝对的（因此该对象是可以移动的）。在插件中，你将看到如果更改了这些值并恢复保存的状态会发生什么。

## 插件

```
function SaveState(id)
O(id).Save_left = S(id).left
O(id).Save_top = S(id).top
O(id).Save_visibility = S(id).visibility
O(id).Save_color = S(id).color
O(id).Save_backgroundColor = S(id).backgroundColor
O(id).Save_display = S(id).display
O(id).Save_opacity = S(id).opacity
O(id).Save_MozOpacity = S(id).MozOpacity
O(id).Save_KhtmlOpacity = S(id).KhtmlOpacity
O(id).Save_filter = S(id).filter
O(id).Save_zIndex = S(id).zIndex
}
```

![](img/95e4c43b430487125c342550cc090977_82_0.png)

## RestoreState()
这是 `SaveState()` 的伙伴插件。它恢复已保存的样式属性。图 3-14 显示了我们在上一个示例中创建的 div；一个警报框已经弹出，让你看到屏幕发生了移动。

### 关于插件
此插件恢复使用 `SaveState()` 保存的样式属性。它接收此参数：

- 要恢复的对象样式属性

图 3-14 SaveState() 和 RestoreState() 的操作

![](img/95e4c43b430487125c342550cc090977_82_1)

## 64 插件 JavaScript：100 个强大的解决方案

## 变量、数组和函数

| | |
|---|--- |
| left | 对象的 style.left 属性 |
| top | 对象的 style.top 属性 |
| visibility | 对象的 style.visibility 属性 |
| color | 对象的 style.color 属性 |
| backgroundColor | 对象的 style.backgroundColor 属性 |
| display | 对象的 style.display 属性 |
| opacity | 对象的 style.opacity 属性 |
| MozOpacity | 对象的 style.MozOpacity 属性 |
| KhtmlOpacity | 对象的 style.KhtmlOpacity 属性 |
| filter | 对象的 style.filter 属性 |
| zIndex | 对象的 style.zIndex 属性 |

### 工作原理
此插件通过从以 "Save" 字符串开头的属性中检索值来反转 `SaveState()` 插件的操作。如果你有任何需要保存和恢复的额外属性，很容易地添加到这些函数中。

### 如何使用
要使用它，只需将已保存状态的对象 ID 传递给此插件，如下：

```
RestoreState('myobject')
```

以下示例扩展了之前的插件，创建一个 div，然后更改它，第一次通过修改它的几个属性，第二次通过调用 `Restore()` 更改。在之间，调用了 JavaScript `alert()` 函数以让你看到屏幕发生了移动的视图：

```html
<div id='mydiv'>Example Text</div>

<script>
window.onload = function() {
  S('mydiv').width = Px(200)
  S('mydiv').height = Px(100)
  S('mydiv').backgroundColor = 'green'
  S('mydiv').color = 'white'
  S('mydiv').position = 'absolute'

}
SaveState('mydiv')

alert('Click OK to see some changes')
</script>
```

