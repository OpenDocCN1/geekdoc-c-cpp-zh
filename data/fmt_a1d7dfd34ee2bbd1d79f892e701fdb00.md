
### STEP 4
`if` 结尾的冒号告诉 Python 冒号后的语句是真的。接下来，将光标移动到编辑器的开头：

```python
word=input("Please enter a four-letter word: ")
word_length=len(word)
if word_length == 4:
```

```
print("is a four-letter word. Well done.")
```

else:

```
print("is not a four-letter word.")
```

## 条件与循环

步骤 5 按下 `F5` 并保存代码以执行。最初在 Shell 中输入一个四个字母的单词，你应该收到返回消息，显示该单词是四个字母的。现在再次按 `F5` 运行程序，这次输入五个字母的单词。Shell 将显示它不是四个字母的单词。

STEP 6 现在扩展代码以包含另一个条件。最终，它可能会变得相当复杂。我们为三个字母单词添加了一个条件：

```python
word=input("Please enter a four-letter word: ")
if len(word) == 4:
    print("word, is a four-letter word. Well done.")
elif len(word) == 3:
    print("word, is a three-letter word. Try again.")
else:
    print("word, is not a four-letter word.")
```

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_40_0.png)

### 循环

循环看起来与条件相似，但在运行机制上有所不同。循环会多次运行同一个代码块，通常在条件的支持下进行。

STEP 1 让我们从简单的 while 开始。像 `IF` 一样，它将检查某些内容是否为真，然后运行缩进的代码：

STEP 3 循环是另一个例子。`for` 用于遍历数据范围的数据，通常是存储在括号中的列表：For:

```python
x = 10
while x > 0:
    print (x)
    x = x - 1 # 注意：从 +1 改为 -1 以使循环终止
```

```python
words=['Cat', "Dog", "Unicorn"]
for word in words:
    print (word)
```

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_40_1.png)

STEP 2 `if` 和 `for` 的区别在于，`while` 执行到缩进代码的结尾，而 `for` 会返回并检查语句仍然 true。在一个例子中 x 小于 10。每次循环它都会打印 x 的当前值，然后将值加 1。当 x 最终等于 0 时，它就会停止。

STEP 4 循环也可以使用 `range` 函数用于倒计时示例中：

```python
for x in range (1, 10):
    print (x)
```

这里不需要 `x=1`，因为 `range` 函数根据第一个和最后一个数字创建一个列表。

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_40_2.png)

## Python 模块

我们之前提到过模块（例如 Math 模块），但由于它们是充分利用 Python 的重要部分，值得花更多时间研究它们。在此情况下，我们使用的是 Windows 版本的 Python 3。

### 掌握模块

将模块视为导入到你的 Python 代码中的扩展，用以增强和扩展其功能。有无数可用模块，正如我们看到的，你可以创建自己的模块。

STEP 1 尽管你可以在 Python 中构建内置函数，但使用模块是为了编写更复杂的程序。如你所知，模块是会被导入的 Python 脚本，例如：

STEP 3 结果是 IDLE 报错，因为该模块没有在 Python 中被识别或安装。要安装它，我们可以使用 PIP `Pip Installs Packages`。关闭 IDLE Shell 并进入命令提示符或终端。在管理员权限的命令提示符中输入：`pip install pygame`

```python
Python 3.6 Shell
File Edit Help Options Window help
Python 3.6.2 (v3.6.2:053b3, Jul 8 2017, 04:14(34)) [MSC v.1900 32 bit (Intel)] on Windows
>>> Type "copyright", "credit" or "license" for more information.
>>> import math
```

```cmd
Command Prompt
C:\Users\david
pip install pygame
```

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_41_0.png)

STEP 2 某些模块（特别是树莓派上的）是默认包含的，`math` 模块就是一个例子。遗憾的是，其他模块并不总是可用。非平台的一个很好的例子是 `pygame` 模块，它包含了许多创建游戏的函数。尝试：`import pygame`。

STEP 4 PIP 安装由于组件被安装在特定位置，需要管理员权限。Windows 用户可以在开始按钮搜索 `CMD`，然后右键点击结果并选择“以管理员身份运行”。Linux 和 Mac 可以使用 `sudo` 命令，即 `sudo install package`。

```python
Python 3.6 Shell
File Edit Help Options Window help
Python 3.6.2 (v3.6.2:053b3, Jul 8 2017, 04:14(34)) [MSC v.1900 32 bit (Intel)] on Windows
>>> Type "copyright", "credit" or "license" for more information.
>>> import pygame
### 第一次调用：
>>> print(pygame.version.version)
('2.0.1', 'release')
>>> import pygame
ImportError: No module named 'pygame'
```

```cmd
Administration Command Prompt
Microsoft Windows [Version 10.0]
C:\Users\david> pip install pygame
  Collecting pygame
  Downloading pygame-2.0.1-cp36-cp36win_amd64.whl (5.5 MB)
  Requirements already satisfied:
Installing collected packages: pygame-2.0.1
Successfully installed pygame-2.0.1
```

## 列表

列表是你 Python 中遇到的最常见数据结构之一。列表简单来说就是项的集合，或者如果你愿意，也可以作为一个整体被访问，也可以根据需要逐个访问。

### 操作列表

列表在 Python 中非常有用。列表可以包含字符串、整数，也可以包含变量。你甚至可以在列表中包含函数，甚至在列表中包含列表。

- 步骤 1：列表是一个称为“项”`items`的数据值序列。你可以创建一个列表名称，后跟一个等号，然后是方括号并用逗号分隔各个项；

```python
numbers = [1, 4, 7, 21, 98, 156]
mystical_creatures = ["Unicorn", "Balrog", "Vampire", "Dragon", "Winteraur"]
```

- 步骤 3：你还可以通过在数字前加上负号 `[-1]` 获取最后一个项，使用 `[-2]` 获取倒数第二个项，以此此类推访问或索引列表中的项。引用一个不在列表中的项（例如 `[10]`）将返回错误：`mythical[-1]`

```python
numbers[-1]
mystical_creatures[-4]
```

| Cell 0 | Cell 1 | Cell 2 | Cell 3 | Cell 4 | Cell 5 | Cell 6 | Cell 7 | Cell 8 | Cell 9 |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| Python 3.4.2 (default. Oct 19 2014, 12:31:17) | | type="copyright": "credits" or "license" for more information. | | numbers = [1, 4, 7, 21, 98, 156] | | mystical_creatures = ["Unicorn", "Balrog", "Vampire", "Dragon", "Winteraur"] | | numbers[-1] | | mystical_creatures[-4] | |

- 步骤 2：一旦定义了列表，你就可以通过引用索引或名称来调用每个元素。列表是有编号的。例如：

`numbers`

调用列表的全部内容。

调用列表中的第三个零索引项（在这种情况下是 21）。

- 步骤 4：切片 `Slicing` 与索引类似，但你可以通过冒号分隔项数字来检索列表中的多个项：

`numbers[1:3]`

将输出 4 和 7，因为当 `numbers[1:3]` 返回 4 和 7 时，返回的值排除了第二个索引（位置）。

| Cell 0 | Cell 1 | Cell 2 | Cell 3 | Cell 4 | Cell 5 | Cell 6 | Cell 7 | Cell 8 | Cell 9 |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| Python 3.4.2 (default. Oct 19 2014, 12:31:17) | | type="copyright": "credits" or "license" for more information. | | numbers = [1, 4, 7, 21, 98, 156] | | mystical_creatures = ["Unicorn", "Balrog", "Vampire", "Dragon", "Winteraur"] | | numbers[1:3] | | |

![](img/8b33dbf2a2ef620c5ea6844ae78b2983_45_0.png)

### 步骤 5

你可以更新现有列表中的项、删除项，甚至合并列表。例如，合并列表可以使用：

```python
everything = numbers + mythical_creatures
```

然后使用以下代码查看合并后的列表：

```python
everything
```

```python
Python 3.4.2
Python 3.4.2 (default, Oct 19 2014, 13:51:11)
print("credits" or "license" for more information.
mythical_creatures = ["unicorn", "Vampire", "Dragon", "Winteresaur"]
numbers = numbers + mythical_creatures
print(numbers)
# [1, 4, 7, 21, 98, 156, "unicorn", "Bairig", "Dragon", "Winteresaur"]
```

### 步骤 8

你可以通过在 Shell 中输入 `dir(list)` 来查看列表可以进行的操作。输出是所有可用的函数，例如 `insert` 和 `pop` 用于在特定位置添加和删除项。在索引 4 处插入 62：

```python
numbers.insert(4, 62)
```

删除：

```python
numbers.pop(4)
```

```python
type 'list' credits or 'license' for more information.
[append, clear, copy, count, extend, filter, get, index, insert, join, len, list, max, min, pop, remove, reverse, sort, sort]
>>> insert(4, 62)
[1, 4, 7, 21, 62, 98, 156, "unicorn", "Bairig", "Dragon", "Winteresaur"]
>>> pop()
[1, 4, 7, 21, 62, 98, 156, "unicorn", "Bairig", "Dragon", "Winteresaur"]
```

### 步骤 6

你可以通过以下方式向列表添加项：

```python
numbers=numbers+[2]
```

对于字符串：

使用 `append` 方法：

```python
mythical_creatures.append("Nessie")
```

```python
>>> mythical_creatures = ["unicorn", "Vampire", "Dragon", "Winteresaur"]
```

### 步骤 9

你还可以使用列表将字符串拆分：将其拆分为 'D', 'a', 'v'。这可以传递给一个新的列表：

```python
list("David")
```

```python
list("Howard")
age=44
```

```python
>>> Python 3.4.2 (default, Oct 19 2014, 13:51:11)
>>> print("credits" or "license" for more information.
>>> name = "David"
>>> age = 44
>>> user = name + age
'David44'
```

### 步骤 7

删除项有两种方法。另一种是通过项：

```python
del numbers["Nessie"]
```

```python
>>> mythical_creatures = ["unicorn", "Vampire", "Dragon", "Winteresaur"]
>>> mythical_creatures.remove("Nessie")
>>> mythical_creatures
['unicorn', 'Vampire', 'Dragon', 'Winteresaur']
```

### 步骤 10

根据这些，你可以创建一个关于名字和年龄的程序：

```python
name=input("What is your name?")
age=input("How old are you?")
```

```python
user = name + age
```

合并的名字和年龄是列表，可以通过在 Shell 中输入 `user` 来调用。实验你可以做什么：

### 元组

元组与列表非常相似。然而，虽然列表可以更新、删除或更改，但类型保持不变。它是不可变的，非常适合存储固定数据项。

### 不可变元组

使用元组的原因取决于程序的意图。通常，元组是为特殊情况保留的，但它们也被用于存储游戏中的非游戏角色名称。

- 元组的创建方式与列表相同，但你使用圆括号而不是方括号。例如，这里有一个名为 `NPC` 可玩角色的元组，包含了角色名称和他们在游戏中的战斗评分：

```python
months=("January", "February", "March", "April", "May", "June")
```

```python
NPC=("Conan", 100), ("beit", 80), ("Valeria", 95)
```

```python
Python 3.4.2 Shell
File Edit Shell Debug Options
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
(GCC 4.8) on linux
type("tuple", "credit" or "license") for more information.
months=("January", "February", "March", "April", "May", "June")
print(months[0])
January
print(months[1])
June
print(months[6])
Traceback (most recent call last):
IndexError: tuple out of range
```

```python
>>> 
>>>File Edit Shell Debug Options
Python 3.4.2 (default, Oct 19 2014, 13:31:11)
(GCC 4.8) on linux
type("tuple", "credit" or "license") for more information.
NPC=("Conan", 100), ("beit", 80), ("Valeria", 95)
print(NPC[0])
```

与列表一样，命名元组中的项可以通过它们在数据中的位置进行索引。这些数据项都可以通过输入 `NPC` 作为整体被访问；或者可以通过它们的元组位置 `[]` 进行索引。

```python
months[]
months[5]
NPC[0]
```

然而，任何删除或添加元组的尝试都将导致错误。将显示 100。
