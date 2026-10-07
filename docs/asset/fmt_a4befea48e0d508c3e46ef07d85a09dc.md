
## 统计项在列表中出现的次数

你可以使用列表的 `count()` 方法来统计项在列表中出现的次数。与其他列表方法一样，其语法简单：

```
listname.count(x)
```

将 `listname` 替换为列表名，将 `x` 替换为你查找的值。如果项不在列表中，它将返回 0。

## 查找项的索引

Python 提供了 `index()` 方法，返回项在列表中的位置数字。语法为：

```
classname.index(x)
```

将 `classname` 替换为列表名，将 `x` 替换为你查找的值。如果项不在列表中，将会发生错误。

为了避免这种情况，可以使用 `if` 语句查看项是否在列表中后再获取索引。代码如下：

```python
grades = ["C", "B", "A", "D", "C"]
## 决定要查找什么。
look_for = "B"
## 查看项是否在列表中。
if look_for in grades:
    # 如果在列表中，获取并显示索引。
    print(str(look_for) + " 在索引 " + str(grades.index(look_for)))
else:
    # 如果不在列表中，不要尝试获取索引。
    print(str(look_for) + " 不在列表中.")
```

## 复制列表

如果你需要对列表的副本进行操作，以免修改原始列表，请使用 `.copy()` 方法。例如，下面的代码与之前的代码相似，不同在于我们没有反转原始列表的顺序，而是创建了列表的副本并反转了它。打印每个列表的内容可以看到第一个列表仍然保持原始顺序，而第二个列表被反转了：

```python
## 创建一个字符串列表
names = ['Zara', 'Lupe', 'Hong', 'Alberto', 'Jake']
## 创建列表的副本。
backward_names = names.copy()
## 反转副本。
backward_names.reverse()
## 打印列表。
print(names)
print(backward_names)
```

```
['Zara', 'Lupe', 'Hong', 'Alberto', 'Jake']
['Jake', 'Alberto', 'Hong', 'Lupe', 'Zara']
```

表 7-1 总结了你在本章中学到的方法。正如你将在接下来的章节中看到的，这些方法适用于其他类型的迭代对象。

### 表 7-1 列表操作方法

| 方法 | 功能 |
|---|---|
| `append()` | 在列表末尾添加一个项 |
| `clear()` | 移除列表中的所有项，使其变为空 |
| `copy()` | 创建列表的副本 |
| `count()` | 统计元素在列表中出现的次数 |
| `extend()` | 将一个列表的项追加到另一个列表的末尾 |
| `index()` | 返回元素在列表中的索引数字（位置） |
| `insert()` | 在特定位置向列表插入一个项 |
| `pop()` | 从列表中移除一个元素，并提供该项的副本，你可以将其存储在变量中 |
| `remove()` | 从列表中移除一个项 |
| `reverse()` | 反转列表中元素的顺序 |
| `sort()` | 按升序对列表排序 |
| `sort(reverse=True)` | 按降序对列表排序 |

## 什么是元组？谁在乎呢？

除了列表之外，Python 还支持一种名为元组 `tuple` 的数据结构。有些人把它读作“two-pull”。有些人把它读得和 `couple` 押韵。但它的拼写不是 `tuple` 也不是 `to`，所以我们最好的猜测是它读作“two-pull”。

无论如何，这个奇怪的名字——元组仅仅是一个不可变的列表。换句话说，元组是一个列表，但在定义之后你无法更改它。它就像一个常量。

创建元组的语法与创建列表的语法相同，只是你不需要使用方括号。你必须使用括号，如下：

```python
prices = (29.95, 9.98, 4.95, 79.98, 2.95)
```

你在表 7-1 中学会的用于列表的大多数技术和方法都不适用于元组，因为它们被用于修改列表中的内容，而元组是不可修改。不过，你可以使用 `len` 获取元组的长度，如下：

```python
print(len(prices))
```

你可以使用 `.count()` 来查看某个项在元组中出现的次数。例如：

```python
print(prices.count(4.95))
```

你可以使用 `in` 来查看某个值是否存在于元组中，如下所示代码所示：

```python
print(4.95 in prices)
```

如果元组包含 4.95，则返回 `True`，否则返回 `False`。

如果项存在于元组中，你可以获取它的索引数字。但是，如果项不存在于元组，你会得到错误。你可以先使用 `in` 检查项是否存在，然后再检查它的索引数字，如果不存在，你可以在代码中返回 `-1` 作为一个无意义的值：

```python
look_for = 12345
if look_for in prices:
    position = prices.index(look_for)
else:
    position = -1
print(position)
```

你可以遍历元组中的项，并使用格式化字符串以你喜欢的任何格式显示它们。这个示例显示了每个项都带有一个美元符号，并且分位保留两位数字：

```python
## 遍历并显示元组中的每个项。
for price in prices:
    print(f"${price:.2f}")
```

使用示例元组运行此代码的输出如下：

```
$29.95
$9.98
$4.95
$79.98
$2.95
```

你不能使用这种语法更改元组中项的值：

```python
prices[1] = 234.56
```

你会得到一条信息为 `TypeError: 'tuple' object does not support item assignment` 的错误消息。这条信息告诉你是，不能使用赋值运算符 `=` 来更改元组中项的值。因为元组是不可变的，一旦创建，你就无法更改它的内容。

## 集合

Python 还提供了集合 `sets`，它们是唯一元素的集合。与列表不同，集合没有顺序，这意味着你不能通过索引数字访问项。你使用大括号定义集合，如下：

```python
fruits = {'apple', 'banana', 'cherry'}
```

如果你向集合添加已项，集合不会改变，因为集合只存储唯一值。你可以使用 `.add()` 方法向集合添加新项：

```python
fruits.add('orange')
```

要一次性添加多个项，可以使用 `.update()` 方法：

```python
fruits.update(['grape', 'kiwi'])
```

如果你想从集合中删除一个项，可以使用 `.remove()` 或 `.discard()` 方法。如果项不存在，`.remove()` 将抛出错误，而 `.discard` 则不会。

你可以使用 `in` 运算符检查项是否在集合中：

```python
if 'apple' in fruits:
    print("Apple is in the set!")
```

## 第8 章：处理更大的代码块

- 创建你自己的函数
- 在函数中包含注释
- 查看如何向函数传递信息
- 从函数返回返回值

创建一个函数非常简单。如果你想获得一些实践经验，请在 `.py` 文件中操作。

要创建一个函数，从新的一行开始以 `def` 开头，后面跟一个空格，然后跟上你任选的名称，再跟一对括号。最后在这一行的末尾加一个冒号。例如，要创建一个名为 `hello()` 的简单函数，输入：

```python
def hello():
```

这是一个函数，但它什么都不做。要让该函数执行某些操作，你必须在随后的行中编写 Python 代码。为了确保新代码在函数“内部”，请对这些每行都进行缩进。

> 记住，缩进在 Python 中至关重要。没有没有任何命令可以标记函数的结束。`def` 行下方所有缩进的行都是该函数的一部分。第一行未缩进的行与 `def` 行对齐。

要让这个函数执行某些操作，请在 `def` 下方写一行缩进的代码。我们先让函数打印 `hello`。因此，在 `def` 行下方缩进输入 `print('Hello')`。现在你的代码看起来像这样：

```python
def hello():
    print('Hello')
```

如果你现在运行这段代码，屏幕上不会发生任何明显的变化。这是因为函数内部的代码在函数被调用之前不会执行的。你调用自己的函数的方法与调用内置函数相同：通过编写调用函数名称的代码，包括末尾的括号。

例如，如果你正在跟着操作，按回车键添加一个空行，然后输入 `hello()` 并确保它没有缩进。所以它看起来是：

```python
def hello():
    print('Hello')
hello()
```

当代码执行时，你应该能看到输出，就是 `Hello` 这个单词。

![](img/be36b4e9a8416f1ae2a353bd745f71cb_105_0.png)

图 8-1：编写并调用一个名为 `hello()` 的简单函数。

### 为函数添加注释

代码中的注释总是可选的。但习惯上是将 `def` 语句下的第一行作为 `docstring`，用于描述函数的功能。通常在第一行的括号右侧也会添加一个以 `#` 符号开头的注释。因为它们只是注释，所以对代码的执行没有任何影响。

```python
def hello(): # Practice function
    """ A docstring describing the function """
    print("Hello, world!")
```

**图 8-2：** 添加了一些注释的示例函数。

### 向函数传递信息

你可以向函数传递信息以便其处理。要做到这一点，对于要传递给函数的每一个信息，在 `def` 语句中输入一个参数名称。你可以为参数使用任何名称，只要它以字母或下划线开头，后跟着字母、下划线或数字即可。

你提供的任何作为参数的名称仅局部于该函数。变量在函数内部工作方式的术语是“局部作用域” `local scope`，这意味着变量的作用域留在函数内部，而不向外延伸。

假设你想让 `hello` 函数对任何使用它的人说 `Hello`。要将信息传递到函数并使用，你需要执行以下操作：

- 在括号内放入一个参数名称，作为传入信息的占位符。
- 在函数内部，使用该名称来处理传递的信息。

例如：

```python
def hello(x):
    """ A docstring describing the function """
    print('Hello ' + x)
```

最好使用更具描述性的名称，例如 `user_name`：

```python
def hello(user_name):
    """ A docstring describing the function """
    print('Hello ' + user_name)
```

如果一个函数有参数，但在调用时没有传递它们，会报错。例如：

```python
def hello(user_name): # Practice function
    """
    docstring describing the function """
    print('Hello ' + user_name)

hello()
```

错误会像这样：

```
TypeError: hello() missing 1 positional argument: 'user_name'
```

创建一个函数非常简单。如果你想获得一些实践经验，请在 `.py` 文件中进行操作。
