
![](img/ba40fbc39febe9db9a35785516d323a7_41_1.png)

# Python 模块

## 第 5 步

关闭命令提示符或终端并重新启动 IDLE Shell。现在当你输入：`import pygame` 时，模块将无问题地导入到代码中。你会发现，大多数从网上下载并复制的代码都会保留模块，除非在执行时通常是因为缺少模块而导致错误：

## 第 8 步

你的代码中可以导入多个模块。为了扩展你的示例，使用：

```python
import random

import math

for i in range(5):
    print(random.randint(1, 25))

print(math.pi)
```

![](img/ba40fbc39febe9db9a35785516d323a7_42_0.png)

## 第 6 步

模块包含了在你的代码中实现某些结果所需的额外代码，正如我们之前实验过的样。例如：

```python
import random
```

引入来自随机数生成器的代码。你可以使用此模块创建类似的内容：

```python
for i in range(10):
    print(random.randint(1, 25))
```

![](img/ba40fbc39febe9db9a35785516d323a7_42_1.png)

## 第 9 步

结果是一串随机数字，后面跟是来自 Math 模块的 Pi 值。你也可以使用 `import from` 命令从模块中提取某些函数，例如：

```python
from random import randint

for i in range(5):
    print(random.randint(1, 25))
```

![](img/ba40fbc39febe9db9a35785516d323a7_42_2.png)

## 第 7 步

这段代码在保存并执行时将显示从 1 到 25 的十个数字。你可以尝试显示更多，或者来自更大或更小的范围。例如：

```python
import random
```
```python
for i in range(25):
    print(random.randint(1, 100))
```

![](img/ba40fbc39febe9db9a35785516d323a7_42_3.png)

## 第 10 步

这有助于创建更简洁的编程方法。你也可以使用 `import*`。然而，这通常被认为是资源的浪费，尽管它确实可以运行。最后，模块可以作为别名导入：

```python
import math as m
```

```python
print(m.pi)
```

当然，添加注释有助于告诉其他人里面有什么。

![](img/ba40fbc39febe9db9a35785516d323a7_42_4.png)

# 数据处理

> “软件开发最重要的方面是清楚你想要构建什么。” —— Bjarne Stroustrup (C++ 之父)

数据就是一切。你可以显示、控制、添加、删除和创建。在接下来的页面中，我们将查看如何创建列表、元组、多维列表；以及如何使用它们创建有趣且的程序。然后你可以学习如何使用时间函数、写入文件。

| | |
|---|---|
| 46 | 列表 |
| 48 | 元组 |
| 50 | 字典 |
| 52 | 字符串分割与合并 |
| 54 | 字符串格式化 |
| 56 | 时间 |
| 58 | 打开文件 |
| 60 | 写入文件 |
| 62 | 异常 |
| 64 | Python 图形 |

### 列表

列表是最常见的数据类型之一。列表仅仅是项的集合，或者如果你愿意，也可以单独访问。列表在 Python 中非常方便。列表可以包含字符串、整数以及变量。你甚至可以在列表中包含函数。

- 列表是数据值的序列。通过等号创建你的列表，然后使用方括号来分隔项；注意字符串使用引号。

```python
numbers = [1, 4, 7, 21, 98, 156]
mystical_creatures = ["Unicorn", "Balrog", "Vampire", "Minotaur"]
```

- **第 3 步** 你可以使用负号或索引访问列表中的项，从第一个项到第二个项，以此此类推。尝试引用列表中不存在的项（如 `[10]`）将报错：

```python
numbers[-1]
mystical_creatures[-4]
```

![](img/ba40fbc39febe9db9a35785516d323a7_45_0.png)

- **第 4 步** 一旦你定义了列表，就可以通过数字调用每一项。列表的第一个项从 0 开始，然后是 1、2、3 等以此此类推。例如：

```python
numbers[3]
```

切片类似于索引，但你可以通过冒号获取多个项。这些项将以列表的形式返回。

```python
numbers[1:3]
```

将输出 4 和 7，即第 1 和第 2 项。注意返回的值不包含第二个索引（位置），如 `[3]` 将返回 4 和 7。调用列表中的第三个（在这种情况下为 21）。

> 输入 "copyright" 或 "license" 获取更多信息。

> 输入 "copyright" 或 "license" 获取更多。

`mystical_creatures = ["Unicorn", "Balrog", "Vampire", "Minotaur"]`

```python
Python 3.4.2 (default) Oct 19 2014, 13:31:13
>>> type "copyright" or "license" for more information.
>>> numbers = [1, 4, 7, 21, 98, 156]
>>> numbers[3]
21
>>> mystical_creatures = ["Unicorn", "Balrog", "Vampire", "Minotaur"]
>>> mystical_creatures[0]
'Unicorn'
>>> mystical_creatures
>>> mystical_creatures[-4]
'Balrog'
```

![](img/ba40fbc39febe9db9a35785516d323a7_45_1.png)

## 第 5 步

你可以更新现有列表中的项，删除项甚至合并列表。例如：

```python
everything = numbers + mythical_creatures
```

然后构建的列表是：

```python
everything
```

![](img/ba40fbc39febe9db9a35785516d323a7_46_0.png)

## 第 8 步

你可以通过在 Shell 中输入 `dir(list)` 来查看对列表进行的操作。输出是所有方法，例如 `insert` 和 `pop` 用于在特定位置添加和删除项。在索引 4 处插入 62：

```python
numbers.insert(4, 62)
```

将其删除：

```python
numbers.pop(4)
```

```python
Python 3.4.2 Shell
>>> Edit Shell Debug Help Break
>>> Python 3.4.2 (default, Oct 19 2014, 13:31:11) [GCC ...]
>>> type("critical" or "license") for more information.
>>> name = "David Howard"
>>> age = str(44)
>>> name + age
'DavidHoward44'
```

## 第 10 步

项的删除可以通过两种方式完成。第一种通过数字：

```python
del numbers[7]
```

或者，通过名称：

```python
mystical_creatures.remove('Nessie')
```

在此此，你可以创建一个程序。

# 元组 (Tuples)

元组与列表（lists）非常相似。然而，列表可以被删除、更新或更改某些部分，而元组则保持不变。这被称为不可变性（immutable），它们是存储固定数据项完美选择。

### 不变元组

使用元组的原因取决于程序的意图。在冒险游戏中，当非玩家角色（NPC）的名称被特殊存储时，它们也被用于，例如：

- **第 1 步** 元组的创建方式与列表相同，但你使用圆括号而不是方括号。例如：

```
months=("January", "February", "March", "April", "May", "June")
```

- **第 2 步** 就像列表一样，命名元组中的项可以通过它们在数据范围中的位置进行索引：

```
months[0]
months[5]
```

然而，任何尝试添加或删除元组的尝试都会在 Shell 中导致错误。

- **第 3 步** 你可以将分组的元组创建为包含多组数据的列表。例如，这里有一个名为 NPC（非玩家角色）的元组，包含角色名称及其冒险游戏中的战斗评分：

```
NPC=(("Conan", 100), ("Belit", 80), ("Valeria", 95))
```

![](img/ba40fbc39febe9db9a35785516d323a7_47_0.png)

![](img/ba40fbc39febe9db9a35785516d323a7_47_1.png)

- **第 4 步** 你可以通过在 Shell 中输入 NPC 来整体访问这些数据项中的每一个；或者可以通过索引访问 NPC 列表中的单个元组：

```
NPC[0]
将显示 100。
```

![](img/ba40fbc39febe9db9a35785516d323a7_47_2.png)

![](img/ba40fbc39febe9db9a35785516d323a7_47_3.png)

## 第 5 步

注意，当在列表中引用多个元组时，索引方式与常规不同。你可能会认为角色 Valeria 的 95 分评分应该是 `NPC[4]`，但事实并非如此：

## 第 8 步

现在将元组解包为两个对应的变量：

```python
(name,combat_rating)=NPC[2]
```

你可以通过输入 `name, combat_rating` 来检查值。

```python
Python 3.4.2
Edit Edit Debug Options Windows Help
Python 3.4.2 (default, Oct 19 2014, 13:31:13)
[GC 4.9] on linux
Type "copyright", "credits" or "license" for more information.
>>> NPC[2]=('Conan', 100), ('Belit', 80), ('Valeria', 95)
>>> (name,combat_rating)=NPC[2]
>>> name
'Conan'
```

## 第 6 步

这这意味着计数遵循以下规则：

- 0 1
- 0 2
- 0 1
- 1 0

## 第 9 步

记住，和列表一样，你可以使用从数据列表倒数的数字来索引元组。对于我们的示例，使用包含多个数据项的元组，你可以这样获取 Valeria：

```
NPC[2][0]
```

你可以想象，当你有大量的元组数据要处理时，这会有点困惑。

```python
Python 3.4.2
Edit Edit Debug Options Windows Help
Python 3.4.2 (default, Oct 19 2014, 13:31:13)
[GC 4.9] on linux
Type "copyright", "credits" or "license" for more information.
>>> NPC[2]=('Conan', 100), ('Belit', 80), ('Valeria', 95)
>>> NPC[2][0]
'Conan'
>>> NPC[2][1]
'Belit'
>>> NPC[2][2]
'Valeria'
```

## 第 10 步

元组可以创建一种特色解包功能，数据项存储在元组中。创建第一个包含两个项（名称和战斗评分）的元组：

```
NPC=('Conan', 100)
numbers=(23.3, 45.2, 109.3, 56.7, 99)
```

整数可以转换为浮点数。输出最高和最低，使用：

```python
Python 3.4.2
Edit Edit Debug Options Windows Help
Python 3.4.2 (default, Oct 19 2014, 13:31:13)
[GC 4.9] on linux
Type "copyright", "credits" or "license" for more information.
>>> max(numbers)
109.3
>>> min(numbers)
23.3
```
