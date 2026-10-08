

# 解鬼魂游戏（Ghost game）

鬼魂游戏展示了 Python 的一些核心特性。你可以拆解代码，查看程序的结构以及各个不同部分所起的功能。

# 代码结构

Python 使用行首的空格来确定哪些指令是相互相关的。这些空格被称为“缩进”。例如，“feeling_brave” 之后的代码缩进了四个空格，以显示它们都是主循环的一部分。

# 另需参考

- 96-97 鬼魂游戏
- 程序 100-101 流程

![](img/72d218a7a73c4d4abc7be582ebd85385_99_0.png)

游戏设置

主循环

代码关键点

此图展示了鬼魂游戏的结构。编号部分在下文中有更详细的解释。

分支部分

这是一个“注释”。在游戏运行时它不会显示。

游戏结束

# 游戏设置

这些指令只运行一次——在游戏开始时。它们设置了标题、变量和 "randint" 命令。

# 鬼魂游戏

```python
from random import randint
print('Ghost Game')
feeling_brave = randint(0)
```

这设置了 "randint" 命令，它可以生成随机数。

"print" 命令在游戏运行时显示文本。

这重置了分数。

# 专家提示

# 小心输入

使用 Python 时，要非常小心地输入代码。如果你漏掉了冒号、引号或括号，程序将无法运行。你还需要精确匹配大写字母和空格。

![](img/72d218a7a73c4d4abc7be582ebd85385_99_1.png)

# 主循环

这个循环讲述故事并接收玩家的猜测。只要选中的门后面没有鬼魂，它就会持续运行。当鬼魂出现时，"feeling_brave" 变量变为 "False"，循环就会停止重复。

```python
while feeling_brave:
```

```python
  ghost_door = randint(1, 3)
```

```python
  print('Three doors ahead...')
```

```python
  print('A ghost behind one.')
```

这在 1 到 3 之间选择一个随机数。

```python
  print('Which door do you open?')
```

"print" 命令在屏幕上显示文本。

```python
  door = input('1, 2 or 3?')
```

这一行询问玩家的输入。

```python
  door_num = int(door)
```

# 分支点

程序根据选中的门后面是否有鬼来采取不同的路径。如果有鬼，"feeling_brave" 变量被设置为 "False"；否则，玩家的分加一。

```python
if door_num == ghost_door:
```

```python
  print('GHOST!')
```

如果玩家选的门后面有鬼，则运行此分支。

```python
  feeling_brave = False
```

```python
else:
```

如果没有鬼魂，玩家会看到这个房间。

```python
  print('No ghost!')
```

```python
  print('You enter the next room.')
```

```python
  score = score + 1
```

这显示了一条消息，告诉玩家逃离鬼魂。

# 游戏结束

这只运行一次，当你遇到鬼魂且循环结束时。Python 知道这不是循环的一部分，因为它被缩进了。

```python
print('Run away!')
```

```python
print('Game over! You scored', score)
```

分数是一个变量——它根据玩家通过了多少房间而改变。

# 记住

# 成就

恭喜你——你创建了自己的第一个 Python 游戏！你将在书中学习更多关于这些命令的知识，但你已经取得了很多：

- 运行程序：你学会了运行 Python 程序。
- 结构化程序：你使用了缩进来结构化程序。
- 使用变量：你 使用了变量来存储分数。
- 输入程序：你在 Python 中输入了程序并保存了它。
- 显示文本：你已经在屏幕上显示了消息。

![](img/72d218a7a73c4d4abc7be582ebd85385_100_0.png)

# 100 玩转 Python

# 程序流程

在学习更多 Python 知识之前，理解程序是如何运作的很重要。在 Scratch 中学习的编程基础也可以应用于 Python。

| 另需参考 |
| :--- |
| 30–31 彩色块和脚本 |
| 简单的 102–103 命令 |
| 复杂的 104–105 命令 |

### 从输入到输出
程序接收输入（输入信息），处理它（或更改它），然后返回结果（输出）。这有点像厨师拿食材，将它们变成蛋糕，然后把蛋糕给你吃。

![](img/72d218a7a73c4d4abc7be582ebd85385_101_0.png)

- 输入命令
  - 键盘
  - 鼠标
- 变量
  - 数学
  - 循环
  - 分支
  - 函数
- Print 命令
  - 屏幕
  - 图形

> Python 中的程序流程
> 在 Python 中，键盘和鼠标用于输入信息，使用循环、分支和变量等元素进行处理。然后将输出显示在屏幕上。

# 通过 Scratch 眼镜观察鬼魂游戏

程序流程在编程语言中的工作方式是相同的。以下是 Python 鬼魂游戏中的输入、处理和输出的一些示例——以及它们在 Scratch 中可能的样子。

# 专家提示
### 一次一个脚本

Scratch 和 Python 之间有一个重要的区别。在 Scratch 中，许多脚本可以同时运行。然而，程序只由一个脚本组成。

![](img/72d218a7a73c4d4abc7be582ebd85385_102_0.png)

- 输入
在 Python 中，“input() 函数从键盘接收输入。它类似于 Scratch 中的“询问并等待”积块。

Scratch 块中的问题

```python
door = input('1, 2 or 3?')
```

“询问并等待” 积块

- 处理
变量用于跟踪分数。Python 的 "randint" 在 1 到 3 之间选择一个随机数。"print()" 函数用于在 Python 中输出内容，而 "say" 同样的功能。

### 通过 Scratch 眼镜观察鬼魂游戏

初看之下，Python 看起来可能非常吓人，尤其是与 Scratch 相比。以下是 Scratch 基础命令之间相似性的指南。

| 命令 | Python 3 | Scratch 2.0 |
| :--- | :--- | :--- |
| 运行程序 | “运行”菜单或按 F5 | |
| 停止程序 | 终端窗口中的“CTRL-C” | |
| 文本写入到 | print('Hello!') | say Hello! |
| 将变量设置为数字 | magic_number = 42 | say magic_number to 42 |
| 将变量设置为字符串 | word = 'dragon' | word to dragon |
| 从键盘读取文本到变量 | age = input('age') | say age? and wait |
| 给变量累加一个数字 | cats = cats + 1 | change cats by 1 |
| 加 | a + 2 | a |
| 减 | a - 2 | a |
| 乘 | a * 2 | a |
| 除 | a / 2 | a |

# 简单命令

初看之下，Python 看起来可能非常吓人，尤其是与 Scratch 相比。以下是 Scratch 基础命令之间相似性的指南。

| 命令 | Python 3 | Scratch 2.0 |
| :--- | :--- | :--- |
| 永远循环 | while True: jump() | forever
jump |
| 重复 10 次 | for i in range(10): jump() | repeat 10
jump |
| 等于？ | a == 2 | a = 2 |
| 小于？ | a < 2 | a = 2 |
| 大于？ | a > 2 | a = 2 |
| 非 | not | not |
| 或 | or | or |
| 和 | and | and |
| 如果那么 | if a == 2: print('Hello!') | if a = 2 then say Hello! |
| 如果...否则 | if a == 2: print('Hello!') else: print('Goodbye!') | if a = 2 then say Hello! else say Goodbye! |

# 高命令

Python 也可以用于完成 Scratch 中可以实现的复杂操作：例如，创建复杂的循环、处理字符串和列表，以及使用乌龟绘图图形。

> 另需参考
* 86–87 什么是 Python?
* 102–103 简单命令

