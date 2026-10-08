
```python
run=1
while(run):
    try:
        os.system('cls')
    except:
        os.system('clear')
    print('--- 文件管理器 ---')
    print('1. 读取文件')
    print('2. 写入文件')
    print('3. 追加文件')
    print('4. 删除文件')
    print('5. 列出目录文件')
    print('6. 检查文件是否存在')
    print('7. 移动文件')
    print('8. 复制文件')
    print('9. 创建目录')
    print('10. 删除目录')
    print('11. 打开程序')
    print('12. 退出')
    dec=input('请选择选项: ')
    if dec=='1':
        Read()
    if dec=='2':
        Write()
    if dec=='3':
        Add()
    if dec=='4':
        Delete()
    if dec=='5':
        Listdir()
    if dec=='6':
        Check()
    if dec=='7':
        Move()
    if dec=='8':
        Copy()
    if dec=='9':
        Makedir()
    if dec=='10':
        Remdir()
    if dec=='11':
        Openfile()
    if dec=='12':
        exit()
    run-let=input("1.返回菜单 2.退出 \n")
    if run-let=='2':
        exit()
```

## 代码改进

由于这是一个用于特定场景的简单脚本，有大量的空间对其进行修改并使其更有趣。也许你可以包含一个添加评分的选项，奖励玩家在第一次尝试时就击中角的“一杆进洞”。

此外，数字猜数字代码为以不同的方式实现你的代码提供了空间。我们的意思是，这段代码可以用于从一个范围内获取随机数，这反过来可以作为冒险游戏中创建角色函数的开头。

想象一个用 Python 编写的文本冒险游戏开头，其中玩家的名字会发生。下一步是运行随机骰子来决定每个角色的战斗属性，然后这些属性可以作为一组变量带入，并根据玩家遇到的情况进行减少或增加。

例如，如截图所示，你可以使用类似的代码：

玩家随后可以决定保留掷骰结果，或者再次尝试以期获得更好的数值。总有方法将这段代码实现到基础冒险游戏中。

![](img/ba40fbc39febe9db9a35785516d323a7_152_0.png)

![](img/ba40fbc39febe9db9a35785516d323a7_152_1.png)

![](img/ba40fbc39febe9db9a35785516d323a7_152_2.png)

![](img/ba40fbc39febe9db9a35785516d323a7_152_3.png)

## 多边形圆

这是一个有趣的数学方法，即用直线绘制圆形。通过使用 `Math` 模块（特别是 `sin` 和 `Pi`），这将使用 `Turtle` 模块绘制一系列直线。最终结果非常显著，并且有很多探索空间。

### POLYGONCIRCLES.PY

这里使用了大量的数学知识，以及对 `Turtle` 模块复杂的操控。输入代码并执行它查看结果。

```
from turtle import*
from math import sin, cos, pi
inc=2*pi/100
t=0
for i in range(100):
x1=sin(t);y1=cos(t)
x2=sin(t+inc);y2=cos(t+inc)
penup();goto(x1,y1)
pend();goto(x2,y2)
t+=inc
```

## 图形增强

有几种方法可以改进这段代码使其更有趣。你可以更改颜色，也许为每一行都使用不同的颜色，并让 Turtle 在圆周上绘图。让你的想象力飞驰并完成它。

Turtle 的图形映射和绘制需要一段时间时间，取决于其的大小和复杂程度。虽然效果可能震撼，但受到显示图像时间的限制。因此值得看看 `turtle.speed()` 函数是否能加速。

例如：

```
for i in range(100):
x1=sin(t);y1=cos(t)
x2=sin(t+inc);y2=cos(t+inc)
speed('fastest')
up();goto(x1,y1)
pend();goto(x2,y2)
t+=inc
```

这将以 Turtle 可可能的“`fastest`”速度运行。这产生了巨大的差异，如果你在为游戏或演示文稿绘制 Turtle 图像，这值得考虑。

`turtle.speed()` 的取值有：

- slowest
- slow
- normal
- fast
- fastest

你可以通过在循环中、`penup` 行之前添加该函数来实验不同的速度。

```
from turtle import *
from math import sin, cos, pi
inc=2*pi/100
t=0
for i in range(100):
x1=sin(t);y1=cos(t)
x2=sin(t+inc);y2=cos(t+inc)
speed('fastest')
up();goto(x1,y1)
pend();goto(x2,y2)
t+=inc
```

![](img/ba40fbc39febe9db9a35785516d323a7_153_0.png)

![](img/ba40fbc39febe9db9a35785516d323a7_153_1.png)

## 随机数生成器

用户输入和处理输入的能力是任何编程语言中的重要元素。这是区分优秀程序与卓越程序的区别，它允许用户进行交互并看到交互的结果。

### RNDNMUMGEN.PY

它可能很简单，但这段代码会向用户询问两组数字，起始值和结束值。代码将在两组数字之间抽取一个随机数并显示。

```
from random import *

print(">>>>Random Number Generator<<<<<<")
nb1=int(input("Enter the start number: "))
nb2=int(input("Enter the last number: "))

x = randint(nb1, nb2)
print(f"The random number between {nb1} and {nb2} is: {x}")
print(x)
```

## 更多输入

虽然易于理解，但如果你提示用户输入，它可能会更有趣。你可以为这些数字提供加法、减法、乘法。如果你觉得自己很聪明，可以将代码传递到第 128 页提供的 Ticker 窗口。

此外，上面的代码可以用于文本冒险游戏，其中角色进行战斗，其血量相应被随机数减少。这可以与之前第 90 页的猜数字游戏混合，在游戏中我们定义冒险角色的属性。

你还可以将 `Turtle` 模块包含在代码中，并为绘制形状定义一些规则，或者根据数字范围内的用户输入值。这需要一些计算，但效果完全有趣。

例如，可以将代码修改为：

```
from random import *
import turtle

print(">>>>Random Turtle Image<<<<<<")
nb1=int(input("Enter the start number: "))
nb2=int(input("Enter the second number: "))
nb3=int(input("Enter the third number: "))
nb4=int(input("Enter the fourth number: "))

```

turtle.forward(nb1)

turtle.left(90)

turtle.forward(nb2)

turtle.left(90)

turtle.forward(nb3)

turtle.left(90)

turtle.forward(nb4)

turtle.left(90)

```

![](img/ba40fbc39febe9db9a35785516d323a7_154_0.png)

# 键盘绘图脚本

`Turtle` 模块是 Python 程序员的一个极佳资源。然而，让它变得如此有趣的之处在于，它能够让用户控制屏幕上的乌龟。这段代码正是实现了这一功能，允许用户释放内心的艺术细胞。

# KEYBOARDRAW.PY

此脚本包含两个模块：`Turtle` 和 `Tkinter`。绘图部分由 turtle 模块显示用户控制界面。

```
所有移动和旋转均为以 5 为单位增增。

右箭头键 = 前移动

左箭头键 = 向后移动

turn = 向右

turn = 向左

pen = 抬笔

pen = 落下

go = 回主页

clear = 清除
```

```python
from tkinter import *

root = tk.root("Controls",height=80, width=600)

troot.insert("Right arrow key = move forward left arrow key

root.bind("<Right", lambda: forward(5), "Right")

root.bind("<Left", lambda: backward(5), "Left")

root.bind("<Up", lambda: turn(left), "Up")

root.bind("<Down", lambda: turn(right), "Down")

root.bind("u", lambda: pen_up())

root.bind("d", lambda: pen_down())

from turtle import *
```

```python
def main():
    width(2)
    speed(0)
    pencolor("blue")
    keyup("u")
    keydown("d")
    keyclear("c")
    home("h")
    keyward(lambda: forward(5), "Right")
    keyward(lambda: backward(5), "Left")
    keyward(lambda: right(5), "r")
    listen()
    return "Done!"

if __name__ == "__main__":
    main()
```

![](img/ba40fbc39febe9db9a35785516d323a7_156_0.png)

仅仅通过这些代码，总有改进空间。在这里，你可以更改颜色，或者询问用户想要用什么颜色开始画画，然后在控制栏中包含一个按键来增加或减少画笔的速度。你还可以大幅扩展控制功能，包含更多细节和选项。

![](img/ba40fbc39febe9db9a35785516d323a7_156_1.png)

![](img/ba40fbc39febe9db9a35785516d323a7_156_2.png)

一组初始注释描述了控制功能，可以使用 tkinter 和 turtle 实现一个独立的窗口。

设置显示控制项的 tkinter 窗口，并创建一个函数来定义绘制线条的宽度、速度和颜色；同时设置用于画笔控制的 onkey 函数。

一种结束代码和循环的简洁方法，让你可以继续画笔绘图。

![](img/ba40fbc39febe9db9a35785516d323a7_156_3.png)

# Pygame 文字示例

使用 Pygame 模块可以做很多与图形无关的内容。该模块包含许多处理文本的函数，例如翻转、侧向显示、倒置甚至带有动画的旋转。

在这里，我们介绍了在 Pygame 模块中显示文本的示例。每个示例在代码中都易于识别，所以你可以将其提取并用到你的项目中。

```python
import pygame
pygame.init()
```

| | |
|---|---|
| BLACK | (0, 0, 0) |
| WHITE | (255, 255, 255) |
| BLUE | (0, 0, 255) |
| GREEN | (0, 255, 0) |
| RED | (255, 0, 0) |

| | |
|---|---|
| size = (400, 50) |
| screen = pygame.display.set_mode(size) |

| | |
|---|---|
| done = False |
| clock = pygame.time.Clock() |

| | |
|---|---|
| rotate = 0 |
| while not done: |

| | |
|---|---|
| for event in pygame.event.get(): |
| if event.type == pygame.QUIT: |
| done = True |

| | |
|---|---|
| screen.fill(WHITE) |
| pygame.draw.line(screen, BLACK, [100, 50], [200, 50], 2) |
| pygame.draw.line(screen, BLACK, [100, 50], [100, 150], 2) |

# Google 脚本

使用 OS 和 Urllib 模块，这段短代码将为用户显示窗口，然后在浏览器中传递输入内容。这是一个非常实用的脚本，很容易引入到自己的代码中。

## GOOGLESEARCH.PY

你需要安装 urllib 模块，除非它已经安装。它还使用了基于 Linux (GNOME) 的工具创建对话框。

```python
import os
import urllib.parse
google = os.popen('zenith --text="Enter your search" --title="Google Search").read(1)
google = urllib.parse.quote(google)
os.system('chromium-browser http://www.google.com/search?q=' + (google))
```

## 搜索更多

我们使用了 Zenith 命令来创建对话框，它在 Linux 机器（如 Ubuntu, Raspberry Pi 和 Linux Mint）上可用。如果你想在 Windows 上执行它，可能会找到 Windows 版本的 Zenith，并通过它传递用户的查询。你可以看到这段特定的代码使用了 Raspberry Pi 上预装的 Chrome 浏览器。你需要将行中的命令更改为你正在使用的浏览器，以便在 Windows 中启动它，例如：

```python
os.system('start firefox http://www.google.com/search?q=' + (google))
```

```python
os.system('start chrome http://www.google.com/search?q=' + (google))
```

```python
os.system('start ie http://www.google.com/search?q=' + (google))
```

最后一个用于 Chrome 和 Internet Explorer 的 Windows 版本 Zenith。你需要在系统文件夹中安装它，不需要管理员权限即可运行。当你安装了 Zenith，可以修改这段 Python 代码的 Windows 版本：

```python
import os
import urllib.parse
google = os.popen('start C:\Temp\zenith --entry="Enter your search query" --title="Google Search").read(1)
google = urllib.parse.quote(google)
os.system('start firefox http://www.google.com/search?q=' + (google))
```

![](img/ba40fbc39febe9db9a35785516d323a7_158_0.png)

# 文本冒险脚本

文本冒险是建立 Python 技能同时增加乐趣的极佳方法。这个示例创建了一个经典的文本冒险；最后由你决定。

## ADVENTURE.PY

冒险游戏最初使用 Time 模块在 print 函数之间创建停顿。有一个帮助系统可以扩展，以及故事本身。
