
使用元组的原因取决于程序的意图。在冒险游戏中，当非玩家角色（NPC）的名称被特殊存储时，它们也被用于，例如：

### 第 1 步
元组的创建方式与列表相同，但你使用圆括号而不是方括号。例如：

```
months=("January", "February", "March", "April", "May", "June")
```

### 第 2 步
就像列表一样，命名元组中的项可以通过它们在数据范围中的位置进行索引：

```
months[0]
months[5]
```

然而，任何尝试添加或删除元组的尝试都会在 Shell 中导致错误。

### 第 3 步
你可以将分组的元组创建为包含多组数据的列表。例如，这里有一个名为 `NPC`（非玩家角色）的元组，包含角色名称及其冒险游戏中的战斗评分：

```
NPC=(("Conan", 100), ("Belit", 80), ("Valeria", 95))
```

![](img/ba40fbc39febe9db9a35785516d323a7_47_0.png)

![](img/ba40fbc39febe9db9a35785516d323a7_47_1.png)

### 第 4 步
你可以通过在 Shell 中输入 `NPC` 来整体访问这些数据项中的每一个；或者可以通过索引访问 `NPC` 列表中的单个元组：

```
NPC[0]
将显示 100。
```

![](img/ba40fbc39febe9db9a35785516d323a7_47_2.png)

![](img/ba40fbc39febe9db9a35785516d323a7_47_3.png)

第 5 步 注意，当在列表中引用多个元组时，索引方式与常规不同。你可能会认为角色 Valeria 的 95 分评分应该是 `NPC[4]`，但事实并非如此：

第 8 步 现在将元组解包为两个对应的变量：

```python
(name,combat_rating)=NPC[2]
```

你可以通过输入 `name`, `combat_rating` 来检查值。

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

第 6 步 这意味着计数遵循以下规则：

- 0 1

- 0 2

- 0 1

- 1 0

第 9 步 记住，和列表一样，你可以使用从数据列表倒数的数字来索引元组。对于我们的示例，使用包含多个数据项的元组，你可以这样获取 Valeria：

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

第 10 步 元组可以创建一种特色解包功能，数据项存储在元组中。创建第一个包含两个项（名称和战斗评分）的元组：

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

# 字符串的分割与合并

在 Python 中处理数据时（尤其是来自用户输入的数据），你无疑会遇到长字符串。Python 编程中有一项实用的技能是能够分割这些字符串以提高可读性。

### 字符串理论

你已经查看过一些函数，如 `.insert`、`.remove` 和 `.pop`，但也有可以应用于字符串的函数。

- 步骤 1 字符串函数工具箱中的主要工具是 `.split()`。通过它，你可以根据获取的参数分割一个数据字符串。例如，这里有一个包含三个项目的字符串，每个项目都由空格分隔：

- 步骤 3 注意 `text.split()` 部分带有括号、引号以及后续的引号。空格是分隔符，表示每个列表项都由空格分隔。同样，CSV（逗号分隔值）由逗号分隔，因此你会使用 `text="January,February,March,April,June" months=text.split(",")`

```
Python 3.4.2 (default) Oct 19 2014, 13:31:11
[SEC 4.9.1] on Linux
>>> type="credit" or "license" for more information.
>>> name="Daniel Hannah Emma"
>>> name.split()
['Daniel', 'Hannah', 'Emma']
```

![](img/ba40fbc39febe9db9a35785516d323a7_51_0.png)

```
Python 3.4.2 (default) Oct 19 2014, 13:31:11
[SEC 4.9.1] on Linux
>>> type="credit" or "license" for more information.
>>> name="January,February,March,April,June"
>>> name.split(",")
['January', 'February', 'March', 'April', 'June']
```

- 步骤 2 现在让我们字符串转换为列表并充分地分割内容。`names=text.split(", ")`。然后输入新列表查看这三个项目。

- 步骤 4 你之前见过如何将一个字符串分割为单独列表，每个列表使用一个名称：`name="David"`

返回的值为 `['D', 'a', 'v', 'i', 'd']`。在通常情况下这似乎没用，但例如在创建一个拼字游戏时它可能很有用。

```
Python 3.4.2 (default) Oct 19 2014, 13:31:11
[SEC 4.9.1] on Linux
>>> type="credit" or "license" for more information.
>>> name="David"
>>> name.split()
['D', 'a', 'v', 'i', 'd']
```

![](img/ba40fbc39febe9db9a35785516d323a7_51_1.png)

# 字符串的分割与合并

- 步骤 5 `.split()` 的反面是 `join`，在其中你将在字符串中有单独的项目，并可以根据需要将它们全部合并成一个单词或仅仅是项目的组合。例如：

```
alphabet="".join(["a","b","c","d","e"])
print(alphabet)
```

这将在 Shell 中显示 'abc'。

- 步骤 8 与 `.split` 合并一样，分隔符不必须是空格，它也可以是逗号、连字符或任何你喜欢的：

```
colors=["Red","Green","Blue"]
col=",".join(colors)
print(col)
```

![](img/ba40fbc39febe9db9a35785516d323a7_52_0.png)

- 步骤 6 随后可以使用 `.join()` 处理你从步骤 4 中创建的分割后的名称，再次组合字母：

`name="".join(name)`

你将字符串合并了回去，并通过 `join` 函数返回了名称。

- 步骤 9 有些可以应用于字符串的有趣函数，例如 `.capitalize()` 和 `.title()`。例如：

```
title="con the cimmerian"
title.capitalize()
title.title()
```

![](img/ba40fbc39febe9db9a35785516d323a7_52_1.png)

- 步骤 7 当你有一个想要合并成字符串的列表时，使用 `join` 函数是一个很好的例子：

```
list=["Conan","raised","his","sword","and","struck","demon"]
text=".".join(list)
```

注意 `join` 函数之前的引号（在步骤 6 中没有引号）。你也可以对字符串使用 `in` 和 `not in` 逻辑运算符。这些允许你检查字符串是否包含（或不包含）字符序列。

```
message="Have a nice day"
"nice" in message
"bad" not in message
```

![](img/ba40fbc39febe9db9a35785516d323a7_52_2)

### 格式字符串

在处理数据、创建列表和对象时，你可能经常想要结果。Python 3 可以很容易地格式化字符串，之前的版本会让事情变得复杂。

### 格式化

从 Python 3 开始，字符串格式化变得更加简洁，使用了带括号的 `.format()` 函数。这比之前的版本方法更好。

### 步骤 1 Python 中的基础格式化是将每个变量调用到字符串中：

```
name="Conan"
print("the barbarian hero of Age is {}".format(name))
```

### 步骤 2 记得使用两组括号的 `.format()` 函数，因为你在其中包含了变量并打印。你可以在单个函数中包含多个格式化情况：

```
name="Conan"
place="Cimmeria"
print("hailed from the North land known as {}".format(name, place))
```

### 步骤 3 你也可以混合混合整数：

```
number=10000
print("{} was a mercenary, and thief stole gold from a merchant.".format(name, number))
```

![](img/ba40fbc39febe9db9a35785516d323a7_53_0.png)

- 步骤 5 有趣的是，你可以使用格式化函数引用列表。你可以在名称前面放置星号：

![](img/ba40fbc39febe9db9a35785516d323a7_54_0.png)

- 步骤 8 你可以用同样的方式打印用户输入的内容：

```
name=input("'s your name?")
print("Hello, {}".format(name))
```

![](img/ba40fbc39febe9db9a35785516d323a7_54_1.png)

- 步骤 6 列表中的索引同样适用于字符串格式化。你可以根据其位置索引每个项目（从 0 到无论有多少个）：

```
numbers=[1, 4, 7]
print("More numbers: {}, {}, {}".format(*numbers))
```

![](img/ba40fbc39febe9db9a35785516d323a7_54_2.png)

- 步骤 9 你可以扩展这个简单的代码示例来显示人的输入的第一个列表：

```
name=input("What's your name?")
print("Hello, {}".format(name))
print("The first list of your name is a {}")
```

![](img/ba40fbc39febe9db9a35785516d323a7_54_3.png)

- 步骤 7 正如你所怀疑的，你可以在列表中混合字符串和整数，以便用 `.format()` 函数调用：

```
characters=["Conan", "Belit", "Valeria", 19, 27, 20]
print("{} is {} years old. Whereas {} is {} years old.".format(*characters))
```

![](img/ba40fbc39febe9db9a35785516d323a7_54_4.png)

- 步骤 10 你可以调用一对列表并在同一个 print 函数中单独引用它们。回看步骤 7 的代码，你可以对其进行修改：

```
names=["Conan", "Belit", "Valeria"]
ages=[25, 21, 20]
Creating lists. 现在你可以调用每个列表，以及单个项目：
print("{0[0]} is {1[0]} years old. Whereas {0[1]} is {1[1]} years old.".format(names, ages))
```

![](img/ba40fbc39febe9db9a35785516d323a7_54_5.png)

# 日期和时间

在处理数据时，你可能经常想要打印结果。例如，你可能想要时间戳或查看多久。获取时间归益于 Time 模块。

### 时间

Time 模块包含帮助你检索当前时间、读取字符串以及格式化时间的函数。

- 步骤 1 如果你需要导入 Time 模块。它是内置于 Python 3 的。一旦导入，你就可以用简单的命令调用当前时间：

```
import time
time.asctime()
```

![](img/ba40fbc39febe9db9a35785516d323a7_55_0.png)

- 步骤 3 你可以看到时间呈现的结构：

```
time.local()
输出为: *time_struct_tm(tm_year=2017, tm_mon=9, tm_day=7, tm_hour=9, tm_min=6, tm_sec=13, tm_wday=3, tm_yday=250, is_dst=0); 显然取决于你的当前时间而不是编写的时间。
```

![](img/ba40fbc39febe9db9a35785516d323a7_55_1.png)

- 步骤 2 该函数被分为九个元组，像任何其他元组一样被划分为索引元组，并在下方所示。

- 步骤 4 Time 模块有许多内置函数。最常用的是 `.strftime()`。通过它，你可以呈现广泛的参数，将时间元组转换为字符串。例如，显示当前的星期几可以使用：

| 索引 | 字段 | 值 |
|---|---|---|
| 0 | 四位年份 | 2016 |
| 1 | 月份 | 1 到 12 |
| 2 | 日期 | 1 到 31 |
| 3 | 小时 | 0 到 23 |
| 4 | 分钟 | 0 到 59 |
| 5 | 秒 | 0 到 61 (60 是闰秒) |
| 6 |  | 0 到 6 (0 是周一) |
| 7 | 一年中的第 | 1 到 366 (儒日) |
| 8 | 夏令时 | -1, 0, 1, -1 表示库定义 DST |

![](img/ba40fbc39febe9db9a35785516d323a7_55_2.png)

# 日期与时间

## 第 5 
这意味着你可以将各种函数整合到代码中，例如：

```
time.strftime("%Y")
time.strftime("%H%M")
time.strftime("%d")
time.strftime("%H")
time.strftime("%Y-%m")
```

## 第 8 
你在第一部分的末尾已经看到，在上面的代码中，你可以在 Python 中格式化特定的事件。取上面的代码并通过更改进行稍微修改：

```
start_time.time(c)
```

然后是：

```
endtime.time()-start_time
```

![](img/ba40fbc39febe9db9a35785516d323a7_56_0.png)

```
Python 3.4.2 (defaults, Oct. 19, 2014, 12:31:11)
(C) copyright, the Python Software Foundation, except
Type "credits" 或 "license" 获取更多信息。
>>> time.strftime("%Y")
2014
>>> time.strftime("%H%M")
1231
>>> time.strftime("%d")
19
>>> time.strftime("%B")
October
>>> time.strftime("%m")
10
>>> time.strftime("%H")
12
>>> time.strftime("%Y-%m")
2014-10
>>> ]
```

## 第 6 
注意最后几项，带有 %H 和 %H%M，你也可以将这些视为最后条目中的小时和分钟，将它们输入为 %H%M 不会在 Shell 中正确显示时间。你可以轻松通过以下代码验证这一点：
