
You must type a whole number!

Try again (y/n)? y

>>> Type a whole number. 5.5

You must type a whole number!

Try again (y/n)? y

>>> See you next time!

>>>

```
图 9-10：
内部异常处理器提供了次级输入。
```

## 9. 按 `Ctrl+C`、`Cmd+C` 或另一个组合键中断程序。

应用程序结束，如图 9-11 所示。注意该消息来自外部异常。在步骤 7 和 9 中，用户通过按下中断键结束了程序。然而，程序使用了两个异常处理器来解决这个问题。

```
Python 3.3.4 Shell

File Edit Shell Debug Options Windows Help

Python 3.3.4 (v3.3.4:ff66215e426, Feb 10 2014, 18:13:51) [MSC v 1600 64 bit (AMD64)] on win32

Type "copyright", "credits" or "license()" for more information.

============================ RESTART =

>>>

>>> Type a whole number. Hello

You must type a whole number!

Try again (y/n)? y

>>> Type a whole number. 5.5

You must type a whole number!

Try again (y/n)? y

>>> See you next time!

>>>
```

图 9-11：
外部异常处理器提供了主要输入。

---

# 第二部分：交流技巧

## 异常处理

到为止，本章中的示例已经对异常进行了响应。当错误发生时，程序提供了错误处理支持。然而，在某些情况下，你可能不知道如何在程序设计过程中处理错误。可能你在某个层级无法处理错误，并需要将其传递给其他层处理。简而言之，在某些情况下，程序必须生成异常。这种行为被称为抛出（raising）或触发（throwing）异常。后续章节将描述抛出异常的具体场景。

## 在特殊情况下抛出异常

本节示例演示了如何抛出一个简单的异常——这不需要特殊操作。以下步骤简单地创建并处理该异常。

## 第 9 章：处理错误

本节的示例展示了创建自定义异常的快速方法。要完成这项任务，你必须创建一个以异常为起点的类。为了让操作更简单易行，本示例创建了一个基于 `ValueError` 异常提供功能的异常。与本章前一节“向调用者传递错误信息”中所示的方法相比，这种方法的优势在于，它能精确地告诉任何人 `ValueError` 异常是什么；此外，它让修改后的源异常更容易使用。此示例也出现在可下载源代码中，命名为 `CustomException.py`。

- 1. 打开一个 Python 文件窗口。

你会看到一个可以在其中输入代码的编辑器。

- 2. 在窗口中输入以下代码 —— 每行后按回车键：

```python
class CustomValueError(ValueError):
    def __init__(self, arg):
        self.strerror = arg
        self.args = {arg}
try:
    raise CustomValueError("Value must be within 1 and 10.")
except CustomValueError as e:
    print("CustomValueError Exception!", e.strerror)
```

此示例基本上复制了本章“向调用者传递错误信息”节示例的功能。然而，它将相同的错误同时放在 `strerror` 和 `args` 中，以便开发者可以访问其中任何一个（就像通常那样）。

代码开始创建一个 `CustomValueError` 类，该类使用 `ValueError` 异常类作为起点。`__init__()` 函数提供了创建该类新实例的方法。可以将该类类为蓝图，而根据蓝图构建的实例。

注意，`strerror` 属性的值是直接赋值的，但 `args` 是以数组的形式接收的。`args` 成员通常包含所有异常值的数组，因此即使 `args` 像这里所示只包含一个值，这仍然是标准操作程序。

使用该异常的代码比直接修改 `ValueError` 要简单得多。你只需要在同一行中调用 `raise`，并带上异常名称以及你想要传递的参数即可。

![](img/ec69aa1535cd82c735ee14abfc05048f_192_0.png)

# 178 第二部分：交流技巧

- 3. 选择运行（Run）：运行模块（Run Module）。

你会看到一个 Python Shell 窗口打开。应用程序显示了字母序列以及字母数字，如图 9-14 所示。

图 9-14：Python 3.3.4 Shell

![](img/ec69aa1535cd82c735ee14abfc05048f_193_0.png)

## 使用 finally 子句

通常，你希望以一种不会导致应用程序崩溃的方式处理发生的任何异常。然而，有时你无法采取任何措施来解决问题，程序程序将会崩溃。在这种情况下，你的目标是让应用程序优雅地崩溃，这意味着关闭文件以防用户丢失数据，并执行其他此类任务。任何你可以使数据和系统的损害降至最低的措施，都是处理崩溃应用程序数据至关重要的部分。

`finally` 子句是崩溃应用程序策略的一部分。你使用此子句执行任何所需的最后任务。通常，`finally` 子句非常短，并且只使用可能成功而不会产生进一步问题的子句。关闭文件、注销用户并执行其他必要任务，然后在糟糕的事情发生（如系统完全故障）之前让应用程序崩溃，这是至关重要的。考虑到这一必要性，以下步骤展示了使用 `finally` 子句的简单示例。此示例也出现在可下载源代码中，命名为 `ExceptionWithFinally.py`。

- 1. 打开一个 Python 文件窗口。

你会看到一个可以在其中输入示例代码的编辑器。

- 2. 在窗口中输入以下代码 —— 每行后按回车键：

```python
import sys
try:
    raise ValueError
    print("Raising an exception.")
except ValueError:
    print("ValueError Exception!")
    sys.exit()
finally:
    print("Taking care of last minute details.")
print("This code will never execute.")
```

在此示例中，代码抛出了 `ValueError` 异常。当这种情况发生时，`except` 子句按常执行。`sys.exit()` 代码意味着应用程序在处理异常后退出。在这种特定情况下，应用程序无法恢复，但应用程序通常会结束，因此最后的 `print()` 函数调用将不会执行。

`finally` 子句始终执行。无论是否发生异常都无关。你放在此块中的代码需要是你想要执行的通用代码。例如，在处理文件时，你将关闭代码放在此块中，以确保数据不会因为留在内存中而不是写入磁盘而损坏。

- 3. 选择：运行模块（Run Module）。

你会看到一个 Python Shell 窗口。应用程序显示了异常消息和 `finally` 子句消息，如图 9-15 所示。`sys.exit()` 调用阻止了任何其他代码的执行。

![](img/ec69aa1535cd82c735ee14abfc05048f_194_0.png)

Python 3.3.4 Shell
File Edit Debug Options Windows Help
Python 3.3.4 (v3.3.4:FT6e241e426, Feb 10 2014, 18:13)

# 180 第二部分：交流技巧

- 4. 在 ValueError 前前加上井号将其注释掉，如下：

```python
## import ValueError
```

这部分展示了如何使用库。

- 5. 保存文件。

- 6. 选择运行模块（Run Module）。

你会看到一个 Python Shell 窗口。应用程序显示了异常消息和 `finally` 子句消息，如图 9-15 所示。

![](img/ec69aa1535cd82c735ee14abfc05048f_195_0.png)

## 第三部分 执行常见任务

![](img/ec69aa1535cd82c735ee14abfc05048f_196_0.png)

## 第 10 章：与模块交互

## 本章内容

- 组织你的代码
- 从外部源向应用程序添加代码
- 在磁盘上定位库
- 查看库代码
- 获取并阅读库文档

在本部分，你将

* 访问 Python 模块。
* 切片处理字符串以满足输出需求。
* 创建你想管理的对象列表。
* 使用集合组织数据。
* 开发类以实现代码的可复用。

# 184 第三部分：执行常用任务

库代码是自包含的且文档完备（至少在大多数情况下是如此）。某些开发者可能觉得他们永远不需要查看库代码，从某种意义上说，他们是正确的——你不需要为了使用库代码而查看它。不过，你可能想要查看库代码，以确保你理解代码是如何运作的。此外，库代码可以教你一些你原本可能无法发现的新编程技术。因此，查看库代码是可选的，但它会很有帮助。

你唯一需要学会如何做的事情就是获取和使用 Python 库文档。本章将展示如何在创建应用程序的过程中获取和使用库文档。

## 创建代码分组

将相似的代码片段组合在一起是非常重要的，这可以使代码更易于使用、修改和理解。随着应用程序的增长，管理单个文件中的代码会变得越来越困难。在某个时刻，代码将变得无法管理，因为文件变得太大，任何人都无法处理。

![](img/ec69aa1535cd82c735ee14abfc05048f_199_0.png)

在这个特定情况下，“代码”一词被宽泛使用。代码分组包括：

- 类 `Classes`
- 函数 `Functions`
- 变量 `Variables`
- 可执行代码 `Runnable code`

模块内类、函数、变量和可执行代码的集合被称为属性。模块拥有你可以通过属性名称访问的属性。本章的后续章节将详细讨论模块访问是如何工作的。

可执行代码实际上可以用 Python 以外的语言编写。例如，发现用 C/C++ 而不是 Python 编写的模块是常见的。开发者使用可执行代码是为了让 Python 应用程序更快、更节省资源，并更好地利用特定平台的资源。然而，使用可执行代码的缺点会降低应用程序的可移植性（在其他平台上运行的能力），除非你为每个平台都提供了可执行模块。

![](img/ec69aa1535cd82c735ee14abfc05048f_199_1.png)

## 第 10 章：与模块交互

你想要支持的。此外，双语言应用程序可能难以维护，因为你必须拥有精通应用程序中所使用的每一种语言的开发者。

创建模块最常用的方法是定义一个单独的文件，其中包含你想要从应用程序其他部分分离的代码。例如，你可能想创建一个打印例程，应用程序在多处使用它。该打印例程的设计并不是为了独立运行，而是作为整个应用程序的一部分。你想要将其分离出来，是因为应用程序在许多地方使用它，而且你可能可能在另一个应用程序中使用相同的代码。重用代码的能力是创建模块理由列表排名靠前的原因。

为了便于理解，本章的示例使用了一个常用模块。该模块没有做任何神奇的事情，但它演示了处理模块的原理。打开 Python 窗口并创建一个名为 `MyLibrary.py` 的新文件。在列表 10-1 中输入代码并将其保存到磁盘。（该模块也以 `MyLibrary.py` 出现在下载源码中。）

## 列表 10-1：一个简单的演示模块

```
def SayHello(Name) :
    print("Hello \ Name)
    return
def Goodbye(Name) :
    print("Goodbye \ Name)
    return
```

示例代码包含两个名为 `SayHello()` 和 `Goodbye()` 的函数。在这两种情况下，你都使用一个 `Name` 来打印，函数会在屏幕上打印该名称以及对你的问候。此时，函数将控制权交还给调用者。显然，你通常会创建更复杂的函数，但这些函数对于本章的目的来说很好。

## 导入模块

为了使用模块，你必须导入它。Python 将模块代码放在与应用程序其他部分分开的地方。这种方法确保了模块是独立的。这种方法是快速的。

# 186 第三部分：执行常用任务

你有两种方法来导入：

- `import` 语句：当你想要导入整个模块时使用 `import` 语句。这种方法非常快速，但它会消耗更多的内存。
- `from ... import` 语句：当你想要选择性导入模块时使用 `from` 语句。这种方法节省内存，但增加了复杂性。

现在你对如何导入模块有了更好的了解，是时候详细查看了。后续章节将帮助你通过以下步骤处理模块：

## 更改当前目录

| 步骤 | 这种操作可以更改 目录。 |
| :--- | :--- |
| **1. 打开 Python 窗口。** | 你看到 Python 窗口。 |
| **2. 输入 `import os` 并按回车。** | 你需要使用 `os` 库。 |
| **3. 输入 `os.chdir("C:\BEF4D\Chapter10")` 并按回车。** | 你现在可以更改目录。 |

## 第 10 章：与模块交互

## 使用 `import` 语句

`import` 语句是导入模块最常用的方法。这种方法很快，并确保整个模块可以使用。以下步骤帮助你开始使用 `import` 语句：

- 打开 Python 窗口。你看到 Python 窗口出现。
- 切换到源码目录。参见“更改当前目录”侧边栏中的说明。
- 输入 `import MyLibrary` 并按回车。Python 导入了你在“创建分组”部分创建的 `Library.py` 文件。整个库现在可以使用。

重要的是，Python 还会 `pycache__` 子目录中创建模块的缓存。当你第一次导入 `MyLibrary` 后，查看你的源码目录，你会看到一个 `pycache__` 目录。如果你想对模块进行更改，必须删除此目录。否则，Python 将继续使用未更改的缓存文件，而不是你的源码。

![](img/ec69aa1535cd82c735ee14abfc05048f_202_0.png)

- 4. 输入 `dir(MyLibrary)` 并按回车。你会看到模块内容的列表，包含了 `SayHello()` 和 `Goodbye()` 函数，如图 10-1 所示。（关于其他条目的讨论出现在本章的“查看模块内容”章节。）

Python 3.3.4 Shell
File Edit Shell Debug Options Help
Python 3.3.4 (v3.3.4:BF7621e426, Feb 10 2014, 18:13:51) [MSC v -
1600 64 bit (AMD64) on win32
Type "copyright", "credits" or "license" for more information.
>>> os.chdir()
>>> os.chdir('C:\BEF4D\Chapter10')
>>> import MyLibrary
>>> dir(MyLibrary)
['SayGoodbye', 'SayHello', '__builtins__', '__cached__', '__doc__', '__file__', '__init__', '__loader__', '__name__', '__package__']
>>> _ Ln: 8 Col: 4

Figure 10-1：一个目录列表显示：
Python 从模块中导入了两个函数。

# 188 第三部分：执行常用任务

## 5. 输入 `MyLibrary.SayHello("Josh")` 并按回车。

`SayHello()` 函数输出预期的文本，如 10-2 所示。

```
Python 3.3.4 Shell

File Edit Shell Debug Windows Help

Python 3.4 (u3.3.4:7ff6241e426, cached _, Feb 10 2014, 18:13:51) [MSC v

-1600 64 bit (AMD64)]
>>> Type "Copyright", "Credit" or "license" for more information.
>>> import os
>>> os.chdir("C\Chapter10")
>>> import MyLibrary
>>> dir(MyLibrary)
>>> SayGoodbye('SayHello', 'builtins', '_cached_', 'doc',
>>> '_file_', '_initializing_', '_loader_', '_name',
>>> '_package_'
>>> MyLibrary.SayHello("Josh")
>>> Josh
>>> 
```
