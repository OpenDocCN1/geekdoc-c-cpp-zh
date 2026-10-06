

# 第 13 章：常见问题解决方案

## TouchEnable()

随着苹果在2010年春天发布iPad，人们对触摸设备的兴趣真正大增，我忍不住为这个合集增加了第101个赠赠插件。这里是最后一个插件，它允许你为网页启用触摸功能。示例 13-8 显示了 Plug-in PHP 的网页副本（它是本插件的配套），在浏览器窗口顶部附加了一个小框架，其中包含开启和关闭触摸功能的链接。

## 关于插件

此插件更改了鼠标点击，使得通过触摸屏幕并移动手指（或手写笔），点击和拖拽操作会变为上、下、左、右滚动，这与你使用 iPhone、iPad、安卓手机或其他触摸设备的方式相同。它需要以下参数：

- * 如果为 1 或 true，则开启触摸功能；否则关闭。

![](img/95e4c43b430487125c342550cc090977_396_0.png)

该插件最初由 Razmus Ralf 于1994年开发，用于替换他维护网站时使用的一组 PHP 脚本。早期阶段就确保了插件的灵活性和扩展性，对语言解析器进行了多次重写，这至今一直是该项目的一个核心理念，并且通过 PEAR（PHP 扩展和应用程序库）加载可以使用许多扩展库。只需访问这些工具，你可能需要在紧迫的截止日期内快速构建项目原型，而这提供了非常特定的功能。这正是本书的价值所在，因为它提供了100个即插即用的插件，你只需将它们放入程序中即可使用，通常只需要一个简单的调用：

图 13-8 使用此插件，你可以为网页启用触摸功能。

# 380 JavaScript 插件：100 个解决方案

## 变量、数组和函数

| db | 说明 |
| :--- | :--- |
| db | 局部变量，document.body 的简写 |
| iid | 局部变量，包含调用 `setInterval()` 的结果，稍后在调用 `clearInterval()` 使用 |
| flag | 局部变量，当开启触摸功能时被设置为 true |
| oldmouse & oldmousey | MOUSE 和 MOUSE_Y 的临时副本，用于调用 `StartTE()` 时保存鼠标位置 |
| tempmouse & tempmousey | MOUSE_X 和 MOUSE_Y 的临时副本，在 `DoTE()` 中用于检查鼠标是否移动 |
| MOUSE_X & MOUSE_Y | 包含鼠标位置的全局变量 |
| MOUSE_IN | 全局变量，如果鼠标在浏览器边界内则设置为 true，否则为 false |
| onmousedown & onmouseup | document.body 的事件，在鼠标点击和释放时触发 |
| StartTE() | 开始启用的子函数 |
| DoTE() | 按需滚动文档的子函数 |
| StopTE() | 关闭触摸功能的子函数 |
| PreventAction() | 防止事件默认行为的插件 |
| setInterval() | 停止对另一个函数进行重复中断的函数 |
| clearInterval() | 停止重复中断的函数 |
| scrollBy() | 按指定量滚动文档的函数 |

## 工作原理

该插件首先在局部变量 `db` 中创建 `document.body` 的副本，从而创建一个简写引用以缩短代码：

```
var db = document.body
```

在测试时传入参数，如果是 1 或 true，则开启触摸功能，初始化变量 `iid` 和 `flag`，调用 `PreventAction()` 禁用 document.body 上拖拽和选择操作的默认行为，并将 document.body 的 `onmousedown` 和 `onmouseup` 事件绑定到 `StartTE()` 和 `StopTE()` 子函数，如下：

```
var iid = null
var flag = false
PreventAction(db, 'both', true)
db.onmousedown = StartTE
db.onmouseup = StopTE
```

如果状态为 0 或 false，则关闭触摸功能，因此调用 `PreventAction()` 恢复 document.body 上拖拽和选择操作的默认行为，移除 `onmousedown` 和 `onmouseup` 事件钩子，插件返回：

```
PreventAction(db, 'both', false)
db.onmousedown = ''
db.onmouseup = ''
```

## StartTE() 子函数

此函数检查 `flag` 变量以查看触摸控制是否已经启用。如果是，则返回 false；否则，将鼠标指针位置的副本放在临时变量中，以便稍后比较或判断是否应该滚动 document body，如下所示：

```
var oldmouse = MOUSE_X
var oldmousey = MOUSE_Y
var tempmousex = MOUSE_X
var tempmouse = MOUSE_Y
```

接下来，将 `flag` 设置为 true 以表示触摸控制已启用，并调用 `setInterval()` 设置对 `DoTE` 的重复中断：

```
flag = true
iid = setInterval(DoTE, 10)
```

## DoTE() 子子子函数

此函数检查鼠标按钮当前是否被按住并在浏览器边界内，如下所示：

```
if (MOUSE_DOWN && MOUSE_IN)
```

