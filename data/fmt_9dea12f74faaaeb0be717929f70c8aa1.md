
10-2 `SayHello()` 函数输了预期的问语。

![](img/ec69aa1535cd82c135ee14abfc05048f_203_0.png)

注意，你必须在属性名称（在此模块中是 `SayHello()` 函数）之前加上模块名称 `MyLibrary`。这两个元素之间用点分隔。对导入的模块进行的任何调用都遵循相同的模式。

## 6. 输入 `MyLibrary.SayGoodbye("Sally")` 并按回车。

`SayGoodbye()` 函数输出预期的文本。

## 7. 关闭 Python Shell。

Python Shell 关闭。

# 使用 from...import 语句

`from...import` 语句的优点是可以只从模块中导入你需要的属性。这种区别意味着模块比 `import` 语句消耗的内存和其他系统资源更少。此外，`from...import` 语句使得模块稍微更容易使用，因为 `dir()` 等命令会显示更少的信息，或者只显示你实际需要。关键在于获取你想要的内容，而不是其他任何。以下步骤演示了如何使用 `from...import` 语句。

# 第 10 章：与模块交互 189

- 1. 打开 Python Shell。

你看到了 Python Shell 窗口。

- 2. 切换目录到下载的源代码目录。

参见“更改当前 Python 目录”侧栏中的说明。

- 3. 输入 `from MyLibrary import SayHello` 并按回车。

Python 导入了你在本章前面的“创建分组”部分中创建的 `SayHello()` 函数。现在只有这个特定的函数可以就绪。

如果你想这样做，仍然可以导入整个模块。完成此任务的两种技术是：创建一个导入列表（名称之间可以用逗号分隔，例如 `from MyLibrary import SayHello, SayGoodbye()`），或使用星号 (`*`) 代替特定的属性名称。星号充当通配符，导入所有内容。

![](img/ec69aa1535cd82c735ee14abfc05048f_204_0.png)

- 4. 输入 `dir(MyLibrary)` 并按回车。

Python 显示了错误信息，如图 10-3 所示。Python 仅导入了你明确请求的属性。这意味着 `MyLibrary` 模块不在内存中——只有你请求的属性在内存中。

图 10-3 来自... import 语句仅导入了你明确请求的项。

```
Python 3.3.4 Shell File Edit Debug Options Windows Help
Python 3.3.4 (v3.3.4:final762215e26, Feb 10 2014, 18:13:51) (MSC v.19)
600 64-bit [AMD64] on win32
>>> type("copyright": "credit" or "license()") for more information.
>>> os.chdir("Chapter10")
>>> from MyLibrary import SayHello
>>> dir(MyLibrary)
Traceback (most recent call last):
  File "<string>", line 1, in <module>
    dir(MyLibrary)
NameError: name 'MyLibrary' is not defined
>>>
Ln: 12 Col: 4
```

- 5. 输入 `dir(SayHello)` 并按回车。

你看到了与 `SayHello` 函数相关的属性列表，如图 10-4 所示。了解这些属性如何工作并不重要，但你将在书的后部分使用其中一些。

```
Python 3.3.4 (v3.3.4:ff6241e26, Feb 10 2014, 18:13:51) (MSC v.1)

600 64 bit (AMD64) on win32

>>> Type "copyright", "credits" or "license()" for more information.

>>> import os

>>> os.chdir('C\Chapter10')

>>> from MyLibrary import SayHello

>>> dir(MyLibrary)

Traceback (most recent call last):

  File "python31.py", line 1, in <module>

Error: name 'MyLibrary' is not defined

>>> dir(os)
```

图 10-4 使用函数获取关于你导入的属性的信息。

```
>>> ['annotations', 'call', 'class', 'closure', 'cod',
      'defaults', 'delattr', 'dict', 'dir', 'doc',
      'format', 'get', 'getattribute', 'getitem',
      'globals', 'hash', 'init', 'kwdefaults',
      'len', 'module', '__name__', '__ne__',
      '__name__', 'reduce', 'reduce_ex', 'repr',
      'setattr', 'sizeof', 'str', '__subclass__']
```

Ln: 13 Col: 4

- 6. 输入 `SayHello("Angie")` 并按回车。

`SayHello()` 输出预期的文本，如图 10-5 所示。

```
Python 3.3.4 (v3.3.4:ff6241e26, Feb 10 2014, 18:13:51) (MSC v.1)

600 64 bit (AMD64) on win32

Type "copyright", "credits" or "license()" for more information.

>>> import os

>>> os.chdir('C\Chapter10')

>>> from MyLibrary import SayHello

>>> dir(MyLibrary)

Traceback (most recent call last):

  File "python31.py", line 1, in <module>

NameError: name 'MyLibrary' is not defined

>>> dir(SayHello)
```>>> ['annotations', 'call', 'class', 'closure', 'cod',
      'defaults', 'delattr', 'dict', 'dir', 'doc',
      'format', 'get', 'getattribute',
      'globals', 'hash', 'init', 'kwdefaults',
      'len', 'module', '__name__', '__ne__',
      '__qualname__', 'reduce', 'reduce_ex', 'repr',
      'setattr', 'sizeof', 'str', '__subclass__']
>>> SayHello("Angie")
Hello Angie
```

Ln: 15 Col: 4

## 第 10 章：与模块交互

当你使用 `from...import` 语句导入属性时，不需要在属性名称前加上模块名称。这一特性使得属性更容易访问。

使用 `from...import` 语句会导致问题。如果两个属性名称相同，你只能导入其中一个。`import` 语句可以防止命名冲突，当有大量属性需要导入时这很重要。总之，使用 `from...import` 语句时必须小心。

- 7. 输入 `SayGoodbye("Harold")` 并按回车。

你只导入了 `SayGoodbye()` 函数，所以 Python 知道导入 `SayGoodbye()` 会显示错误信息。当你假设一个属性存在时，`from...import` 语句的选择性会导致问题。

- 8. 关闭 Python Shell。

Python Shell 窗口关闭。

# 在磁盘上查找模块

为了使用模块中的代码，Python 必须定位模块并将其加载到内存中。位置信息存储为 Python 中的路径。每当你请求 Python 导入模块时，Python 都会查看其路径列表中的所有文件。路径信息来自三个来源：

- 环境变量：第三章介绍了 环境变量，例如 `PYTHONPATH`，它告诉 Python 在磁盘哪里查找模块。

- 当前目录：在本章前面你发现可以更改当前的 Python 目录，以便程序定位任何模块。

- 默认目录：即使你没有定义任何环境，且当前目录没有可用的模块，Python 仍然可以在包含路径信息中的默认集中找到自己的库。

了解当前的路径信息是有帮助的，因为缺少路径会导致你的程序失败。以下步骤演示了如何获取路径信息：

- 1. 打开 Python Shell。

你看到了 Python Shell 窗口出现。

- 2. 输入 `import sys` 并按回车。

- 3. 输入 `for p in sys.path:` 并按回车。

Python 自动为你缩进下一行。`sys.path` 属性始终包含默认路径列表。

- 4. 输入 `print(p)` 并按回车。

你看到了路径信息的列表，如图 10-6 所示。你的列表可能与图 10-6 所示的不同，取决于你的版本、安装的 Python 版本以及你安装的功能。

![](img/ec69aa1535cd82c735ee14abfc05048f_207_0.png)

| C:\Windows\system32\lib3 |

| C:\Windows\system32\python3.zip |

| C:\Python33\DLL |

| C:\Python33\lib |

| C:\Python33 |

| C:\Python33\lib\site-packages |

`sys.path` 属性是可靠的，但可能并不包含 Python 能看到的所有路径。如果你没有看到需要的路径，始终可以检查另一个 Python 查找信息的地方。以下步骤显示了如何执行此任务：

- 1. 输入 `import os` 并按回车。

- 2. 输入 `os.environ['PYTHONPATH'].split(os.pathsep)` 并按回车。

当你定义了 `PYTHONPATH` 环境变量时，你会看到路径列表，如图 10-7 所示。然而，如果你没有定义该环境变量，你会看到错误信息。

注意，在这种情况下，`sys.path` 和 `os.environ['PYTHONPATH']` 属性都包含 `C:\BP4D\Chapter-10` 条目。`sys.path` 属性不包含 `()` 函数，

# 第 10 章：与模块交互 193

该示例使用了 for 循环来处理它。然而，环境变量 `['PYTHONPATH']` 属性并不包含 `split()` 函数，因此你可以使用它来创建一个路径列表。

你必须为 `split()` 提供一个值以便查找分割的项目列表。`os.pathsep`（一个单一、不变且已定义的常量变量）定义了当前平台的路径分隔符，因此你可以在任何支持 Python 的平台上使用相同的代码。

## 3. 关闭 Python Shell

Python Shell 关闭了。

![](img/ec69aa1535cd82c735ee14abfc05048f_208_0.png)

图 10-7：你必须单独请求有关环境变量的信息。

你还可以从 `sys.path` 中添加和删除项。例如，如果你想将第 9 章添加到模块列表中，你可以在 Python Shell 窗口中输入 `sys.path.append("C:\BP4D\Chapter09")` 并按回车键。当你再次列出 `sys.path` 内容时，你会发现添加了新项。同样，当你想要删除某个项（如第 9 章）时，输入 `sys.path.remove("C:\BP4D\Chapter09")` 并按回车键。

# 查看模块内容

Python 提供了几种查看模块内容的方法。开发者最常用的方法是使用 `dir()` 函数，它会告诉你该模块提供的属性。

194 第三部分：执行常见任务

查看本章前面的图 10-1。除了之前讨论的 `SayGoodbye()` 和 `SayHello()` 函数外，列表还有其他条目。这些属性是 Python 为你自动生成的。这些属性执行以下任务或包含以下信息：

- `__built__`：包含所有可以从该模块访问的内置属性的列表。Python 会自动为你添加这些属性。

- `__cached__`：告诉你与该模块关联的缓存文件的名称和位置。该位置（路径）相对于当前的 Python 目录。

- `__doc__`：输出模块的帮助信息，前提是你确实已经填充了它。例如，如果你输入 `os.__doc__` 并按回车键，Python 将输出与该库相关的帮助信息。

- `__file__`：告诉你模块的名称和位置。该位置（路径）相对于当前的 Python 目录。

- `__initializing__`：确定模块是否处于初始化过程中。通常情况下此属性返回值为 `False`。当你需要等待一个模块加载完成后再导入依赖于它的另一个模块时，此属性非常有用。

- `__loader__`：输出此模块的加载器信息。加载器是一段软件，用于获取模块并将其放入内存中，以便 Python 使用它。这是一个很少（如果从未）被用到的属性。

- `__name__`：告诉你模块的名称。

- `__package__`：此属性由导入系统内部使用，以便更容易加载和管理模块。你不需要担心这个属性。

发现你可以更深入地钻取属性可能会感到惊讶。输入 `dir(MyLibrary.SayHello)` 并按回车键。你会看到图 10-8 中的条目。

这些条目中的某些（如 `__name__`）也出现在模块列表中。然而，你可能对其他一些条目好奇。例如，你可能想知道 `__sizeof__` 是怎么的。获取额外信息的方法是输入 `help("__sizeof__")` 并按回车键。你会看到一些简略（但有用）的帮助信息，如图 10-9 所示。

第 10 章：与模块交互

![](img/ec69aa1535cd82c735ee14abfc05048f_210_0.png)

图 10-3：根据需要深入钻取以理解 Python 中使用的模块。

![](img/ec69aa1535cd82c735ee14abfc05048f_210_1.png)

图 10-9：尝试获取你想了解的属性的帮助信息。

```
>>> __sizeof__(..)
>>> __sizeof(_) -> int
size of object in memory, in bytes
>>>
```

196 第三部分：执行常见任务

如果你尝试访问该属性，Python 并不会崩溃。即使 shell 出现问题，你也可以启动一个新的。因此，检查模块的另一种方法是简化属性。例如，如果你输入 `MyLibrary.SayHello.__size__()` 并按回车键，你会看到 `SayHello()` 的大小（单位为字节），如图 10-10 所示。

```
Python 3.4 Shell
File Edit Debug Options Windows Help
Python 3.4 (v3.4.7-ff7261e26, Feb 10 2014, 18:13:51) [MSC v.1600 64 bit (AMD64)] on win32
Type "copyright, credits" or "license()" for more information.
>>> import MyLibrary
>>> dir(MyLibrary)
['__built__', 'SayHello', '__builtins__', '__cached__', '__doc', '__file', '__init__', '__loader__', '__name__', '__package__']
>>> dir(MyLibrary.SayHello)
['__annotations__', 'class', 'closure', '__code', '__defaults__', 'delattr__', '__dict__', '__doc__', '__format__', '__ge__', '__getattr__', '__getattribute___', '__globals__', '__hash', '__init__', '__kwarg__', 'lets', 'le', '__lt__', '__module', '__name__', '__new__', '__setattr__', '__sizeof__', '__reduce', '__reducees__', '__repr__', '__state__', '__qualname__', '__str__', '__subclasshook__']
>>> help("sizeof")
Help on built-in function
sizeof(...) -> int
size of object in memory, in bytes
>>> MyLibrary.SayHello.__size__()
|
```

图 10-10：使用属性将帮助你更好地感受它们的工作原理。

与其他编程语言不同，Python 还提供了原生库的源代码。例如，当你查看 `\Python33\Lib` 目录时，你会看到一系列 .py 文件，你可以毫无问题地在 IDLE 中打开它们。

## 第 10 章：与模块交互

199
