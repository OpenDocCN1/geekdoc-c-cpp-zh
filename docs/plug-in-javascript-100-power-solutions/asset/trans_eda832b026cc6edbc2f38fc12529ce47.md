

# 第 6 章：移动与动画

在插件的早期部分将使用默认值。第三行通过调用 `Resize()` 插件来执行缩放。

之后，用于居中对象的值被放置在 `midx` 和 `midy` 中，如下：

```
var midx = O(id).ZO_X + Math.round((maxx - O(id).ZO_W) / 2)
var midy = O(id).ZO_Y + Math.round((maxh - O(id).ZO_H) / 2)
```

这些值是通过获取对象的最大宽度和高度，从中减去其宽度和高度计算出来的。这些值除以 2，用于偏移左对象的起始位置，它已存储在 `ZO_X` 和 `ZO_T` 属性中。

# 当参数为真时

如果参数大于零，调用此插件将在更改时进行填充，以保持整体尺寸，因此贴靠在上面的元素都将保持在原位置。如果没有此设置，且高度和 id 发生变化，周围的任何对象都会移动以适应新尺寸。下一行代码调用 `ZoomPad()` 函数来创建填充：

```
if (pad > 0) ZoomPad(Math.max(fromw, tow), Math.max(fromh, toh, O(id).ZO_W, O(id).ZO_H)
```

这通过使用 `Math.max()` 函数找到对象相对于起始值以及 `fromw`、`tow`、`fromh` 和 `toh` 值之间的最大宽度和高度。对象在添加填充后将变大，周围会被填充，在这种情况下缩放可以增长。或者，如果是在缩小，则不添加填充，但随着对象的缩小，会添加更多的填充来补偿尺寸的减少。最终结果是，当 `pad` 大于零时，`id` 始终具有整体尺寸（当你将其宽度和高度加上填充时）。

否则，如果 `pad` 的值不是 -1，则移动 `id` 以保持保持居中（如果 `pad` 为 -1，则不需要填充，也不希望移动 `id`）。

# 如果此插件被 DockBar() 插件调用

接下来，有一段仅供 `DockBar()` 插件使用的代码，将在第 8 章中介绍。它看起来如下：

```
else if (O(id).DB_Parent)ToGoEdge(O(id).DB_Parent, O(id).DB_Where, 50)
```

这段代码检查 `id` 的 `DB_Parent` 属性。在这种情况下，`GetToGoEdge()` 插件由 `DockBar()` 调用，此时会调用第 4 章的内容来跟踪由 `DB_Where` 属性值赋值给的对象。

如果此插件没有作为 `DockBar()` 插件的一部分使用，则有必要保持 `id` 居中（除非 `pad` 参数为 -1，此时禁用居中）。当然，如果 `id` 没有通过设置为 'absolute'（绝对）、'relative'（相对）或其他定位样式而脱离页面，则任何更改其位置的尝试都将被忽略（在这种情况下，保持对象居中的最佳方法是将 `pad` 设置为 `true`）。

# 162 插件 JavaScript：100 个解决方案

然而，如果对象设置了 x 和 y 坐标，那么每当它缩小或放大时，它的左上角都需要轻微移动以保持其中心在中间，尽管使用填充的对象在变化时不会改变位置，因为它们始终具有相同的尺寸。

# 当动画完成后

要检查缩放是否完成，使用以下 `if()` 语句：

```
if (++o(id)).ZO_Count >= (msecs / INTERVAL)
```

该语句增加 `id` 的 `ZO_Count` 属性，然后检查它是否大于或等于 `msecs / INTERVAL` 的结果（这给动画步数）。如果不是，则 `if()` 语句的内容将被忽略，子函数返回将在 `INTERVAL` 毫秒后被再次调用。

否则，缩放完成，并执行以下语句：

```
var end = O(id).ZO_X + Math.round(maxx - tow) / 2
var windy = O(id).ZO_Y + Math.round(maxh - toh) / 2
O(id).ZO_Flag = false
Resize(id, tow, toh)
clearInterval(O(id).ZO_IID)
```

前两行计算对象的最终 x 和 y 位置，并将其放置在 `end` 和 `windy` 中。下一行将 `id` 的 `ZO_Flag` 属性设置为 `false`，表示 `id` 上没有正在缩放。接下来，将对象调整为 `tow` 和 `toh` 中的最终宽度和高度，并通过调用 `clearInterval()` 停止循环中断，传递的是调用 `setInterval()` 时存储的属性 `ZO_IID`。

之后，如果正在使用填充，则调用 `ZoomPad()` 来更新填充；否则，如果 `pad` 不是 -1，则调用 `GoTo()` 插件以确保 `id` 准确地位于 `end` 和 `windy` 的位置。

```
if (pad = 0) ZoomPad(fromw, fromh, tow, toh)
else if (pad = -1) GoTo(id, end, windy)
```

然后，如果此插件被 Dock() 插件调用，将移动到所需的边缘：

```
if (O(id).DB_Parent) GoToEdge(O(id).DB_Parent, O(id).DB_Where, 50)
```

最后的语句检查是否传递了 `CB` 参数，如果是，则调用 `eval()`对其进行评估，如第 7 章所述：

```
if (typeof CB != UNDEF) eval(CB)
```

# ZoomPad() 子函数

`ZoomPad()` 子函数为 `id` 应用足够的 CSS 填充，以便对象始终具有相同的尺寸。它接收四个参数：`frw`、`frh`、`padw` 和 `padh`。变量 `frw` `frh` 包含 `id` 的初始宽度和高度，而 `padw` 和 `padh` 包含所需的宽度和高度。

