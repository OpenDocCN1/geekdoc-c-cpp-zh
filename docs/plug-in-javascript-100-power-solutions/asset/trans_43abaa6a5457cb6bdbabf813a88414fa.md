

## Repeat()

除了将插件链联在一起，你还可以使用 `Repeat()` 插件让一个或多个插件重复指定的次数。在当前的媒体中，无法捕获这些示例中的动作，因此图 7-2 显示了球（略微灰色）在使用此插件创建的动画的不同重复次数中被捕获的状态。

## 关于插件

此插件允许你根据意愿次数重复一个动作链。它需要以下参数：

- *number*: 链应该重复的次数
- *calls*: 一个包含要调用插件序列的字符串数组

## 变量、数组和函数

| 变量 |  |
|---|---|
| j | 用于计数重复次数的局部变量 |
| temp | `calls` 数组的本地副本 |
| concat() | 合并两个或多个数组的函数 |
| Chain() | 用于将一组插件链在一起的插件 |

## 工作原理

此插件获取 `calls` 数组并将其复制多次，直到有 `number` 份 `calls` 拷贝，如下所示：

```
var temp = calls
for (var j = 1 ; j < number ; ++j)
  calls = calls.concat(temp)
Chain(calls)
```

![](img/95e4c43b430487125c342550cc090977_202_0.png)

首先，数组 `temp` 被赋值为 `calls` 的副本，然后 `concat()` 函数将 `temp` 的内容与 `calls` 合并，直到总共有 `number` 份。最后，调用 `Chain()` 插件来启动第一次运行。

## 如何使用

使用此插件与调用 `Chain()` 相同，只是你还传递了一个额外的参数来指定链重复的次数。以下示例对 `Chain()` 和 `NextInChain()` 插件部分的示例进行了微调，使球在浏览器中弹跳 10 次：

```html
<img id='ball' src='ball.png' />

<script>
window.onload = function() {
  Position('ball', ABS)
  width = GetWindowWidth()
  height = GetWindowHeight()
  r = width - 100
  b = height - 100
  x = width / 20
  y = height / 50

  ch1 = InVars('Slide('ball', #1, #2, #3, #4, 500, 0)*', 0, y, x, 0)
  ch2 = InVars('Slide('ball', #1, #2, #3, #4, 500, 0)*', x, 0, r, y)
  ch3 = InVars('Slide('ball', #1, #2, #3, #4, 500, 0)*', r, y, x, b)
  ch4 = InVars('Slide('ball', #1, #2, #3, #4, 500, 0)*', x, b, 0, y)

  Repeat(10, Array(ch1, ch2, ch3, ch4))
}
</script>
```

## 插件

```javascript
function Repeat(number, calls) {
  var temp = calls

  for (var j = 1; j < number ; ++j)
    calls = calls.concat(temp)

  Chain(calls)
}
```

## While()

有时你可能会发现让插件链在某个条件为真时保持重复是很方便的；例如，如果没有按键被按下或鼠标未被点击。通过此插件，你可以提供链的同时提供一个测试条件，只要条件返回为真，链就会不断重复。

## 第 7 章：链链与交互 187

图 7-3 显示了一个en帆船的动画，它缓慢地淡入并横跨浏览器，然后再次淡出。在每次旅行之前，都会检查全局变量 `KEY_PRESS`，动画会不断重复，直到按下空格键为止。

## 关于插件

此插件接收一个表达式和一个语句数组，如果表达式求值为为真，则将它们链联起来。它需要以下参数：

- *expr*: 一个包含可以求值为真或为假的表达式的字符串
- *calls*: 一个包含要放入链中的插件序列的字符串数组

## 变量、数组和函数

| 变量 | 描述 |
|---|---|
| temp | 用于从 `calls` 数组中重构字符串的局部字符串变量 |
| j | 用于遍历 `calls` 数组的局部变量 |
| eval() | 评估 JavaScript 表达式的函数 |
| replace() | 替换字符串部分的函数 |
| substr() | 返回字符串部分内容的函数 |
| push() | 将值推入数组的函数 |
| InsVars() | 向字符串中插入值的插件 |
| Chain() | 用于将插件序列链在一起的插件 |

## 工作原理

此插件存在于 `if` 语句中，只有当传递给 `expr` 的字符串求值为真时才会完成，如下所示：

```javascript
if (eval(expr))
```

![](img/95e4c43b430487125c342550cc090977_204_0.png)

## 188 插件 JavaScript：解决方案

While() 插件的逻辑是什么？让我们来看看代码。该插件接收一个表达式和一个语句数组，如果表达式求值为真，则将它们链联起来。它需要以下参数：

- *expr*: 一个包含可以求值为真或为假的表达式的字符串
- *calls*: 一个包含要放入链中的插件序列的字符串数组

此插件存在于 `if` 语句中，只有当传递给 `expr` 的字符串求值为真时才会完成，如下所示：

```javascript
if (eval(expr))
```

While() 插件的逻辑是检查表达式，如果它为真，则执行调用链。然后再次检查表达式。此过程一直持续，直到表达式求值为假。

以下是 While() 插件的代码：

```javascript
function While(expr, calls) {
  while (eval(expr)) {
    Chain(calls)
  }
}
```

在下面的示例中，表达式是 `KEY_PRESS == 0`。只要用户没有按下任何键，动画就会继续进行。

```javascript
While("KEY_PRESS == 0", Array(Slide('ship', 1, 2, 3, 4, 500, 0), FadeOut('ship', 1, 2, 3, 4, 500, 0)))
```

这显示了如何使用 While() 插件创建一个直到满足特定条件为止的循环。

