

## 216 JavaScript 插件：100 种强大解决方案

注意：无需为所有对象设置相同的尺寸——它们仍然会整齐地排列，彼此之间的间距通过 `gap` 参数传递的值来控制。你也可以将 `gap` 设置为 0，让所有菜单直接相邻对齐。此外，不要忘记如果你使用 `absolute`（绝对定位），你的菜单将随页面滚动；但如果你使用 `fixed`（固定定位），它们将保持在原来的位置，即使页面滚动。

## 插件

```javascript
function HoverSlideMenu(ids, where, offset, showing, gap, msecs)
{
  var len = ids.length
  var total = gap * (len - 1)
  var start = (offset != '%') ? 0 : offset.substr(1) / 100
  var a = []
  var jump = 0

  if (where == TP || where == BM) {
    for (var j = 0; j < len; ++j) {
      a[j] = W(ids[j])
      total += a[j]
    }
    start = start ? (GetWindowWidth() * total) * start : offset * 1
  } else {
    for (var j = 0; j < len; ++j) {
      a[j] = H(ids[j])
      total += a[j]
    }
    start = start ? (GetWindowHeight() * total) * start : offset * 1
  }

  for (var j = 0; j < len; ++j) {
    HoverSlide(ids[j], where, start + jump, showing, msecs)
    jump += a[j] + gap
  }
}
```

## PopDown()

通过此函数，你可以使用不同的过渡效果从浏览器中移除对象。该插件特别适用于菜单效果，正如本章其他其他中所示。图 8-2 显示了来自资源网站 art.conworks.com 的四个头像。

![](img/95e4c43b430487125c342550cc090977_233_0.png)

## 第 8 章：菜单与导航 217

图 8-2
为头像附加四种不同的 PopDown() 效果

![](img/95e4c43b430487125c342550cc090977_234_0.png)

每个头像在 `onmouseover` 事件上绑定了不同的 PopDown() 样式，当鼠标悬停在上面时，它们会以不同的方式消失。

## 关于插件

此插件接收一个对象并以多种样式之一从浏览器中移除。它需要以下参数：

- *id* 一个对象 ID 或对象和/或对象 ID 数组
- *type* 弹出的类型，可选有 'fade'（淡出）、'inflate'（膨胀）、'zoom'（缩放）或 'instant'（立即）
- *w* 如果为 true 或 1，对象的宽度（如适用）将缩小
- *h* 如果为 true 或 1，对象的高度（如适用）将缩小
- *msecs* 过渡持续的毫秒数，'instant' 类型除外，它不使用计时
- *interruptible* 如果为 true 或 1，插件可以通过对同一对象的另一个调用来中断

## 变量、数组与函数

| j | 如果 id 是数组，则用于遍历 id 的局部变量 |
|---|---|
| PO_IsUp | id 的属性，如果对象已弹出则为 false，否则为已弹出状态 |
| FadeOut() | 让对象随时间淡出的插件 |
| Deflate() | 让对象尺寸随时间逐渐减小的插件 |
| ZoomDown() | 让对象围绕其中心点向内缩放的插件 |
| Hide() | 隐藏对象的插件，使其不再在浏览器中显示 |
| InsVars() | 向字符串插入值的插件 |

## JavaScript 插件：100 种强大解决方案

## 工作原理

该插件从标准代码开始，如果 `id` 是数组，它会遍历 id 并在递归地将每个元素传回自身进行单独处理，如下所示：

```javascript
if (id instanceof Array) {
  for (var j = 0 ; j < id.length ; ++j) {
    PopDown(id[j], type, w, msecs, interruptible)
    return
  }
}
```

接下来，一组 `if() ... else if()` 语句会检查参数 `type` 中请求的各种弹出类型，如下：

```javascript
if (type == 'fade') {
  FadeOut(id, msecs, interruptible,
  InsVars('Hide('#1', id))
} else if () {
 ...
```

第一部分调用了 `FadeOut()` 插件，并传递 `Hide()` 的回调函数名及其参数，这样对象在淡出后就会被隐藏。其他部分以相同的方式和相同的回调字符串调用 `Deflate()` 和 `Zoom()`，最后一部分在请求的弹出类型为 'instant' 时，简单地调用 `Hide()` 插件。

最后，设置 `id` 的 `PO_IsUp` 属性，以指示其他插件该对象正在弹出（或正在弹出）。

## 如何使用

使用此插件非常简单，只需传递一个对象（或对象数组）以及你所需的弹出类型（'fade'、'instant'、'zoom'）。如果 `type` 为 'instant' 或 'zoom'，你需要指定是否应该修改宽度或高度（或二者）。如果 `type` 为 'fade' 或 'instant'，你可以为这些参数传递任何值（如 0 或 null），它们将被忽略。最后，你指定弹出效果所需的毫秒级时间（如果不是 'instant'），并且插件是可以被中断的。

以下是用不同样式弹出代码显示四张图像的示例：

```html
<center><a href=example.html.Reload()><a><br /><br />
<img id='a1' src='avatar1.jpg' /> &nbsp;&nbsp;
<img id='a2' src='avatar2.jpg' /> &nbsp;&nbsp;
<img id='a3' src='avatar3.jpg' /> &nbsp;&nbsp;
<img id='a4' src='avatar4.jpg' /> 
</center>
```

