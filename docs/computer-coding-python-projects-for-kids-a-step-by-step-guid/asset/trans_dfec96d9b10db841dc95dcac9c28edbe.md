
### 测试代码

运行程序，检查这个改动是否有效。你应该会在 shell 窗口中看到这条消息出现。

```
Choose difficulty (type 1, 2, or 3):
1 Easy
2 Normal
3 Hard
```

### 设置关卡

现在使用 if、elif 和 else 语句来设置每个关卡的生命数。试试简单关卡用 12 条命，普通关卡用 9 条命，困难关卡用 6 条命。如果你测试后觉得关卡太简单或太难，可以再修改生命数。把这段代码添加到询问玩家选择关卡的那些行之后。

![](img/1bd24ab186f69fb18194b4174ca15178_66_0.png)

```python
difficulty = input('Choose difficulty (type 1, 2 or 3):\n 1 Easy\n 2 Normal\n 3 Hard\n')
difficulty = int(difficulty)

if difficulty == 1:
    lives = 12
elif difficulty == 2:
    lives = 9
else:
    lives = 6
```

## 长度不固定的单词

如果你想玩一个单词长度会变化的游戏，该怎么办？如果在程序运行前不知道秘密单词的长度，你就不知道该把保存线索的列表做多长。有一个巧妙的解决办法可以解决这个问题。

![](img/1bd24ab186f69fb18194b4174ca15178_66_1.png)

### 1. 使用空列表

创建保存线索的列表时，不要用问号填充它——只需让列表保持为空。对线索列表做这个修改。

```python
clue = []
```

方括号里什么都没有。

### 添加一个新循环

为了让线索在秘密单词选定后具有正确长度，使用这个简单的循环。它会统计单词中有多少个字母，并为每个字母添加一个问号。

```python
clue = []
index = 0
while index < len(secret_word):
    clue.append('?')
    index = index + 1
```

append() 函数只是把一个项目添加到列表末尾。

## 让结尾更智能

目前，只有完整输入单词后游戏才会结束。让我们把代码改得更智能，这样当你猜中最后一个字母时游戏就结束。

### 再创建一个变量

首先创建一个变量来记录还有多少个字母未知。把这段代码添加到 update_clue 函数上方。

```python
unknown_letters = len(secret_word)
```

起初所有字母都是未知的。

### 编辑函数

接下来按下图所示修改 update_clue() 函数。现在，每当玩家正确猜出一个字母，程序就会从 unknown_letters 中减去该字母在秘密单词中出现的次数。

![](img/1bd24ab186f69fb18194b4174ca15178_67_0.png)

```python
def update_clue(guessed_letter, secret_word, clue, unknown_letters):
    index = 0
    while index < len(secret_word):
        if guessed_letter == secret_word[index]:
            clue[index] = guessed_letter
            unknown_letters = unknown_letters - 1
        index = index + 1

    return unknown_letters
```

将这个新参数添加到 update_clue 函数中。

每当猜中的字母在单词中出现一次，代码就会从 unknown_letters 中减去 1。

这一行让函数返回未知字母的数量。

![](img/1bd24ab186f69fb18194b4174ca15178_68_0.png)

> 我猜这个单词是“assist”。

`_ s s _ s t`

### 工作原理

为什么必须在 update_clue() 函数中更新 unknown_letters？为什么不能在知道猜中的字母在秘密单词中时直接减去 1？如果每个字母在秘密单词中只出现一次，这样做是可行的。但如果该字母出现多次，你的计数就会出错。通过在函数中更新这个变量，每当该字母在秘密单词中出现一次，代码就会从 unknown_letters 中减去 1。这是因为函数会检查秘密单词中的每一个字母，看它是否与猜中的字母匹配。

### 3. 调用函数

你还需要修改 update_clue() 函数，传入 unknown_letters 变量并存储新值。

![](img/1bd24ab186f69fb18194b4174ca15178_68_1.png)

> 你好，能请帮我接通这个函数吗？

```python
if guess in secret_word:
    unknown_letters = update_clue(guess, secret_word, clue, unknown_letters)
else:
    print('Incorrect. You lose a life')
    lives = lives - 1
```

这一行将新值赋给 unknown_letters 变量。

这里传入了 unknown_letters 变量。

### 4. 赢得游戏

当 unknown_letters 达到 0 时，用户已经正确猜出单词。将这段代码添加到主循环末尾。现在，当你猜出所有字母后，游戏会自动宣布你获胜。

```python
lives = lives - 1

if unknown_letters == 0:
    guessed_word_correctly = True
    break
```

当玩家猜出正确单词时，break 语句会退出循环。

![](img/1bd24ab186f69fb18194b4174ca15178_68_2.png)

> 哇哦！我猜中最后一个字母了！

![](img/1bd24ab186f69fb18194b4174ca15178_69_0.png)

## 机器人建造师

在 Python 中创建图形很容易。Python 的 turtle 模块让你在屏幕上移动一个机器人“海龟”，它一边移动一边用画笔绘制图片。在这个项目中，你将编写程序让海龟建造更多机器人——或者至少绘制机器人的图片！

### 会发生什么

运行程序时，Python 的 turtle 会出发，在屏幕上快速移动，绘制一个友好的机器人。看着它用不同的颜色一块一块地组装机器人。

![](img/1bd24ab186f69fb18194b4174ca15178_71_0.png)

Python 海龟绘图

![](img/1bd24ab186f69fb18194b4174ca15178_71_1.png)

你可以把机器人的配色方案改成你喜欢的任何样式。

通过改变构成机器人身体各部分的矩形大小来自定义你的机器人。

### 工作原理

你将先编写一个绘制矩形的函数。然后把这些矩形组合起来建造机器人。你可以通过修改传给函数的参数来改变矩形的大小和颜色。这样，你就可以用细长的方块做腿，用正方形做眼睛，等等。

### 别把我命名为 turtle！

注意千万不要把你的任何海龟程序命名为“turtle.py”。如果这样做，Python 会非常困惑，并给你大量错误信息。

![](img/1bd24ab186f69fb18194b4174ca15178_72_0.png)

### 用海龟绘图

turtle 模块允许你控制一只携带画笔的机器人海龟。通过向海龟发出如何在屏幕上移动的指令，你可以绘制不同的图片和图案。你还可以告诉海龟何时落下画笔开始绘制，或何时抬起画笔，以便它移动到屏幕的另一部分而不留下凌乱的痕迹。

海龟向前移动 100 像素，左转 90 度，然后向前移动 50 像素。

```python
t.forward(100)
t.left(90)
t.forward(50)
```

![](img/1bd24ab186f69fb18194b4174ca15178_72_1.png)

### 机器人建造师流程图

流程图展示了这个项目的代码如何组合在一起。首先，程序设置背景颜色和海龟移动的速度。然后，它从脚部开始，逐渐向上到头部，一次绘制机器人的一个部分。

![](img/1bd24ab186f69fb18194b4174ca15178_72_2.png)

### 绘制矩形

我们先导入 turtle 模块，并用它创建一个绘制矩形的函数。

- **1. 创建一个新文件**

打开 IDLE 并创建一个新文件。将其保存为“robot_builder.py”。

![](img/1bd24ab186f69fb18194b4174ca15178_73_0.png)

- **2. 导入 Turtle 模块**

在程序顶部输入这一行。命令 `import turtle as t` 让你可以使用 turtle 模块中的函数，而不必每次都完整输入“turtle”。这就像把名叫 Benjamin 的人简称为“Ben”一样。

```python
import turtle as t
```

这给 Turtle 模块起了个绰号“t”。

- **3. 创建一个矩形函数**

现在创建用于绘制搭建机器人所用方块的函数。这个函数有三个参数：水平边的长度、垂直边的长度和颜色。你将使用一个循环，每次运行时绘制一条水平边和一条垂直边，并让它运行两次。把这个矩形函数放在第 2 步添加的代码下面。

```python
def rectangle(horizontal, vertical, color):
    t.pendown()
    t.pensize(1)
    t.color(color)
    t.begin_fill()
    for counter in range(1, 3):
        t.forward(horizontal)
        t.right(90)
        t.forward(vertical)
        t.right(90)
    t.end_fill()
    t.penup()
```

落下海龟的画笔以开始绘制。

使用 `range(1, 3)` 让循环运行两次。

抬起海龟的画笔以停止绘制。

![](img/1bd24ab186f69fb18194b4174ca15178_73_1.png)

这个代码块绘制矩形。

海龟按照这里显示的顺序绘制各条边。

### 专家提示

**海龟模式**

你将使用海龟的标准模式。这意味着海龟一开始面向屏幕右侧。如果你把朝向（heading，方向的另一种说法）设为 0，它就会面向右侧。将朝向设为 90 会让它指向屏幕顶部，180 指向左侧，270 则让它指向屏幕底部。

![](img/1bd24ab186f69fb18194b4174ca15178_73_2.png)

海龟通常看起来像一个箭头。这一行把它变成海龟形状。

```python
t.shape('turtle')
t.setheading(0)
t.forward(80)
```

