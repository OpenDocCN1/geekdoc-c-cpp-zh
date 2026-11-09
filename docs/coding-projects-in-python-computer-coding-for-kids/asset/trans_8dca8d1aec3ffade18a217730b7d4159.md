
## 给海龟盖章！

使用 Turtle 模块的 `stamp()` 函数，把海龟的图片添加到每条线的开头，从而将彩虹的各条线“铆接”在一起。（你也可以用海龟绘制一条完全由盖章海龟组成的线，并用它代替 `t.forward` 和 `t.backward`。）把这些新代码行添加到 `move_turtle()` 函数中，放在画笔命令之后，就可以开始铆接了！

![](img/6b18a113f7aa9338e32f3ac1fa217987_107_0.png)

海龟印章看起来就像把各条线固定在一起的铆钉。

```python
def move_turtle():
    t.fillcolor(random.choice(pen_colors))
    t.shapesize(3,3,1)
    t.stamp()
```

- 输入这行代码，在屏幕上盖上一个海龟图案。
- 这会让海龟比平常大三倍。
- 这些代码把海龟的颜色设为随机颜色。

## 大转弯还是小转弯？

你可以添加一个提示，让用户决定海龟转弯的角度。转弯可以是大角度、直角或小角度。按照以下步骤操作，看看这会如何改变图案。

### 创建一个函数

创建一个让用户选择转弯大小的函数。把它添加到你已在主项目第 3 步中添加的 `get_turn_size()` 函数中。

![](img/6b18a113f7aa9338e32f3ac1fa217987_107_1.png)

```python
def get_turn_size():
    turn_size = input('Enter turn size (wide, square, narrow): ')
    return turn_size
```

### 2. 不同的移动方式

用这里显示的新版本替换 `move_turtle()` 函数。它会在你使用该函数时，把 `turn_size` 添加到传给函数的参数中。它还会把 `angle = random.randint(0, 180)` 这一行替换为根据 `turn_size` 的值选择不同转弯角度的代码。

```python
def move_turtle(line_length, turn_size):
    pen_colors = ['red', 'orange', 'yellow', 'green', \
                  'blue', 'purple']
    t.pencolor(random.choice(pen_colors))
    if inside_window():
        if turn_size == 'wide':
            angle = random.randint(120, 150)
        elif turn_size == 'square':
            angle = random.randint(80, 90)
        else:
            angle = random.randint(20, 40)
        t.right(angle)
        t.forward(line_length)
    else:
        t.backward(line_length)
```

- 直角转弯在 80 到 90 度之间。
- 小角度转弯在 20 到 40 度之间。
- 大角度转弯在 120 到 150 度之间。

### 3. 用户输入

接下来，在程序主体部分添加一行代码，使用 `get_turn_size()` 函数获取玩家选择的转弯大小。

```python
line_length = get_line_length()
line_width = get_line_width()
turn_size = get_turn_size()
```

### 4. 主程序

最后，修改使用 `move_turtle()` 函数的那一行，加入 `turn_size`。

```python
while True:
    move_turtle(line_length, turn_size)
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_108_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_108_1.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_108_2.png)

- 短、粗、小角度
- 中等、超粗、直角
- 长、细、大角度

## 4. 倒计时日历

当你期待某个激动人心的活动时，知道还要等多久会很有帮助。在这个项目中，你将使用 Python 的 Tkinter 模块构建一个方便的程序，为那个重要日子倒计时。

![](img/6b18a113f7aa9338e32f3ac1fa217987_111_0.png)

> 好耶！距离我的生日还有 0 天！

### 会发生什么

运行程序时，它会显示未来事件列表，并告诉你距离每个事件还有多少天。第二天再次运行，你会看到它已从每个“距离……还有”数字中减去一天。把即将到来的冒险日期填进去，你就再也不会错过重要日子——或作业截止日期了！

给你的日历起一个个性化的标题。

```text
My Countdown Calendar

It is 20 days until Halloween
It is 51 days until Spanish Test
It is 132 days until School Trip
It is 92 days until My Birthday
```

运行程序时会弹出一个小窗口，每个事件占一行。

### 工作原理

程序通过从文本文件读取信息来获知重要事件——这称为“文件输入”。文本文件包含每个事件的名称和日期。代码使用 Python 的 `datetime` 模块计算从今天到每个事件的天数。它把结果显示在由 Python 的 `Tkinter` 模块创建的窗口中。

### ▽ 倒计时日历流程图

在这个项目中，重要事件列表作为文本文件与代码分开创建。程序首先从该文件读取所有事件的列表。一旦所有天数都计算并显示完毕，程序就会结束。

### ▷ 使用 Tkinter

`Tkinter` 模块是 Python 程序员用来显示图形和获取用户输入的一组工具。`Tkinter` 可以把结果显示在一个单独的窗口中，而不是在 shell 中显示输出；你可以自行设计和设置该窗口的样式。

![](img/6b18a113f7aa9338e32f3ac1fa217987_112_0.png)

### 图形用户界面

Tkinter 非常适合创建程序员所说的 GUI（发音为“gooey”）。GUI（图形用户界面）是程序中人们与之交互的可见部分，例如你在智能手机上使用的图标和菜单系统。Tkinter 可以创建弹出窗口，你可以向其中添加按钮、滑块和菜单。

![](img/6b18a113f7aa9338e32f3ac1fa217987_112_1.png)

智能手机的 GUI 使用图标来显示 WiFi 信号的强弱以及电池电量的多少。

```text
Start

Get today's date

Get the lists of important events from the text file

Get an event

Calculate the number of days until the event

Display the result

Calculated all events?

N

Y

End
```

### 创建并读取文本文件

倒计时日历的所有信息都必须存储在文本文件中。你可以使用 IDLE 创建它。

### 1. 创建一个新文件

打开一个新的 IDLE 文件，然后输入几个对你来说重要的即将发生的事件。每个事件占一行，并在事件和日期之间输入逗号。确保逗号和事件日期之间没有空格。

![](img/6b18a113f7aa9338e32f3ac1fa217987_113_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_113_1.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_113_2.png)

events.txt

```text
Halloween,31/10/17
Spanish Test,01/12/17
School Trip,20/02/18
My Birthday,11/01/18
```

事件名称在前。

日期按日/月/年的格式输入。

### 2. 将其保存为文本文件

接下来，将文件保存为文本文件。单击“文件”菜单，选择“另存为”，并将文件命名为“events.txt”。现在你可以开始编写 Python 程序了。

![](img/6b18a113f7aa9338e32f3ac1fa217987_113_3.png)

- 关闭
- 保存
- 另存为...
- 保存副本为...

### 3. 打开一个新的 Python 文件

现在你需要为代码创建一个新文件。将其保存为“countdown_calendar.py”，并确保它与你的“events.txt”文件位于同一文件夹中。

![](img/6b18a113f7aa9338e32f3ac1fa217987_113_4.png)

### 4. 设置模块

这个项目需要两个模块：Tkinter 和 datetime。Tkinter 将用于构建简单的 GUI，而 datetime 可以让你轻松进行日期计算。在新程序顶部输入以下两行来导入它们：

```python
from tkinter import Tk, Canvas
from datetime import date, datetime
```

导入 Tkinter 和 datetime 模块。

### 5. 创建画布

现在设置用于显示重要事件以及距离每个事件还有多少天的窗口。把这段代码放在你在第 4 步添加的代码行下面。它会创建一个包含“画布”的窗口——画布是一个空白矩形，你可以向其中添加文本和图形。

```python
root = Tk()
c = Canvas(root, width=800, height=800, bg='black')
c.pack()
c.create_text(100, 50, anchor='w', fill='orange', \
font='Arial 28 bold underline', text='My Countdown Calendar')
```

- 此命令将画布打包到 Tkinter 窗口中。
- 创建一个 Tkinter 窗口。
- 创建一个名为 c 的画布，宽 800 像素、高 800 像素。
- 这一行向画布添加文本。文本从 x = 100、y = 50 处开始。起始坐标位于文本的左侧（西侧）。

### BINGO：画布

在 Tkinter 中，画布是一个区域，通常是矩形，你可以在其中放置不同的形状、图形、文本或图像，供用户查看或交互。可以把它想象成艺术家的画布——只不过你是用代码而不是画笔来创作！

### 6. 运行代码

现在试着运行代码。你会看到一个窗口出现，上面显示程序标题。如果运行不成功，记得阅读所有错误信息，并仔细检查代码以找出可能的错误。

![](img/6b18a113f7aa9338e32f3ac1fa217987_114_0.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_114_1.png)

你可以通过修改代码中的 `c.create_text()` 这一行来更改颜色。

### 7. 读取文本文件

接下来创建一个函数，用于读取并存储文本文件中的所有事件。在代码顶部、导入模块之后，创建一个名为 `get_events` 的新函数。函数内部有一个空列表，用于在文件读取后存储事件。

```python
from datetime import date, datetime

def get_events():
    list_events = []
root = Tk()
```

创建一个名为 `list_events` 的空列表。
