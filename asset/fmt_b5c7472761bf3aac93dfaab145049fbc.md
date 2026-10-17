
## 第 7 章：链式与交互 195

### 如何使用

要使用此插件，你需要将它作为一个字符串插入到链命令数组中，如下所示：

`"WaitKey()"`

然后你可以选择被按下的按键，或者让链中的后续命令使用 `GetLastKey()` 插件来返回按键并使用它。

下面的示例替换了上一个示例中 `Pause()` 插件部分相同的放大和缩小操作，将其替换为一个淡入的“按任意键”消息，该消息会等待按键按下，然后再次淡出——让飞船继续航行：

```html
<div id='sea'></div>
<img id='sea' src='ship.png'>
<span id='note'><font size='5'>Press any key</font></span>

<script>
window.onload = function() {
  width = GetWindowWidth()
  height = GetWindowHeight()
  x = width - 200
  y = height - 150
  mid = width / 2 - 100

  Locate('sea', ABS, 0, height - 50)
  Resize('sea', width, 50)
  S(document.body).backgroundColor = '#b7d4dc'
  S('sea').backgroundColor = '#90a5a6'
  Locate('ship', ABS, 0, y)
  Locate('note', ABS, 0, y + 115)
  CenterX('note')
  Opacity('note', 0)

  While('KEY_PRESS != ' ', {
    FadeIn('ship', 'slide', 0, y)
    InsVars('Slide('ship', 0, #1, #2, #1, 2500, 0)', mid, y)
    FadeIn('note', 1000, 0)
    WaitKey()
    FadeOut('note', 1000, 0)
    InsVars('Slide('ship', #1, #2, #3, 2500, 0)', mid, y, x)
    FadeOut('ship', 500, 0)
    InsVars(Callback('Goto("ship", 0, #1)'))
  })
}
</script>
```

此示例与上一个示例的区别已用**粗体**标记。在 HTML 部分，添加了一个带有消息文本的新 `span` 标签。在 `<script>` 部分，将 `span` 移动到将显示的位置，并将其透明度设置为零以使其不可见。

196 插件 JavaScript：100 种解决方案

最后，在命令链中，之前的缩放指令被替换为 `FadeIn()`、`WaitKey()` 和 `FadeOut()` 的调用。如果在显示消息时按除了空格键以外的任何按键，飞船将继续航行并循环。然而，如果按下空格键，`While()` 命令开头的表达式将变为 `true`，链将停止。

### 插件

```javascript
function WaitKey() {
  GetLastKey()
  setTimeout(DoWaitKey, INTERVAL)
}

function DoWaitKey() {
  if (KEY_PRESS == '') NextIn()
  else setTimeout(DoWaitKey, INTERVAL)
}
```

## Flip()

此插件提供了专业的翻转效果，使物体旋转以显示反面。提供了三种不同的旋转效果，这是为你的网页提供有趣视觉效果的好方法。

在图 7-6 中，爱因斯坦的照片被绑定到鼠标事件上，当鼠标悬停时，它会翻转以显示更多信息。无法在书中显示该效果，但可以将图像想象成一张类似的卡片，正面有图片，背面有更多信息。图 7-7 显示了鼠标悬停时图像的“反面”。

图 7-6

网页中的图像在鼠标悬停时是可翻转的。

![](img/95e4c3b40487125c342550cc_213_0.png)

## 第 7 章：链式与交互 197

FIGURE 7-7

当鼠标经过图像时，它会平滑地翻转。

![](img/95e4c3b40487125c342550cc_2214_0.png)

### 关于插件

此插件接收两个对象并对它们进行动画处理，使它们看起来像是翻转到了背面。它返回这些参数：

- `id1`: 对象或对象 ID——可以不是数组
- `id2`: 对象或对象 ID——可以不是数组
- `w`: 如果为 true 或 1，则宽度会被翻转
- `h`: 如果为 true 或 1，则高度会被翻转
- `msecs`: 翻转所需的毫秒数
- `pad`: 如果设置，对象将进行填充以在翻转期间保持整体尺寸

### 变量、数组和函数

| `swap` | 包含命令的本地字符串，适用于 `InsVars()` 添加 `VisibilityToggle()` 调用 |
| `fast` | 包含命令的本地字符串，适用于 `InsVars()` 添加 1 毫秒的 `ZoomToggle()` 调用 |
| `slow` | 包含命令的本地字符串，适用于 `InsVars()` 添加 `msecs / 2` 秒的 `ZoomToggle()` 调用 |
| `ZO_Flag` | `id1` 或 `id2` 的属性，如果对象正在进行缩放，则该属性被设置为 true |
| `CallBack()` | 允许将任何命令添加到链中的插件 |
| `VisibilityToggle()` | 切换对象可见性的插件 |
| `ZoomToggle()` | 切换对象缩放状态的插件 |
| `Chain()` | 启动执行命令链的插件 |

198 插件 JavaScript：100 种解决方案

### 工作原理

此函数首先检查 `id1` 和 `id2` 的 `ZO_Flag` 属性。如果其中一个为 `true`，则对象正在进行缩放，函数返回如下：

```javascript
if (O(id1).ZO_Flag || O(id2).ZO_Flag) return
```

接下来，创建了三个长变量：

# 200 个 JavaScript 插件：100 个解决方案

```javascript
Resize('c', width - 220, 260)
Show('c')
ids = Array('a', 'b')
Locate(ids, ABS, width - 205, 5)
Resize(ids, 200, 264)
VisibilityToggle('b')
('a').onmouseover = function () { Flip('a', 'b', 1, 0, 250, 0) }
('b').onmouseout = function () { Flip('b', 'a', 1, 0, 250, 0) }
```

HTML 显示了两个图片，并包含一个带有文章文本的 `div`。随后，`<section>` 标签通过调用 `Hide` 隐藏了文本，因为它将进行尺寸调整；如果不这样做， 浏览器在下一次计数时将返回错误的宽度，因为它会准备好可能需要的滚动条。在调整文章文本大小后，调用 `Show()` 插件再次显示它。现在由于它已经缩小到适应当前窗口，浏览器将不会尝试为可能需要的滚动条留出空间。

现在，`ids` 数组填充了图片 ID，并将其传递到边界右上角的 `Locate()` 插件。同时也调用了 `Resize()` 插件，因为遗憾的是，取决于使用的浏览器，奇数宽度和高度有时会导致动画出现轻微抖动（这与它们处理的方式有关），确保 `Flip()` 对象的两个维度一致是获得最佳结果简单方法。它还确保了两个图片具有相同的尺寸并能够整齐地翻转。

接下来，在设置鼠标事件到 `Flip()` 之前，将第二个对象设置为可见。这可能是因为两个图片是相互叠的，并且可能具有不同的 `zindex` 值，你必须通过让另一个不可见来确保其中一个在前面。

在这两行代码中，对象 'a' 的 `onmouseover` 事件被绑定到从对象 'a' 到 'b' 的翻转，而对象 'b' 的 `onmouseout` 事件被绑定到从对象 'b' 到 'a' 的翻转。

在翻转之前，对象 'b' 将是可见的，因此鼠标悬停在其上方将开始翻转。翻转完成后，对象 'b' 仍然在它上面（除非用户快速移开），此时对象 'b' 的 `onmouseout` 事件已被触发：因此，当鼠标移开时，动画将再次翻转回来。

### 对象以及图片

尽管为了获得最佳效果，你也可以将任何类型的对象（如 `div` 或 `table`）传递给 `Flip()` 插件。这意味着例如，你可以设置一个电子邮件按钮，当鼠标经过它时它会翻转，显示出一个小表单，用于输入你的电子邮件地址以订阅新闻邮件。如果你这样做，文本将从旋转离开的对象中流出，从而获得略有不同的效果。

你可以使用 `Flip()` 根据单选按钮的选择来交换 HTML 部分，并且不要忘记你可以沿水平和垂直方向翻转对象，甚至可以同时进行这两种操作，创建一个“缩放-再缩回”的效果。通过改变最后两行 `Flip()` 调用中的值，看看你会得到什么结果。

注意，使用一个或多个维度为奇数的对象可能会在翻转期间出现水平或垂直方向的轻微抖动。这是由于不同浏览器处理分数的方式存在差异，通过在恢复之前对对象的位置进行翻转来解决此问题。尽管这种抖动几乎察觉不到，但如果你希望避免这种干扰，你应该只处理具有偶数值的维度。在使用 `Flip()` 之前调用 `Resize()` 很容易确保这一点。

### 翻转效果 (Flip-in)

```javascript
function Flip(id1, id2, w, h, msecs, pad) {
  if (O(id1).Zo_Flag || O(id2).Zo_Flag) return
  var swap = "ChainToggle('#1',')"
  var fast = "ZoomToggle('#1', #2, #3, 1, 0)"
  var slow = "ZoomToggle('#1', #2, #3, #4, 0)"

  Chain(
    InsVars(slow, id1, w, h, msecs / 2, pad),
    InsVars(fast, id2, w, h, pad),
    InsVars(swap, id2),
    InsVars(slow, id2, w, h, msecs / 2, pad),
    InsVars(swap, id1),
    InsVars(fast, id1, w, h, pad)
  )
}
```

## HoverSlide()

此插件将对象放置在浏览器的一侧边缘，显示一小部分并保持隐藏状态。当你将鼠标悬停在其上方时，对象会滑出窗口以显示自己，当移动鼠标时它又会滑回去。图 7-8 显示了一个附加在浏览器顶部的对象，只显示了钢琴琴键。在图 7-9 中，鼠标已经经过并让对象滑入浏览器以显示自己。

### 插件

此插件将对象跨越浏览器边界的一个边缘，其大部分部分在浏览器外是不可见的，并通过一小区域显示你可以通过鼠标移动来让对象滑出。它需要以下参数：

- 或者是一个 或一个对象 ID——这不能是对象数组
- 对象应该附着的边缘：‘top’、‘left’、‘right’ 和‘bottom’

图 7-8 一个附着在浏览器顶部的对象，显示其底部。

![](img/7-8.jpg) 一个对象附着在浏览器边缘，大部分部分在浏览器外是不可见的，通过一小区域显示你可以通过鼠标移动来让对象滑出。

- 或者是一个 或一个对象 ID——这不能是对象数组
- 对象应该附着的边缘：‘top’、‘left’、‘right’ 和‘bottom’

图 7-8 一个对象附着在浏览器顶部的对象，显示其底部。

![](img/7-8.jpg)
