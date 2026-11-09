
## 星空

接下来的步骤会把你的星星封装成一个 Python 函数。然后你就可以使用该函数来绘制一片布满星星的天空。

`draw_star()` 函数使用五个参数来定义星星的形状、大小、颜色和位置。

### 9. 创建星星函数

按此处所示编辑代码。它会用新版本替换几乎你现有的所有代码。这一大块代码把所有绘制星星的指令封装起来，并将它们整齐地组合成一个函数。现在你可以在主代码中使用这个函数绘制一颗星星，而无需编写一行 Python 代码，只需调用 `draw_star()`。

```python
import turtle as t

def draw_star(points, size, col, x, y):
    t.penup()
    t.goto(x, y)
    t.pendown()
    angle = 180 - (180 / points)
    t.color(col)
    t.begin_fill()
    for i in range(points):
        t.forward(size)
        t.right(angle)
    t.end_fill()

# Main code
t.Screen().bgcolor('dark blue')
draw_star(5, 50, 'yellow', 0, 0)
```

x 和 y 坐标设定星星在屏幕上的位置。

这会将背景颜色设置为深蓝色。

海龟会在窗口中央绘制一颗尺寸为 50 的黄色五角星。

这条以井号（`#`）开头的“注释”行不是 Python 运行的代码的一部分。它就像一个标签，帮助你理解程序。

这一行调用（运行）该函数。

### 10. 运行项目

海龟应该在蓝色背景上绘制一颗黄色星星。

![](img/6b18a113f7aa9338e32f3ac1fa217987_96_0.png)

### 记住

#### 注释

程序员经常在代码中添加注释，以提醒自己程序不同部分的作用，或解释项目中棘手的部分。注释必须以 `#` 开头。Python 会忽略你在 `#` 之后同一行输入的任何内容，不会将其视为代码的一部分。在自己的项目中编写注释（例如上面显示的 `# Main code` 行）在你离开一段时间后再回来看程序时，会非常有帮助。

### 11. 添加随机数

现在通过向代码中添加一些随机数来增加变化。在导入 Turtle 的那一行下面输入这一行。它会从 Python 的 random 模块中引入 randint() 和 random() 函数。

```python
import turtle as t
from random import randint, random

def draw_star(points, size, col, x, y):
```

### 12. 创建循环

对 #Main code 部分做此修改。它会添加一个 while 循环，不断随机化用于设置星星大小、形状、颜色和位置的参数。

ranPts 行将星星的角数限制为 5 到 11 之间的奇数。

这一行也有变化。当它调用 draw_star() 函数时，现在会使用 while 循环中的随机变量。

```python
# Main code
t.Screen().bgcolor('dark blue')

while True:
    ranPts = randint(2, 5) * 2 + 1
    ranSize = randint(10, 50)
    ranCol = (random(), random(), random())
    ranX = randint(-350, 300)
    ranY = randint(-250, 250)

    draw_star(ranPts, ranSize, ranCol, ranX, ranY)
```

### 13. 再次运行项目

随着海龟绘制一颗又一颗颜色、形状和大小各异的星星，窗口应该会慢慢被填满。

### 记住！

如果你不想看到海龟，请记住有一个命令可以让它隐形。将这行添加到程序中，你的星星就会神奇地出现，而不会有一只隐形的海龟！

```python
# Main code
t.hideturtle()
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_97_0.png)

海龟随机绘制星星。

![](img/6b18a113f7aa9338e32f3ac1fa217987_97_1.png)

### 技巧与调整

现在你可以按需创建星星了。为什么不试试在自己的项目中使用 `draw_star()` 代码呢？这里有几个想法。

![](img/6b18a113f7aa9338e32f3ac1fa217987_98_0.png)

- **△ 改变你的星星**

  要改变星星的多样程度，可以修改 while 循环中 `ranPts` 和 `ranSize` 变量括号里的数字。

- **▷ 点击生成星星**

  与其让海龟随机绘制星星，不如试试使用 `turtle.onscreenclick()` 函数，在你用鼠标点击的任何位置绘制一颗星星。

  ![](img/6b18a113f7aa9338e32f3ac1fa217987_98_1.png)

- **▽ 加速海龟**

  你可以通过创建 `speed()` 函数来改变海龟绘制星星的速度。只需在主代码开头添加 `t.speed(0)`，就能让海龟更快。你可以在 Python 的“帮助”部分查看 turtle 包的所有函数。

- **▽ 设计星座**

  星座是夜空中星星的图案。试着为你自己设计的星座创建一个包含星星 (x, y) 位置的列表。然后使用 `for` 循环在这些位置绘制星星。

  ![](img/6b18a113f7aa9338e32f3ac1fa217987_98_2.png)

  ![](img/6b18a113f7aa9338e32f3ac1fa217987_98_3.png)

  ![](img/6b18a113f7aa9338e32f3ac1fa217987_98_4.png)

  ![](img/6b18a113f7aa9338e32f3ac1fa217987_98_5.png)

  ![](img/6b18a113f7aa9338e32f3ac1fa217987_98_6.png)

  ![](img/6b18a113f7aa9338e32f3ac1fa217987_98_7.png)

- **▷ 绘制一些行星**

  研究 `turtle.circle()` 函数，看看能否用它编写一些绘制行星的代码。下面是一些帮助你入门的代码。

```python
def draw_planet(col, x, y):
    t.penup()
    t.goto(x, y)
    t.pendown()
    t.color(col)
    t.begin_fill()
    t.circle(50)
    t.end_fill()
```

## 变异彩虹

你可以编写 Python 海龟程序来绘制各种图案和设计。但要小心！这个项目里的海龟似乎有点失控了——你在天空中可看不到这样的彩虹！

### 会发生什么

程序会要求你选择海龟绘制线条的长度和粗细。然后海龟会在屏幕上快速移动，直到你停止程序，一边移动一边绘制彩色线条。它生成的图案类型会因线条长度和粗细而变化。

![](img/6b18a113f7aa9338e32f3ac1fa217987_99_0.png)

Python 海龟图形

海龟有一支“笔”，当它在窗口上移动时会画出线条。

### 专家提示

#### 下一种颜色是什么？

在“变异彩虹”中，当你让海龟画线时，你会使用 Python 的 random 库中的 `choice()` 函数来选择颜色。这意味着你无法真正预测海龟每次会使用哪种颜色。

```python
t.pencolor(random.choice(pen_colors))
```

海龟会从你放入列表 `pen_colors` 的六种颜色中进行选择。

> 这是充满可能性的彩虹！

![](img/6b18a113f7aa9338e32f3ac1fa217987_100_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_100_1.png)

海龟可以涂绘绿色、红色、橙色、黄色、蓝色和紫色。

海龟可以向右转 0 到 180 度。

你可以使用 `line_length()` 函数让海龟绘制长线、中线或短线。

#### 色彩展示

因为这个程序使用无限 `while` 循环，所以海龟会一直绘制，直到你关闭它的窗口。你不仅可以改变线条的颜色、宽度和长度，还可以改变海龟本身的形状、颜色和速度。

### 工作原理

这个项目中的每个图案都不同，因为程序会在绘制每条线之前让海龟朝向一个随机的新方向。每条线的颜色也是从你编码的可能颜色列表中随机选择的。所以你永远无法准确预测海龟会做什么！

![](img/6b18a113f7aa9338e32f3ac1fa217987_101_0.png)

长而粗

![](img/6b18a113f7aa9338e32f3ac1fa217987_101_1.png)

中等而细

![](img/6b18a113f7aa9338e32f3ac1fa217987_101_2.png)

短而超粗

> 一只神奇的海龟？我一定要弄一只！

![](img/6b18a113f7aa9338e32f3ac1fa217987_101_3.png)

### 变异彩虹流程图

该程序使用无限循环，只要程序运行，就会不断绘制彩色线条。只有当你关闭窗口时，海龟才会停止它疯狂的游荡。

![](img/6b18a113f7aa9338e32f3ac1fa217987_101_4.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_102_0.png)

### ◁ 逃跑的海龟！

如果让海龟完全自由地漫游，它往往会游荡到窗口之外。在搭建程序的过程中，你会编写一些代码来检查海龟的位置，并阻止它偏离太远。否则，这个项目就会变成“消失的海龟”项目！

### 开始

首先，新建并保存一个文件，导入程序所需的模块，并编写几个用于获取用户输入的有用函数。

![](img/6b18a113f7aa9338e32f3ac1fa217987_102_1.png)

- **1. 创建新文件**

  打开 IDLE 并新建一个文件。将其保存为 `rainbow.py`。

- **2. 添加模块**

  在文件顶部输入这两行，以导入 Turtle 模块和 random 模块。记住要使用 `import turtle as t`，这样每次想使用 Turtle 模块中的函数时，就不必输入“turtle”这个词。你只需称它为 `t`。

```python
import random
import turtle as t
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_102_2.png)

### 指定线条长度

接下来编写一个函数，让用户决定海龟绘制长线、中线还是短线。直到第 4 步才会用到它，但这会让程序为你需要时做好准备。将这段代码输入到第 1 步代码的下方。

```python
def get_line_length():
    choice = input('Enter line length (long, medium, short): ')
    if choice == 'long':
        line_length = 250
    elif choice == 'medium':
        line_length = 200
    else:
        line_length = 100
    return line_length
```

这会要求用户选择线条的长度。

对于短线，将 `line_length` 设置为 100。

此命令会将 `line_length` 传回调用该函数的代码。

