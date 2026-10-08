

# 修改内容

一旦在画布上绘制了图形，它就不再需要保持不变。可以使用代码来改变它的外观，或者让它在屏幕上移动。

> 另见
> 158–159 绘制形状
> 响应事件 162–163 >

# 移动形状

要让形状在画布上移动，你需要告诉电脑要移动哪一个（你给形状命的名称或 ID）以及将其移动到哪里。

> 记住
> 有意义的名称
> 使用通的名称来识别画布上的形状是一个好主意。这些页面使用了“eyeball”（眼球）和“mouth”（嘴巴）等名称，以便代码易于阅读和理解。

![](img/72d218a7a73c4d4abc7be582ebd85385_161_0.png)

眼球
向左转，然后
返回
形状的名称，
或 ID

```
>>> c.move(eyeball, -10, 0)
>>> c.move(eyeball, 10, 0)
```

移动眼球
将此代码输入到 shell 窗口中，让眼球
向左转，然后再转回来。

此函数
移动形状
设置移动的
坐标

# 修改颜色

你可以通过简单改变椭圆的颜色，让嘴巴看起来像是在张开和闭合。

![](img/72d218a7a73c4d4abc7be582ebd85385_161_1.png)

嘴巴打开
嘴巴关闭

- 编写代码
输入此代码创建两个函数，让嘴巴看起来在张开和闭合。

函数
"itemconfig() 改变
你已经绘制的
形状的属性

张开的
嘴
将会是黑色的

- 打开和关闭
将此代码输入到 shell 窗口，让嘴巴张开和闭合。

```python
def mouth_open():
    c.itemconfig(mouth, fill='black')
def mouth_close():
    c.itemconfig(mouth, fill='red')
```

形状的 ID
闭合的
嘴
将会是红色的

```
>>> mouth_open()
>>> mouth_close()
```

使用这些命令
让外星人张开并关闭嘴巴

# 隐藏和显示

可以使用 "itemconfig()" 函数隐藏形状。如果你隐藏了眼球，稍过一会儿再次显示它，外星人看起来就像在眨眼。

眨眼的外星人
要让外星人眨眼，你需要隐藏瞳孔并让外星人的白色部分变成绿色。

![](img/72d218a7a73c4d4abc7be582ebd85385_162_0.png)

- 创建眨眼函数
此代码创建了两个函数，让你外外星人眨眼。

眨眼和睁眼
将此代码输入 shell 窗口让外星人眨眼。

将外星人的白色变为绿色

```python
def blink():
  itemconfig(eye, fill='green')
  itemconfig(eyeball, state=HIDDEN)
def unblink():
  再次变为白色
  itemconfig(eye, fill='white')
  itemconfig(eyeball, state=NORMAL)
```

```
>>> blink()
>>> unblink()
```

形状的 ID

"unblink()" 命令让眼睛再次睁开

隐藏瞳孔

显示瞳孔

# 说话

文本也可以显示在屏幕上，让外星人说话。你甚至可以让它响应用户的命令说不同的内容。

> 我是一个外星人！

- 添加文本
此代码在外星人的图形上添加文本，并创建一个函数来偷走它的帽子。

在画布上
定位文本

将你想让
外星人说的话
放在引号中

```python
words = c.create_text(200, 280, text='I am an alien!')
def steal_hat():
  itemconfig(hat, state=HIDDEN)
  itemconfig(words, text='Give my hat back!')
```

隐藏
帽子

帽子一消失，外星人
就会向它要

当帽子消失时
会出现一条新消息

- 偷帽子
将此代码输入 shell 窗口，看看会发生什么。

输入此代码
来偷帽子

```
>>> steal_hat()
```

把我的帽子还给我！

# 响应事件

当按下键或移动鼠标时，电脑会接收到一个信号。这被称为“事件”。程序可以指示电脑响应它检测到的任何事件。

- 另见
* 158–159 绘制形状
* 160–161 修改内容

# 事件名称

使用鼠标或键盘等输入设备可以触发许多不同的事件。Tkinter 有相应的名称来描述这些每一个事件。

![](img/72d218a7a73c4d4abc7be582ebd85385_163_0.png)

# 鼠标事件

# 键盘事件

![](img/72d218a7a73c4d4abc7be582ebd85385_163_1.png)

要让程序响应鼠标事件，只需将函数绑定（bind）到事件。在这里，创建了函数“burp”（打嗝），然后将其绑定到“Button-1”事件。

这会将 Tkinter 窗口带到屏幕前方

![](img/72d218a773c4d4abc7be582ebd85385_163_2.png)

```python
window.attributes('-topmost', 1)
def burp(event):
    mouth_open()
    c.itemconfig(words, text='Burp!')
c.bind_all('<Button-1>', burp)
```

# 键事件

同样，也可以将函数绑定到键盘上的按键。输入下面的代码，让外星人在按下 "A" 和 "Z" 键键时眨眼。

```python
def blink2(event):
  c.itemconfig(eye, fill='green')
  c.itemconfig(eyeball, state=HIDDEN)
def unblink2(event):
  c.itemconfig(eye, fill='white')
  c.itemconfig(eyeball, state=NORMAL)
c.bind_all('<KeyPress-a>', blink2)
c.bind_all('<KeyPress-z>', unblink2)
```

![](img/72d218a7a73c4d4abc7be582ebd85385_164_0.png)

按键移动

按键也可以触发移动。此代码将按键绑定到移动眼球的函数。

```python
def eye_control(event):
  key = event.keysym
  if key == "Up":
    c.move(eyeball,0,-1)
  elif key == "Down":
    c.move(eyeball,0,1)
  elif key == "Left":
    c.move(eyeball,-1,0)
  elif key == "Right":
    c.move(eyeball,1,0)
window.bind('<Key>', eye_control)
```

**让外星人眨眼**
运行此代码时，“A" 键会让眼睛闭上，“Z" 键会让它再次睁开。

# 项目 7 泡泡发射

该项目使用了本章节的所有技能。这是一个大项目，请分阶段进行。

## 游戏目标

在编写任何代码之前，考虑游戏的整体规划以及它是如何运行的。这里是规则：
- 玩家控制潜艇
- 破泡得分
- 开始时设置计时器为 30 秒
- 获得 1000 分获得额外奖励
- 时间结束时游戏结束

![](img/72d218a7a73c4d4abc7be582ebd85385_165_0.png)

# 创建游戏窗口和潜艇

首先设置场景。在 IDLE 中打开新窗口。输入以下代码创建游戏窗口以及玩家控制的潜艇。

IDLE 文件 编辑 运行
泡泡发射

![](img/72d218a7a73c4d4abc7be582ebd85385_166_0.png)

使用 Tkinter 库构建用户界面 (GUI)。此代码将创建游戏窗口。

```python
from tkinter import * # 导入所有的
Tkinter 函数
HEIGHT = 500 # 设置窗口的
WIDTH = 800 # 大
window = Tk() # 给游戏
一个标题
window.title('Bubble Blaster') # 设置深蓝色为
背景（的）
c = Canvas(window, width=WIDTH, height=HEIGHT, bg='darkblue')
c.pack()
```

图形将代表游戏中的潜艇。可以使用 Tkinter 的绘制函数制作。输入这段代码，然后运行它。

潜艇将由一个内部的三角形表示

```python
ship_id = c.create_polygon(5, 5, 5, 25, 30, 15, fill='red')
ship_id2 = c.create_oval(0, 0, 30, 30, outline='red')
SHIP_R = 15 # 潜艇的半径
MID_X = WIDTH / 2 # 变量 "MID_X 和
"MID_Y" 给出了屏幕中间的坐标
MID_Y = HEIGHT / 2
c.move(ship_id, MID_X, MID_Y) # 将潜艇的两个部分
移动到屏幕中心
c.move(ship_id2, MID_X, MID_Y)
```

