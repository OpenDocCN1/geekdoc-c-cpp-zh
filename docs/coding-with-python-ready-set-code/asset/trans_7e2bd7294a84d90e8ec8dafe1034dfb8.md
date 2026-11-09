
## 7. 使用图章积木并设置程序颜色

`stamp` 积木会生成你在程序中使用的角色（一只海龟）的图像，并将其盖印到白色画布上。

向程序中添加 `stamp` 和 `set color to` `yellow` 积木，以制作一个图章并将其颜色设为红色。再添加一个 `go to x: 0 y: 0` 积木来定位图章。

```text
when green flag clicked
pen up
go to x: 250 y: 40
set color to yellow
stamp
go to x: -20 y: 40
say "Hello! What are you doing?" for 2 seconds
```

按 ▶ 运行来测试你的程序。

## 8. 添加另一只海龟

现在你可以添加另一只海龟来与第一只对话。你需要让它看起来与第一只不同，因此需要使用不同的颜色。在步骤 7 的程序下方添加以下积木：

```text
pen up
go to x: 250 y: -10
set color to green
stamp
go to x: -20 y: -10
say "I am coding with Python!" for 1 second
```

按 ▶ 运行来测试你的程序。

> `pen up` 积木可以拼接到上一步的 `go to x: 0 y: 0` 积木下方，也可以就放在下面并保持分开。

> **你知道吗？**
> 
> 最大的海龟是棱皮龟。它的体重可超过 1,900 磅！

![](img/a1849c7d7e98817476d64684d9c96952_13_0.png)

## 完成对话

要完成海龟之间的对话，请向程序中添加以下积木。

```text
get [say] [Hello!]
when [green flag clicked]
say [Hello!]
wait [2] seconds
say [What can you code?]
wait [4] seconds
```

> 你可以右键单击白色画布中的任意积木并复制它。

![](img/a1849c7d7e98817476d64684d9c96952_14_0.png)

### 挑战

向程序中添加更多语句，让海龟进行更长的对话。

- 你好！你在做什么？
- 我正在用 Python 编程。
- 你能编什么程序？
- 一个圆
- 哇！太棒了。
- 谢谢。

## 画一个圆

在对话结束时，蓝色海龟将画一个圆。添加以下积木：

```text
pen up
move [20] steps
pen down
set color to [orange]
forward [25]
turn right [20]
```

按 ▶ 运行来测试你的程序。

### 故障排除

如果你希望文本居中，请使用 [go to x: 0 y: 0] 积木将对话定位到屏幕中间。尝试为 x 坐标使用 [go to x: 0 y: 0]。

## 阿根廷

制作国旗并发现一些关于阿根廷的有趣事实！

### 准备

在这段代码中，你将通过绘制不同颜色的矩形来制作阿根廷国旗。

### 开始

- 1. 访问 Trinket：https://trinket.io/ 并登录。
- 2. 输入你的用户名和密码。

![](img/a1849c7d7e98817476d64684d9c96952_15_0.png)

> 阿根廷是南美洲仅次于巴西的第二大国，也是世界第八大国。

### 你知道吗？

莱昂内尔·梅西出生于阿根廷罗萨里奥。11 岁时，他随父亲搬到巴塞罗那。他现在保持着巴塞罗那的大部分进球纪录，并且是阿根廷历史最佳射手。

![](img/a1849c7d7e98817476d64684d9c96952_15_1.png)

## 设置

在开始编码之前，你需要打开一个新的 Trinket。

> **你知道吗？**
> 
> 阿根廷这个名字来自拉丁语中表示银的词：argentum。

### 打开新的 Trinket

单击 **新建 Trinket**，然后单击 Blocks。

![](img/a1849c7d7e98817476d64684d9c96952_16_0.png)

你将看到以下窗口。单击 Loops。

你将把程序所需的积木拖放到这个白色画布中。

以下菜单将会打开。

![](img/a1849c7d7e98817476d64684d9c96952_16_1.png)

> **什么是循环？**
> 
> 循环是重复的命令或命令集。循环会重复执行动作。

![](img/a1849c7d7e98817476d64684d9c96952_16_2.png)

当你单击左侧的任何其他选项时，会打开不同的菜单。

## 编码！

现在你需要创建彩色矩形来组成你的国旗。

![](img/a1849c7d7e98817476d64684d9c96952_17_0.png)

### 3. 使用循环绘制矩形

使用 Loops 和 Turtle 菜单向程序中添加以下积木：

```text
repeat 2 times
do
  turn right by 90
  move forward by 50
  turn right by 90
  move forward by 150
```

按 ▶ 运行来测试你的程序。你应该会在屏幕右侧看到一个矩形。

### 4. 给矩形上色

使用 Turtle 菜单在程序的开头和结尾添加以下三个积木：

这个积木将设置程序的颜色。

```text
set color to blue
repeat 2 times
do
  turn right by 90
  move forward by 50
  turn right by 90
  move forward by 150
```

这个积木将给矩形上色。

按 ▶ 运行来测试你的程序。你应该会在屏幕右侧看到一个蓝色矩形。

![](img/a1849c7d7e98817476d64684d9c96952_17_1.png)

函数就像食谱。例如，煮米饭需要遵循一系列指令：烧水、加盐、倒入大米、炖煮 20 分钟、沥干剩余的水，并用叉子把米饭拨松。函数让程序员可以把所有这些指令放在一个积木下，并给它起个名字，例如“Rice”。每次需要煮米饭时，你都可以使用“Rice”函数。

### 创建函数

阿根廷国旗分为三个水平矩形，颜色依次为蓝色、白色、蓝色。使用 Functions 菜单向程序中添加以下积木：让我们通过删除“do something”并将函数命名为“蓝色矩形”来创建一个函数。

从 Functions 菜单中，将你刚刚创建的 **蓝色矩形** 函数添加到程序旁边，如下所示：

按 ▶ 运行来测试你的程序。你仍应看到与步骤 4 相同的矩形，但它现在是一个函数，你将在下一步再次使用它。

![](img/a1849c7d7e98817476d64684d9c96952_18_0.png)

### 复制函数

右键单击步骤 5 开头使用的积木，然后选择 Duplicate。

![](img/a1849c7d7e98817476d64684d9c96952_18_1.png)

> 探戈舞蹈和音乐诞生于阿根廷布宜诺斯艾利斯。

![](img/a1849c7d7e98817476d64684d9c96952_18_2.png)

### 7. 更改函数的颜色

你可能记得阿根廷国旗有两种颜色和三个矩形，因此你需要更改第二个函数的颜色。单击你在步骤 6 中创建的第二个函数中的 **颜色** 积木，然后选择白色。

将函数名从“蓝色矩形2”改为“白色矩形”。

![](img/a1849c7d7e98817476d64684d9c96952_19_0.png)

### 8

![](img/a1849c7d7e98817476d64684d9c96952_19_1.png)

### 使用函数绘制国旗

将函数放在白色画布的一侧，并使用 Turtle 和 Functions 菜单，在你在步骤 5 末尾创建的蓝色矩形积木下方添加以下积木。请记住，紫色积木位于 Functions 菜单中；浅绿色积木位于 Turtles 菜单中。

按 ▶ 运行来测试你的程序。

> **你知道吗？**
> 
> 伊瓜苏瀑布位于阿根廷和巴西边境，是世界上最大的瀑布系统。伊瓜苏瀑布由 275 个瀑布组成，落差达 246 英尺。

![](img/a1849c7d7e98817476d64684d9c96952_19_2.png)

### 添加彩色消息

让我们添加一条彩色文本消息。

向程序中添加以下积木：

这条消息将显示在国旗上方。

字体大小将自动设置为 14，但你可以将其更改为任意大小。

```text
    when flag clicked
    set size to 14
    go to x: -150 y: 50
    say 'This is the Argentine flag!' for 2 secs
```

按 ▶ 运行来测试你的程序。

### 你知道吗？

卢西亚娜·艾马尔是一位退役的阿根廷曲棍球运动员。她是历史上唯一一位八次获得年度最佳球员奖的球员，并被认为是史上最优秀的女子曲棍球运动员之一。

![](img/a1849c7d7e98817476d64684d9c96952_20_0.png)

### 10 添加文本

现在我们可以使用 Text 菜单中的 print 积木添加一些事实：

这些行将分别显示在屏幕底部。

```text
    when flag clicked
    go to x: -150 y: 50
    set size to 14
    print 'This is the Argentine flag!'
    print 'The capital of Argentina is Buenos Aires.'
    print 'The official language is Spanish.'
    print 'Lionel Messi was born in Argentina.'
```

按 ▶ 运行来测试你的程序。

![](img/a1849c7d7e98817476d64684d9c96952_20_1.png)

### 挑战

运用你的 Python 编写技巧以及你在本项目读到的事实，向程序中添加关于阿根廷的信息。尝试将这些事实放在屏幕上的不同位置。

### 故障排除

如果消息“这是阿根廷国旗。”没有正好位于国旗上方，请更改这些积木中的坐标：

```text
    when flag clicked
    set size to 14
    go to x: -150 y: 50
    say 'This is the Argentine flag!'
```

