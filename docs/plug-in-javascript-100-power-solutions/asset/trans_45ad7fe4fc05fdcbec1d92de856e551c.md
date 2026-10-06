

## 第 10 章：音频与视觉效果 317

工作原理
该插件首先检查 `id` 是否为数组。如果是，它将遍历该数组并递归调用自己，将数组中的每个元素单独传递进行处理，如下：

```javascript
if (id instanceof Array) {
  for (var j = 0; j < id.length; ++j)
    PulsateOnmouseover(id[j], opl, op2, msecs)
  return
}
```

接下来，将变量 `finish` 设置为 `false`——每当鼠标离开停止区域且必须停止脉动效果时，它将被设置为 `true`。还声明了变量 `id`，将用于存储 `setInterval()` 函数返回的值：

```javascript
var finish = false
var iid
```

此之后，`id` 的透明度被设置为参数 `opl` 中的水平，同时 `id` 的 `FA_Level` 属性也被设置为该值。该属性被 `Fade()` 插件使用，但此插件需要访问它以判断对象何时已按正确幅度淡入或淡出：

```javascript
Opacity(id, opl)
(id).FA_Level = opl
```

最后，在停止部分，`id` 的事件被绑定到 `PulsateOn()` 子函数以停止脉动，并绑定到一个内联匿名函数中，该函数用于在鼠标移开对象时将变量 `finish` 设置为 `true`，如下：

```javascript
O(id).onmouseover = PulsateOn
(id).onmouseout = function() { finish = true }
```

### PulsateOn() 子函数
该函数的作用是在调用 `DoPulsate()` 子函数之前设置所需的变量。它首先声明变量 `faded` 并赋值为 `false`，表示对象处于淡出状态——当对象淡出时它将变为 `true`。当插件在之前停止后重启时，`finish` 变量也会被设置为 `false`：

```javascript
var faded = false
finish = false
```

如果变量 `iid` 有值，说明之前已调用过插件，因此将其传递给 `clearInterval()` 函数以停止当前可能正在运行重复中断。之后，调用 `setInterval()` 来设置每隔 `INTERVAL` 毫秒向 `DoPulsate()` 插件发送一次重复中断，如下：

```javascript
if (iid) clearInterval(iid)
iid = setInterval(DoPulsate, INTERVAL)
```

## 插件 JavaScript：100 Power Solutions

### DoPulsate() 子函数

该函数是脉动发生的地方，分为两部分：一部分用于淡出，另一部分用于淡入。第一部分检查 `faded` 变量，如果为 `true`，则对象已淡出。接着它检查 `id` 的 `FA_Level` 属性，如果它与 `op1` 中的值相同，则 `id` 处于默认透明度，并准备好淡出。以下是执行这些测试的代码行：

在 `if()` 语句内部，会检查 `finish` 变量是否已设置为 `true`。如果是的话，则不需要淡出对象，而是需要停止重复中断，如下：

```javascript
if (finish) clearInterval(id)
```

当函数返回时，除非另一个鼠标悬停事件触发了新的中断集，否则它不会被再次调用。然而，如果 `finish` 不是 `true`，则按照函数逻辑执行，通过调用 `Fade()` 插件并传入最终透明度值 `op2` 来引发淡入。将 `faded` 变量设置为 `true` 以表示对象已淡出或正处于该过程中，如下：

```javascript
Fade(id, op1, msecs / 2, 0)
faded = true
```

使用 `msecs / 2` 作为过渡持续是因为每个完整周期中包含两次过渡，因此每次过渡必须花费 `msecs` 值的一半时间才能完成。在函数的第二部分，如果变量 `faded` 为 `true`，则测试 `id` 的 `FA_Flag` 属性。当淡入过渡正在进行时，`Fade()` 插件会将该属性设置为 `true`，在过渡完成后将其设置为 `false`。如果 `FA_Flag` 为 `true`，函数将返回淡入状态，且不能被中断：

```javascript
else if (!O(id).FA_Flag)
```

否则，将执行 `if()` 语句内的代码，如下：

```javascript
Fade(id, op2, msecs / 2, 0)
faded = false
```

在此处调用 `Fade()` 时传入的最终透明度值为 `op1`，将对象淡回到默认透明度级别，并将变量设置为 `false` 以表示对象已淡出或正处于该过程中。

## 如何使用

该插件的编写方式确保了当鼠标移开时，对象总是会淡回默认透明度。要使用它，请将其绑定到任何你希望在鼠标经过时产生脉动效果的对象上。这些可以是图像、`div`、`span` 或任何具有可以更改的透明度属性。

## 第 10 章：音频与视觉效果 319

这是一个示例，使用了三次相同的图像，每个图像使用不同的参数绑定到插件：

```html
<img id='a' src='ghost.png' />
<img id='b' src='ghost.png' />
<img id='c' src='ghost.png' />
```

```html
<script>
window.onload = function() {
  PulsateOn('a', 1, 0.5, 500)
  _PulsateOn('b', 0, 0.5, 500)
  PulsateOn('c', 1, 0.5, 500)
}
</script>
```

第一张图像被设置为脉动，第二张被设置为保持静态。第三张图像被设置为以不同的持续时间脉动，但在这里使用了与第一个相同的参数。

使用 `msecs / 2` 作为过渡持续是因为每个完整周期中包含两次过渡，因此每次过渡必须花费 `msecs` 值的一半时间才能完成。在函数的第二部分，如果变量 `faded` 为 `true`，则测试 `id` 的 `FA_Flag` 属性。当淡入过渡正在进行时，`Fade()` 插件会将该属性设置为 `true`，在过渡完成后将其设置为 `false`。如果 `FA_Flag` 为 `true`，函数将返回淡入状态，且不能被中断：

```javascript
else if (!O(id).FA_Flag)
```

否则，将执行 `if()` 语句内的代码，如下：

```javascript
Fade(id, op2, msecs / 2, 0)
faded = false
```

在此处调用 `Fade()` 时传入的最终透明度值为 `op1`，将对象淡回到默认透明度级别，并将变量设置为 `false` 以表示对象已淡出或正处于该过程中。

