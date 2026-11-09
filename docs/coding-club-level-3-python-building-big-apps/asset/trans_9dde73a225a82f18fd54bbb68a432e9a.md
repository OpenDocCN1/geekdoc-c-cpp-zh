
## Table 类规划页

这是一张规划草图和一份 Table 类设计表。

![](img/c4403822ba1e00f0a2ce532b3f9d5054_38_0.png)

| 类名 | Table |
| --- | --- |
| 属性 |  |
|  | window |
|  | width=600 |
|  | height=400 |
|  | colour=black |
|  | net_colour=green |
|  | vertical_net (T/F) |
|  | horizontal_net (T/F) |
| 方法 |  |

### 说明

提供大量**默认值**（例如宽度为 600 像素）会很有帮助。

这些属性将放入一个冗长的构造函数中。

通过为球网位置设置一些**布尔变量**，就可以轻松使用这个类构建各种球桌，其球网可以是垂直的、水平的或不存在！

目前这个球桌类不需要任何方法。

> 啊，是的，布尔变量：它们让我们能清楚地看到世界上什么是真、什么是假。

![](img/c4403822ba1e00f0a2ce532b3f9d5054_38_1.png)

## tkinter 工具包

Python 3 安装时还会附带安装一组额外的模块，它们为我们提供了一些 GUI 控件。这些内容在 *Python: Next Steps* 中已经探讨过。

由于我们将使用 tkinter 类中的许多方法，可以选择使用下面这行代码：

```python
from tkinter import *
```

> 这样导入模块的缺点是，我们现在必须避免在自己的代码中使用任何 tkinter 方法名。

![](img/c4403822ba1e00f0a2ce532b3f9d5054_39_0.png)

这意味着，在后续代码中，我们可以直接引用 tkinter 的任意方法。我们不再需要在每个方法前加上其所在模块的名称：不再需要在每次调用 tkinter 方法时在前面加上 `tkinter.`。

## Table 类构造函数

我们的构造函数需要为每个属性传入一个参数，这些属性是我们在创建一个新对象时希望能够选择的。然后，像之前一样，我们会把它们赋值给所有 `self.variables`。

打开 `pong-table-start` 文件夹中的 `table.py`。该文件位于 Chapter 3 文件夹中。用 IDLE 打开它，并添加代码框 3.1 中缺失的代码。将你的代码添加到代码框标题栏所示文件中。

你能看出这如何与我们计划的第一部分相匹配吗？

### 代码框 3.1 — `table.py`

```python
# This class defines a Table that is a 2D rectangle that is a play area.

from tkinter import *

class Table:
    #### constructor
    def __init__(self, window, colour='black', net_colour='green',
                 width=600, height=400,
                 vertical_net=False, horizontal_net=False):
        self.width = width
        self.height = height
        self.colour = colour
```

这样构建的类非常像工厂。在 main.py 中，我们将能够用类似下面的代码快速制造一个球桌：

`my_table = table.Table(window)`

由于我们在构造函数的 `__init__` 行中提供了所有默认值，唯一必需的参数将是 window。这个类将创建一个与我们想要的球桌几乎一样的球桌对象，但有一个例外。

> 我以前从未意识到英国人拼写 colour 时会带一个“u”。

![](img/c4403822ba1e00f0a2ce532b3f9d5054_40_0.png)

### 快速测验 3.1

回看代码框 3.1 中的 `__init__` 行，以及 Table 类规划页上所需球桌的示意图。我们得到的球桌与想要的球桌之间会有什么区别？

以这种方式构建类意味着，将来我们可以用一行代码构建各种球桌。Table 类变成了一个非常有用的小工厂（图 3.2）。你想要一张带水平球网、尺寸为 300 像素 × 300 像素的红色球桌吗？只需这样写：

```python
my_table = table.Table(window, horizontal_net=True, width=300, height=300, colour='red')
```

![](img/c4403822ba1e00f0a2ce532b3f9d5054_41_0.png)

图 3.2 一些球桌对象。

### 快速测验 3.2

要创建一个带垂直红色球网、宽 600 像素、高 400 像素的蓝色球桌对象，代码会是什么样？

## 更多 tkinter 工具

构造函数方法还没有完全完成，因为我们还没有让它真正构建球桌或球网。我们会把窗口的绘制留给 main.py（很快就会编写）。要构建球桌，我们必须使用一些 tkinter 代码，可能需要在 tkinter 网站上查找说明。这是一个相当大的库，你不需要担心自己去做这件事，因为已经为你完成了。如果你感兴趣，可以随意查看。在撰写本书时，可以在以下位置找到说明：

http://docs.python.org/py3k/library/tk.html

首先，我们需要创建画布，其代码如下：

```python
self.canvas = Canvas(window, bg=self.colour, height=self.height, width=self.width)
```

Canvas 类是 tkinter 的一个工厂，需要窗口、背景颜色、高度和宽度这些参数——这些参数在构造函数的第一部分中都有对应的变量。

## 深入探索

### 何时使用 self，何时不需要

当我们构建一个诸如 Table 类的类时，需要把构建其球桌对象所需的任何属性传给它。例如，球桌要放入一个窗口对象中——因此我们需要把 window 作为参数传给它。

另一方面，如果我们要传给 Table 类一个属性（例如 width），并且可能希望其他类或文件查询它（例如：Table，你有多宽？），那么就需要在构造函数中用 self 将其声明为对象变量。然后，其他类或文件就可以询问这个球桌对象它有多宽。

接下来要做的是调用 canvas 的 pack() 方法。它不需要任何参数：

```python
self.canvas.pack()
```

需要调用 pack() 方法，才能让我们的球桌在执行其他任务时可见。接下来，我们可以使用 canvas 的 create_line() 方法绘制球网。其形式如下：

```python
self.canvas.create_line([top x-coord], [top y-coord], [bottom x-coord],
                         [bottom y-coord], width=2, fill=net_colour, dash=(15, 23))
```

宽度以像素为单位，因此我们要一条两像素粗的线。

fill 是线条的颜色——我们已经为此准备好了一个变量。

dash 属性接受两个数字——虚线的长度和间隔，同样以像素为单位。

要理解坐标，需要知道：与学校里的数学和科学不同，计算机通常从屏幕或窗口的左上角开始计算像素。Python 中就是这样。请看图 3.3 了解其工作方式。

![](img/c4403822ba1e00f0a2ce532b3f9d5054_44_0.png)

**图 3.3** 坐标。

因此，实现 `create_line()` 方法的调用可以写成：

```python
self.canvas.create_line(300, 0, 300, 400, width=2, fill=net_colour, dash=(15, 23))
```

然而，这不是一个好办法，因为我们正试图构建一个 Table 类。一个只能构建一种球桌的工厂没有多大用处。如果我们想要一张更长的球桌呢？球网就会太靠左。更高的球桌则会有球网够不到底部的问题！但我们有保存球桌对象宽度和高度属性的变量，因此可以在方法中根据这些变量计算坐标。这样球网就总会处于正确的位置：

对于垂直球网：

- [顶部 x 坐标] 变为 self.width/2
- [顶部 y 坐标] 变为 0
- [底部 x 坐标] 变为 self.width/2
- [底部 y 坐标] 变为 self.height

对于水平球网：

- [左侧 x 坐标] 变为 0
- [左侧 y 坐标] 变为 self.height/2
- [右侧 x 坐标] 变为 self.width
- [右侧 y 坐标] 变为 self.height/2

现在，你可以将代码框 3.2 中的额外代码添加到你的 `table.py` 副本中。使用所提供文件中的注释来指导你把新代码添加到何处。

### 代码框 3.2

```python
# order a canvas to draw on from the tkinter factory:
self.canvas = Canvas(window, bg=self.colour, height=self.height, width=self.width)
self.canvas.pack()

# add a net to the canvas using a method from the tkinter factory:
if(vertical_net):
    self.canvas.create_line(self.width/2, 0, self.width/2,
                            self.height, width=2, fill=net_colour, dash=(15, 23))
if(horizontal_net):
    self.canvas.create_line(0, self.height/2, self.width,
                            self.height/2, width=2, fill=net_colour, dash=(15, 23))
```

### 警告！

在某些阶段很容易出现输入错误。请仔细检查代码，完成之后运行程序，看看能否发现并纠正任何问题。如果你遇到困难并开始感到沮丧，那么可以从配套网站获取完整文件。毕竟，编程应该是有趣的。在使用完整文件之前，请务必尝试自己输入代码，并在输入时思考每一行代码是如何工作的。这样做会让你更好地学习编程。（这句话似乎陷入了无限循环！）
