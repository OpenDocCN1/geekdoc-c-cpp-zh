
## 技巧与调整

你可以通过许多方式重新组合和改编这个游戏。你可以添加新单词、改变单词长度，或者让游戏变得更容易或更难。

![](img/6b18a113f7aa9338e32f3ac1fa217987_67_0.png)

### 添加更多单词

试着向程序的单词列表中添加更多单词。你想加多少都可以，但请记住只使用五个字母长的单词。

```python
words = ['pizza', 'fairy', 'teeth', 'shirt', 'otter', 'plane', 'brush', 'horse', 'light']
```

### 改变生命数

你可以通过给玩家更多或更少的生命，让游戏变得更容易或更难。要做到这一点，只需修改你在第 3 步中创建的 lives 变量。

![](img/6b18a113f7aa9338e32f3ac1fa217987_67_1.png)

### 使用更长的单词

如果你认为只使用五个字母的单词会让游戏太简单，可以改用稍长一些的单词——但请记住让它们长度全都相同。若想把游戏变得极其困难，可以在词典中搜索你能找到的最长、最不寻常的单词！

### 添加难度等级

为了让游戏更有趣，让玩家在游戏开始时选择难度等级。较简单的设置会给玩家更多生命。

![](img/6b18a113f7aa9338e32f3ac1fa217987_67_2.png)

### 获取等级

将这段代码放在主程序的开头，就在 while 循环上方。它会要求玩家选择一个等级。

```python
difficulty = input('Choose difficulty (type 1, 2, or 3):\n 1. Easy\n 2. Normal\n 3. Hard\n')
difficulty = int(difficulty)

while lives > 0:
```

difficulty 目前是一个字符串。这一行将它改为整数。

### 测试代码

运行程序，检查这一改动是否有效。你应该会在 shell 窗口中看到这条消息。

- 选择难度（输入 1、2 或 3）：
- 1. 简单
- 2. 普通
- 3. 困难

### 设置等级

现在我们已经有了 `if` 和 `else` 语句，让我们为每个等级设置生命数。试试简单用 12 条命、普通用 9 条命、困难用 6 条命。如果你测试后对等级的难易程度不满意，可以再修改生命数。在要求玩家选择等级的那一行之后添加这段代码。

![](img/6b18a113f7aa9338e32f3ac1fa217987_68_0.png)

```python
if difficulty == 1:
    lives = 12
elif difficulty == 2:
    lives = 9
else:
    lives = 6
```

### 长度不一的单词

如果你想要玩一个单词长度不一的游戏，该怎么办？如果你在程序运行前不知道秘密单词的长度，你就不知道应该把保存线索的列表做多长。有一个巧妙的修复方法可以解决这个问题。

![](img/6b18a113f7aa9338e32f3ac1fa217987_68_1.png)

### 使用空列表

当你创建保存线索的列表时，不要用问号填充它——只需让列表保持为空。对线索列表做这个修改。

```python
clue = []
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_68_2.png)

### 添加一个新循环

为了让线索在秘密单词被选中后具有正确的长度，请使用这个简单的循环。它会统计单词中有多少个字母，并为每个字母添加一个问号。

```python
clue = []
index = 0

while index < len(secret_word):
    clue.append('?')
    index = index + 1
```

append() 函数只是把一个项添加到列表末尾。

### 让结尾更智能

目前，游戏要等你把单词完整输入出来才会结束。让我们把代码改得更智能，这样当你猜出最后一个字母时游戏就会结束。

- **1. 创建另一个变量**

首先创建一个变量来记录还有多少个字母未知。在 update_clue 函数上方添加这段代码。

```python
unknown_letters = len(secret_word)
```

- **2. 编辑函数**

接下来按如下所示修改 update_clue() 函数。现在，每当玩家猜一个字母时，程序都会从 unknown_letters 中减去该字母在秘密单词中出现的次数。

![](img/6b18a113f7aa9338e32f3ac1fa217987_69_0.png)

一开始所有字母都是未知的。

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

每当猜中的字母出现在单词中时，这段代码就会从 unknown_letters 中减去 1。

这一行让函数返回未知字母的数量。

![](img/6b18a113f7aa9338e32f3ac1fa217987_70_0.png)

> 我猜这个单词是“assist”。

### 工作原理

为什么必须在 `update_clue()` 函数中更新 `unknown_letters`？为什么不能在知道猜中的字母在秘密单词中时只减去 1？如果每个字母在秘密单词中只出现一次，这样做是可行的。但如果该字母出现多次，就会使你的计数出错。通过在函数中更新这个变量，每当该字母出现在秘密单词中时，代码都会从 `unknown_letters` 中减去 1。这是因为函数会检查秘密单词中的每一个字母，看它是否与猜中的字母匹配。

- **3. 调用函数**

你还需要修改 `update_clue()` 函数，传入 `unknown_letters` 变量并保存新的值。

![](img/6b18a113f7aa9338e32f3ac1fa217987_70_1.png)

> 你好，能请帮我接通这个函数吗？

```python
unknown_letters = update_clue(guess, secret_word, clue, unknown_letters)

else:
    print("Incorrect. You lose a life")
    lives = lives - 1
```

这会传入 `unknown_letters` 变量。

这一行将新值赋给 `unknown_letters` 变量。

- **4. 赢得游戏**

当 `unknown_letters` 达到 0 时，用户就正确猜出了单词。在主循环末尾添加这段代码。现在，当你猜出所有字母后，游戏会自动宣布你获胜。

```python
lives = lives - 1

if unknown_letters == 0:
    guessed_word_correctly = True
    break
```

当玩家猜出正确单词时，`break` 语句会退出循环。

![](img/6b18a113f7aa9338e32f3ac1fa217987_70_2.png)

> 哇哦！我猜出了最后一个字母！

![](img/6b18a113f7aa9338e32f3ac1fa217987_71_0.png)

## 机器人建造器

在 Python 中创建图形很容易。Python 的 Turtle Graphics 模块让你可以在屏幕上移动一个机器人“海龟”，它一边移动一边用画笔绘制图片。在这个项目中，你将编写程序让海龟建造更多机器人——或者至少是机器人的图片！

### 会发生什么

运行程序时，Python 的海龟会在屏幕上快速爬动，绘制出一个友好的机器人。看着它用不同的颜色把机器人一块一块地组装起来。

![](img/6b18a113f7aa9338e32f3ac1fa217987_73_0.png)

你可以把机器人的配色方案改成你喜欢的任何样式。

通过改变组成机器人身体各部分的矩形大小，来自定义你的机器人。

### 绘制矩形

我们先导入 Turtle 模块，并用它创建一个绘制矩形的函数。

- **1. 创建一个新文件**

打开 IDLE 并创建一个新文件。将其保存为“robot_builder.py”。

![](img/6b18a113f7aa9338e32f3ac1fa217987_75_0.png)

- **2. 导入 Turtle 模块**

在程序顶部输入这一行。命令 `import turtle as t` 让你可以使用 Turtle 模块中的函数，而不必每次都完整输入“turtle”。这就像把名叫 Benjamin 的人简称为“Ben”一样。

```python
import turtle as t
```

这给 Turtle 模块起了个绰号“t”。

- **3. 创建一个矩形函数**

现在创建用来绘制积木块的函数，你将用这些积木块来建造机器人。该函数有三个参数：水平边的长度、垂直边的长度和颜色。你将使用一个循环，每次运行时绘制一条水平边和一条垂直边，并让它运行两次。把这个 rectangle 函数放在你在第 2 步添加的代码下面。

和所有编程语言一样，Python 使用美式拼写“color”。

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

将海龟的画笔放下以开始绘制。

使用 range(1, 3) 会让循环运行两次。

将海龟的画笔重新抬起以停止绘制。

![](img/6b18a113f7aa9338e32f3ac1fa217987_75_1.png)

这个代码块绘制矩形。

海龟按这里显示的顺序绘制各条边。

### 专家提示

### 海龟模式

你将使用海龟的标准模式。这意味着海龟一开始面向屏幕右侧。如果你把朝向（heading，即方向的另一种说法）设为 0，它就会面向右侧。将朝向设为 90 会让它指向屏幕顶部，180 指向左侧，270 则让它指向屏幕底部。

![](img/6b18a113f7aa9338e32f3ac1fa217987_75_2.png)

海龟通常看起来像一个箭头。这一行会把它改成海龟形状。

```python
t.shape('turtle')
t.setheading(0)
t.forward(80)
```
