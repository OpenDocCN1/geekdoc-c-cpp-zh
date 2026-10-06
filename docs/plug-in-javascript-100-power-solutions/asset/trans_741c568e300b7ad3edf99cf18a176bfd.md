

# 142 JavaScript 插件：100 个强大的解决方案

![](img/95e4c43b430487125c342550cc090977_159_0.png)

**图 6-3** 此插件支持的不同收缩类型

- **msecs** 动画应该持续的毫秒数
- **interruptible** **如果为 true**（或 1），则此插件可以被对同一对象上的新调用所中断；否则，如果为 **false**（或 0），则该调用是不可中断的

## 变量、数组与函数**

| | |
|---|---|
| j | 如果 id 是数组，则作为索引 id 的局部变量 |
| stepw | 包含每帧水平变化量的局部变量 |
| steph | 包含每帧垂直变化量的局部变量 |
| width | 包含每一步 id 应该改变的宽度的局部变量 |
| height | 包含每一步 id 应该改变的高度的局部变量 |
| overflow | 对象的 `style.overflow` 对象，被设置为 HID ('hidden') 以防止对象内容在收缩时溢出 |
| DF_Flag | id 的属性，如果正在进行 `Deflate()` 则包含为 true |
| DF_Int | id 的属性，如果收缩是可中断的则包含为 true 或 1 |
| DF_ID | 用于 `clearInterval()` 清除中断的属性 |
| DF_OldW | id 的属性，包含 id 未收缩前的宽度 |
| DF_OldH | id 的属性，包含 id 未收缩前的高度 |
| DF_Count | id 的属性，包含动画中的帧数 |
| Deflated | id 的属性，如果已收缩则设为 true——供 `DeflateToggle()` `plugin` 使用 |

# 第 6 章：运动与动画 143

| | |
|---|---|
| INTERVAL | 值为 30 的全局变量 |
| HID | 值为 'hidden' 的全局变量 |
| setInterval() | 设置重复中断的函数 |
| clearInterval() | 停止重复中断的函数 |
| DoDeflate() | 执行动画的子函数 |
| W() | 获取对象宽度的插件 |
| H() | 获取对象高度的插件 |
| Resize() | 调整对象大小的插件 |

##原理

此插件包含几个不同的部分。第一部分测试 id 是否为数组；如果是，则使用以下代码对 id 的每个元素递归地调用自身：

```
if (id instanceof Array)
  for (var j = 0; j < id.length; ++j)
    Deflate(id[j], w, h, msecs, interruptible, CB)
  return
```

这允许许多对象同时收缩，只要它们是以数组的形式传递给 Deflate() 即可。

接下来，代码必须考虑到这样事实：当图像的某个维度发生变化时，大多数浏览器会自动修改另一个维度以保持图像的相同比例。然而，在这种情况下并不需要这种功能，因此如果水平宽度或垂直高度没有被改变（由 w 和 h 参数中的值决定），则该维度将被赋予一个代表其当前长度的固定值，以替换其默认值 'auto'。这允许一个维度被更改，而另一个保持不变：

```
if (!w) ResizeWidth(id, W(id))
if (!h) ResizeHeight(id, H(id))
```

接下来，如果 id 正在进行收缩（通过其 DF_Flag 值为 true 或 1 来确定），则会检查其 DF_Int 属性。如果动画可以中断，则该属性包含 true 或 1；如果不是 true 或 1，则函数返回。否则，如果当前正在运行任何收缩间隔器，则通过调用 clearInterval() 停止它。这两个动作的代码如下：

```
if (O(id).DF_Flag)
  if (!O(id).DF_Int) return
  else clearInterval(O(id).DF_IID)
```

# 144 JavaScript 插件：100 个强大的解决方案

否则，如果这是第一次由 Deflate() 插件使用 id 对象，则需要分配某些属性，如下所示：

```
else
{
  if (w) O(id).DF_OldW = W(id)
  if (h) O(id).DF_OldH = H(id)
  O(id).DF_Count = msecs / INTERVAL
}
```

在本节中，属性 DF_OldW 和 DF_OldH 被赋值为对象的当前宽度和高度，以便它们稍后可以使用——但仅限于没有保存此值的情况下调整大小的维度。

此外，DF_Count 属性被赋值为 msecs / INTERVAL，即动画中的步骤数。该变量将每次计算一个步骤（在 Deflate() 函数中），每一步它的值都将与 stepw 和/或 step 中的值相乘，以计算动画每一步 id 的正确宽度/和高度。

接下来，通过以下语句为某些属性分配了特定值（无论这是否是第一次用此插件使用 id）：

```
var stepw = O(id).DF_OldW = (msecs / INTERVAL)
var steph = O(id).DF_OldH = (msecs / INTERVAL)
```

```
O(id).DF_OldW = (msecs / INTERVAL)
O(id).DF_OldH = (msecs / INTERVAL)
```

```
O(id).overflow = true
O(id).Deflated = true
O(id).DF_Flag = true
O(id).DF_Int = interruptible
O(id).DF_IID = setInterval(DoDeflate, INTERVAL)
```

首先，通过 stepw 和 steph 分配每一步的水平和垂直距离。

收缩每隔 msecs 毫秒，通过将 overflow 属性设置为 HID ('hidden') 来确保内容不会溢出。

如果 DF_Int 属性被设为 true 或 1，此插件就不会被中断。

收缩状态被设为 true，如 DeflateToggle() 所示。

在插件的最后部分，DF_Flag 被设为 true，以表示正在进行收缩。

最后，每隔 INTERVAL 毫秒调用一次。

### DoDeflate() 子函数
一旦由插件部分初始化，DoDeflate() 每隔 INTERVAL 毫秒调用一次，每次都会缩小对象一点，如下：

```
if (w) ResizeWidth(id, stepw * O(id).DF_Count)
if (h) ResizeHeight(id, steph * O(id).DF_Count)
```

这两行计算了 id 的新宽度/高度，以及是调整大小还是两者。

接下来，检查是否为最后一次调整以及动画是否可以停止。这是通过检查 DF_Count 的值来实现的，该值在动画每帧后递减。

## 动画结束时
如果 DF_Count 属性小于 1，则动画已完成，且 id 的 DF_Flag 属性被设为 false，表示没有正在运行的收缩。最后将调整大小的维度设置为 0 以完成过渡。在插件的最后几行中，调用 clearInterval() 函数以防止任何中断。位于 CB 中的此回调函数使用 eval() 函数进行评估，但仅当参数 CB（第 7 章解释）有值时。这些动作的代码为：

```
if (O(id).DF_Count-- < 1)
{
  O(id).DF_Flag = false
  if (w) ResizeWidth(id, 0)
  if (h) ResizeHeight(id, 0)
  clearInterval(O(id).DF_ID)
  if (typeof CB != UNDEF) eval(CB)
}
```

> DF_Count 后的双减运算符--) 是一种非常方便的方法，告诉 JavaScript 递减变量，但是在其当前值被用于 if () 语句之后，节省了一行代码。

