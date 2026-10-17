
`if (O(id).Deflated) return`

```
```

其次，它不是让 `DF_Count` 计数递减到零，而是从 0 开始递增（在 `Deflate()` 插件中赋值为 `msecs / INTERVAL` 的值）。`DoRelate()` 函数在每一帧增加计数（在 `Deflate()` 插件中递减）：

```javascript
if (O(id).DF_Count >= msecs / INTERVAL
```

此时 `id` 的 `Deflated` 属性指示对象是否已收缩（在 `Deflate()` 插件中被置为 false）。

## 如何使用

你应该在对象使用 `Deflate()` 插件收缩后对其调用此插件。如果你尝试对一个尚未收缩的对象使用它，插件将简单返回。

以下示例由 `Deflate()` 部分扩展而来。在图像之前插入了一个 `div`，你可以通过鼠标悬停收缩或展开图像：

```html
<span id='d'>Mouse Me</span>

<img id='p1' src='photo1.jpg' />

<img id='p2' src='photo2.jpg' />

<img id='p3' src='photo3.jpg' />

<script>
window.onload = function() {
  Locate('p1', ABS, 0, 30)
  Locate('p2', ABS, 160, 30)
  Locate('p3', ABS, 320, 30)
  O('d').onmouseover = down
  O('d').onmouseout = up
  function down() {
    Deflate('p1', 1, 0, 2000, 1)
    Deflate('p2', 1, 1, 2000, 1)
    Deflate('p3', 0, 1, 2000, 1)
  }
}
</script>
```

```javascript
function up()
{
  Reflate('p1', 1, 2000, 1)
  Reflate('p2', 1, 2000, 1)
  Reflate('p3', 0, 2000, 1)
}
</script>
```

```javascript
{
  O(id).DF_Flag = false
  if (w) ResizeWidth(id, O(id).DF_OldW)
  if (h) ResizeHeight(id, O(id).DF_OldH)
  clearInterval(O(id).DF_IID)
  if (typeof CB != UNDEF) eval(CB)
}
```

## DeflateToggle()

如果你使用此插件，就不再需要跟踪哪些对象已经收缩（deflated）哪些还没有，这还能节省额外的代码。在图 6-5 中，`Relate()` 插件部分的示例已更新为使用此插件。

## 关于插件

此插件用于在对象在收缩（deflated）或膨胀（inflated）状态之间进行切换。它接受以下参数：

- 一个对象、一个对象 ID，或者一个对象和/对象 ID 的数组
- 如果为 true 或 1，对象的宽度将收缩或恢复；如果为 true 或 1，对象的高度将收缩或恢复
- 动画应该显示的毫秒数
- interruptible 如果为 true（或 1），此插件可以被对同一对象的后续调用中断；否则，如果为 false（或 0），调用将不会被中断

![](img/95e4c43b430487125c342550cc090977_168_0.png)

图 6-5 图片自动在膨胀和收缩状态之间切换。

## 变量、数组和函数

| j | 如果 id 是数组，则用于索引 id 的局部变量 |
| Deflated | 如果 id 是收缩状态，则该属性为 true |
| Deflate () | 将对象 O 收缩到 O 的插件 |
| Reflate () | 将对象恢复到其原始尺寸的插件 |

## 工作原理

此插件使用了与其他插件类似的标准递归技术来判断 id 是否为数组。如果是，则将数组的每个元素递归地传回同一个函数进行单独处理，如下：

```javascript
if (id instanceof Array)
{
  for (var j = 0; j < id.length; ++++)
    DeflateToggle(id[j], w, h, msecs, interruptible, CB)
  return
}
```

之后有两种情况，其中第一种测试 id 的 `Deflated` 属性。如果是 true，则对象已经收缩（或正处于收缩过程中），因此调用 `Reflate()` 插件。否则，对象处于膨胀状态（或正处于膨胀过程中），因此调用 `Deflate()` 插件，如下：

```javascript
if (O(id).Deflated) Reflate(id, w, h, msecs, interruptible, CB)
else Deflate(id, w, h, msecs, interruptible, CB)
```

## 如何使用

你可以使用此插件来替代同时调用 `Deflate()` 和 `Reflate()` 插件，并节省了跟踪它们收缩/膨胀状态的精力。以下代码与 `Reflate()` 部分之前的示例类似，不同在于它更短，因为它在 `Deflate()` 和 `Reflate()` 插件内部都使用了 `DeflateToggle()`：

```html
<span id='d'>Mouse Me //</span>>
<img id='p1' src='photo1.jpg' />
<img id='p2' src='photo2.jpg' />
<img id='p3' src='photo3.jpg' />
```

```javascript
<script>
window.onload = function() 
{
  Locate('p1', ABS, 0, 30)
  Locate('p2', ABS, 160, 30)
  Locate('p3', ABS, 320, 30)
  Deflate('p2', 1, 0, 1)
}
</script>
```

```javascript
O('d').onmouseover = toggle
O('d').onmouseout = toggle
```

## 第 6 章：移动与动画

```javascript
function toggle() {
  DeflateToggle('p1', 1, 2000, 1)
  DeflateToggle('p2', 1, 0, 2000, 1)
  DeflateToggle('p3', 0, 1, 2000, 1)
}
```

为了增加变化性，可以在调用 `Locate()` 插件之后立即调用 `Deflate()`，这样第二张图片将从收缩状态开始。注意我在调用时传递了 1 毫秒的值（允许的最快速度），以便在实际意义上，它是瞬间完成的。

尝试将鼠标移入移出“Mouse Me”，并观察图片如何切换它们的收缩/膨胀状态，每当你移动光标时，它们都会平滑地在各种动画类型之间切换。

为了完全熟悉此插件能为你做什么，你可能想要将动画长度从 2000 毫秒更改为其他值，将 interruptible 参数改为 0，通过改变 w 和 h 参数来改变动画类型，或者在位置中使用不同的图片。

> 请记住第二个第二个第三个参数（w 和 h）指定的宽度和高度对于对象上的所有收缩、膨胀和切换必须保持一致，以便正确地收缩和膨胀。例如，如果你收缩了对象的宽度，然后尝试只膨胀它的高度，那么什么都不会发生，因为高度还没有被收缩。在这种情况下，只有对象的宽度可以膨胀。

## 插件

```javascript
function DeflateToggle(id, w, msecs, interruptible, CB) {
  if (id instanceof Array) {
    for (var j = 0; j < id.length; ++j)
    DeflateToggle(id[j], w, msecs, interruptible, CB)
  }
  return
}
if (O(id).Deflated) Reflate(id, w, msecs, interruptible, CB)
else Deflate(id, w, msecs, interruptible, CB)
```

## DeflateBetween()

此插件提供了与 `FadeBetween()` 插件类似的功能，不同在于它对对对象进行三种不同的（高度、宽度或宽度/高度）尺寸调整，而不是简单地从一个淡入到另一个。此插件非常适合创建专业的幻灯片效果或切换内容。在图 6-2 中，两张图片已经

![](img/95e4c43b430487125c342550cc090977_168_0.png)

## JavaScript 插件：100 个解决方案

## 插件

```javascript
function DeflateBetween(id1, id2, w, h, msecs, interruptible, CB) {
  Deflate(id1, w, h, msecs, interruptible, CB)
  Relate(id2, w, h, msecs, interruptible, CB)
}
```

## Zoom()

该插件在某些方面与 `Deflate()` 和 `Relate()` 插件类似，但它可以实现更多功能，包括以对象中心为焦点进行放大和缩小、在缩放期间填充内边距以保持相同的宽度和高度（确保其他对象不会因调整大小受到干扰），以及指定结束宽度和高度。

在图 6-7 中，显示了四个图标，每个图标都通过其鼠标事件和 `Zoom()` 插件绑定，因此当鼠标悬停在它们上方时，它们会放大；当鼠标移开时，它们会缩小。图中，第二个图标当前正处于放大状态。

## 关于插件

该插件将在给定的宽度和高度范围内在一段时间内对对象进行缩放。它还可以对对象进行填充以保持其整体尺寸，并支持三种缩放样式。它需要以下参数：

- id 一个对象、对象 ID 或对象和/或对象 ID 数组
- w 如果为 true 或 1，则对对象的宽度进行缩放
- h 如果为 true 或 1，则对对象的高度进行缩放
- fromw 对象开始缩放的宽度
- fromh 对象开始缩放的高度
- tow 对象要缩放的目标宽度

![](img/95e4c43b430487125c342550cc090977_173_0.png)

图 6-7 鼠标悬停在图标上时的缩放

## 第 6 章：移动与动画 157

- toh 对象要缩放的高度
- msecs 动画应持续的毫秒数
- pad 如果大于 0，则对象将使用 CSS padding 填充填充（使其始终保持相同的尺寸）；否则，如果为 -1，则不需要填充，且在缩放期间可能不会移动。如果 pad 为 0 或 null，则在不应用填充的情况下，对象将移动并调整大小以保持居中。
- interruptible 如果为 true（或 1），此插件可以通过对同一对象的新调用进行中断；否则，如果为 false (0)，则调用是不可中断的

## 变量、数组和函数

|  |  |
|---|---|
| j | 如果 id 是数组，用于索引的局部变量 |
| tox | 包含最终水平偏移的局部变量 |
| toy | 包含最终垂直偏移的局部变量 |
| midx | 包含水平中心偏移的局部变量 |
| midy | 包含垂直中心偏移的局部变量 |
| width | 对象左侧填充的量局部变量 |
| width2 | width 的拷贝，包含对象右侧填充的量 |
| height1 | 包含对象顶部填充量的局部变量 |
| height2 | height1 的拷贝，包含对象底部填充的量 |
| stepw | 包含每步宽度变化量的局部变量 |
| steph | 包含每步高度变化量的局部变量 |
| INTERVAL | 包含值 30 的全局变量 |
| HID | 包含值 'hidden' 的全局变量 |
| ZO_W | id 的属性，包含其当前宽度 |
| ZO_H | id 的属性，包含其当前高度 |
| ZO_Flag | id 的属性，如果正在缩放或可以被中断，则设置为 true |
| ZO_Int_Count | id 的属性，包含动画的当前帧数 |
| ZO_IID | id 的属性，包含使用 clearInterval() 取消中断所需的数值 |

## JavaScript 插件：100 个解决方案

|  |  |
|---|---|
| paddingLeft | id 的 style.paddingLeft 属性 |
| paddingTop | id 的 style.paddingTop 属性 |
| paddingRight | id 的 style.paddingRight 属性 |
| paddingBottom | id 的 style.paddingBottom 属性 |
| overflow | id 的 style.overflow 属性 |
| setInterval() | 开始对另一个函数重复中断的函数 |
| clearInterval() | 停止重复中断的函数 |
| Math.max() | 返回两个值最大值的函数 |
| Math.floor() | 去浮点数小数点后的任何数字并返回整数的函数 |
| Math.round() | 将浮点数舍入到最近的整数的函数 |
| DoZoom() | 执行缩放动画的子函数 |
| ZoomPad() | 缩放时填充对象以保持相同尺寸的子函数 |
| NoPx() | 移除属性中 'px' 后缀的插件 |
| Px() | 为属性添加 'px' 后缀的插件 |
| W() | 返回对象宽度的插件 |
| H() | 返回对象高度的插件 |
| X() | 返回水平偏移的插件 |
| Y() | 返回垂直偏移的插件 |
| GoTo() | 将对象移动到位置的插件 |
| Resize() | 调整对象大小的插件

## 它是如何工作的

该插件将在一段时间内在给定的宽度和高度范围内对对象进行缩放。它还可以对对象进行填充以保持其整体尺寸，并支持三种缩放样式。如果 id 是数组，则通过以下方式处理每个元素：

```javascript
if (id instanceof Array)
  for (var j = 0; j < id.length; ++j)
    Zoom(id[j], w, h, msecs, interruptible, CB)
```

## 第 6 章：移动与动画 157

设置后，id 的局部变量如下：

```javascript
var maxw = Math.max(fromw, tow)
var maxh = Math.max(fromh, toh)
var stepw = (tow - fromw) / INTERVAL
var steph = (toh - fromh) / INTERVAL
```

## 设置变量

设置后，id 的属性如下：

```javascript
if (pad > 0) {
  id.style.width = pad + 'px';
  id.style.height = pad + 'px';
} else if (pad == 0 || pad == null) {
  id.style.width = 'auto';
  id.style.height = 'auto';
}
```

## 缩放正在进行

如果正在缩放，则检查 `ZO_Int` 属性。如果不是，则通过调用 `clearInterval()` 停止。

```javascript
if (id.ZOInt) {
  clearInterval(id.ZOIID)
}
```

## 缩放未进行

```javascript
if (!id.ZOFlag) {
  id.overflow = 'hidden';
  id.ZOFlag = true;
  id.ZOInt = interruptible;
  id.ZOIID = setInterval(DoZoom, INTERVAL);
}
```

## DoZoom() 函数

`DoZoom()` 函数的作用是在每次调用时通过更改对象的尺寸来执行缩放。前三行计算调整大小所需的新宽度高度：

```javascript
if (w) ZOW = Math.max(fromw + stepw * id.ZOOCount)
if (h) ZOH = Math.max(fromh + steph * id.ZOOCount)
Resize(id, ZOW, ZOH);
```

id.ZOOCount++;
if (id.ZOOCount * INTERVAL >= msecs) {
  clearInterval(id.ZOIID);
  id.ZOFlag = false;
  id.ZOOCount = 0;
}

## 第 6 章：移动与动画

在插件的早期部分将使用默认值。第三行通过调用 `Resize()` 插件来执行缩放。

之后，用于居中对象的值被放置在 `midx` 和 `midy` 中，如下：

```
var midx = O(id).ZO_X + Math.round((maxx - O(id).ZO_W) / 2)
var midy = O(id).ZO_Y + Math.round((maxh - O(id).ZO_H) / 2)
```
