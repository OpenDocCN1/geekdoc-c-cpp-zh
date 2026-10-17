
# 第 3 步
你可以通过函数传递变量，就像一个人的姓氏中的字母数量一样，你可以使用以下代码（在此示例中进入文本编辑器）：

```python
name=input("Enter your surname: ")
Count=len(name)
print("Your surname has", count, "letters in it")
```

```
Python 3.4.2 Sheet
Edit Shell Debug Options Windows Help
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
(C) Python Software Foundation, Inc. on linux
Type "copyright", "credits" 或 "license" 获取更多信息。
print("antisestablishmentarianism")
>>>
```

按下 `F5` 并保存代码以执行。

![](img/0b5e7d59f3578d974082f03180129000_37_0.png)

# 第 2 步
函数接收数据，使用变量，根据函数的编程方式对其进行处理并返回值。处理的数据位于括号内，所以如果你想知道单词 `antidisestablishmentarianism` 有多少字母，你只需要输入 `len("antidisestablishmentarianism")` 和数字 28。

# 第 4 步
Python 内置了数十个函数，多到在这里有限的空间内无法介绍。然而，可以通过 `docs.python.org/3/library/functions.html` 查看预定义函数，但用户还创建了更多。

```
Python 3.4.2 Sheet
Edit Shell Debug Options Windows Help
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
(C) Python Software Foundation, Inc. on linux
Type "copyright", "credits" 或 "license" 获取更多信息。
print("antisestablishmentarianism")
>>>
```

![](img/0b5e7d59f3578d974082f03180129000_37_0.png)

## 创建函数

## 酷炫函数
函数是你输入到 Python 中执行某些操作的命令。它是一段自包含的小代码，对其进行处理并返回结果。

### 第 1 步
不仅仅是可以运行的函数。它们可以在 Python 中做所有实用的事情，例如排序数据、将项目从一种格式转换为另一种格式，以及检查项目的长度或类型。例如，函数是一个后面跟着括号的短单词。`len()`、`list()` 或 `type()`。

### 第 3 步
你可以通过函数传递变量，就像一个人的姓氏中的字母数量一样，你可以使用以下代码（在此示例中进入文本编辑器）：

```python
name=input("Enter your surname: ")
Count=len(name)
print("Your surname has", count, "letters in it")
```

### 第 2 步
函数接收数据，使用变量，根据函数的编程方式对其进行处理并返回值。处理的数据位于括号内，所以如果你想知道单词 `antidisestablishmentarianism` 有多少字母，你只需要输入 `len("antidisestablishmentarianism")` 和数字 28。

### 第 4 步
Python 内置了数十个函数，多到在这里有限的空间内无法介绍。然而，可以通过 `docs.python.org/3/library/functions.html` 查看预定义函数，但用户还创建了更多。

## 条件与循环
条件和循环是程序变得有趣的关键。它们可以简单，也可以复杂。

## TRUE 条件
保持条件简单会让学习编程更加愉快。让我们从检查某物是否为 TRUE 开始，然后处理它不是的情况。

### 第 1 步
我们创建一个新程序，要求用户输入一个单词，然后检查它是否是四字母单词。从 `File = New` 开始，并输入输入：

```python
word=input("Please enter a four-letter word: ")
```

### 第 2 步
我们现在创建一个新变量，然后使用函数并将单词传递进去以获取用户输入的总字母数：

```python
word=input("Please enter a four-letter word: ")
word_length=len(word)
```

### 第 4 步
`if` 结尾的冒号告诉 Python 冒号之后的内容是成立的。接下来，将光标回到编辑器的开头：

```python
word=input("Please enter a four-letter word: ")
word_length=len(word)
if word_length == 4:
    print("is a four-letter word. Well done.")
else:
    print("is not a four-letter word.")
```

# 第 5
按下 `F5` 并保存代码以执行。首先在 Shell 中输入一个四个字母的单词，你应该会收到消息显示该单词是四个字母。现在再次按下 `F5` 运行程序，这次输入一个五个字母的单词。Shell 将显示它不是四个字母单词。

# 第 6
现在扩展代码包含其他条件。最终，它可能会变得相当。我们添加了一个针对三个字母单词的条件：

```python
word=input("Please enter a four-letter word: ")
if len(word) == 4:
    print("is a four-letter word. Well done.")
elif len(word) == 3:
    print("is a three-letter word. Try again.")
else:
    print("is not a four-letter word.")
```

![](img/0b5e7d59f3578d974082f03180129000_40_0.png)

![](img/0b5e7d59f3578d974082f03180129000_40_1.png)

## 循环
循环看起来类似于条件，但它们在操作方式上有所不同。循环会在条件的支持下多次运行同一个代码块。

# 第 1
让我们从一个简单的 While 语句开始。像 `IF` 一样，它将检查某些内容是否为真（TRUE），然后缩进代码：

```python
x = 0
while x < 10:
    print(x)
    x = x + 1
```

# 第 3
`For` 循环是另一个例子。`For` 用于遍历数据范围，该范围通常列在方括号内的变量中。例如：

```python
words = ["Cat", "Dog", "Unicorn"]
for word in words:
    print(word)
```

![](img/0b5e7d59f3578d974082f03180129000_40_2.png)

![](img/0b5e7d59f3578d974082f03180129000_40_3.png)

# 第 2
`if` 和缩进代码之间的区别在于，它回到结尾并检查语句是否仍然为真。示例中 `x` 小于 10。使用循环会打印 `x` 的当前值，然后给值加 1。当 `x` 等于 10 时，它停止。

# 第 4
`For` 循环也可以使用 `range` 函数用于倒计时示例：

```python
for x in range(1, 10):
    print(x)
```

这里没有 `x++1`，因为 `range` 函数会在第一个和最后一个使用的数字之间创建一个列表。

![](img/0b5e7d59f3578d974082f03180129000_40_4.png)

![](img/0b5e7d59f3578d974082f03180129000_40_5.png)

## Python 模块
我们之前提到过模块（`Math` 模块），因为模块是充分利用 Python 的的重要组成部分，然而，值得花更多时间在它们上。在此情况下，我们使用的是 Windows 版本的 Python 3。

## 掌握模块
将模块视为导入到你的 Python 代码中的扩展，以增强和扩展其功能。正如我们看到的，有无数模块可用，你甚至可以创建自己的模块。

### 步骤 1
尽管很好，但 Python 内置函数是有限的。然而，模块的使用允许我们编写更复杂的程序。正如你所知，，导入脚本。

### 步骤 3
在 IDLE Shell 中的结果是错误，未识别或未安装。要安装模块，我们可以使用 `pip`（关闭 IDLE Shell 并进入命令行）。在管理员提示符中，输入：

```bash
pip install pygame
```

### 步骤 2
某些模块在 Raspberry Pi 上默认包含，`math` 模块。因此，其他并不总是可用。非 Pi 平台的很好的例子是 `pygame` 模块，它包含许多帮助创建游戏的函数。尝试：`import pygame`

### 步骤 4
`PIP` 安装需要管理员权限安装在不同的位置。Windows 用户可以通过开始按钮搜索并右键点击“以管理员身份运行”。Linux 和 Mac 用户可以使用 `sudo` 安装包。

```cmd
C:\Users\david>pip install pygame
Microsoft Windows [Version 10.0.15063] (C)2017 Microsoft. All rights reserved.
Collecting pygame
Collecting pygame-1.9.3-cp36-win32.whl
Successfully installed pygame-1.9.3
C:\WINDOWS\system32>
```

# 第 5
关闭命令行提示符并重启 IDLE Shell。当你输入 `import pygame`，模块将导入到代码中没有任何问题。你会发现大多数从互联网下载或拷贝的代码通常由于缺少它们而产生错误语句。

```python
Pygame 1.9.2 (SDL) Python 3.7.0 [win64] Jul 14:39
>>> 
```

# 第 8
多个模块可以导入到你的代码中。为了扩展你的示例，使用：

```python
import random
import math

for i in range(5):
    print(random.randint(1,25))
    print(math.pi)
```

![](img/0b5e7d59f3578d974082f03180129000_42_0.png)

# 第 6
模块包含了在代码中实现某些结果所需的额外代码，正如我们之前解释过的。通过随机生成器，你可以使用它创建类似：

```python
File Edit Run Help
import random
for i in range(10):
    print(random.randint(1,25))
```

![](img/0b5e7d59f3578d974082f03180129000_42_1.png)

# 第 9
结果是随机数以及从 `math` 模块提取的 Pi 值。你也可以使用 `from import` 命令从模块中提取某些函数，例如：

```python
from random import randint

for i in range(5):
    print(random.randint(1,25))
```

```python
C:/Users/Dev/Documents/Python/RandomNumber.py
File Edit Run Help
from random import randint
for i in range(5):
    print(random.randint(1,25))
```

![](img/0b5e7d59f3578d974082f03180129000_42_2.png)

# 第 7
这段代码保存并执行时，将显示从 1 到 25 的随机数。你可以尝试更大或更小的范围，例如：

```python
import random

for i in range(25):
    print(random.randint(1,100))
```

```python
File Edit Run Options Help
import random
for i in range(25):
    print(random.randint(1,100))
```

![](img/0b5e7d59f3578d974082f03180129000_42_3.png)

# 第 10
有助于创建更简洁的方法。你也可以导入模块，这将导入命名模块内的所有内容。然而，它通常被视为一组资源，但为模块保留别名：

```python
import math as m

print(m.pi)
```

当然，添加注释有助于告诉他人正在发生什么。

```python
C:/Users/Dev/Documents/Python/RandomNumber.py
File Edit Run Options Help
import math as m
print(m.pi)
```

![](img/0b5e7d59f3578d974082f03180129000_42_4.png)

## 处理数据
![](img/0b5e7d59f3578d974082f03180129000_44_0.png)

数据就是一切。通过数据，你可以根据每个需求显示、控制、添加、删除、创建和操作 Python。在接下来的页面中，我们将如何创建列表、元组、字典和多维列表；并查看如何使用它们来编写有趣实用的程序。

然后，你可以学习如何使用日期时间函数，向你的系统写入文件，甚至创建图形用户界面将你的编程技能推向新的水平和新的项目想法。

- 46 列表
- 48 元组
- 50 字典
- 52 字符串的分割与合并
- 54 字符串格式化
- 56 日期与时间
- 58 打开文件
- 60 写入文件
- 62 异常
- 64 Python 图形

## 列表
列表是在 Python 中遇到的最常见的数据结构类型之一。列表是项的简单集合（如果你愿意的话，也可以称为数据），可以作为一个整体访问，也可以根据需要单独访问。

## 处理列表
列表在 Python 中非常实用。列表可以是字符串、整数，也可以是变量。你甚至可以在列表中包含函数，并在列表内部包含列表。

列表是一个被称为项的数据值序列。你通过等号创建列表的名称，然后使用方括号用逗号分隔项；注意列表使用引号：

```python
numbers = [1, 4, 7, 21, 98, 156]
mythical_creatures = ["Unicorn", "Balrog", "Vampire", "Dragon", "Minotaur"]
```

![](img/0b5e7d59f3578d974082f03180129000_45_0.png)

步骤 3 你可以通过使用负号来访问或索引列表中的项，例如 `[-1]`，或倒数第二个项 `[-2]`，依此类推。尝试引用列表中不存在的项，例如 `[10]`，将返回错误：

```python
numbers[-1]
mythical_creatures[-4]
```

![](img/0b5e7d59f3578d974082f03180129000_45_1.png)

步骤 2 一旦你定义了列表，就可以通过引用调用每个项。列表从 0 开始第一个项，然后是 1, 2, 3 等。例如：

`numbers`

要调用列表的所有内容：

`numbers[3]`

要调用列表中的第三个零索引项（在本例中为 21）：

![](img/0b5e7d59f3578d974082f03180129000_45_2.png)

步骤 4 切片类似于索引，但你可以通过冒号分隔项编号来获取列表中的多个项。

`numbers[1:3]`

将输出 4 和 7，即项编号 1 和 2。注意，返回的值不包含第二个索引（位置），所以 `numbers[1:3]` 返回 4 到 7, 21。

# 第 5 步
你可以更新现有列表中的项，移除项甚至同时移除多个列表。例如，你可以：

```
everything = numbers + mythical_creatures
```

然后通过以下命令查看合并后的列表：

```
everything
```

![](img/0b5e7d59f3578d974082f03180129000_46_0.png)
