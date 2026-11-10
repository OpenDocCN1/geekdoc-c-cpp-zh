
## 工作原理

本项目使用 Tkinter 来创建形状。Tkinter 的 mainloop() 函数会调度一个由你创建的函数，用来显示下一个形状。random 模块的 shuffle() 函数确保形状始终以不同的顺序出现。“q”和“p”键绑定（关联）到 snap() 函数，因此每当按下其中一个键时，它都会更新相应玩家的分数。

▷ Snap 流程图

只要还有待揭示的形状，程序就会一直运行。当玩家认为自己看到了一个 snap 时，它会响应玩家按下的键。当没有更多形状时，就会宣布获胜者并结束游戏。

### 专家提示

**休眠**

计算机的运行速度远比你快。有时这会造成问题。如果你让计算机向用户显示一个形状，然后紧接着又把它隐藏起来，中间没有停顿，计算机执行得太快，以至于人根本看不到这个形状。为了解决这个问题，Snap 使用了 time 模块的 sleep() 函数，它会让程序暂停指定的秒数：例如，time.sleep(1) 会让程序休眠 1 秒，然后再运行下一行代码。

![](img/1bd24ab186f69fb18194b4174ca15178_168_0.png)

## 开始使用

首先需要导入相关模块并创建图形用户界面（GUI）。然后需要创建一个画布来绘制形状。

![](img/1bd24ab186f69fb18194b4174ca15178_169_0.png)

- **1. 创建新文件**

打开 IDLE。创建一个新文件，并将其保存为“snap.py”。

- **2. 添加模块**

首先导入 random 和 time 模块，以及 Tkinter 的部分内容。time 模块让你可以创建延迟，以便玩家在显示下一个形状之前能够看到“SNAP!”或“WRONG!”消息。HIDDEN 让你可以隐藏每个形状，直到你想用 NORMAL 显示它——否则所有形状都会在游戏开始时出现在屏幕上。

你将使用 random 模块打乱形状。

```python
import random
import time
from tkinter import Tk, Canvas, HIDDEN, NORMAL
```

使用 Tkinter 创建 GUI。

- **3. 设置 GUI**

现在输入这里显示的代码，创建一个标题为“Snap”的 Tkinter 窗口（也称为根组件）。运行代码进行检查。该窗口可能被桌面上的其他窗口遮住。

```python
from tkinter import Tk, Canvas, HIDDEN, NORMAL

root = Tk()
root.title('Snap')
```

- **4. 创建画布**

输入这一行来创建画布——形状将出现在这块空白区域上。

```python
root.title('Snap')
c = Canvas(root, width=400, height=400)
```

## 制作形状

下一阶段是使用 Tkinter 的 Canvas 组件中的函数创建彩色形状。你将绘制圆形、正方形和矩形，每种形状都有四种不同颜色。

![](img/1bd24ab186f69fb18194b4174ca15178_169_1.png)

- **5. 为形状创建存储**

你需要创建一个列表，以便将所有形状存储在某个地方。在文件底部添加这一行。

```python
c = Canvas(root, width=400, height=400)
shapes = []
```

### 6 创建圆形

要绘制圆形，请使用 Canvas 组件的 create_oval() 函数。在 shapes 列表下方输入以下代码。它会创建四个大小相同的圆形——分别为黑色、红色、绿色和蓝色——并将它们添加到 shapes 列表中。

将状态设置为 HIDDEN，这样程序启动时该形状不会出现在屏幕上。
它必须等待轮到自己。

这些是 (x0, y0) 坐标（见方框）。

这些是 (x1, y1) 坐标（见方框）。

![](img/1bd24ab186f69fb18194b4174ca15178_170_0.png)

别忘了保存你的工作。

```python
    shapes = []

    circle = c.create_oval(35, 20, 365, 350, outline='black', fill='black', state=HIDDEN)
    shapes.append(circle)
    circle = c.create_oval(35, 20, 365, 350, outline='red', fill='red', state=HIDDEN)
    shapes.append(circle)
    circle = c.create_oval(35, 20, 365, 350, outline='green', fill='green', state=HIDDEN)
    shapes.append(circle)
    circle = c.create_oval(35, 20, 365, 350, outline='blue', fill='blue', state=HIDDEN)
    shapes.append(circle)
    c.pack()
```

这一行将形状放到画布上。没有它，所有形状都不会显示。

圆形的颜色由 outline 和 fill 决定。

### 专家提示

**创建椭圆形**

create_oval() 函数绘制的椭圆形就像位于一个不可见的方框内。括号内的四个数字决定圆形在屏幕上的位置。它们是方框两个对角的坐标。两组数字之间的差值越大，圆形就越大。

![](img/1bd24ab186f69fb18194b4174ca15178_170_1.png)

第一组数字 (x0, y0) 表示方框左上角的位置。

(x0, y0)

(x1, y1) 表示右下角的位置。

(x1, y1)

### 7 显示圆形

试着运行程序。你看到任何形状了吗？记住，你把它们的状态设置成了 HIDDEN。将一个形状的状态改为 NORMAL，然后再次运行代码。现在你应该能在屏幕上看到那个形状了。注意不要将多个形状设置为 NORMAL。如果这样做，它们会同时显示，一个叠一个地绘制出来。

![](img/1bd24ab186f69fb18194b4174ca15178_170_2.png)

> 我试过吹泡泡，但我吹出来的是圆圈！

### 8 添加一些矩形

现在使用 Canvas 的 `create_rectangle()` 函数创建四个不同颜色的矩形。将此代码块插入到绘制圆形的代码和 `c.pack()` 之间。为了避免全部手动输入，只需输入前两行，然后复制并粘贴三次，再更改颜色。

```python
shapes.append(circle)

rectangle = c.create_rectangle(35, 100, 365, 270, outline='black', fill='black', state=HIDDEN)
shapes.append(rectangle)
rectangle = c.create_rectangle(35, 100, 365, 270, outline='red', fill='red', state=HIDDEN)
shapes.append(rectangle)
rectangle = c.create_rectangle(35, 100, 365, 270, outline='green', fill='green', state=HIDDEN)
shapes.append(rectangle)
rectangle = c.create_rectangle(35, 100, 365, 270, outline='blue', fill='blue', state=HIDDEN)
shapes.append(rectangle)
c.pack()
```

![](img/1bd24ab186f69fb18194b4174ca15178_171_0.png)

### 9 添加一些正方形

接下来绘制正方形。你可以使用创建矩形时用过的同一个函数，但这次要让所有边长相等，从而把矩形变成正方形。将此代码块插入到矩形代码和 `c.pack()` 之间。

![](img/1bd24ab186f69fb18194b4174ca15178_171_1.png)

```python
shapes.append(rectangle)

square = c.create_rectangle(35, 20, 365, 350, outline='black', fill='black', state=HIDDEN)
shapes.append(square)
square = c.create_rectangle(35, 20, 365, 350, outline='red', fill='red', state=HIDDEN)
shapes.append(square)
square = c.create_rectangle(35, 20, 365, 350, outline='green', fill='green', state=HIDDEN)
shapes.append(square)
square = c.create_rectangle(35, 20, 365, 350, outline='blue', fill='blue', state=HIDDEN)
shapes.append(square)
c.pack()
```

### 10 打乱形状

为了确保形状每次不会以相同的顺序出现，你需要打乱它们——就像打乱一副牌一样。random 中的 shuffle() 函数可以为你完成这件事。在 c.pack() 之后插入这一行。

```python
random.shuffle(shapes)
```

## 做好准备

在构建的下一部分中，你将设置几个变量，并编写一些让游戏准备好运行的代码。不过，在我们添加最后阶段的函数之前，它还不能工作。

### 专家提示

**其实无关紧要**

程序员经常需要设置起始值为零的变量，比如本游戏中的分数。但如果变量保存的是字符串而不是数字，该怎么办呢？答案是使用一对中间没有任何内容的引号。然而，有些变量并没有像 0 或空字符串这样明显的默认值。在这种情况下，你可以使用“None”这个词，如下所示。

![](img/1bd24ab186f69fb18194b4174ca15178_172_0.png)

### 11 设置变量

你需要一些变量来跟踪程序运行期间的各种信息，包括当前形状、上一个和当前颜色，以及两个玩家的分数。

两名玩家在开始时都没有分数，因此两者的值都设置为 0。

```python
random.shuffle(shapes)

shape = None
previous_color = ''
current_color = ''
player1_score = 0
player2_score = 0
```

shape 变量还没有值。

颜色变量保存的是空字符串。

### 12 添加延迟

现在添加一行代码，在第一个形状出现之前创建 3 秒延迟。这给玩家时间找到 Tkinter 窗口，以防它被桌面上的其他窗口遮住。你将在后面的步骤 16 和 17 中创建 next_shape() 函数。

```python
player2_score = 0

root.after(3000, next_shape)
```

程序会等待 3,000 毫秒（即 3 秒），然后显示下一个形状。

