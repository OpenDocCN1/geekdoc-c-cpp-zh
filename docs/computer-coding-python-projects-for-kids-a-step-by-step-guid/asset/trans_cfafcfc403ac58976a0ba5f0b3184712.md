

![](img/1bd24ab186f69fb18194b4174ca15178_90_0.png)

> 我看到星星啦！

你可以选择任何你想要的背景颜色，但星星在像这种蓝色一样浓重、深暗的颜色上可能看起来最好。

海龟（黄色箭头）仍在绘制这颗星星。当星星绘制完成后，Python 会用颜色填充它。

![](img/1bd24ab186f69fb18194b4174ca15178_90_1.png)

![](img/1bd24ab186f69fb18194b4174ca15178_90_2.png)

每颗星星都画在随机位置。

使用三个随机数为每颗星星选择一种新颜色。

你可以使用代码更改每颗星星的大小和角数。

### 满屏星星

星空项目会一颗一颗地绘制星星，但由于它使用了无限的 `while` 循环，它会永远绘制星星！你可以通过调整代码中随机数的范围限制来改变星星的大小范围。

![](img/1bd24ab186f69fb18194b4174ca15178_91_0.png)

## 工作原理

这个项目的代码会在海龟绘图窗口中的随机位置绘制星星形状。你将编写 Python 代码来创建一个可以绘制单颗星星的函数。然后，你会创建一个循环，一遍又一遍地重复它，在屏幕上绘制许多不同的星星。

### 星空流程图

这个流程图相当简单，不需要提出问题或做出判断。一旦海龟画完第一颗星星，程序就会循环回去，不停重复绘制星星的步骤，直到你退出。

- 开始 → 绘制天空 → 为星星随机选择角数 → 随机选择一种颜色 → 在天空中随机选择一个位置 → 绘制星星 ↺

![](img/1bd24ab186f69fb18194b4174ca15178_91_1.png)

> “202，202，203……哦，我想我漏数了一颗！”

> “你试过用循环吗？”

### 数星星

在晴朗的夜晚，天空中大约有 4,500 颗可见的星星。要让你的程序绘制这么多星星，你需要让它运行超过 3 个小时！

## 画一颗星星

在创建函数之前，你需要了解如何在海龟绘图中画一颗星星。掌握之后，你就能构建项目其余部分的代码了。

- **1. 创建一个新文件**

  打开 IDLE。转到“文件”菜单，然后选择“新建文件”。将文件保存为“starry_night.py”。

- **2. 导入 turtle**

  在出现的编辑器窗口中输入这一行。它会加载海龟模块，让你可以开始绘制星星。

  ```python
  import turtle as t
  ```

  加载海龟

### 编写一些指令

现在，在导入海龟的命令下方添加这段代码。它会创建变量，用于设置星星的大小和形状。它还会告诉海龟如何在窗口中移动以绘制星星。

```python
import turtle as t

size = 300
points = 5
angle = 144

for i in range(points):
    t.forward(size)
    t.right(angle)
```

这些是指示星星大小和形状的指令。

这是每个星角形成的角度，以度为单位。

这个 for 循环让海龟对星星的每个角重复相同的移动。

### 画一颗测试星星

从 IDLE 菜单中，选择 Run，然后选择 Run Module 来测试项目。海龟绘图窗口会出现（它可能在另一个窗口后面），你会看到海龟箭头开始绘制你的星星。

![](img/1bd24ab186f69fb18194b4174ca15178_92_0.png)

海龟箭头在窗口中移动，一边移动一边画线。

星星是一次画一条线绘制出来的。

![](img/1bd24ab186f69fb18194b4174ca15178_92_1.png)

别忘了保存你的工作。

### 添加角度计算器

如果能够绘制不同角数的星星，那就太好了。对代码做这个更改。它会计算海龟绘制具有任意所选角数的星星所需转动的角度。

```python
import turtle as t

size = 300
points = 5
angle = 180 - (180 / points)

for i in range(points):
    t.forward(size)
    t.right(angle)
```

角度取决于星星的角数。

## 6 给它上色！

你已经画出了一颗漂亮、整齐的星星，但它目前看起来相当单调。我们来添加一些颜色，让它更吸引人。按右侧所示更改代码，把你的星星涂成黄色。

```python
import turtle as t

size = 300
points = 5
angle = 180 - (180 / points)

t.color('yellow') # This sets the star's colour to yellow.
t.begin_fill()    # This fills the star with colour.
for i in range(points):
    t.forward(size)
    t.right(angle)

t.end_fill()
```

## 7 运行项目

海龟应该会画出一颗黄色星星。看看你能否通过编辑代码来改变星星的颜色。

![](img/1bd24ab186f69fb18194b4174ca15178_93_0.png)

## 8 画不同的星星

试着更改变量 points 中等号后面的数字，你会看到可以绘制不同的星星。请注意，这段代码只适用于角数为奇数的星星。偶数会把事情搞乱。

![](img/1bd24ab186f69fb18194b4174ca15178_93_1.png)

## 专家提示

### 有洞的星星

在某些计算机上，你的星星可能看起来略有不同，甚至中间有个洞。Python 海龟绘图的外观会因你使用的计算机类型而异，但这并不意味着你的代码有错。

![](img/1bd24ab186f69fb18194b4174ca15178_93_2.png)

![](img/1bd24ab186f69fb18194b4174ca15178_93_3.png)

别忘了保存你的工作。

## 星空

接下来的步骤会把你的星星封装成一个 Python 函数。然后你就可以使用该函数绘制布满星星的天空。

![](img/1bd24ab186f69fb18194b4174ca15178_94_0.png)

`draw_star()` 函数使用五个参数来定义星星的形状、大小、颜色和位置。

### 9. 创建星星函数

按此处所示编辑代码。它用新版本替换了几乎你现有的所有代码。这一大块代码将所有绘制星星的指令封装起来，并整齐地把它们组织成一个函数。现在，你可以在主代码中用一行 Python 代码 `draw_star()` 来绘制一颗星星。

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

x 和 y 坐标设置星星在屏幕上的位置。

这将背景颜色设置为深蓝色。

这条以井号（#）开头的“注释”行不是由 Python 运行的代码的一部分。它就像一个标签，帮助你理解程序。

这一行调用（运行）该函数。

海龟在窗口中心绘制一颗大小为 50 的黄色五角星。

### 10. 运行项目

海龟应该在蓝色背景上绘制一颗黄色星星。

![](img/1bd24ab186f69fb18194b4174ca15178_94_1.png)

### 注释

程序员经常在代码中写注释，以提醒自己程序不同部分的作用，或解释项目中棘手的地方。注释必须以 # 开头。Python 会忽略你在 # 之后同一行输入的任何内容，不会将其视为代码的一部分。在自己的项目中写注释（例如上面显示的 # Main code 这一行）在你离开一段时间后再回来看程序时非常有用。

## 添加随机数

现在，通过向代码中添加一些随机数来增加变化。在导入 `turtle` 的那一行下方输入这一行。它会从 Python 的 random 模块中引入 `randint()` 和 `random()` 函数。

```python
import turtle as t
from random import randint, random

def draw_star(points, size, col, x, y):
```

### 创建一个循环

对 #Main code 部分做这个更改。它添加一个 while 循环，不断随机化用于设置星星大小、形状、颜色和位置的参数。

`ranPts` 这一行将星星角数的范围限制为 5 到 11 之间的奇数。

这一行也变了。当它调用 `draw_star()` 函数时，现在会使用 while 循环中的随机变量。

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

### 再次运行项目

随着海龟绘制一颗又一颗颜色、形状和大小各异的星星，窗口应该会慢慢被填满。

![](img/1bd24ab186f69fb18194b4174ca15178_95_0.png)

海龟随机绘制星星。

### 记住——隐藏海龟

如果你不想看到海龟，请记住有一条命令可以让它隐形。把这行添加到程序中，你的星星就会神奇地出现，由一只看不见的海龟绘制！

```python
# Main code

t.hideturtle()
```

![](img/1bd24ab186f69fb18194b4174ca15178_95_1.png)

> 哇！

