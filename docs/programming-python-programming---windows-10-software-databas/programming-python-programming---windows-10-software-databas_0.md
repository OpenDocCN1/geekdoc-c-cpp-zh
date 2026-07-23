# 编程：Python 编程 - Windows 10 软件与数据库 (Java, Html, C++, C语言编程、初学者编程指南、PHP、网站设计)

















## 引言

知道如何开始计算机编程是一个真正的挑战。大多数人对于如何编写计算机代码或编写计算机程序从从何开始几乎无所知。Python 是一种容易学习的语言，它的功能远超简单的编程。

它是一种通用语言，最早出现于 20 世纪 80 代，信你不信，它是以蒙提派森剧（Monty Python）命名的。它被广泛用于，从测试微芯片到为世界上一些最大的网站提供支持，再到构建视频游戏。Python 是一门小型的语言，接近英语，并包含了数百个第三方库。

由于 Python 与英语相似，因此很容易阅读。它在标点符号方面也遵循非常严格的规则，这意味着不像某些计算机语言，你的代码不会充斥着烦人的大括号 `{ }`，这些大括号会阻碍阅读。Python 还包含 `PEP 8`，这是一套告诉每个 Python 开发者如何格式化代码的规则，这意味着你总是知道该做什么、在哪里应该换行，并帮助你阅读其他 Python 脚本，无论它们是谁写的。

Python 已经存在了 20 多年，关于它的代码多。它也是一种开源语言，意味着任何人都可以获取、读取并修改它供自己使用。有很多 Python 社区小组，用户可以去那里寻求帮助或只是加入通用的 Python 聊天。

在书中，我想谈谈 Python 可以做什么，以及如何在你的 Windows 10 PC 上让它运行起来，以及如何使用它。这适用于初学者或更高级的用户，我希望每个人都能从书中获益。

## 为 Python 配置你的 Windows 10 环境

所以，你想学习如何在 Windows 10 电脑上使用 Python。你需要做的第一件事是配置你的 Windows 环境，即你的电脑，并为使用该编程语言做好准备。

### 你需要什么

- 一台 Windows 10 台式电脑或笔记本电脑
- Python
- Cygwin
- 一个文本编辑器

让我们一步来看：

### 在 Windows 上安装 Python

为了让 Python 环境在你的 Windows 电脑上运行，你需要完成几件事：

- 下载并安装 Python
- 使用 Windows Python 安装
- 安装包管理器

### 下载并安装 Python

- 首先，你需要下载正确的安装包，请访问 `http://www.python.org/download/windows/`
- 点击 Individual Releases（独立发布）
- 你现在将进入一个版本列表，选择最新的一个
- 确保你下载的版本与你运行的 Windows 版本对应，以及是 32 位还是 64 位。
- 如果你运行的是 Mozilla 浏览器，点击“另另文件为”。如果你使用的是 Internet Explorer，点击“运行”。
- Python 安装程序将打开，选择谁可以在你的系统上访问 Python——是你或系统上的任何人。点击“下一步”。
- 现在你需要选择安装 Python 的目录——保持默认选择并点击“下一步”。
- 勾选接受安装选项并点击“下一步”。
- Python 现在将开始在你的系统上安装。等待其完成，然后点击“完成”。

### 使用 Windows Python 安装

- 点击开始菜单并寻找 Python v.* ——取决于你安装的版本
- 你将看到安装了几个项目：
    - IDLE – Python GUI – 类似于命令行 Python 提示符，但它有一个图形界面
    - Module Docs – 一个关于已安装模块的帮助文件
    - Python (命令行) – 类似于服务器提示符
    - Python Manuals – 手册，以备不时
    - Uninstall Python – 希望你永远不需要使用

在可以通过命令行提示符直接访问 Python 之前，我们需要设置 Windows PATH 变量，我们下一步完成。

### 安装包管理器

你很快就会发现你需要安装未包含在 Python 标准发行版中的模块。为了实现这一点，我们需要安装一个包管理器来安装新包。在这一部分，我们使用 EasyInstall，但之后我还会教你如何安装 Cygwin，以便你可以选择。

- 访问 `http://peak.telecommunity.com/DevCenterEasyInstall`
- 点击 安装 “Easy Install”
- 右键点击链接的 `setup.py` 并选择“链接另存为”或“保存目标为”
- 完成后，在 PC 上找到该 `.py` 文件并双击运行它。它将在 Python 内部运行并完成安装




为了设置 `PATH` 变量，让 Windows 10 知道去哪里查找 Python：

*   右键点击`我的电脑`
*   选择`属性`
*   在下一个界面中，点击`高级系统`
*   在下一个界面中，点击`环境变量`
*   我假设你在安装 Python 时，选择了仅为你当前用户安装，而不是为系统中的所有人安装——点击“用户变量”框下的 `Path`
*   点击`编辑`
*   在下一个界面中，找到变量值框，并将光标置于表示最后一条条目的分号（`;`）之后
*   在框中输入以下内容作为最后一条条目，并**不要**忘记在末尾包含分号（`;`）—— `C:\Python25\Scripts;`
*   连续点击三次`确定`以退出`系统属性`
*   现在通过点击`开始`、`运行` 并输入 `cmd` 来打开命令提示符。点击`确定`
*   在下一个框中输入 `easy_install BeautifulSoup` –这将安装 `BeautifulSoup` 模块 – 对你想要使用的任何其他模块重复此操作，它们将会被安装
*   当你回到命令提示符时，输入 `Python` 然后按回车。
*   输入 `import BeautifulSoup`（或任何其他模块的名称）
*   将出现另一个提示，且不会显示任何错误信息。我们现在知道已经正确设置了 `PATH` 变量，并且 `EasyInstall` 已正确安装。
*   你现在也知道如何安装新包了！

在你的电脑上安装 Python 和 `EasyInstall` 的就到此了。接下来是 Cygwin。

## 安装 Cygwin

这并不那么简单

*   访问 `http://cygwin.com/http://cygwin.com/`
*   点击左侧菜单上的`Install Cygwin`
*   点击 `setup-x86.exe` 然后运行它

`Cygwin` 是一个非常有用的程序，因为它可以从互联网下载其他程序并为你安装。你需要提供有关你的互联网连接的信息，尽管在在整个设置过程中，你大多数情况下都可以接受默认设置。

一旦完成，你将看到一个下载站点列表。它们都是完全相同的，所以只需从列表中任选一个并点击`下一步`即可。

现在你会收到一个`升级`警告——这仅适用于那些从旧版本 `Cygwin` 升级的用户。如果你是第一次安装它，请忽略此消息。

现在你将看到要下载的软件列表。你需要三个包——`openssh`、`git` 和 `curl`。在网站的搜索中输入每个包的名称，当包出现时，点击`Skip`（跳过）。这将确保安装的是最新版本——对每个包执行此操作。

一旦这三个包准备好安装，`Cygwin` 会通知你你需要安装其他包作为依赖项。这意味着，如果你想使用某个特定的包（例如 `A`），而 `A` 需要另一个名为 `B` 的包才能正常运行，`Cygwin` 将知道并询问是否可以同时安装包 `B` 和 `A`。

当此消息出现时，只需点击`下一步`，`Cygwin` 将开始下载并安装你请求的三个包以及它们所有的依赖项。这可能需要一段时间，尽管取决于你互联网连接的速度。在你的屏幕上，你将看到三个独立的进度条——当中间名为 `TOTAL` 的进度条满满时，`Cygwin` 就完成了。

如果你请求 `Cygwin` 在桌面上创建一个图标，它将执行该操作，你会看到一个名为 `Cygwin Terminal` 的快捷方式。这是你运行 Python 代码以及通过 `Cygwin` 下载包时将使用的图标。

点击它，一个终端窗口将会出现，我们就可以开始使用它了。首先，我们需要找出实际上安装了哪些包，因此在命令提示符下输入单词 `which`。

将一个包列表，并且很可能向你显示你安装的所有 `Cygwin` 包，但它可能不会显示 Python 本身。这没关系，因为你没有使用 `Cygwin` 安装 Python。现在你需要告诉 `Cygwin` 寻找 `Python`，你通过输入以下命令来实现：

```bash
$ echo "PATH=$PATH:/cygdrive/c/Python32" >> .bash_profile
```

确保你输入的是你正在使用的 Python 版本——如果你安装了不同版本，请将 `Python32` 替换为正确的名称。你只需要执行这一步；在此之后，终端将始终找到 Python。

`Cygwin` 已安装并设置完毕，最后一步是设置你的文本编辑器。我为你提供 `Sublime Text` 的说明——如果你使用不同的编辑器，请确保遵循其附带的安装说明。请注意，`Microsoft Word` **不是**文本编辑器；它是一个文字处理程序，因此不能用于此。

## 安装 Sublime Text

`lime text` 是一个非常强大的文本编辑器，它非常有用，而且还有一个永不过期的免费试用版。

*   访问 `http://www.sublimetext.com/` 并下载安装程序
*   运行它

虽然 `Sublime Text` 不是免费的，但你可以根据需要一直进行试用。不过，我建议，如果你喜欢它并用它来编写许多程序，请购买完整版的许可——对你使用的任何软件都如此。

## 检查一切工作正常

现在一切都安装好了，是时候检查它们是否工作正常了。任何程序员编写的第一个程序都是现在著名的“Hello World!”程序。这个程序的作用是在终端上输出文本，是检查一切是否按预期运行的好方法。在你的终端中输入：

```bash
$ python -c 'print("Hello World!")'
```

如果这有效，打开 `Sublime Text`，我们将写一个程序。在文本编辑器中输入以下内容：

```python
#!/usr/bin/env python
print("Hello, World!")
```

将其保存到你的主目录，确保它进入 `C:\win` 并命名为 `hello.py`。打开你的终端并输入：

```bash
$ chmod+x hello.py
$ ./hello.py
```

你应该会在屏幕上看到“Hello, World!”。如果是，你就准备好学习如何在 Windows 10 上使用 Python 了。

## 熟悉 Python

在你的 Windows 桌面上，你应该看到一个 Python 图标。双击它，这将打开交互式解释器。你将在这里输入单个命令并查看结果。它是实验命令作用的好方法，它也是一个非常有用的工具。输入：

```python
>>> x = 3
>>> print x
3
>>>
```




# 变量

还记得我们在在本章开始创建的那个简单程序吗？`x` 是一个变量，我们在将其打印到屏幕之前，将它与一个数字（在本例中为 3）相关联。变量是任何编程语言中最基础的概念，是我们在处理数据时用于存储值的工具。

我们写的代码 `x = 3` —— 是一个语句——语句执行特定的任务，而在这种情况下，任务是将值 (3) 赋值给变量 (`x`)。在 Python 中，这被称为“绑定”（binding），是一个非常重要的概念。

Python 中的变量名几乎可以可以是任何内容，只要你遵循以下简单规则：

* 它必须只包含 ASCII 字符、下划线和数字——你不能使用任何其他符号或空格
* 它不能以数字开头
* 它不能是保留关键字列表中的任何单词。

## 保留关键字

* `and`
* ` as`
* `assert`
* `break`
* `class`
* `continue`
* `def`
* `del`
* `elif`
* `else`
* `except`
* `exec`
* `finally`
* `for`
* `from`
* `global`
* `if`
* `import`
* `in`
* `is`
* `lambda`
* `not`
* `or`
* `pass`
* `print`
* `raise`
* `return`
* `try`
* `while`
* `with`
* `yield`

这些关键字都不能用于任何文件名或程序名，因为它们被 Python 保留了。由于 Python 是一种动态语言，这些关键字未来可能会发生，因此为了保持更新，你可以通过在终端输入以下内容定期检查当前的关键字列表：

```python
#!/usr/bin/python
## keywords.py
import sys
import keyword
print "Python version: ", sys.version_info
print "Python keywords: ", keyword.kwlist
```

[基础变量类型](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

我们现在知道变量是 Python 的基本概念，变量拥有的所有值类型也是。这些被称为数据类型（data-types），表示存储数据的所有方式。“类型”一词在计算机编程中有其特殊含义，指的是对不同类型的对象进行特定分类的方法。每个对象都有类型，最基本的数据类型是：

[数字](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

### 整数

整数是整数，理论上，它们是从正无穷到负无穷范围内的任何整数。范围受计算机的限制，但在 Python 中，绝对最大大小仅限于一个因素——你计算机的内存大小。

Python 使用两种整数类型——整数（integer）和长整数（long integers），后者是超过特定长度的整数。

### 浮点数

计算机在处理整数或整数方面非常擅长。浮点数是指小数点后带有数字的数字，例如 5.2 或 -8.1。

整数可以存储为浮点数——你只需要在写它时添加一个小数点即可，例如 1.0 或 9.0。浮点数的处理速度要慢得多，因为计算机认为它们稍微复杂一些。

在较新版本的 Python 中，如果你尝试用一个整数除以另一个整数，你将得到一个意料之外的结果，例如：

```python
>>> 7/2
3
```

为了得到正确的结果，必须将其中一个整数转换为浮点数：

```python
>>> 7.0/2
3.5
```

[字符串](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

字符串仅仅是一段文本，Python 不会区分包含单个字符还是包含整块字符或文本的字符串。Python 包含两种不同的字符串类型——基础字符串（basic）和 Unicode 字符串。

基础字符串类型用于在数字序列或字节序列中存储文本，每个字符仅占用一个字节。只有当你确定文本中包含 ASCII 值时，才应该使用它们。它们还用于存储二进制数据，通常被称为字节字符串（byte-strings）。

Unicode 字符串使用 Unicode 标准在内部存储文本。这些使用起来稍微复杂一点，因为当你读取或保存它时，必须知道存储代码时使用的编码。下面是关于如何使用每种类型的概述：

**基础字符串** – 你通过单引号或双引号括起相关文本向程序中添加字符串，例如：

```python
x = 'This is a string'
y = "And so is this."
```

你还可以使用三引号包含带有换行符或跨越几行的字符串，如下：

```python
x = """This string
goes over multiple lines.
So it includes line breaks."""

y = '''This string uses single quotes.
But it is still multi-line.
As you might have guessed.'''
```

你还可以通过转义字符包含特殊字符，如引号字符或换行符。Python 使用 UNIX 惯例使用反斜杠键作为转义字符。例如：

```python
## 变量 x 是一个字符串，包含
### 单行换行符
x = '\n'
### 变量 y 包含一个转义引号
### 而不是
### 终止字符串的引号
y = 'Don\'t worry about quotes'
```

**原始字符串** – 如果你不想使用转义键，可以使用原始字符串（raw strings）。为了表示这一点，你可以在字符串前加 `r`。由于原始字符串用于某些表达式，例如 Windows 路径，它们不能以反斜杠结尾。

```python
z = r'
```

**Unicode 字符串** – 这些字符串包含内部表示，允许将文本存储为文本。实际上，计算机通过文本知道哪些字符。

Unicode 字面量可以通过在字符串前面加 `u` 包含在程序中。如果你不在开头指定编码，你只能使用 ASCII 字符，但 Python 将你的数据存储为 Unicode 而非字节字符串。

Unicode 的引号和转义规则与字节字符串相同：

```python
x = u'A unicode string'
y = u'''A multi-line
string.'''

y = ru"""This is a
raw, multi-line
unicode string !!!
```

你可以通过指定编码来强制解释器在 Unicode 和字节字符串之间进行相互转换，但你可能会遇到以下错误之一：

* `UnicodeEncodeError`
* `UnicodeDecodeError`

其中任何一个错误都会导致你的程序崩溃。当这种情况发生时，通常是因为你尝试“隐式”转换的字符串包含默认编码（通常是 ASCII）无法表示的字符。

[其他有用值](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

还有一些非常有用的值：

* `None` - 在其他编程语言中通常视为 Null，它代表“无”。
* `True` - 真的布尔值。
* `False` - 假的布尔值。

你会在编程生涯中经常看到这些值，通过编写以下内容可以将它们包含在你编写的任何程序中：

```python
x = None
y = True
z = False
```

[更复杂的数据类型](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)




当你在处理更复杂的信息时，你可能想要将某些数据分组。Python 有许多概念可以让你实现这一点，包括列表推导式、生成器和迭代器等。对这些数据进行分组的基本方法是使用所谓的“数据结构”。这些对象会将所有值存储在一起，在 Python 中，你可以创建自定义的数据结构。不过，它也有四种内置的数据结构。用于存储数据的对象被称为容器。

以下数据类型可以对它们执行执行许多不同的操作，其中许多操作已经内置在数据类型中（称为方法）。

### [列表 List](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

这用于按顺序存储一组项目。你可以随时向其添加或删除项目，对它们进行排序，或在列表中搜索特定值。你甚至可以从一个空列表开始，随着过程不断添加，或者使用一个已经预填充好的列表。你列表中包含的项目可以是任何其他对象，也包括其他列表。这意味着你可以拥有许多不同的列表以及嵌套列表，并使用它们创建一个复杂的结构——这些列表作为构建块非常有用。

当你写一个列表时，它应该带有方括号，每个项目之间用逗号隔开：

● # `w` 是一个空列表
● `w = []`
● # `x` 只有一个成员
● `x = [3.0]`
● # `y` 是一个数字列表
● `y = [1, 2, 3, 4, 5]`
● # `z` 是一个字符串列表
### 以及其他列表
● `z = ['first', [], 'second', [1, 2, 3, 4], 'third']`

你可以通过“索引”访问列表上的任何内容。该索引必须是一个表示项目在列表中位置的整数。第一个位置是零。可以通过在变量后放置包含索引的方括号对变量进行索引。

如果你尝试访问尚未创建的位置，将在屏幕上收到一个 `IndexError`。如果你想从列表末尾访问，可以使用负索引。`-1` 是你列表上的最后一个位置，接着是 `-2`、`-3` 等：

```python
>>> x = [1, 2, 3, 4, 5]
>>> print x[0]
1
>>> print x[4]
5
>>> print x[-1]
5
>>> print x[-5]
1
>>> print x[10]
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
IndexError: list index out of range
```

### [元组 Tuples](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

元组与列表相似，它们都存储顺序信息。然而，与列表不同，元组在创建后无法更改。解释器确切地知道元组成员的类型和长度，因此，处理元组时比处理列表更高效。元组可以被切片或索引，但不能被更改，你会在 Python 中到处“隐式地”遇到它们。一个例子是返回多个值的函数将把这些值作为元组返回。

要创建一个元组，你使用圆括号而不是方括号：

```python
>>> x = (1, 2, 3,4)
>>> x
(1, 2, 3, 4)
>>> x[0]
1
>>> x = (1,)
>>> x
(1,)
>>> x[0]
1
>>> x = ()
>>> x
()
>>> x[0]
Traceback (most recent call last):
  File "<stdin>", line 1, in ?
IndexError: tuple index out of range
```

即使元组中只有一个成员，你仍然需要添加逗号。例如，如果你只放一个 `1`，那么 `t` 不会被归类为元组，而 `1,` 则是。如果你需要创建一个空元组，可以使用以下内容之一：

● `()`
● `tuple ()`

### [字典 Dictionaries](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

字典是最实用且灵活的数据类型之一，Python 是基于它们构建的。字典会存储数据，但它们使用“键”。这意味着你可以使用该键查找特定的数据片段。与其他数据类型一样，Python 内置了语法允许你创建字典：

```python
>>> x = {'key1': 'value1', 'key2': 'value2'}
>>> print x
{'key2': 'value2', 'key1': 'value1'}
```

可以通过索引检索值，就像你处理列表一样并使用相同的语法。然而，你使用的不是位置，而是键：

```python
>>> x = {'key1': 'value1', 'key2': 'value2'}
>>> print x['key1']
value1
```

字符串不必用作键，相反，任何对象都可以被用，只要它是不可变的（即它不会改变）。这是元组派上用场的另一个好例子：

```python
>>> attemptedKey = {}
... Traceback (most recent call last):
  File "<stdin>", line 1, in ?
TypeError: unhashable type
```

### [集合 Sets](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

集合是最实用且灵活的数据类型之一，Python 是基于它们构建的。字典会存储数据但它们使用键。这意味着你可以使用该键查找特定的数据片段。与其他数据类型一样，Python 内置了语法允许你创建字典：

```python
>>> x = {'key1': 'value1', 'key2': 'value2'}
>>> print x
{'key2': 'value2', 'key1': 'value1'}
```

值可以通过索引检索，就像你处理列表一样并使用相同的语法。然而，你使用的不是位置，而是键：

```python
>>> x = {'key1': 'value1', 'key2': 'value2'}
>>> print x['key1']
value1
```

字符串不必用作键，相反任何对象都可以被用，只要它是不可变的（即它不会改变）。这是元组派上用场的另一个好例子：

```python
>>> attemptedKey = {}
... Traceback (most recent call last):
  File "<stdin>", line 1, in ?
TypeError: unhashable type
```

（注：提供的文本包含重复章节和碎片化句子。）

### 条件 Conditions
当你在处理更复杂的信息时，你可能想要将某些数据分组。Python 有许多概念可以让你实现这一点，包括列表推导式、生成器和迭代器等。对这些数据进行分组的基本方法是使用所谓的“数据结构”。这些对象会将所有值存储在一起，在 Python 中，你可以创建自定义的数据结构。不过，它也有四种内置的数据结构。用于存储数据的对象被称为容器。

### 布尔运算符 Boolean operators
你可以使用 `and` 和 `or` 来构建复杂的表达式。例如：

● `name = "John"`
● `age = 23`
● `if name == "John" and age == 23:`
● `print "Your name is John, and you are also 23 years old."`

● `if name == "John" or name == "Rick":`
● `print "Your name is either John or."`

### "in" 运算符
这可以用于检查特定对象是否存在于容器中，例如列表：

```python
if name in ["John", "Rick"]:
    print "Your name is either John or Rick."
```

### 'is' 运算符
`is` 运算符不匹配变量值；相反，它匹配实例本身。一个例子：

```python
x = [1,2,3]
y = [1,2,3]
print x == y # 输出 True
print x is y # 输出 False
```

### "not" 运算符
如果你在布尔运算符前面使用 `not`，它将反转它：




● `print not False` # 输出 True

● `print (not False) == (False)` # 输出 False

# 循环

Python 有两种不同类型的循环——`For` 和 `While`。“for” 循环会遍历特定的序列，例如：

● `primes = [2, 3, 5, 7]`
● `for prime in primes:`
● `print prime`

它们能够遍历使用 `range` 和 `xrange` 函数的数字序列。这两者的区别在于，前者会返回一个包含特定范围数字的新列表，而后者返回一个迭代器，后者的效率高得多。

● ` # 输出数字 0,1,2,3,4
● `for x in xrange(5):` # 或 `range(5)`
● `print x`

● ` # 输出 3,4,5`
● `for x in xrange(3, 6):` # 或 `range(3, 6)`
● `print x`

● ` # 输出 3,5,7`
● `for x in xrange(3, 8, 2):` # 或 `range(3, 8, 2)`
● `print x`

“while” 循环在特定布尔条件满足时会重复，例如：

● ` # 输出 0,1,2,3,4`
● `count = 0`
● `while count < 5:`
● `print count`
● `count += 1` # 这等于 `count = count + 1`

## "break" 和 "continue" 语句

这两者的区别在于，“break” 用于退出 “for” 循环，而 “continue” 会跳过当前的文本块并返回到 “for” 或 “while” 语句。几个例子：

● ` # 输出 0,1,2,3,4`
● `count = 0`
● `while True:`
● `    print count`
● `    count += 1`
● `    if count >= 5:`
● `        break`

● ` # 只输出奇数 - 1,3,5,7,9`
● `for x in xrange(10):`
● `    # 检查 x 是否为偶数`
● `    if x % 2 == 0:`
● `        continue`
● `    print x`

# 函数

函数是将代码划分为有用块的一种极非常有用的方法。这允许你组织代码，使其更具可读性，以便重复使用，并在此过程中节省时间。函数也是定义接口的一种方式，以便程序员能够共享他们的代码。

我们知道 Python 将使用块，它是一段编写如下形式的代码：

● `block_head:`
● `    第一行块内容`
● `    第 2 行块内容`
● `    ...`

在块行是某些 Python 代码或另一个块的情况下，块头以以下格式书写——`block_keyword block_name(argument1, argument2...)`。你已经知道一些块关键字——`if`、`for`、`while` 等。我们使用关键字 `def` 在 Python 中定义一个函数，后面紧跟的是函数名：

```python
def my_function():
    print "Hello From My Function!"
```

函数还可以接收参数——这些是从调用者传递给函数的变量。例如：

```python
def my_function_with_args(username, greeting):
    print "Hello, %s , From My Function!, I wish you %s"%(username, greeting)
```

## 执行代码

函数还可以通过关键字 `return` 返回一个值，例如：

```python
def sum_two_numbers(a, b):
    return a + b
```

## 如何在 Python 中调用函数

你只需要编写函数名，后面跟着 `()`。在括号内放入任何所需的参数。例如：

```python
## 打印一个简单的问候
my_function()
# # 输出 - "Hello, John Doe, From My Function!, I wish you a great year!"
my_function_with_args("John Doe", "a great year!")
### 在此行之后 x 将持有值 3!
x = sum_two_numbers(1,2)
```

# 类和对象

对象仅仅是将变量和函数封装进单个实体中。每个对象都从类中获取它的函数和变量，而类仅仅是用于创建对象的模板。一个基础类看起来如下：

```python
class MyClass:
    variable = "blah"

    def function(self):
        print "This is a message inside the class."
```

为了将此类分配给特定对象，你需要这样做：

```python
myobjectx = MyClass()
```

现在，名为 `MyObjectx` 的变量持有一个来自 `MyClass` 的类对象。它包含了在 `MyClass` 类内部定义的变量和函数。

## 访问对象变量

为了访问名为 `MyObject` 的新对象内部的变量，你需要这样做：

```python
myobjectx.variable
```

因此，以下将产生字符串“blah”：

```python
print myobjectx.variable
```

可以创建许多相同的对象，即它们具有相同的函数和变量。然而，每个对象都是独立的副本。例如，如果你使用 `MyClass` 定义了一个不同的对象，可以使用如下代码：

```python
myobjecty = MyClass()
myobjecty.variable = "yack"
```

然后打印两个值：

```python
print myobjectx.variable  # 输出 "blah"
print myobjecty.variable  # 输出 "yack"
```

## 访问对象函数

如果你想访问对象函数，将使用与访问变量类似的符号：

```python
myobjectx.function()
```

打印该消息将得到“This is a message inside the class.”

# 模块和包

所有的 Python 模块都是具有 .py 扩展名的文件，实现了一组函数。通过 `import` 命令从另一个模块导入模块。

第一次加载模块时，它会被初始化。下次导入它时，不会再次加载。

如果你想从 URL 读取数据，你会这样做：

```python
## import urllib
urllib.urlopen(...)
```

## 内置模块

有两个函数在探索模块时非常有用——`dir` 和 `help`。你可以使用 `dir` 函数查看每个模块中实现的函数：

```python
>>> import urllib
>>> dir(urllib)
['ContentTooShortError', 'FancyURLopener', 'MAXFTPCACHE', 'URLopener', '__all__', '__builtins__', '__doc__', '__file__', '__name__', '__package__', '__version__', '_ftperrors', '_get_proxies', '_get_proxy_settings', '_have_ssl', '_hexdig', '_hextochr', '_hostprog', '_is_unicode', '_localhost', '_noheaders', '_nportprog', '_passwdprog', '_portprog', '_queryprog', '_safe_map', '_safe_quoters', '_tagprog', '_thishost', '_typeprog', '_urlopener', '_userprog', '_valueprog']
```

当你定位到模块中想要使用的函数时，可以在解释器中使用 `help` 函数来获取关于它的更多信息：

```python
help(urllib.urlopen)
```

## 编写模块

编写 Python 模块是一个非常简单的任务。你所需要创建一个与模块名同名的 .py 文件，然后使用 Python 名称（不使用 .py 扩展名）通过 `import` 命令来导入它。

## 编写包




包（package）是一个命名空间，包含许多模块和包。它们是带有特殊之处的目录。每个 Python 包都是一个必须包含名为 `__init__.py` 的特殊文件的目录。该文件本身可以是空的，仅表示该目录是一个 Python 包 —— 这样你就可以像导入模块一样来导入它了。

如果你创建一个名为 `foo` 的目录（这将作为包名），你可以在该包中创建一个名为 `bar` 的内内模块。不要忘记你还需要向 `foo` 目录中添加 `__init__.py` 文件。为了使用名为 `bar` 的模块，你可以通过两种方式之一导入它：

- `import foo.bar`，或者
- `from foo import bar`

### `__init__.py` 和 `__all__` 变量

如果你使用第一种方法，每当你访问 `bar` 时都必须使用前缀 `foo`。但在第二种方法中，你不需要这样做，因为你正在将模块本身导入到命名空间中。

你还可以使用 `__init__.py` 文件来决定包将将哪些模块导出为 API，同时通过重写 `__all__` 变量来保持其他模块为内部模块 —— 示例：

`__init__.py`:
- `__all__ = ["bar"]`

# MySQL Python 教程

在最后一章节中，我想和你们讨论如何使用 Python 为 MySQL 数据库编程。我将介绍使用 `MySQLdb` 模块的 Python 编程基础。

## 关于 MySQL 数据库

MySQL 是世界上最好的数据库管理系统之一。作为一个多用户系统，它在互联网上非常流行，并可以在大多数最大的操作系统平台上使用。除了 Windows 之外，它运行在 Linux、BSD UNIX 和 Mac OS 上。像 YouTube 和 Wikipedia 这样的大型知名网站都在 MySQL，这些网站每天可以处理数百万次查询。

## 在开始之前

为了在你的计算机上运行这些示例，你需要安装许多包，首先是 MySQL（如果你还没有安装它的话）。

从命令行提示符中输入以下内容：

```bash
$ sudo apt-get install mysql-server
```

这将安装 MySQL 服务器以及许多其他包。在安装期间，系统会提示你输入 MySQL root 账户的密码：

```bash
$ apt-cache search MySQLdb
- `python-mysqldb` - MySQL 的 Python 接口
- `python-mysqldb-dbg` - MySQL 的 Python 接口（调试扩展）
- `bibus` - 文献数据库
- `eikazo` - 专为大量扫描设计的 SANE 图形前端
```

在现阶段，我们不知道 `MySQLdb` 模块包的名称是什么，因此可以使用以下命令来查找：

```bash
$ sudo apt-get install python-mysqldb
```

现在是时候创建一个新的数据库用户以及新数据库了：

```bash
$ mysql -u root -p
- Enter password:
- Welcome to the MySQL monitor. 命令以 ; 或 \g 结束。
- Your MySQL connection id is 30
- Server version: 5.0.67-0ubuntu6 (Ubuntu)
```

输入 'help;' 或 '\h' 获取帮助。
输入 '\c' 清除缓冲区。

```sql
mysql> SHOW DATABASES;
- Database
- information_schema
- mysql
- 2 rows in set (0.00 sec)
```

使用 root 账户我们可以连接到数据库。要显示所有可用数据库，只需在命令行提示符处输入 `Show Databases`。

```sql
mysql> CREATE DATABASE testdb;
- Query OK, 1 row affected (0.02 sec)
```

我们现在可以创建一个 `testdb` 数据库，这就是你在整个章节中将使用的：

```sql
mysql> CREATE USER 'testuser'@'localhost' IDENTIFIED BY 'test623';
- Query OK, 0 rows affected (0.00 sec)
mysql> USE testdb;
- Database changed
mysql> GRANT ALL ON testdb.* TO 'testuser'@'localhost';
- Query OK, 0 rows affected (0.00 sec)
mysql> quit;
- Bye
```

接下来，你需要创建一个新用户，并将赋予该用户对 `testdb` 数据库中所有表的所有权限。我们创建一个新的数据库用户。授予该用户对 `testdb` 数据库中所有表的所有权限。

## `MySQL` 模块

这将用于实现 MySQL 的 C API，并且它与 Python 中的 DB API 接口完全不兼容。大多数程序员倾向于使用 `MySQL` 模块，因为它是面向对象的，所以我们将在这里使用它。以下是一个使用 `_mysql` 模块的示例：

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

import _mysql
import sys

try:
    con = _mysql.connect('localhost', 'testuser', 'test623', 'testdb')
    con.query("SELECT VERSION()")
    result = con.use_result()
    print "MySQL version: %s" % \
        result.fetch_row()[0]
except _mysql.Error, e:
    print "MySQL version: %s" % \
        result.fetch_row()[0] # 注意：原文此处有一个逻辑错误，但保留了内容
```

## `MySQLdb` 模块

`MySQLdb` 是 Python 的包装器，与 DB API 兼容，使得代码更具可移植性。在第一个示例中，我们使用 `MySQLdb`：

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

import MySQLdb
import sys

try:
    con = MySQLdb.connect('localhost', 'testuser', 'test623', 'testdb')
    cur = con.cursor()
    cur.execute("SELECT VERSION()")
    ver = cur.fetchone()
    print "MySQL version: %s" % ver
except MySQLdb.Error, e:
    print "MySQL version: %s" % (e.args[0], e.args[1])
    sys.exit(1)
finally:
    if con:
        con.close()
```

## 创建并填充表

现在我们将创建一个表并向其中放入一些数据，或者填充它，如大家周知：

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-

import MySQLdb

con = MySQLdb.connect('localhost', 'testuser', 'test623', 'testdb')

with con:
    cur = con.cursor()
    cur.execute("DROP TABLE IF EXISTS Writers")
    cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, Name VARCHAR(25))")
    cur.execute("INSERT INTO Writers(Name) VALUES('Jack London')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Honore de Balzac')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Lion Feuchtwanger')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Emile Zola')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Truman Capote')")
```



使用 `with` 关键字，解释器会自动释放这些资源，并执行错误处理。

```python
cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, Name VARCHAR(25))")
```

上面的 SQL 语句将创建一个名为 `writers` 的新数据库表。该表有两个列：`ID` 和 `Name`。

```python
cur.execute("INSERT INTO Writers(Name) VALUES('Jack London')")
cur.execute("INSERT INTO Writers(Name) VALUES('Honore de Balzac')")
# ...
```

要向表中插入新作者，我们使用 `INSERT` 语句并添加另外两行：

```text
mysql> SELECT * FROM Writers;
+----+-------------------+
| Id | Name              |
+----+-------------------+
|  1 | Jack London       |
|  2 | Honore de Balzac  |
|  3 | Lion Feuchtwanger |
|  4 | Emile Zola         |
|  5 | Truman Capote      |
+----+-------------------+
5 rows in set (0.00 sec)
```

脚本执行后，我们可以使用 `mysql` 客户端工具查询该表中的所有数据。

## 获取数据

现在我们已经在数据库中存了一些数据，是时候检索它们了：

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import MySQLdb as mdb
con = mdb.connect('localhost', 'testuser', 'test623', 'testdb');
with con:
    cur = con.cursor()
    cur.execute("SELECT * FROM Writers")
    rows = cur.fetchall()
    for row in rows:
        print row
```

上面的示例展示了你如何从名为 `Writers` 的表中检索所有数据。

```python
cur.execute("SELECT * FROM Writers")
```

该语句选择了该表中的所有数据。

```python
rows = cur.fetchall()
```

我们使用 `fetchall()` 方法检索所有记录，这些记录以结果集的形式返回。

```python
for row in rows:
    print row
```

现在我们可以逐行将所有数据打印到窗口中。

```text
$ ./retrieve.py
(1L, 'Jack London')
(2L, 'Honore de Balzac')
(3L, 'Lion Feuchtwanger')
(4L, 'Emile Zola')
(5L, 'Truman Capote')
```

并不是总是能够同时检索所有数据，因此，我们将改为一次地获取每一行。

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import MySQLdb as mdb
con = mdb.connect('localhost', 'testuser', 'test623', 'testdb');
with con:
    cur = con.cursor()
    cur.execute("SELECT * FROM Writers")
    for i in range(cur.rowcount):
        row = cur.fetchone()
        print row[0], row[1]
```

再次，我们可以打印表中的数据并一次地获取每一行。

```python
for i in range(cur.rowcount):
    row = cur.fetchone()
    print row[0], row[1]
```

我们使用 `fetchone()` 方法获取每一行，而 `rowcount` 属性将显示 SQL 语句返回的总行数。

```text
$ ./retrieve2.py
1 Jack London
2 Honore de Balzac
3 Lion Feuchtwanger
4 Emile Zola
5 Truman Capote
```

上面是示例的输出。

## 字典游标

在 `MySQLdb` 模块中，有许多类型的游标。默认游标以元组的元组的形式返回数据。字典游标以字典的格式发送数据，允许我们通过列名来引用数据：

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import MySQLdb as mdb
con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')
with con:
    cur = con.cursor(mdb.cursors.DictCursor)
    cur.execute("SELECT * FROM Writers LIMIT 4")
    rows = cur.fetchall()
    for row in rows:
        print row["Id"], row["Name"]
```

在上面的示例中，你可以看到我们使用字典游标从名为 `Writers` 的表中检索了前四行。分解来看，该示例看起来如下：

```python
cur = con.cursor(mdb.cursors.DictCursor)
cur.execute("SELECT * FROM Writers LIMIT 4")
for row in rows:
    print row["Id"], row["Name"]
```

`DictCursor` 用于从表中引入四行数据。数据通过列名引用。

```text
$ ./dict.py
1 Jack London
2 Honore de Balzac
3 Lion Feuchtwanger
4 Emile Zola
```

上面是输出的一个示例。

## 列标题

接下来，我们将查看如何打印数据库表中带有数据的列标题：

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import MySQLdb as mdb
con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')
with con:
    cur = con.cursor()
    cur.execute("SELECT * FROM Writers LIMIT 5")
    rows = cur.fetchall()
    desc = cur.description
    print "%s %s" % (desc[0][0], desc[1][0])
    for row in rows:
        print "%s %s" % (row[0], row[1])
```

我们通过 `description` 对象从表中获取列元数据，并逐行打印所有数据。

```text
$ ./columnheaders.py
Id Name
1 Jack London
2 Honore de Balzac
3 Lion Feuchtwanger
4 Emile Zola
5 Truman Capote
```

## 预处理语句

现在让我们看看预处理语句。当我们编写这些时，使用占位符而不是直接写入值。预处理语句可以提高性能和安全性，Python DB 支持这种 ANSI 格式。

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import MySQLdb as mdb
con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')
with con:
    cur = con.cursor()
    cur.execute("UPDATE Writers SET Name = %s WHERE Id = %s", ("Guy Mauasant", "4"))
    print "Number of rows updated:", cur.rowcount
```

让我们更改第 4 行作者的名字：

```python
cur.execute("UPDATE Writers SET Name = %s WHERE Id = %s", ("Guy Mauasant", "4"))
```

在此处，我们使用了由 `%s` 标识的占位符。值在 SQL 语句执行之前绑定到占位符。

```text
$ ./prepared.py
Number of rows updated: 1
One row has been updated
mysql> SELECT Name FROM Writers WHERE Id=4;
+------------------+
| Name           |
+------------------+
| Guy Mauasant |
+------------------+
1 row in set (0.00 sec)
```

我们更改了第 4 行作者的名字。

## 插入图片

有时你可能将图片放入数据库。并不是所有人推荐这样做，因为图片被称为二进制数据；然而，MySQL 数据库有一种专门用于存储二进制的数据类型 `BLOB`（二进制大对象）。其他变体有 `TINYBLOB`、`LONGBLOB` 和 `MEDIUMBLOB`。

```text
mysql> CREATE TABLE Images(Id INT PRIMARY KEY, Data MEDIUMBLOB);
Query OK, 0 rows affected (0.08 sec)
```

我们创建了一个名为 `Images` 的新表。

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import MySQLdb as mdb
def read_image():
    fin = open("woman.jpg")
    img = fin.read()
    return img
con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')
with con:
    cur = con.cursor()
    data = read_image()
    cur.execute("INSERT INTO Images VALUES(1, %s)", (data, ))
```

在上面的脚本中，我们从磁盘读取了一个 .JPG 文件并将其放入名为 `Images` 的表中。




我们现在知道如何将图像插入到表中，但我们如何读取这些图像呢？

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import MySQLdb as mdb
def writeImage(data):
    fout = open('woman2.jpg', 'wb')
    with fout:
        fout.write(data)
con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')

with con:
    cur = con.cursor()
    cur.execute("SELECT Data FROM Images WHERE Id=1")
    data = cur.fetchone()[0]
    writeImage(data)
```

上面的脚本显示了我们如何从 `images` 表中读取文件。

`cur.execute("SELECT Data FROM Images WHERE Id=1")`
我们从表中选取了一条记录。

`fout = open('woman2.jpg', 'wb')`
现在我们打开了一个可写的二进制文件。

`fout.write(data)`
然后我们将该数据写入磁盘。

你现在应该在当前目录下看到一个名为 `woman2.jpg` 的图像，我们可以查看它是否是正确的，即你在上一个示例中插入的那个。

## 事务支持

事务是针对一个或多个不同数据库中的数据进行的数据库操作原子单元。每个事务中 SQL 语句的影响可以对该数据库进行回滚（rollback）或提交（commit）。

如果数据库支持事务，Python 将在游标创建时自动——静默地启动一个事务。我们使用 `commit()` 方法来提交使用该游标进行的更新，并使用 `rollback()` 方法来回滚或丢弃它们。这些方法中的每一个都将启动一个新的事务。

MySQL 数据库包含几种不同的存储引擎类型，最常见的是 `MyISAM` 和 `InnoDB`。InnoDB 现在是默认引擎，尽管在速度和安全性之间存在权衡。`MyISAM` 表的处理速度快得多，但不支持事务。`rollback()` 和 `commit()` 方法没有实现，因此不起任何作用。然而，`InnoDB` 表在防止数据丢失方面安全得多，而且它们支持事务，尽管处理速度较慢。

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import MySQLdb as mdb
import sys
try:
    con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')
    cur = con.cursor()
    cur.execute("DROP TABLE IF EXISTS Writers")
    cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, Name VARCHAR(25)) ENGINE=INNODB")
    cur.execute("INSERT INTO Writers(Name) VALUES('Jack London')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Honore de Balzac')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Lion Feuchtwanger')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Emile Zola')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Truman Capote')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Terry Pratchett')")
    con.commit()
except mdb.Error, e:
    if con:
        con.rollback()
    print "Error %d: %s" % (e.args[0],e.args[1])
    sys.exit(1)
finally:
    if con:
        con.close()
```

`writers` 表已重新创建，我们现在将显式地处理事务。

`cur = con.cursor()`
在 Python DB API 中，并没有调用 `BEGIN` 语句来启动事务。相反，事务在游标创建时就已经启动了。

`cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, Name VARCHAR(25)) ENGINE=INNODB")`
在这个例子中，我们查看的是 `InnoDB` 表类型——如果你使用的是旧版本的 MySQL，则需要指定引擎类型。

`con.commit()`
事务必须通过两种方法之一结束——`commit()` 或 `rollback()` 方法。如果你在这一行加上以井号（`#`）开头的注释，表仍然会被创建，但数据不会被写入其中。

到目前为止，我们一直在使用事务，但还没有显式地使用。相反，我们使用了上下文管理器（context managers），它们在代码块执行时处理运行时的进入和退出。你可以在 `Mysdb` 中将连接对象作为上下文管理器。它们会自动回滚或提交事务，并通过消除 `try` 和 `finally` 语句来清理代码。

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
import MySQLdb as mdb
con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')
with con:
    cur = con.cursor()
    cur.execute("DROP TABLE IF EXISTS Writers")
    cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, Name VARCHAR(25))")
    cur.execute("INSERT INTO Writers(Name) VALUES('Jack London')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Honore de Balzac')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Lion Feuchtwanger')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Emile Zola')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Truman Capote')")
    cur.execute("INSERT INTO Writers(Name) VALUES('Terry Pratchett')")
```

在上面的示例中，上下文管理器处理了错误处理的所有工作，并自动提交或回滚了事务。

## 结论

Python 是一种非常好用的语言，易于阅读和理解。虽然它看起来可能很复杂，但其实并非如此，一旦你掌握了它，你可以花几个小时创建简单的程序，然后过渡到更复杂的程序。

当你准备好使用 Python 进行更高级的编程时，你可以在网上找到大量信息来帮助你。在此期间，请花时间熟悉在 Windows 10 上使用 Python，而且最重要的是，享受其中！

感谢下载我的书。如果你觉得它对你有帮助，请考虑在 Amazon.com 上给我留评价。
