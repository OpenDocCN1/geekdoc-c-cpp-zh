

```python
def start_ball(self, x_speed, y_speed):
    self.x_speed = -x_speed if random.randint(0,1) else x_speed
    self.y_speed = -y_speed if random.randint(0,1) else y_speed
    self.start_position()

def move_next(self):
    self.x_posn = self.x_posn + self.x_speed
    self.y_posn = self.y_posn + self.y_speed
    # if the ball hits the left wall:
    if(self.x_posn <= 3):
        self.x_posn = 3
        self.x_speed = -self.x_speed
    # if it hits right wall:
    if(self.x_posn >= (self.table.width - (self.width - 3))):
        self.x_posn = (self.table.width - (self.width - 3))
        self.x_speed = -self.x_speed
    # if the ball hits the top wall:
    if(self.y_posn <= 3):
        self.y_posn = 3
        self.y_speed = -self.y_speed
    # if it hits bottom wall:
    if(self.y_posn >= (self.table.height - (self.height - 3))):
        self.y_posn = (self.table.height - (self.height - 3))
        self.y_speed = -self.y_speed
    # finally move the circle:
    x1 = self.x_posn
    x2 = self.x_posn + self.width
    y1 = self.y_posn
    y2 = self.y_posn + self.height
    self.table.move_item(self.circle, x1, y1, x2, y2)

def stop_ball(self):
    self.x_speed = 0
    self.y_speed = 0
```

> 当我抄写代码时，我总是试着预测接下来会是什么。Ball 类中有相当多相似的方法，所以借助这一点，我成功猜对了不少。

![](img/c4403822ba1e00f0a2ce532b3f9d5054_57_0.png)

除了 `move_next()` 方法之外，这里没有什么是你应付不了的。本章末尾会完整解释 `move_next()` 方法。现在，别忘了保存你的工作，然后我们继续写代码。

## 通过改进球桌让球动起来

要让球动起来，我们需要给 `Table` 类添加几个工具，因为球必须在这里绘制。我们已经在 `table.py` 中写过一个 `Table` 类。本章的 `pong-ball-start` 文件夹中还有这个类的另一份副本。它包含之前的所有代码，并留有一块空白区域供你再添加一点内容。

**代码框 4.3** `table.py`

```python
# extra tool for adding an oval to the canvas
def draw_oval(self, oval):
    x1 = oval.x_posn
    x2 = oval.x_posn + oval.width
    y1 = oval.y_posn
    y2 = oval.y_posn + oval.height
    c = oval.colour
    return self.canvas.create_oval(x1, y1, x2, y2, fill=c)
```

这个方法首先接收一个椭圆作为参数。我们将把一个球实例传给它。为了提高可读性，我们根据球对象的属性来定义 tkinter 所需的参数。然后我们把球绘制到画布上。

## 另外三个 Table 方法

球桌还需要能够移动球和矩形、移除它们并改变它们的颜色。椭圆和矩形等几种对象在 tkinter 中使用相同的方法名，这让我们只需为球桌提供三个通用方法来操作其上的项目。将代码框 4.4 中的代码复制到你的 `table.py` 文件中，以完成 Table 类。

**代码框 4.4 — `table.py`**

```python
# extra tools for manipulating items on the canvas:
def move_item(self, item, x1, y1, x2, y2):
    self.canvas.coords(item, x1, y1, x2, y2)

def remove_item(self, item):
    self.canvas.delete(item)

def change_item_colour(self, item, c):
    self.canvas.itemconfigure(item, fill=c)
```

`move_item()` 方法是我们提供给球桌工厂的最有趣的新工具。它接收六个参数：

- **self** —— 对由这个类构建的当前球桌对象的引用。我们不提供它，因为它由 Python 自动提供（不过，它必须被声明）。
- **item** —— 我们将把一个引用传给它，指向画布上我们想要移动的项目。这对任何包含在边界框中的项目都有效。在本章中，我们传入代表球的圆。
- **x1, y1, x2, y2** —— 这些是边界框的坐标。x1 和 y1 是框左上角的坐标。x2 和 y2 是框右下角的坐标（图 4.3）。

> 当你想到新方法时，通过提供这些新方法来改进你的类绝对没有问题。这就像为工厂提供新机器，使其更加灵活。

![](img/c4403822ba1e00f0a2ce532b3f9d5054_61_0.png)

![](img/c4403822ba1e00f0a2ce532b3f9d5054_62_0.png)

## 调整 main.py

现在我们必须调整 `main.py`。这里是我们存储规则并运行球等对象的地方。同样，上次有一个起始文件，其中留有一些空白供你添加新代码。最终文件应该像代码框 4.5 中的那样。

**代码框 4.5** `main.py`

```python
from tkinter import *
import table, ball

# initialise global variables
x_velocity = 10
y_velocity = 10

# order a window from the tkinter window factory
window = Tk()
window.title("MyPong")

# order a table from the table factory
my_table = table.Table(window, net_colour="green", vertical_net=True)

# order a ball from the ball factory
my_ball = ball.Ball(table=my_table, x_speed=x_velocity, y_speed=y_velocity,
                    width=24, height=24, colour="red", x_start=288, y_start=188)

#### functions:
def game_flow():
    my_ball.move_next()
    window.after(50, game_flow)

# call the game_flow loop
game_flow()

# start the tkinter loop process
window.mainloop()
```

别忘了导入 ball

### 代码框 4.5 分析

确保把 `Ball` 加到导入行中——我们有一个新的工厂要使用。

在构造函数中，你从 Ball 类订购一个新球——它叫作 `my_ball`。

要把它变成一个游戏，我们需要添加几个函数。因为 `main.py` 不是类，所以它将使用函数而不是方法。首先，我们需要一个让球动起来的函数。`game_flow()` 在接下来两章中会变得更复杂，但现在它调用 `my_ball` 的 `move_next()` 方法，然后使用 `window.after()` 方法创建一个动画循环：

```python
window.after(50, game_flow)
```

第一个参数选择 50 毫秒的等待时间，第二个参数给出等待之后要调用的函数。`after()` 函数被设计为向 `mainloop()` 添加一个事件。在我们的代码中，`after()` 调用包含它的函数；因此，它实际上产生了一个**无限循环**，其中 `my_ball.move_next()` 函数每 50 毫秒被调用一次。

在 `main.py` 末尾调用 `mainloop()` 方法之前，我们还需要添加一行代码来让新函数开始运行：`game_flow()`。完成了！

## 深入探索

### 全局还是局部？

在函数或方法中创建的变量称为**局部变量**。这些变量存在于函数内部，但不能在程序的其他部分被调用或使用。它们甚至可以与其他函数或方法中的变量同名，尽管这不是一个好主意。**全局变量**通常在我们的代码开头声明。我们希望随时能访问它们的值。有时我们可能想在方法或函数内部使用全局变量。如果我们只想读取变量的值，那没问题。如果方法或函数需要改变全局变量的值，那么必须在函数内部重新声明它，并在前面加上关键字 `global`。

如果省略关键字 `global`，就会创建一个同名的新局部变量。如果我们完全不在函数内部声明它，那么当函数试图改变它的值时，就会得到“局部变量在赋值前被引用”的错误！换句话说，计算机不会把它识别为我们想要的全局变量，并告诉我们正在尝试访问一个不存在的局部变量。

### 测试与调试

现在我们可以测试 Ball 类了。首先确保你的三个文件都已保存。在 IDLE 中运行 `main.py` 文件。如果一切正常，你应该会看到一个带球网的球桌，以及一个会在墙上反弹的红色球！

如果有任何错误，试着解决它们，并特别注意错误发生在哪个文件中。有时涉及多个文件时会相当棘手，所以如果你已经尝试了几次仍毫无进展，请使用配套网站上的文件。这些文件可以在 Chapter 4 文件夹中的 `pong-ball-final` 文件夹里找到。仔细比较你的文件与可运行文件是一次很好的学习经历。你年轻时玩“找不同”的那些日子现在真的会有回报。注意到代码中悄悄混入了哪些错误是件好事，这样你以后就能尽量避免它们。

### move_next() 方法

前面说过我们会回来解释 `ball.py` 中的 `move_next()` 方法——好了，解释就在这里！

