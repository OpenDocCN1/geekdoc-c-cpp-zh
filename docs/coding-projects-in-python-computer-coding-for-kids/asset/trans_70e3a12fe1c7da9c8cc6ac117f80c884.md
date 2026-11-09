
## 2. 添加手臂

接下来，将原先位于注释行 `# arms` 和注释行 `# neck` 之间的代码替换为下面显示的代码。它使用 arm 函数绘制三条手臂。

```python
# arms
t.goto(-90, 85)
t.setheading(180)
arm('light blue')

t.goto(-90, 20)
t.setheading(180)
arm('purple')

t.goto(10, 85)
t.setheading(0)
arm('goldenrod')
```

-   将海龟设置为指向机器人的右侧（窗口的左边缘）。
-   使用 arm 函数绘制一条浅蓝色的手臂。
-   将海龟设置为指向机器人的左侧（窗口的右边缘）。

### 专家提示

**反复试验**

当你设计机器人或为现有机器人添加新功能时，可能需要反复试验才能让一切完全符合你的想法。如果你在 `t.speed('slowest')` 这一行之后添加 `print(t.window_width())` 和 `print(t.window_height())` 这两行，Python 将在 shell 中显示 Turtle 窗口的高度和宽度。然后在方格纸上标出该尺寸的网格，以帮助你算出每个身体部位的坐标。

![](img/6b18a113f7aa9338e32f3ac1fa217987_82_0.png)

### 移动手臂

现在你可以一次性绘制整条手臂，因此可以改变它的位置，让机器人看起来像在挠头，或者可能在跳高地舞！为此，在开始绘制手臂时，使用 `setheading()` 函数改变海龟的朝向。

```python
# arms
t.goto(-90, 80)
t.setheading(135)
arm('hot pink')

t.goto(10, 80)
t.setheading(315)
arm('hot pink')
```

-   将海龟设置为指向窗口的左上角。
-   使用 arm 函数在右侧绘制一条手臂。
-   将海龟设置为指向窗口的右下角。
-   使用 arm 函数在左侧绘制一条手臂。

> “可以请你跳下一支舞吗？”

![](img/6b18a113f7aa9338e32f3ac1fa217987_82_1.png)

## 万花筒螺旋

正如简单的代码行可以组成优秀的程序一样，简单的形状也可以组成复杂的画面。通过代码将形状和颜色组合起来，万花筒螺旋将帮助你创作一幅足以登上艺术画廊的数字艺术杰作！

### 会发生什么

Python 的 turtle 在屏幕上一个接一个地画圆。每画一个圆，海龟都会改变下一个要画的圆的位置、角度、颜色和大小。一个图案逐渐显现出来。

![](img/6b18a113f7aa9338e32f3ac1fa217987_83_0.png)

代码会隐藏海龟，因此它在画圆时不会被看到。

![](img/6b18a113f7aa9338e32f3ac1fa217987_83_1.png)

**△ 移动的螺旋**

随着圆圈层层叠叠，它们不断变化的位置形成了一条从中心蜿蜒而出的螺旋。

每个圆的大小和颜色都与前一个不同。

![](img/6b18a113f7aa9338e32f3ac1fa217987_83_2.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_84_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_84_1.png)

它们都是杰作！

![](img/6b18a113f7aa9338e32f3ac1fa217987_84_2.png)

海龟从屏幕中心开始绘制。

**◁ 可调整的程序**

万花筒螺旋运行的时间越长，屏幕上的图案就越复杂。通过更改画圆函数的参数，你可以创造出更令人惊叹的图案。

### 工作原理

在这个项目中，你将使用 `turtle` 模块和一种巧妙的循环技术，以螺旋模式将圆圈层层叠加。每画一个圆，程序都会稍微增加画圆代码的参数。每个新圆都与上一个不同，使图案更加有趣。

### 万花筒螺旋流程图

程序会设置一些始终保持不变的值，例如海龟的速度，然后开始循环。循环会选择新的画笔颜色、画一个圆、转动并移动海龟，然后重复。当你退出程序时，循环停止。

![](img/6b18a113f7aa9338e32f3ac1fa217987_85_0.png)

### 专家提示

**循环**

为了让图案色彩丰富，这个项目使用了 `itertools` 模块中名为 `cycle()` 的函数。`cycle()` 函数允许你一遍又一遍地循环使用一个包含不同颜色的列表。这样就能轻松地为每个圆使用不同的画笔颜色。

![](img/6b18a113f7aa9338e32f3ac1fa217987_85_1.png)

### 开始绘制！

你将在屏幕上绘制的第一样东西是一个简单的圆。接下来，你将重复这个圆，但稍作改变。最后，你将调整代码，使图案更加丰富多彩、更有趣。

1.  **创建一个新文件**
    打开 IDLE 并创建一个新文件。将其保存为 `kaleido-spiral.py`。

### 导入 turtle

首先需要导入 turtle 模块。这将是你使用的主要模块。在程序顶部输入这一行。

```python
import turtle
```

加载整个 turtle 模块。

### 设置海龟

这里显示的代码调用 turtle 模块中的函数来设置背景颜色，以及海龟的速度和大小。

```python
import turtle

turtle.bgcolor('black')
turtle.speed('fast')
turtle.pensize(4)
```

背景颜色

海龟的速度

海龟轨迹的粗细

### 选择画笔颜色，画一个圆

接下来设置海龟轨迹的颜色，并通过画一个圆来测试代码。将这两行添加到代码末尾并运行程序。

```python
import turtle

turtle.bgcolor('black')
turtle.speed('fast')
turtle.pensize(4)

turtle.pencolor('red')
turtle.circle(30)
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_86_0.png)

画笔颜色

这会告诉海龟画一个圆。

### 绘制更多圆

现在你应该能看到一个单独的圆，但我们需要更多圆。巧妙的地方来了。将绘制红色圆的命令放入一个函数中，但添加一行让该函数调用自身。这种技巧称为递归，它使函数重复执行。记住，函数需要先定义再使用，因此你需要将 turtle 移到调用它的那一行上方。

```python
import turtle

def draw_circle(size):
    turtle.pencolor('red')
    turtle.circle(size)
    draw_circle(size)

turtle.bgcolor('black')
turtle.speed('fast')
turtle.pensize(4)
draw_circle(30)
```

这一行使用 size 参数。

函数调用自身，从而使其无休止地重复。

这一行第一次调用该函数。

![](img/6b18a113f7aa9338e32f3ac1fa217987_86_1.png)

### 专家提示

**递归**

当一个函数调用自身时，这称为递归。这是在你的程序中创建循环的另一种方式。在大多数递归用法中，每次调用函数时，函数的参数都会改变。例如，在万花筒螺旋中，每次调用函数时，圆的大小、角度和位置都会改变。

![](img/6b18a113f7aa9338e32f3ac1fa217987_87_0.png)

### 6. 测试你的代码

运行程序。你会看到海龟一遍又一遍地画同一个圆。别担心——你将在下一步解决这个问题。

![](img/6b18a113f7aa9338e32f3ac1fa217987_87_1.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_87_2.png)

### 7. 改变颜色，增大尺寸

要创建更令人兴奋的图案，请对代码进行以下更改，以增大圆的尺寸并改变其颜色。这段代码使用了 `cycle()` 函数，它接受一个值列表作为参数，并返回一种特殊类型的列表，你可以在 `next()` 函数中无休止地循环使用它。再次运行代码。

```python
import turtle
from itertools import cycle

colors = cycle(['red', 'orange', 'yellow', 'green', 'blue', 'purple'])

def draw_circle(size):
    turtle.pencolor(next(colors))
    turtle.circle(size)
    draw_circle(size + 5)

turtle.bgcolor('black')
turtle.speed('fast')
turtle.pensize(4)
draw_circle(30)
```

导入 `cycle()` 函数。

这一行创建列表中颜色的循环。

使用循环中的下一种颜色。

将上一个圆的尺寸增加 5。

