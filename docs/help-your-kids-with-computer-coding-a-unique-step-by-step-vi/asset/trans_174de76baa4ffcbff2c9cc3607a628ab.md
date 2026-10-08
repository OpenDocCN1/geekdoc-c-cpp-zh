

# 创建窗口

许多程序都有窗口和按钮，可以使用它们来控制程序。这些构成了“图形用户界面”，或“GUI”（读音为 gooey）。

## 创建一个简单的窗口

创建 GUI 的第一步是创建一个用于存放内部所有内容的窗口。可以使用 Tkinter（来自 Python 标准库）来创建一个简单的窗口。

- 输入代码
这段代码从库中导入 Tkinter 并创建一个新窗口。在使用 Tkinter 之前，必须先导入它。

- 出现一个 Tkinter 窗口
运行代码，会弹出一个窗口。现在它看起来有点单调，但这仅仅是你 GUI 的第一部分。

```
from tkinter import *
window = Tk() # 这将创建了一个 Tkinter 窗口
```

![](img/72d218a7a73c4d4abc7be582ebd85385_155_0.png)

# 在窗口中添加按钮

通过添加按钮让 GUI 更具交互性。当用户点击每个按钮时，将显示不同的消息。

- 创建两个按钮
编写此代码创建一个带有两个按钮的简单窗口。

```
from tkinter import * # 按下按钮 A 时显示此消息
def bAction():
    print('Thank you!') # 按下按钮 B 时显示此消息
def bAction():
    print('Ouch! That hurt!')
window = Tk()
buttonA = Button(window, text='Press me!', command=bAction)
buttonB = Button(window, text='\t press!', command=bAction)
buttonA.pack() # 这个标签将出现在按钮 A 上
buttonB.pack() # 这个标签将出现在按钮 B 上
这段代码告诉计算机将按钮放在窗口中
```

![](img/72d218a7a73c4d4abc7be582ebd85385_155_1.png)

# 创建窗口

## 点击按钮打印消息
当程序运行时，会出现两个按钮。点击按钮，shell（终端）中就会出现不同的消息。你制作了一个对用户命令做出响应的交互式 GUI。

Tk

点击按钮显示消息

输出出现在 shell 窗口中

点击我！

谢谢！

不要按！

哎哟！好疼！

# 掷骰子

Tkinter 可用于为简单应用程序构建 GUI。下面的代码创建了一个模拟掷六面骰子的程序。

- 创建骰子模拟器
此程序创建了一个按钮，按下时会告诉 `roll()` 函数显示一个 1 到 6 之间的随机数。

![](img/72d218a7a73c4d4abc7be582ebd85385_156_0.png)

```
from tkinter import *
from random import randint
def roll():
    text.delete(0.0, END)
    text.insert(END, str(randint(1,6)))
window = Tk()
text = Text(window, width=1, height=1)
buttonA = Button(window, text='Press to roll!', command=roll)
text.pack()
buttonA.pack()
```

这从 random 库导入函数 "randint"

这清除框内的文本并将其替换为 1 到 6 之间的随机数

这创建了一个显示随机数的文本框

这告诉程序在点击按钮时运行函数

这个标签出现在按钮上

- 点击按钮掷骰子
运行程序，然后点击按钮掷骰子并查看结果。此程序可以简单修改，以模拟 12 面骰子或抛硬币。

Tk

# 专家技巧

## 简洁明了

在设计 GUI 时，不要用许多按钮填满屏幕以免困扰用户。为每个按钮标记一个合理的名称，使应用程序易于理解。

6

点击掷掷！

每次点击按钮，这里都会出现一个新数字

![](img/72d218a7a73c4d4abc7be582ebd85385_156_1.png)

# 颜色与坐标

屏幕上的图像和图形由微小的彩色点（像素）组成。要在程序中创建图形，需要精确告诉计算机每个像素应该是什么颜色。

## 另请

- 154–155 创建窗口
- 158–159 创建形状
- 160–161 改变内容

# 选择颜色

# 专家技巧

用计算机可以理解的方式描述颜色非常重要。Tkinter 包含一个实用的工具来帮助你。

## 混合颜色

每个像素都可以发出红、绿、蓝光。通过混合这些颜色，你可以制造任何想象中的颜色。

- 1 启动颜色选择工具
在 shell 窗口中输入以下代码启动 Tkinter 颜色选择工具。

这了所有的 Tkinter 函数

红和绿混合黄色
红和蓝混合紫色

```
>>> from tkinter import *
>>> t = Tk()
>>> colorchooser.askcolor()
```

使用美式拼写 color

通过点击选择你需要的颜色

混合所有三种颜色会得到白色

- 2 选择颜色
将出现“颜色选择器”窗口。 pick 出你需要的颜色，然后点击“OK”按钮。

![](img/72d218a7a73c4d4abc7be582ebd85385_157_0.png)

此窗口可以轻松选择你所需的精确颜色

- 3 颜色值
当选择颜色时，shell 窗口中会出现一个数字列表。这些数字是组成所选颜色的红、绿、蓝值。

```
((60.234, 190.742, 52.203), '#3cbe34')
```

- 红色值
- 绿色值
- 蓝色值
- 十六进制颜色代码（见第 182–183 页）

# 在画布上绘制

要使用 Python 创建图形，你需要创建一个用于绘制的区域。这被称为画布（canvas）。你可以使用 x 和 y 坐标精确告诉 Python 在画布的什么位置绘制。

> 专家技巧

## 坐标

在 Tkinter 中，x 坐标向右移动增大，y 坐标向下移动增大。(0,0) 位于左上角。

![](img/72d218a7a73c4d4abc7be582ebd85385_158_0.png)

# 创建图形程序

使用此代码创建一个窗口并在其中放入画布。它将在画布上绘制随机圆圈。

```
from random import *
from tkinter import *
size = 500
window = Tk()
canvas = Canvas(window, width=size, height=size)
canvas.pack()
while True:
    col = choice(['pink', 'orange', 'yellow'])
    x0 = randint(0, size)
    y0 = randint(0, size)
    canvas.create_oval(x0, y0, x0 + d, y0 + d, fill=col)
    window.update()
```

![](img/72d218a7a73c4d4abc7be582ebd85385_158_1.png)

# 彩色画布

运行代码，程序将开始绘制圆圈。圆圈在随机位置绘制

# 创建形状

除了添加窗口、按钮和颜色（GUI），Tkinter 还可以用于绘制形状。矩形和椭圆有助于绘制。一旦创建了画布，就可以使用以下函数在其上绘制![](img/72d218a7a73c4d4abc7be582ebd85385_159_0.png)

```
>>> tkinter import * # 创建画布
>>> window = Tk()
>>> drawing = Canvas(window,500,500)
>>> drawing.pack() # 绘制矩形
>>> drawing.create_rectangle(100, 100, 300, 200)
>>> # 绘制椭圆
>>> drawing.create_oval(170, 70, 230, 130)
>>> # 在椭圆内绘制黑点
>>> drawing.create_oval(190, 90, 210, 110)
```

设置坐标

第一个数字（x）告诉向右。第二个数字（y）告诉向下。矩形的左上角在 (50,50)。右下角在 (250,300)。

```

# 为形状添加颜色

也可以创建彩色形状。可以使用代码设置形状的轮廓和填充颜色（fill）。

带有红色边框的实心圆

![](img/72d218a7a73c4d4abc7be582ebd85385_160_0.png)

```
>>> drawing.create_oval(30, 30, 80, 80, outline='red', fill='blue')
```

# 画一个星人

通过组合不同的形状可以绘制任何内容。以下是使用椭圆、直线和三角形创建星人的指令。

- 创建星人
对于星人的每个部分，你必须定义形状类型、大小、画布位置和颜色。每个形状都有一个存储在变量中的 ID。

| from tkinter import * 设置 'Alien' 为窗口标题 |
| window = Tk() |
| window.title('Alien') 创建画布 |
| c = Canvas(window, height=300, width=400) 绘制绿色的椭圆身体 |
| c.pack() | |
| body = c.create_oval(100, 150, 300, 250, fill='green') | 在眼睛内绘制一个黑点 |
| eye = c.create_oval(170, 70, 230, 130, fill='white') | \
| eyeball = c.create_oval(190, 90, 210, 110, fill='black') |
| mouth = c.create_oval(150, 220, 250, 240, fill='red') | 绘制红色的椭圆嘴 |
| neck = c.create_line(200, 150, 200, 230) | |
| hat = c.create_polygon(180, 75, 220, 75, 200, 20, fill='blue') | 绘制蓝色的三角形作为星人的帽子 |

- 认识星人
运行代码绘制星人。它有绿色的身体、红色的嘴和一只长在柄上的眼睛。它还戴着一顶漂亮的蓝色帽子。

