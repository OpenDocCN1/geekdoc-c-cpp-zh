
## 18 是抢拍吗？

要完成游戏，创建最后一个函数：`snap()`。这个函数将检查哪个玩家按下了自己的按键，以及这次抢拍是否有效（正确）。然后它会更新分数并显示一条消息。在 `next_shape()` 函数下方添加这段代码。

![](img/6b18a113f7aa9338e32f3ac1fa217987_177_0.png)

别忘了保存你的工作。

```python
def snap(event):
    global shape
    global player1_score
    global player2_score
    valid = False

    c.delete(shape)

    if previous_color == current_color:
        valid = True

        if valid:
            if event.char == 'q':
                player1_score = player1_score + 1
            else:
                player2_score = player2_score + 1
            shape = c.create_text(200, 200, text='SNAP! You score 1 point!')
        else:
            if event.char == 'q':
                player1_score = player1_score - 1
            else:
                player2_score = player2_score - 1
            shape = c.create_text(200, 200, text='WRONG! You lose 1 point!')
    c.pack()
    root.update_idletasks()
    time.sleep(1)
```

将这些变量标记为全局变量，以便函数可以修改它们。

检查这次抢拍是否有效（即前一个形状的颜色是否与当前形状的颜色匹配）。

如果抢拍有效，检查是哪个玩家抢拍的，并给其分数加 1。

这一行在玩家有效抢拍时显示一条消息。

否则（else），从抢拍的玩家分数中减去一分。

这一行在玩家抢拍时机错误时显示一条消息。

这一行强制程序立即用抢拍消息更新 GUI。

## 19 测试你的代码

现在运行程序检查它是否正常工作。记住，你需要先点击 Tkinter 窗口，它才会响应“q”和“p”键。

等待 1 秒，让玩家阅读消息。

## 技巧与调整

![](img/6b18a113f7aa9338e32f3ac1fa217987_178_0.png)

Tkinter 除了圆形、正方形和矩形之外，还可以显示许多不同的颜色和形状，因此有充足的空间来自定义你的游戏。这里有一些可以尝试的想法——包括让游戏防作弊！

### 彩色轮廓

程序在判断是否进行了有效抢拍时，看的是 `fill` 参数，而不是 `outline`。你可以给形状设置不同颜色的轮廓，只要它们的填充颜色匹配，仍然可以抢拍成功。

### 加快游戏速度

你可以随着游戏进行，缩短每个形状之间的时间延迟，让游戏稍微难一点。试着把时间存储在一个变量中，从 1000 开始，每显示一个形状就减去 25。这些数字只是建议——请自行试验，看看哪种效果最好。

![](img/6b18a113f7aa9338e32f3ac1fa217987_178_1.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_178_2.png)

### 添加更多颜色

你可能已经注意到抢拍游戏相当短。为了延长游戏，可以添加使用不同颜色的额外正方形、矩形和圆形。

### 制作新形状

你可以更改 `create_oval()` 的参数，生成椭圆而不是圆形。Tkinter 还可以绘制弧线、线条和多边形。试试这里展示的示例，并摆弄这些参数。记住将 `state` 保持为 `HIDDEN`，以便在需要显示形状之前将其隐藏。

![](img/6b18a113f7aa9338e32f3ac1fa217987_178_3.png)

![](img/6b18a113f7aa9338e32f3ac1fa217987_178_4.png)

### 绘制弧线

使用 `create_arc()` 函数绘制弧线。除非你给弧线指定样式，否则绘制的是实心弧线。要使用 Tkinter 的不同弧线样式，请通过更改程序的第三行来导入 `CHORD` 和 `ARC`，如下所示。然后如下页所示，将一些弦形和弧线添加到你的形状列表中。

试试这个来修改弧线样式。

```python
from tkinter import Tk, Canvas, HIDDEN, NORMAL, CHORD, ARC
```

```python
arc = c.create_arc(235, 120, 365, 370, outline='black', \
    fill='black', state=HIDDEN)
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_179_0.png)

```python
arc = c.create_arc(235, 120, 365, 370, outline='red', \
    fill='red', state=HIDDEN, style=CHORD)
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_179_1.png)

```python
arc = c.create_arc(235, 120, 365, 370, outline='green', \
    fill='green', state=HIDDEN, style=ARC)
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_179_2.png)

### 绘制线条

现在尝试使用 `create_line()` 函数向我们的形状列表中添加一些线条。

```python
line = c.create_line(35, 200, 365, 200, fill='blue', state=HIDDEN)
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_179_3.png)

```python
line = c.create_line(35, 20, 365, 350, fill='black', state=HIDDEN)
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_179_4.png)

### 绘制多边形

接下来尝试使用 `create_polygon()` 为你的形状集合制作一些多边形。你需要为多边形的每个角提供坐标。

代码中的三对数字给出了三角形三个角的坐标。

```python
polygon = c.create_polygon(35, 200, 365, 200, 200, 35,
    outline='blue', fill='blue', state=HIDDEN)
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_179_5.png)

### 阻止玩家作弊

现在，如果调用了一个形状，并且两个玩家同时按下各自的形状键，他们都会得到一分。事实上，在下一个形状显示之前，他们仍然能够得分，因为前一个形状和当前形状仍然相同。试试这个技巧来阻止玩家作弊。

### 1. 设为全局变量

现在我们需要在 `snap()` 函数中设置 `previous_color` 和 `current_color` 变量，因为除非将它们设为全局变量，否则在函数内部无法访问它们。

```python
global previous_color
```

### 2. 阻止多次抢拍

接下来，在 `snap()` 函数中添加下面这一行，在正确抢拍后将 `previous_color` 的值设置为空字符串（`''`）。现在，如果玩家在下一个形状显示之前再次按下按键，他们将失去一分。这是因为 `''` 永远不会等于当前颜色，除非是在第一个形状显示之前。

```python
shape = c.create_text(200, 200, text='SNAP!')  # scored 1 point!
previous_color = ''
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_180_0.png)

> 关于多次抢拍，没有我不知道的！

### 3. 防止提前抢拍

由于游戏开始时 `previous_color` 和 `current_color` 相等，玩家仍然可以在第一个形状出现之前按下按键来作弊。要解决这个问题，请在开始时将这两个变量设置为不同的字符串。将它们的值改为“a”和“b”。

```python
previous_color = 'a'
current_color = 'b'
```

> 以不同的字符串开始，意味着在形状出现在屏幕上之前无法进行抢拍。

### 4. 更改消息

如果两个玩家几乎同时按下按键，可能会让人搞不清谁得分或谁失分。要解决这个问题，你可以更改玩家尝试抢拍时显示的消息。

![](img/6b18a113f7aa9338e32f3ac1fa217987_180_1.png)

别忘了保存你的工作。

```python
if previous_color == current_color:
    if event.char == 'q':
        player1_score = player1_score + 1
        shape = c.create_text(200, 200, text='SNAP! Player 1 scores 1 point!')
    else:
        player2_score = player2_score + 1
        shape = c.create_text(200, 200, text='SNAP! Player 2 scores 1 point!')
    previous_color = current_color
else:
    if event.char == 'q':
        player1_score = player1_score - 1
        shape = c.create_text(200, 200, text='WRONG! Player 1 lost 1 point!')
    else:
        player2_score = player2_score - 1
        shape = c.create_text(200, 200, text='WRONG! Player 2 lost 1 point!')
```

## 配对游戏

你的记忆力有多好？在这个有趣的游戏中测试一下吧，你需要找到成对的匹配符号。看看你能多快找到全部 12 对匹配项！

### 会发生什么

运行程序时，它会打开一个窗口，显示一个按钮网格。成对点击按钮以揭示隐藏的符号。如果两个符号相同，你就找到了一对匹配项，这些符号会保持在屏幕上可见。否则，这两个按钮会被重置。试着记住每个隐藏符号的位置，以便快速找到所有配对。

![](img/6b18a113f7aa9338e32f3ac1fa217987_181_0.png)

网格显示 24 个按钮，排列成四行六列。

点击一个按钮以揭示一个符号。

每个符号只有两个。

GUI 窗口

网格窗口是由 Python 的 Tkinter 模块创建的图形用户界面（GUI）。

如果匹配错误，符号会再次隐藏。

匹配的符号会留在网格上显示。
