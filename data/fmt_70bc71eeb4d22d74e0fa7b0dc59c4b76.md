
# 第 7 章
## 链式调用与交互
### JavaScript 插件：100 种强大的解决方案

在本章中，我将向你展示如何将书中的许多插件链式组合以形成动作或动画序列。这些是你编写用于创建惊艳开场效果的动画，也可以作为小链来执行简单动作（如移动菜单元素）。

链式调用对于确保一个动作跟随另一个动作也非常有用。这在 JavaScript 中很难实现，因为它是事件驱动的，因此同时调用的插件通常会并行运行。然而，通过在许多插件的末尾添加所谓的回调函数 `callback function`，可以设置一个插件在完成后调用另一个——这就是“链式”。

你还将学习如何在支持链式调用的函数上使用回调（类似于一个微型的、两部分的链）。

## 53 `Chain()`, `NextChain()`, 和 `Callback()`

这些插件是一组函数，允许你将一组插件调用连接起来按顺序执行，每个插件在完成后调用下一个。这是在 JavaScript 中创建动画效果的一种极方法，你可能认为这种效果只能在 Java 或 Flash 等程序中实现。图 7-1 显示了一个球通过链式调用四次 `Slide()` 插件，被设置为在屏幕上弹跳。

### 关于插件

`Chain()` 接受一个插件调用的数组，并将其推入堆栈中，每个调用都可以逐个从栈中弹出，并在前一个调用完成后执行。它需要以下内容：

- `calls`: 一个包含一系列待调用插件的字符串数组。

表 7-1 列出了可以通过回调调用其他插件的插件。

![](img/95e4c43b430487125c342550cc090977_195_0.png)

图 7-1 一个小球在屏幕上弹跳

## 第 7 章：链式调用与交互 179

| `Chain()` | `DeflateToggle()` | `FadeToggle()` | `Repeat()` | `While()` |
|---|---|---|---|---|
| `CallBack()` | `Fade()` | `Hide()` | `Show()` | `Zoom()` |
| `ChainThis()` | `FadeBetween()` | `HideToggle()` | `Slide()` | `ZoomDown()` |
| `Deflate()` | `FadeIn()` | `Pause()` | `SlideBetween()` | `ZoomRestore()` |
| `DeflateBetween()` | `FadeOut()` | `WaitKey()` | `ZoomToggle()` |

表 7-1 支持被链式调用的插件

### 工作原理

表 7-2 支持使用回调的插件

### 变量、数组与函数

| `j` | 用于迭代的局部变量 |
|---|---|
| `CHAIN_S` | 全局数组 |
| `push()` | 推入数组的函数 |
| `pop()` | 从数组弹出的函数 |
| `eval()` | 将字符串作为代码执行的函数 |

### `NextChain()` 插件 ...

### `Callback()` 插件

此插件允许在当前一个完成后附加插件，如下：

```javascript
var insert = expr.lastIndexOf('')
var left = expr.substr(0, insert)
var right = expr.substr(insert)
var middle = 'NextChain()'
```

```javascript
if (expr.substr(insert, 1) != '')
  middle = ', ' + middle
```

```javascript
eval(left + middle + right)
```

## 第 7 章：链式与交互 181

这段代码的工作原理是通过向支持该功能的函数的 `CB` 参数中传递要调用的插件名称。它是通过使用该表达式指向该处，然后将链中的下一个调用作为其最终参数插入到该表达式中来实现的。

为了实现这一操作，首先创建了字符串变量 `left`、`right` 和 `middle`，其中 `left` 包含到插入点为止的所有表达式，`middle` 是一个包含对 `'NextChain()'` 插件引用的字符串，而 `right` 是插入点之后表达式的剩余部分。对 `'NextChain()'` 的引用在双引号内使用了单引号，以确保字符串被求值；单引号内的字符串将被处理为字符串本身，而不是字符串中调用函数名的结果。

如果紧随其后的字符不是 `'('`（这意味着传递给 `Callback()` 的表达式包含参数），则变量 `middle` 的前面带有一个逗号和空格，作为变量分隔符。否则，它保持为赋值的值 `'NextChain()'`。最后，将 `left`、`middle` 和 `right` 的三个值拼接并传递给 `eval()`。

当插件被调用时，它会通知 `CB` 不空，并对其进行求值。在此实例中，`NextChain()` 插件将被调用。

> 注意：以这种方式在 `CB` 中传递函数（或表达式）的名称，而不是简单地让插件调用 `NextChain()`，是为了让你能够传递自己的表达式作为回调来执行。你只需要在字符串中传递一个表达式（或函数调用），并将其传递给任何接收它的插件（列于表 7-1）。你的表达式将在插件执行时被求值。

### `ChainThis()` 插件

此插件允许你获取一个不可链的插件或函数（你可以通过检查表 7-2 来确定），并在链中使用它。代码简单如下：

```
eval(expr)
NextChain()
```

例如，假设对于链中的某条指令，你想使用以下语句进行移动：

```
Goto('myobject', x / 2, y + 100)
```

你也可以通过将其转换为字符串，使用 `InsVars()` 插件和 `ChainThis()` 来实现链式，如下：

```
string = InsVars("ChainThis(\"myobject\", #1, #2)", x / 2, y + 100)
```

`InsVars()` 插件可以方便地使用 `#1` 和 `#2` 等标记作为占位符将变量插入字符串中，并在主字符串之后传递变量或表达式。

如果你将字符串 `string` 作为链中的元素之一传递给 `Chain()` 或 `Repeat` 或 `While()`，那么 `Goto()` 调用将在轮到它时执行，并且程序流将传递到链中的下一个项目（如果有）。

### 插件 JavaScript：100 种解决方案

这种技术仅对于在单个进程中从头到尾按过程运行的函数效果良好。如果你对一个使用事件或中断完成工作的函数使用 `ChainThis()`，你通常会得到意料之外的结果。

> 注意：你可能会在 `InsVars()` 插件中发现你用完了主要的两层引号（双引号和单引号），以及第三层引号。这可以通过在引号前使用转义字符轻松实现：`\"` 或 `\'`。事实上，你会发现上一个示例语句在向 `Goto()` 传递 `"myapp"` ID 时使用了这种技术，因为双引号已经用于字符串的外部，而单引号用于 `Callback()` 内部的子字符串。

### 如何使用它们

要使用 `Chain()` 插件，你需要创建一个要链式连接的插件链数组，并且每个调用在被放入数组之前必须组装成一个字符串。例如，假设你想向链中添加以下内容：

```
FadeOut(myobject, 1000, 0)
```

要做到这一点，你必须首先将其转换为字符串，如下：

```
string1 = 'FadeOut(' + myobject + ', ' + 1000, 0)'
```

或者，如果你有一个更复杂的调用，如下：

```
Slide('a', width / 2, height / 2 - 50, width / 2 -20, height / 2, 500, 0)
```

那么它就需要转换为字符串，如下：

```
string2 = "Slide(' + a + \', ' + width / 2 + \', + height / 2 - 50 + \', ' + width / 2 - 29 + \', ' + height / 2 - 500, 0) + "
```

显然，这变得非常混乱，在上述两个语句的这两个版本中，利用插件 15 `InsVars()` 几乎要简单得多：

```
string1 = InsVars('FadeOut('#1, 1000, myobject)')
string2 = InsVars('Slide('#1, #2, #3, #4, #5, 500, 0', width / 2 - 50, width / 2 -20, height / 2)
```

在这两行中，参数列表被放在主字符串的末尾，每个值都被替换为 `#1`、`#2` 等，用于插入每个值。这两个字符串可以放在链中，并使用以下方式启动链中的第一个：

```
Chain(Array(string1, string2))
```

## 第 6 章：运动与动画 175

最后两个语句检查 `id` 的 `Zoomdown` 属性。如果为 `false`，则对象未缩小，因此调用 `ZoomDown()` 插件；否则，对象已缩小，因此调用 `ZoomRestore()` 插件，如下所示：

```
if (!id.Zoomdown) ZoomDown(id, w, h, msecs, pad, interruptible, CB)
else
    ZoomRestore(id, w, h, msecs, pad, interruptible, CB)
```

### 如何使用

要使用此插件，你不需要跟踪对象的缩放状态；你只需要调用它，插件就会判断对象是否需要缩小或放大。你只需要指定缩放是在水平方向还是垂直方向（或两者）、缩放速度、对象的填充 `pad`，以及缩放是否可以被中断，例如：

```
ZoomToggle(myobject, 1, 0, 750, 0, 0)
```

此语句将切换对象的缩小状态，并允许缩放仅在其宽度上进行（对象将绕其垂直轴旋转）。缩放将耗时 750 毫秒，不会对 `myobject` 进行填充，且不可中断。接下来的示例类似于使用插件的示例，通过鼠标移入和离开图标来控制这四个图标及其缩放状态：

```
<img id='i1' src='i6.gif' />
<img id='i2' src='i2.gif' />
<img id='i3' src='i1.gif' />
<img id='i4' src='i5.gif' />
```

```script
<script>
window.onload = function() {
    ids = Array('i1', 'i2', 'i3', 'i4');
    ZoomToggle('i1', 'i3', 1, 1, 1, 0);
    O(ids, 'onmouseover', 'toggle');
    O(ids, 'onmouseout', 'toggle');
}
function toggle() {
    ZoomToggle(this, 1, 0, 500, 1, 1)
}
</script>
```

在分配 `ids` 数组之后紧有一个额外的 `ZoomToggle()` 调用，它会切换第一个和第三个图标的缩小状态。这意味着当你将鼠标悬过图标时，可以很容易地看到 `ZoomToggle()` 的效果，某些图标进入视图而另一些则缩小。我选择允许缩放仅在对象的宽度上发生，以便图标绕其垂直轴旋转。

## 176 JavaScript 插件：100 种强大的解决方案

在第 7 章中，我将向你展示如何将书中许多插件链式组合在一起，使得每个插件只有在前一个插件完成后才被调用。这可以实现一些非常具有创意且看起来专业的动画效果，并进一步增强用户交互。注意 请记住，在本章中我关注的是图像，所有插件都适用于任何类型的对象，因此你可以滑动、压缩和缩放 HTML 块或任何可以放置其中或可见的对象。

### 插件

```
function ZoomToggle(id, w, h, msecs, pad, interruptible, CB) {
  if (id instanceof Array) {
    for (var j = 0 ; j < id.length ; ++j)
      ZoomToggle(id[j], w, h, msecs, pad, interruptible, CB)
    return
  }
  if (O(id).ZO_Flag && !O(id).ZO_Int) return
}
if (!O(id).Zoomdown) ZoomDown(id, w, h, msecs, pad, interruptible, CB)
else ZoomRestore(id, w, h, msecs, pad, interruptible, CB)
```
