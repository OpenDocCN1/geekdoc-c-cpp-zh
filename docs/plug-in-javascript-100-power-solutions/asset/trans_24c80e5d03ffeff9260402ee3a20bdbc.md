
# 第 6 章：运动与动画 175

最后两个语句检查 id 的 `Zoomdown` 属性。如果为 `false`，则对象未缩小，因此调用 `ZoomDown()` 插件；否则，对象已缩小，因此调用 `ZoomRestore()` 插件，如下所示：

```
if (!id.Zoomdown) ZoomDown(id, w, h, msecs, pad, interruptible, CB)
else
    ZoomRestore(id, w, h, msecs, pad, interruptible, CB)
```

## 如何使用

要使用此插件，你不需要跟踪对象的缩放状态；你只需要调用它，插件就会判断对象是否需要缩小或放大。你只需要指定缩放是在水平方向还是垂直方向（或两者）发生、缩放速度、对象的填充（pad），以及缩放是否可以被中断，例如：

```
ZoomToggle(myobject, 1, 0, 750, 0, 0)
```

此语句将切换对象的缩小状态，并允许缩放仅在其宽度上进行（对象将绕其垂直轴旋转）。缩放将耗时 750 毫秒，不会对 myobject 进行填充，且不可中断。

接下来的示例类似于使用插件的示例，通过鼠标移入和离开图标来控制这四个图标及其缩放状态：

```
<img id='i1' src='i6.gif' />
<img id='i2' src='i2.gif' />
<img id='i3' src='i1.gif' />
<img id='i4' src='i5.gif' />
```

```
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

在第 7 章中，我将展示如何将书中一系列插件连接或链式组合在一起，使得每个插件只有在前一个插件完成后才被调用。这可以实现一些非常具有创意且看起来专业的动画效果，并进一步增强用户交互。

注意 请记住，在本章中我关注的是图像，所有插件都适用于任何类型的对象，因此你可以滑动、压缩和缩放 HTML 块或任何可以放置其中或可见的对象。

## 插件

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

## 第 7 章

链式调用与交互

## JavaScript 插件：100 种强大的解决方案

在本章中，我将向你展示如何将书中的许多插件链式组合以形成动作或动画序列。这些是你编写用于创建惊艳开场效果的动画，也可以作为小链来执行简单动作（如移动菜单元素）。

链式调用对于确保一个动作跟随另一个动作也非常有用。这在 JavaScript 中很难实现，因为它是事件驱动的，因此同时调用的插件通常会并行运行。然而，通过在许多插件的末尾添加所谓的回调函数（callback function），可以设置一个插件在完成后调用另一个——这就是“链式”（chaining）。

你还将学习如何在支持链式调用的函数上使用回调（类似于一个微型的、两部分的链）。

## 53 Chain(), NextChain(), 和 Callback()

这些插件是一组函数，允许你将一组插件调用连接起来按顺序执行，每个插件在完成后调用下一个。这是在 JavaScript 中创建动画效果的一种极方法，你可能认为这种效果只能在 Java 或 Flash 等程序中实现。图 7-1 显示了一个球通过链式调用四次 `Slide()` 插件，被设置为在屏幕上弹跳。

## 关于插件

`Chain()` 接受一个插件调用的数组，并将其推入堆栈中，每个调用都可以逐个从栈中弹出，并在前一个调用完成后执行。它需要以下内容：

- calls: 一个包含一系列待调用插件的字符串数组。

表 7-1 列出了可以通过回调调用其他插件的插件。

![](img/95e4c43b430487125c342550cc090977_195_0.png)

图 7-1 一个小球在屏幕上弹跳

## 第 7 章：链式调用与交互 179

| Chain() | DeflateToggle() | FadeToggle() | Repeat() | While() |
|---|---|---|---|---|
| CallBack() | Fade() | Hide() | Show() | Zoom() |
| ChainThis() | FadeBetween() | HideToggle() | Slide() | ZoomDown() |
| Deflate() | FadeIn() | Pause() | SlideBetween() | ZoomRestore() |
| DeflateBetween() | FadeOut() | WaitKey() | ZoomToggle() |

表 7-1 支持被链式调用的插件

## 工作原理

| Chain() | DeflateToggle() | FadeToggle() | Repeat() | While() |
|---|---|---|---|---|
| Fade() | FadeIn() | Pause() | SlideBetween() | ZoomRestore() |
| FadeBetween() | FadeOut() | WaitKey() | ZoomToggle() |

表 7-1 支持链式调用的插件（OCR 文字在表格结构上有些重叠，根据片段进行了重建）。

表 7-2 支持使用回调的插件

## 变量、数组与函数

| j | 用于迭代的局部变量 |
|---|---|
| CHAIN_S | 全局数组 |
| push() | 推入数组的函数 |
| pop() | 从数组弹出的函数 |
| eval() | 将字符串作为代码执行的函数 |

## NextChain() 插件 ...

## Callback() 插件

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
[/content]

*我注意到结尾表格的 OCR 文字非常重复。我将根据源文本提供一个干净的最终版本。*

---[content]
# 第 6 章：运动与动画 175

最后两个语句检查 id 的 `Zoomdown` 属性。如果为 `false`，则对象未缩小，因此调用 `ZoomDown()` 插件；否则，对象已缩小，因此调用 `ZoomRestore()` 插件，如下所示：

```
if (!id.Zoomdown) ZoomDown(id, w, h, msecs, pad, interruptible, CB)
else
    ZoomRestore(id, w, h, msecs, pad, interruptible, CB)
```

## 如何使用

要使用此插件，你不需要跟踪对象的缩放状态；你只需要调用它，插件就会判断对象是否需要缩小或放大。你只需要指定缩放是在水平方向还是垂直方向（或两者）、缩放速度、对象的填充（pad），以及缩放是否可以被中断，例如：

```
ZoomToggle(myobject, 1, 0, 750, 0, 0)
```

此语句将切换对象的缩小状态，并允许缩放仅在其宽度上进行（对象将绕其垂直轴旋转）。缩放将耗时 750 毫秒，不会对 myobject 进行填充，且不可中断。接下来的示例类似于使用插件的示例，通过鼠标移入和离开图标来控制这四个图标及其缩放状态：

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

## 插件

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

## 第 7 章

链式调用与交互

## JavaScript 插件：100 种强大的解决方案

在本章中，我将向你展示如何将书中的许多插件链式组合以形成动作或动画序列。这些是你编写用于创建惊艳开场效果的动画，也可以作为小链来执行简单动作（如移动菜单元素）。链式调用对于确保一个动作跟随另一个动作也非常有用。这在 JavaScript 中很难实现，因为它是事件驱动的，因此同时调用的插件通常会并行运行。然而，通过在许多插件的末尾添加所谓的回调函数，可以设置一个插件在完成后调用另一个——这就是“链式”。你还将学习如何在支持链式调用的函数上使用回调（类似于一个微型的、两部分的链）。

## 53 Chain(), NextChain(), 和 Callback()

这些插件是一组函数，允许你将一组插件调用连接起来按顺序执行，每个插件在完成后调用下一个。这是在 JavaScript 中创建动画效果的一种极方法，你可能认为这种效果只能在 Java 或 Flash 等程序中实现。图 7-1 显示了一个球通过链式调用四次 `Slide()` 插件，被设置为在屏幕上弹跳。

## 关于插件

`Chain()` 接受一个插件调用的数组，并将其推入堆栈中，每个调用都可以逐个从栈中弹出，并在前一个调用完成后执行。它需要以下内容：

- calls: 一个包含一系列待调用插件的字符串数组。

表 7-1 列出了可以通过回调调用其他插件的插件。

![](img/95e4c43b430487125c342550cc090977_195_0.png)

图 7-1 一个小球在屏幕上弹跳

## 第 7 章：链式调用与交互 179

| Chain() | DeflateToggle() | FadeToggle() | Repeat() | While() |
|---|---|---|---|---|
| CallBack() | Fade() | Hide() | Show() | Zoom() |
| ChainThis() | FadeBetween() | HideToggle() | Slide() | ZoomDown() |
| Deflate() | FadeIn() | Pause() | SlideBetween() | ZoomRestore() |
| DeflateBetween() | FadeOut() | WaitKey() | ZoomToggle() |

表 7-1 支持被链式调用的插件

## 工作原理

| Chain() | DeflateToggle() | FadeToggle() | Repeat() | While() |
|---|---|---|---|---|
| Fade() | FadeIn() | Pause() | SlideBetween() | ZoomRestore() |
| FadeBetween() | FadeOut() | WaitKey() | ZoomToggle() |

表 7-1 支持链式调用的插件（OCR 文字在表格结构上有些重叠，根据片段进行了重建）。

表 7-2 支持使用回调的插件

## 变量、数组与函数

| j | 用于迭代的局部变量 |
|---|---|
| CHAIN_S | 全局数组 |
| push() | 推入数组的函数 |
| pop() | 从数组弹出的函数 |
| eval() | 将字符串作为代码执行的函数 |

## NextChain() 插件 ...

## Callback() 插件

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
