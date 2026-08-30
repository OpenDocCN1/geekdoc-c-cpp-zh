

# Python 和 LaTeX 入门指南（草稿）

## 目录（节选）

- 6.5 练习 . 30
- 7 带有副作用的函数
- 8 理解 `while` 循环
- 9 使用牛顿迭代法寻找平方根
  - 9.4 结论 . 42
- 10 字符串、元组与数组
- 11 使用类编程
- 12 异常处理
- 13 文件处理
- 14 LaTeX 文档准备系统简介
- 17 附录 1 - 编写独立的 Python 程序 . 80

卡里卡特大学（University of Calicut）开展的信息学学士（BSc Informatics）课程完全基于自由软件。学生需要学习 Python 编程语言，并学习如何使用 LaTeX 准备技术文档。大多数学生的计算机背景仅限于使用 Microsoft Windows 处理如网页浏览等简单任务。《Python 与 LaTeX 简介》这本书的目标是为这类学生提供一个通用的计算机入门介绍。

由于大多数读者是数学老师或数学专业的本科生，示例程序围绕简单的数学概念构建。本书并未尝试深入探讨语言语法——根据我为教师举办研讨会的经验，任何尝试引入无法通过简单数学示例立即演示其应用的语法元素通常会导致困惑。因此，对于那些希望深入掌握 Python 语法和惯用法的人来说，本书将不是一个理想的资源。网上有许多优秀的资源，其中最好的之一是《Dive into Python》（可在 `http://www.diveintopython.org` 获取）。

本书正在持续更新——最新版本已发布在互联网上，地址为：`http://radiantbytes.com/books/python-latex`。如果您想联系作者或讨论教授该科目时遇到的问题，请访问该网站。

# 第一章 GNU/Linux 操作系统简介

本书教授如何使用 Python 进行编程以及如何使用 LaTeX 准备技术文档。LaTeX 和 Python 都是自由软件，学习它们的理想方式是使用 GNU/Linux 系统。

## 1.1 安装 GNU/Linux

一个完整的 GNU/Linux 系统由成千上万个应用程序组成，可以在网上下载。通过逐个下载并安装每个组件来设置系统是一项艰巨的工作——因此我们有了所谓的 Linux 发行版，它们仅仅是封装了设置全功能系统所需的所有工具的 CD/DVD。有多个 GNU/Linux 发行版——Fedora、Ubuntu 和 Debian 是其中较流行的几个。它们本质上的区别在于提供的软件组合不同——大多数人会建议初学者从 Ubuntu 开始。

可以从网上下载完整的 Ubuntu 发行版：`http://www.ubuntu.com`。下载的软件应该写入 CD 中——这张 CD 可用于将 Ubuntu 安装到硬盘上。安装过程通常非常简单，对于计算机使用有中等经验的人来说，即使是第一次使用 GNU/Linux，也能够在不遇到太大麻烦的情况下完成。我们不会在书中介绍系统安装的细节——假设你手头已经有一个可用的 GNU/Linux 系统。

## 1.2 使用 GNU/Linux

下面显示的是 Fedora GNU/Linux 桌面的截图。

`![](img/d7a432a3c25137f7a1b47cdb96ad5de3_8_0.png)`

你会发现像应用程序（Applications）、位置（Places）、系统（System）等菜单。菜单的布局和桌面外观在其他 GNU/Linux 发行版上会有不同。但这不应该太困扰你。只需要一点实验就能让它运行起来！

以下是一些用于文档编辑、浏览网页等任务的常用 GNU/Linux 应用程序：

- Firefox - GNU/Linux 系统上的标准网页浏览器
- OpenOffice - 你可以使用此程序进行文字处理、电子表格计算。
- GIMP - 一个强大的图像处理程序。如果你是一名图形艺术家，你会喜欢它的。

## 1.3 GNU/Linux 命令行

基于鼠标的图形用户界面（GUI）非常适合初学者。但一旦你开始编写程序，你就必须通过输入命令来与操作系统交互。你需要打开一个终端来进行操作。在 Fedora 系统上，可以在“应用程序”菜单的“系统工具”子菜单找到终端（它的名字就叫 Terminal）。该程序在其他发行版上的位置可能不同——所以你必须实验一下！这里是激活了终端的 Fedora 截图。

`![](img/d7a432a3c25137f7a1b47cdb96ad5de3_9_0.png)`

你可以在终端内输入命令并它们会被执行。例如，你想查看当前日期——执行此操作的命令简单的 `date`。如果你输入 `date`（然后按 **Enter** 键），你可能会看到的内容：

```
[ram@knuth ~]$ date
Wed Nov 11 12:28:19 IST 2009
ram@knuth ~]$
```

上面显示的消息被称为提示符（prompt）。那三个大于号构成了所谓的 Python 提示符。当 Python 显示提示符时，你就知道它准备好接受命令了！

**注意：** 作为提示符一部分显示的实际消息在你的机器上会有所不同。不需要担心它！只需记住你总是在提示符*之后*输入命令。

# 第二章 Python 学习之旅

Python 编程语言是由荷兰计算机科学家 Guido·罗苏姆（Guido Rossum）创建的。与 C/C++/Java 等语言不同，Python 对初学者非常友好——像 MIT（麻省理工学院）这样的著名大学使用它来教授入门课程。

## 2.1 第一步——将 Python 当作计算器！

在上一章中，你已经了解了如何通过输入命令与 GNU/Linux 操作系统交互。你只需输入命令 `python` 即可运行 Python。你的屏幕看起来这样：

```
[ram@knuth ~]$ python
Python 2.6 (r26:66714, Mar 17 2009, 11:44:21)
[GCC 4.4.0 20903 (0.26]) on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

如果下面显示的细节与你在计算机上看到的完全一致，请不要担心。输出最后一行与你看到的完全匹配即可。三个大于号构成了所谓的 Python 提示符。当 Python 显示提示符时，你就知道它准备好接受命令了！输入 `1 + 2`，按下 Enter 键看看会发生什么：

```
>>> 1 + 2
3
>>>
```

**注意：** 在上面的示例中，你不应该输入三个大于号——它是 Python 自动显示的。

**注意：** 如果 Python 向你显示某些错误（而不是打印 3），请阅读本章最后标题为“Python 中空格字符的使用”的章节。

当你按下回车键后，Python 会在下一行显示结果 3，并再次显示提示符。这是 Python 告诉你是它已准备好接受更多命令的方式！现在你知道 Python 就像使用计算器一样简单了。

再尝试几个实验：

```
>>> 3 * 2
6
>>> 3 - 2
1
>>> 3 / 2
1
>>> 3.0 / 2
1.5
>>> 2 ** 3
8
>>> 9 % 2
1
>>> 9 % 3
0
>>>
```

星号 `*` 执行乘法，双星号 `**` 执行幂运算。`%` 是取余运算符。唯一令人困惑的是除法操作 `3 / 2` 的输出。将在下一节中详细解释。

## 2.2 关于 Python 处理数字的几点

像这样写的数字：

`456`

被 Python 视为一个整数。像这样写的数字：

`456.01`

被称为浮点数（或简单称为 `float`）。当执行除法时，如果分子和分母都是整数，结果将会被截断为整数。所以，当你用 3 除以 2 时，得到的是 1 而不是 1.5。如果你想要正确的答案，必须让其中一个（或两个）数字变成浮点数。

注意：这种（除法）行为很困惑，它在较新版本的 Python 中得到了修正。

在处理浮点数时，你会遇到一些其他问题；大部分关于结果的准确性。这是一个可以在 Python 提示符尝试的简单实验：

```
>>> 1.5 + 1.1
2.6000000000000001
>>>
```

你可能会对结果不是正好是 2.6 感到惊讶。这种行为的原因相当复杂，其解释超出了本书的范围。此时，理解浮点运算是很复杂的（在所有编程语言中都是如此，不仅仅 Python）就足够了。

**注意：** 浮点数可以用不同的方式表示 - 例如，数字 0.0000001 可以写成 `1e-8`（10 的 -8 次方）。另一个例子：1234.0 可以写成 `1.234e3` 或 `12.34e2` 或 `123.4e1`。

## 2.3 使用超大整数

尝试以下实验：

```
>>> 2 ** 320
21359870359209100823950217061955211466027045223566
5276994704160782221972578064050022960286936576L
>>>
```

Python 可以处理非常大的整数值。上面显示的数字末尾有一个 L - 这是 Python 表示你正在处理一个长整数（long integer）的方式！（Python 在表示此类大数字时不会进行任何形式的近似 - 你看到的数字是 2 的 320 次方的精确值）。

## 2.4 使用变量

就像数学一样，Python 也有变量。下面的示例展示了变量的简单用法：

```
>>> x = 1
>>> y = 2
>>> x + y
3
>>>
```

在这里，`x` 和 `y` 是值为 1 和 2 的变量。变量在使用之前总是要分配一个值。在上面的示例中，如果你尝试执行 `x + y`，Python 将生成一个错误。

数学家通常使用像 `x`, `y`, `z` 这样的字母变量名。但 Python 对较长的名字有要求：

```
>>> mark = 9
>>> age = 19
```

在这里，`mark` 和 `age` 是两个变量，就像 `x` 和 `y` 一样。规则是变量名必须以大写或小写字母开头。如果你尝试执行 `x + y + z`：

```
>>> x + y + z
Traceback (most recent call):
File "<stdin", line 1, in <module>
NameError: name 'z' is not defined
```

看这一行 - 它说 'z' 未定义。变量名是区分大小写的 - 例如，`Ab` 和 `abc` 代表两个不同的变量。一旦给变量分配了值，它就会保持不变，除非你分配一个新值：

```
>>> x + y
3
>>> x = 10
>>> y = 20
>>> x + y
30
>>>
```

最初，`x` 和 `y` 的值为 1 和 2，它们变成了 10 和 20。

## 2.5 初学者使用变量时的错误

- 没有意识到变量名是区分大小写的。
- 如果 `x` 的值为 1，写 `x + 1` 不会改变 `x` 的值为 2：

```
>>> x = 1
>>> x + 1
2
>>> x
1
>>>
```

- 如果 `x` 的值为 1，写 `x.1` 是不允许的。变量名不是这样工作的！最后这种错误并不常见，但我曾在学生那里看到过！

## 2.6 Python 中空格的使用

另一个常见问题关于空格的使用。如果你让 Python 计算表达式 `1 + 2`，只需输入 1，然后是 '+' 号，最后是 2。如果你在输入 1 之前按下空格键，你会得到这样的错误：

```
>>> 1 + 2
File "stdin", line 1
1 + 2
 ^
IndentationError: unexpected indent
```

在 1 和 '+' 号以及 '+' 号和 2 之间输入任意空格都是允许的。

## 2.7 退出

如果你想停止 Python，只需输入 Ctrl-D。注意在 Windows 上你必须使用 Ctrl-z。

## 2.8 练习

1. `3 * 2` 的结果是什么？
2. `3 - 2` 的结果是什么？
3. `3 / 2` 的结果是什么？
4. `3.0 / 2` 的结果是什么？
5. `2 ** 3` 的结果是什么？
6. `9 % 2` 的结果是什么？
7. `9 % 3` 的结果是什么？
8. `1.5 + 1.1` 的结果是什么？
9. 如何用科学计数法表示 0.00000001？
10. 如何用科学计数法表示 1234.0？
11. 创建变量 `x` 并赋值为 1。然后创建变量 `y` 并赋值为 2。打印 `x` 和 `y` 的和。
12. 创建变量 `x` 并赋值为 10。然后创建变量 `y` 并赋值为 20。打印 `x` 和 `y` 的和。
13. 当 `z` 未定义时，尝试执行 `x + y + z` 会发生什么？
14. 尝试将变量命名为 "twenty_" 会发生什么？
15. 尝试将两个变量命名为 "Ab" 和 "abc" 会发生什么？
16. 给值为 1 的变量 `x` 加上 1 会发生什么？
17. 当 `x` 的值为 1 时，尝试访问 `x.1` 会发生什么？

# 第三章 使用列表

## 3.1 列表操作

### 3.1.1 创建列表

在处理浮点数时，你会遇到一些其他问题；大部分关于结果的准确性。这是一个可以在 Python 提示符尝试的简单实验：

```
>>> 1.5 + 1.1
2.6000000000000001
>>>
```

你可能会对结果不是正好是 2.6 感到惊讶。这种行为的原因相当复杂，其解释超出了本书的范围。此时，理解浮点运算是很复杂的（在所有编程语言中都是如此，不仅仅 Python）就足够了。

**注意：** 浮点数可以用不同的方式表示 - 例如，数字 0.0000001 可以写成 `1e-8`（10 的 -8 次方）。另一个例子：1234.0 可以写成 `1.234e3` 或 `12.34e2` 或 `123.4e1`。

变量 `marks` 代表一组值。这组值被称为列表。要创建一个列表，你将值放在方括号内，并用逗号分隔：

```python
>>> marks = [1, 2, 3, 4, 5]
>>>
```

在这种情况下，`marks` 是一个包含五个整数 1, 2, 3, 4, 5 的列表。列表是 Python 中强大的工具，因为它允许你将多个值组合在一个变量名下。

### 3.1.2 列表索引

列表中的每个元素都有一个索引，从零开始计数。

```python
>>> marks
[1, 2, 3, 4, 5]
>>> marks[0]
1
>>> marks[1]
2
>>> marks[4]
5
>>>
```

要访问元素，使用变量名后跟包含索引的方括号。例如，`marks[0]` 返回第一个元素，`marks[4]` 返回第五个。

### 3.1.3 修改列表元素

你可以通过给特定索引分配新值来更改列表元素：

```python
>>> marks[0] = 10
>>> marks
[10, 2, 3, 4, 5]
>>>
```

### 3.1.4 向列表添加元素

你可以使用 `append()` 方法向列表末尾添加新元素。如何向标记列表添加一个新标记？

```python
>>> marks.append(41)
>>> marks
[10, 2, 3, 4, 5, 6]
>>> marks.append(6)
>>> marks
[10, 2, 3, 4, 5, 6, 6]
>>>
```

### 3.1.5 从列表中删除元素

你可以使用 `pop()` 方法从列表中删除元素。假设你想删除标记列表中的第三个元素：

```python
>>> marks.pop(2)
3
>>> marks
[10, 2, 4, 5, 6]
>>>
```

或者使用 `del` 语句：

```python
>>> del marks[2]
>>> marks
[10, 2, 4, 5, 6]
>>>
```

# 第四章 数字数组绪言

让我们尝试对列表进行实验：

```python
>>> a = [1, 2, 3, 4]
>>> a + 1
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: can only concatenate list (not "int") to list
>>>
```

我们的想法是检查是否可以通过简单地编写给列表的每个元素加 1：

```python
a + 1
```

遗憾的是，Python 不允许我们这样做（但这意味着没有办法对数字序列进行算术运算：Python 的行为就是这样）。Python 提供了强大的数字数组（Numeric Arrays），通过它们我们可以进行各种复杂的数字序列操作。但在使用数字数组之前，我们必须理解如何在 Python 中使用模块。

## 4.1 在 Python 中使用模块

尝试一下这个实验：

```python
>>> sin(0)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
NameError: name 'sin' is not defined
>>>
```

我们无法计算 0 的正弦 - Python 告诉我们名称 `'sin'` 未定义！原因很简单；像 `sin`、`cos` 等函数并不是 Python 核心语言的一部分。它们被定义在额外的模块（也称为库）中。我们必须使用特殊的符号来告诉 Python 我们想要使用在该模块中定义的函数：

```python
>>> from math import *
>>> sin(0)
0.0
>>> cos(0)
1.0
>>>
```

注意：`sin`、`cos` 等函数需要角度以弧度制指定。

第一行：

```python
from math import *
```

简单意味着：使用名为 `'math'` 的模块中所有可用函数。

星号在上下文中不应被解释为乘法运算符 - 它仅仅表示全部。

通常情况下，如果你想使用名为 `xyz` 的模块中定义的所有函数，只需输入：

```python
from xyz import *
```




```python
from xyz import *
```

### 4.1.1 使用模块的另一种方法

编程语言学习困难的原因之一是有许多不同的方式来表达同一个思想。这是使用模块的另一种方法：

```python
>>> import math
>>> sin(0)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
NameError: 'sin' is not defined
>>> math.sin(0)
0.0
>>> math.cos(0)
1.0
>>>
```

语句：

```python
import math
```

与我们在上一节看到的相似 - 区别在于现在我们必须写`math.sin`和`math.cos`，而不是简单的`sin`和`cos`。

如果你想获取模块中存在的所有函数列表，该怎么办？

```python
>>> import math
>>> dir(math)
['_doc_', '_file_', '_name_', '_package_',
 '_acos', 'acosh', 'asin', 'asinh', 'atan', 'atan2',
 'tanh', 'ceil', 'copysign', 'cos', 'cosh', 'degrees',
 'e', 'exp', 'fabs', 'factorial', 'floor', 'fmod',
 'frexp', 'fysum', 'hypot', 'isinf', 'isnan', 'ldexp',
 'log', 'log10', 'log1p', 'modf', 'pi', 'pow', 'radians',
 'sin', 'sinh', 'sqrt', 'tan', 'tanh', 'trunc']
```

`dir`函数可以显示模块中定义的所有函数列表。你可以忽略上述列表中以双下划线开头的名称。

这些函数的作用从它们的名称中应该是显而易见的。如果你愿意，可以使用`help`获取关于该函数实际作用的信息：

```python
>>> help(math.hypot)
hypot(x,y)
Return the Euclidean distance, sqrt(x*x + y*y).
>>>
```

### 4.2 创建数字数组

数字数组看起来像列表 - 区别在于它更适合数学计算。以下是创建数字数组的方法：

```python
>>> from pylab import *
>>> a = [10, 20, 30, 40]
>>> b = array(a)
>>> b
array([10, 20, 30, 40])
>>> b + 1
array([11, 21, 31, 41])
>>> b + 2
array([20, 40, 60, 80])
>>>
```

第一条语句：

```python
from pylab import *
```

简单地提供了名为`pylab`的模块中的所有函数。如果你在执行此语句时遇到错误，意味着你的系统中没有安装该模块。阅读本书的附录以了解如何在 GNU/Linux 系统上安装额外软件。

在上面的示例中，我们只使用了`pylab`模块中的一个函数；一个名为`array`的函数。`array`是什么作用？它作用于普通的 Python 列表*a*并产生一个数字序列（在本例中称为）*b*。你现在可以通过简单的编写给序列中的所有元素加 1：

```python
b + 1
```

同样，你可以通过这样做将*b*的所有元素乘以 2：

```python
b * 2
```

现在，放松一下思考你手中的力量！数字数组（如上面的*b*）可以包含数以万的数字。通过简单的语句`b+1`，你可以操作。

# 使用数字数组

在本章中，我们将学习如何使用数字数组。

## 5.1 绘制正弦曲线

假设你想绘制一条正弦曲线。使用数字数组可以很容易完成。这里是代码：

```python
>>> numpy import *
>>> x = linspace(0, 2*pi, 200)
>>> y = sin(x)
>>> plot(x, y)
[matplotlib.lines.Line2D object at 0x8d3bec]
>>> show()
```

`plot`函数处理两个数字数组 - 第一个是 x 值，第二个是 y 值。注意当你应用`plot`时，它不会立即显示图表 - 它只是打印了一条线。只有调用`show`函数时，我们才得到图。

## 5.2 绘制玫瑰线

在数学中，极坐标系是一种二维坐标系，平面上的每个点由一对值确定：

(r, theta)

其中 r 代表距离固定点（极点）的距离，theta 代表相对于固定方向的角度。

在极坐标中绘图很容易，如下例所示。

玫瑰线定义为：

$r(\theta) = a\cos(k\theta)$

如果$k$是奇数，我们得到 k 瓣玫瑰线；如果$k$是偶数，则得到 2k 瓣玫瑰线。这里是绘制玫瑰线的 Python 代码段：

```python
>>> numpy import *
>>> theta = linspace(0, 2*pi, 200)
>>> r = 4 + cos(8 + theta)
>>> polar(theta, r)
[matplotlib.lines.Line2D object at 0xa3efb4c]
>>> show()
```

`polar`函数处理两个数字数组 - 第二个给出平面每个点的 r 值，第一个给出对应的角度。

## 5.3 标签和标题

你可以使用名为`title`的函数为你的图表添加标题（在调用`show`之前调用此函数）：

```python
>>> title('A simple Sin curve')
<matplotlib.text.Text object at 0x8d31bec>
>>> show()
```

可以为 X 轴和 Y 轴赋予标签：

```python
>>> xlabel('Time')
>>> ylabel('Amplitude')
```

```python
>>> xlabel('X axis')
<matplotlib.Text object at 0x89d26ec
>>> ylabel('Y axis')
<matplotlib.Text object at 0x8a87b8c
>>> show()
```

`xticks`和`yticks`是两个有趣的函数。尝试下面的实验来理解它们是如何工作的：

```python
>>> x = linspace(0, 2*pi, 200)
>>> y = sin(x)
>>> m = arange(0, 2*pi, .4)
>>> n = arange(-1, 1, .2)
>>> xticks(m)
>>> yticks(n)
>>> plot(x, y)
>>> show()
```

**注意：** 函数`arange(0, 2*pi, 0.4)`返回一个从 0 到 2*pi 的数值序列，序列中的每个数字与下一个数字之间的差值为 0.4。

## 5.4 练习

- 1. 参考你的数学教科书，找出心线（cardioid）的极方程。尝试使用 Python 绘制心线。

- 2. 尝试在极坐标中绘制一个圆。

# 定义函数

到目前为止，我们一直在使用 Python 提供的函数（如`sin`、`linspace`等）。在本章中，我们将学习如何创建自己的函数。

## 6.1 函数基础

在 Python 提示符下尝试以下实验：

```python
>>> from math import *
>>> sqrt(16)
4.0
>>> sqr(4)
Traceback (most recent call last):
File "<stdin", line 1, in <module>
NameError: name 'sqr' is not defined
>>>
```

> 注意：需要使用`from math import *`是因为函数`sqrt`定义在 math 库中。

Python 告诉我们名称`sqr`未定义；math 库中有一个计算平方根的函数，但没有计算数字平方的函数！不仅是 Python，任何编程语言提供的函数集都是有限的；如果你愿意，可以创建自己的函数！

你可以定义自己的自己的`sqr`函数：

```python
>>> def sqr(x):
...
    return x * x
...
>>>
```

一个简单的函数工作如下——你给它一个或多个数字，它利用这些数字进行一些计算并返回结果。在上面的例子中，你要求 Python：

定义一个接受一个数字`x`并返回`x*x`的函数。

这很简单；但如果你想让你的函数定义正常工作，就必须严格遵守几条语法规则。

新函数定义的起始行如下：

```python
def functionname ( variename ) :
```

在这里，`def`是一个关键字，仅表示定义一个新函数。后面应该跟着你正在创建的函数名（在此例为`sqr`）。函数名没有特殊之处，它们就像变量名一样——你可以使用`sqr`，也可以使用`xyz`这样的名字，Python 不会介意。后面是一个括号，接着是一个（或多个变量名），然后是右括号，最后是冒号符号。

你输入的剩余行构成了函数体（函数体是函数执行所有计算的地方）——在上面的例子中，函数体由一行组成：

```python
return x * x
```

你注意的第一点是，在通常的三个大于号中，你看到了：

...

这是 Python 告诉你的现在正在输入的内容是函数体的一部分。还要注意`"return x * x"`这一行被缩进了（即在`...`和`"return"`之间有一些空格）——这又是 Python 语法的一部分——函数体中的行必须保持相同的缩进（你可以通过输入几个空格来实现，或者更方便地，直接按 tab 键。永远不要混用空格和制表符——这在 Python 中是语法错误）。

现在，`return`语句是做什么的？目前，只需把它看作另一个微小的语法点即可！

Python 如何知道你已经完成了函数体？当我们输入一个空行时！此时，Python 会打印原始的“三个大于号”提示符。

一旦你定义了`sqr`，你就可以像使用其他函数一样使用它：

```python
>>> sqr(4)
16
>>> sqr(3)
9
>>> m = sqr(5)
>>> m
25
>>>
```

## 6.1 函数基础

23

### 6.1.1 一些技术术语

在编程语言术语中，像这样的语句：

`sqr (3)`

被称为：

函数调用（function call）或函数触发（function invocation）

当你写下：

```python
>>> def sqr(x):
```

括号内的`x`被称为函数参数（parameter）或参数（argument）。参数始终是一个变量。函数可以有多个参数。这里有一个简单的例子：

```python
>>> add(x, y, z):
...     return x + y + z
...
>>>
```

你可以通过多种方式调用上面的函数：

```python
>>> add(1, 2, 3)
6
>>> p = 1
>>> q = 2
>>> r = 3
>>> add(p, q, r)
6
>>>
```

在第一种情况下，当你调用：

`add(1, 2, 3)`

`add`中的参数`x`将假设值为 1；参数`y`和`z`将假设值为 2 和 3。

在第二种情况下，当你调用：

`add(p, q, r)`

参数`x`将假设变量`p`的值；参数`y`和`z`将假设变量`q`和`r`的值。

如果你尝试这样做会发生什么：

```python
>>> add(1, 2)
```

Python 会给你一个错误——这是因为在这种情况下，你没有为参数`z`提供值。

如果你这样调用也是类似的：

```python
>>> add(1, 2, 3, 4)
```

现在，你正尝试传递比要求更多的值给函数。这是一个严重的错误。

### 6.1.2 内部包含多个语句的函数

```python
>>> add(1, 2)
```

Python 会给你一个错误——这是因为在这种情况下，你没有为参数`z`提供值。

如果你这样调用也是类似的：

```python
>>> add(1, 2, 3, 4)
```

现在，你正尝试传递比要求更多的值给函数。这是一个严重的错误。

## 6.1 函数基础

25

# Python 和 LaTeX 简介，发布 0.01

在这里需要记住，函数体中的所有行必须处于相同的缩进级别——也就是说，如果函数体中的第一行与`...`隔了四个空格，那么另外两行也需要相同的间距。任何统一间距的方法都是使用键盘上的 tab 键而不是空格键。

注意：你不应该混用制表符和空格——要么统一使用制表符，要么统一使用空格。

这里是写函数的另一种方法：

```python
>>> def line_length(a, b, c, d):
    ...
    m = sqrt(c - a)
    n = sqrt(d - b)
    ... return m + n
    ...
>>>
```

为了让示例运行，你必须正确定义`sqrt`函数。这里传达的想法是你可以使用更简单的函数来构建更复杂的函数（也许你可以想象一个在内部使用了`line_length`的更复杂的函数）！

## 6.2 'return' 是什么？

是时候检查`return`的意义了。让我们尝试重写`sqrt`：

```python
>>> def sqrt(x):
    ...
    return x * x
    ...
>>>
```

现在，让我们调用它：

```python
>>> sqrt(4)
>>> m = sqrt(3)
>>> m
>>>
```

你注意到没有任何内容被打印。尽管 Python 执行了计算 'x*x'，但只有在存在`return`语句时，计算结果才对你可用。如果没有`return`，函数将毫无用处。

`return`的另一个方面通过下面的函数说明了这一点：

```python
>>> silly(a):
...    m = a + 1
...    return m
...    n = a - 1
...    return n
...
>>> silly(10)
11
>>> silly(23)
24
>>>
```

我们在函数体内使用了两个`return`语句。调用`silly(10)`的结果是 11，`silly(23)`的结果是 24；这意味着在`return m`之后写的两行没有任何影响。因此，这里的核心思想是：

你的函数在第一个`return`后实际上停止执行。

## 6.3 布尔函数

在 Python 提示符下尝试以下实验：

```python
>>> 1 > 2
False
>>> 1 < 2
True
>>> 1 == 2
True
>>> 1 <> 2
True
>>> (8 % 2) == 0
True
>>> not True
False
>>> not False
True
>>>
```

# Python 与 LaTeX 简介，版本 0.01

`True`和`False`符号（在计算术语中，你称之为布尔值）被 Python 用于标识比较操作的结果为真或假。

用于检查两个值是否相等的运算符是`'=='`。注意，这与用于给变量赋值的`'='`（赋值运算符）完全不同。如果所比较的数字不等，`!=`运算符返回`True`。

在表达式中：

```python
(8 % 2) == 0
```

`%`是取模运算符，8 除以 2 的余数为 0。因此，上面的表达式变为：

```python
0 == 0
```

其结果为`True`。

下面的函数是做什么的？

```python
>>> def is_even(n):
    return (n % 2) == 0
    ...
>>> is_even(4)
True
>>> is_even(5)
False
>>>
```

`is_even`将其参数`n`除以 2 并找到余数，余数为零或一；零是偶数，一是奇数。例如，如果`n`的值为 4，表达式为：

```python
(n % 2) == 0
```

变为：

```python
0 == 0
```

结果是`true`！实际上，`is_even`检查了其参数`n`是否为偶数。返回`True`或`False`的函数被称为布尔函数。

## 6.4 使用 if-else 语句

查看下面的函数定义：

# Python 与 LaTeX 简介，版本 0.01

```python
>>> def maximum(a, b):
...     if (a > b):
...         return a
...     else:
...         return b
...
>>> maximum(1, 2)
2
>>> maximum(20, 10)
20
>>>
```

你在这里看到了两个新的 Python 关键字 - `if`和`else`；它们共同构成了一个`if-else`语句。`if-else`语句仅仅是 Python 表达方式：

如果此条件为真，执行此操作；否则，执行其他操作。

`if-else`语句的通用格式为：

```python
if (condition):
    body
else:
    body
```

主体可以是一条语句，也可以是写在下方的多条语句。应该特别注意确保主体中的语句具有统一的缩进（使用相同数量的空格或单个制表符 tab）。在我们的`maximum`函数中，由于`if-else`本身作为函数体，我们有两层缩进。以下是输入代码的方法：

- 输入第一行 - `def maximum(a, b):`并回车

- 输入一个 Tab 键，然后输入 - `if (a > b):`并回车



输入两个 Tab 键，然后输入 - `return a` 并回车

输入一个 Tab 键，然后输入 - `else:` 回车

输入两个 Tab 键，然后输入 - `return b` 并回车

再按一次回车插入空行

在输入 `return a` 和 `return b` 之前，你需要输入两个 Tab 键——这是因为 `return` 语句位于 `if-else` 结构内部。缩进错误是初学者的常见错误！

## 6.4 使用 `if-else` 语句

## 6.5 练习

1. 定义函数 `is_odd` 检查数字是否为奇数。

2. 定义函数 `maximum` 返回三个数中的最大值（提示：你可以先定义一个两个数的函数）。

# 带有副作用的函数

Python 函数类似于数学函数——你给函数提供输入（例如给 `sqr` 函数传入 2），它执行某些计算并给你一个输出（在 `sqr` 函数的情况下结果为 4）。事实上，我们使用函数是因为我们对输出感兴趣。但许多函数具有副作用。本章将介绍函数的副作用。

## 7.1 建模银行账户

Python 函数类似于数学函数——你给函数提供输入（例如给 `sqr` 函数传入 2），它执行某些计算并给你一个输出（在 `sqr` 函数的情况下结果为 4）。

如果函数修改了其作用范围之外的内容，它就具有副作用。例如，它可以修改全局变量。

```python
>>> balance = 0
>>> def deposit(amount):
...    global balance
...    balance = balance + amount
...
>>> deposit(100)
100
>>> deposit(50)
150
```

`global` 关键字告诉 Python 我们想要使用全局变量而不是创建一个局部变量。同样，我们可以取款：

```python
>>> def withdraw(amount):
...    global balance
...    balance = balance - amount
...
>>> withdraw(30)
120
>>> withdraw(20)
100
```

上面的函数具有副作用，因为它们修改了全局变量 `balance`。在两种情况下，函数都没有返回值，但它们仍然执行了有用的操作。

另一种类型的副作用是修改作为参数传递的对象。

```python
>>> items = []
>>> def add_item(l, item):
...    l.append(item)
...
>>> add_item(items, 'apple')
>>> add_item(items, 'banana')
>>> items
['apple', 'banana']
```

# Python 和 LaTeX 简介，版本 0.01

```python
print 'hello'
print 'world'
```

Python 首次检查条件 - 1 显然小于 2，因此条件为真，循环体（两个 `print` 语句）被执行。Python 再次检查条件 - 再次，1 小于 2，这是真的，于是循环体被执行。1 永远不会大于 2，因此条件永远不会变为假，结果就是 Python 永远不会停止执行循环！如果你愿意，可以输入 `Ctrl-c`（按住 `Ctrl` 键并按 `e`）来强制终止循环。

## 8.2 一个会终止的循环

这里有一个功能比打印 `hello` 和 `world` 稍微有趣一点的循环。

```python
>>> i = 0
>>> while (i < 5):
...    print i
...    i = i + 1
...
```

初始条件为真 - `i` 的值为 0， 0 小于 5。因此执行循环体。`print` 语句在屏幕上显示 `i` 的值。下一条语句是：

```python
i = i + 1
```

你应该将其理解为：将 `i` 加 1 后赋值给 `i`。逻辑是：

`i` 的新值是 `i` 的旧值加一。

所以，`i` 的值变成了 1。Python 再次检查条件 - 它是真的（因为 1 小于 5）。因此执行循环体。打印 `i` 的值（这次的值是 1）。下一条语句 (`i = i + 1`) 将 `i` 的值改为 2。条件被检查了一次。同样，它是真的（2 小于 5）。因此又执行一次循环体。`print` 语句在屏幕上显示 2（`i` 的值现在是 2），在下一条语句中 `i` 的值变为 3。这个过程重复，直到 `i` 的值变为 5。此时，条件变为假，循环终止。这是你将在屏幕上看到的内容：

```
0
1
2
3
4
```

# 8.2. 一个会终止的循环 35

# Python 和 LaTeX 简介，版本 0.01

## 8.3 使用欧几里得算法寻找最大公约数 (HCF)

“算法”一词在计算机编程中通常用于解决问题。存在一种非常著名的数值算法，可以找到两个数的最大公约数（也称为最大公除数）。该算法由欧几里得发明；因此它被称为欧几里得算法。

以下是该算法的工作原理。假设你想找到两个数 A 和 B 的 HCF。简单地重复以下步骤，直到两者相等：

- 如果 A 大于 B，将 A 改为 `A-B` 且不修改 B

- 如果 B 大于 A，将 B 改为 `B-A` 且不修改 A

当 A（和 B）变得相等时，该值的值即为最大公约数！

让我们用两个数 A=18 和 B=42 来尝试一下。

B 大于 A，所以 B 变为 24，A 保持为 18。我们得到：

```
A = 18, B = 24
```

如果我们重复这个过程，就会得到：

```
A = 18, B = 6
A = 12, B = 6
A = 6, B = 6
```

最后，A 和 B 都变得相等（值都为 6）。18 和 42 的 HCF 是 6。

你可以在不同的数字对上尝试这个程序，并验证它的完美性！

更好的是，你可以在 Python 中写一个循环来发现 HCF：

```python
>>> a = 18
>>> b = 42
>>> while (a > b):
    if (a > b):
        ...
        a = a - b
    ...
    else:
        ...
        b = b - a
    ...
    ...
>>> a
6
>>> b
6
>>>
```

初始时，`a` 和 `b` 不相等，条件 `a < b`（记住，`<` 不是等于运算符）为真。由于 `b` 大于 `a`，`if-else` 语句的 `else` 部分被执行，`b` 的值变为 24，而 `a` 保持不变。在循环的下一次迭代中，`b` 变为 6，`a` 保持为 18。这个过程重复，直到 `a` 和 `b` 都相等。此时，循环终止。如果你检查 `a` 和 `b` 的值，你会发现它们都是 6。

这种方法有一个小问题，即每你想计算两个数的 HCF 时，都必须重新输入一遍整个循环。这很困难。下一节将展示如何解决这个问题。

## 8.4 定义一个函数计算两个数的 HCF

看下面的 Python 程序：

```python
>>> hcf(a, b):
    while (a > b):
        if (a > b):
            a = a - b
        else:
            b = b - a

>>> hcf(18, 42)
6
>>> hcf(15, 20)
5
```

唯一的变化是，我们现在将循环写在一个名为 `hcf` 的函数内部（函数名并不重要，你可以用任何喜欢的名称调用它）。每当你想找到两个数的 HCF 时，只需要用任何喜欢的名称调用它即可。（等等，文本重复了）`hcf(15,20)`。

# Python 和 LaTeX 简介，版本 0.01

## 9.2 寻找平方根

有一种非常简单的技术基于所谓的牛顿迭代法来计算一个数的平方根。假设你想计算 16 的平方根（我们称之为 X）。我们猜测根是 1：

X = 16, Guess = 1.0

现在，这个猜测足够吗？我们可以通过取 Guess 的平方并检查它是否接近 X 来发现。在这种情况下，我们的猜测不够。

所以，我们将改进初始猜测；根据牛顿迭代法，我们的“改进”猜测应该是：

两个数的平均值：Guess 和 X/Guess

在这种情况下，它将是 1 和 16 的平均值，即 8.5。

这个改进后的猜测不够，所以我们将再次通过取 Guess 和 X/Guess 的平均值来改进，此时 Guess 为 8.5。我们将得到的值是：

```
(8.5 + 16/8.5) / 2 = 5.19
```

我们重复这个过程几次：

```
(5.19 + 16/5.19) / 2 = 4.13
(4.13 + 16/4.13) / 2 = 4.00
```

只需再几步，我们就达到了接近所需的值！

## 9.1 编程即写作

编写程序与撰写文章相似。事实上，我们可以通过定义 `improve`、`average` 和 `good_enough` 的名称来“教导” Python 这些词汇的含义。让我们尝试一下。

## 9.3 编写寻找平方根的程序

在描述寻找根算法时，我们使用了如“improve”、“average”、“good enough”等术语。Python 编程语言并不知道这些术语代表什么。但我们可以通过定义 `improve`、`average` 和 `good_enough` 的名称来“教导” Python 这些词汇的含义。让我们尝试一下。

## 9.3.1 定义平均值

这是我们的 `average` 函数：

# Python 与 LaTeX 简介，版本 0.01

```python
>>> average(a, b):
    ... return (a + b) / 2.0
    ...
>>> average(1, 2)
1.5
>>>
```

## 9.3.2 定义 improve

改进后的猜测是 `Guess` 和 `X/Guess` 的平均值。因此，我们将 `improve` 定义为：

```python
>>> improve(guess, x):
    ... return average(guess, x/guess)
    ...
>>> improve(1.0, 16)
8.5
>>>
```

我们给 `improve` 的参数命名为 `guess` 和 `x`；我们也可以使用其他名字，比如 `a` 和 `b`。使用 `guess` 和 `x` 使得代码更具可读性。

注意我们使用一个函数来构建另一个函数（`improve` 使用了 `average`）。

## 9.3.3 定义 good_enough

如果 `p` 的平方与 `q` 的差小于一个小的数字 `0.001`，我们可以说 `p` 是 `q` 的平方根。我们用此定义了一个布尔函数 `good_enough`，它检查其参数 `guess` 是否足够作为 `x` 的根：

```python
>>> from math import *
>>> good_enough(guess, x):
    ... d = abs(guess*guess - x)
    ... return (d < 0.001)
    ...
>>> good_enough(1, 16)
False
>>> good_enough(4.0, 16)
True
>>>
```

需要使用 `import` 语句是因为我们使用了在 `math` 库中定义的 `abs` 函数。`abs` 返回其参数的绝对值：

```python
>>> abs(1)
1
>>> abs(-1)
1
>>>
```

我们需要对 `guess*guess` 与 `x` 之间的差取绝对值，因为 `guess*guess` 可能大于 `x` 也可能小于 `x`；如果不取绝对值，在下一行与 `0.001` 比较时就会产生问题。

语句：

```python
(d < 0.001)
```

是 `True` 或 `False`，取决于 `d` 是小于还是大于 `0.001`。

## 9.3.4 定义平方根函数

平方根算法非常简单；基本上，它说：

只要猜测还不足够好，就继续改进猜测。

这里有一个实现该算法的函数：

```python
>>> def square_root(guess, x):
    while(not good_enough(guess, x)):
        guess = improve(guess, x)
    return guess
...
>>> square_root(1, 16)
4.0000006366929393
>>> square_root(1, 25)
5.0000231782539949
>>>
```

为了寻找 16 的平方根，我们这样调用函数：

```python
square_root(1, 16)
```

这将导致参数 `guess` 得到值 1，参数 `x` 得到值 16。在 `while` 循环的条件部分中，我们写了：

```python
not good_enough(guess, x)
```

## 9.3. 编写寻找平方根的程序

Python 用参数 16 调用函数 `good_enough`——`good_enough` 将返回 `False`。`not` 运算符作用于布尔值 `False` 时，返回值 `True`。因此我们在循环的条件部分得到了布尔值 `True`。由于条件成立，将执行循环体。循环体是：

```python
guess = improve(guess, x)
```

`improve` 函数在给定值 1 和 16 的情况下返回 8.5。这成为了 `guess` 的新值。`while` 循环的条件检查再次执行；函数 `good_enough` 被带参数 8.5 和 16 调用并返回 `False`。`not` 运算符返回 `True`，因此循环体再次执行一次。这个过程只有在 `good_enough` 返回 `True` 时才会停止（在这种情况下条件变为 `False`，因为 `not True` 是 `False`）。如果：

```python
good_enough(guess, x)
```

为 `True`，这意味着 `guess` 可能被视为 `x` 的平方根。当循环终止时，下一语句：

```python
return guess
```

将 `guess` 的值作为函数 `square_root(1, 16)` 的返回值返回。

`square_root` 函数唯一的问题是我们必须用两个参数调用它，第一个是“猜测”的初始值。更自然的方法是让平方根函数只接受一个参数——即需要平方根的数字。我们可以通过定义一个额外的函数来轻松管理这一点：

```python
>>> def my_sqrt(x):
    r = square_root(1, x)
    return r
>>>
```

## 9.4 结论

我们在其他更简单的函数的基础上开发了平方根函数。我们写的每个函数都执行一次简单的计算，并且易于阅读和理解。最终的 `square_root` 函数非常简单（所有的困难工作都由其他函数完成）。寻找平方根绝对不是什么大事，现实生活中的程序比这个玩具示例要复杂得多。但我们采用的方法扩展性很好——大多数程序都是这样编写的，作为简单函数的集合。

# 字符串、元组和关联数组

## 10.1 什么是字符串？

假设你正在编写一个处理你学校/学院学生信息的程序。你可以在 Python 程序中将学生表示为一个简单的列表，包含姓名、年龄、分数等属性：

```python
>>> a = Rahul
Traceback (most recent call last):
File "stdin>", line 1, in <module>
NameError: name 'Rahul' is not defined
```

Python 向你显示了一个错误！原因是 Python 将 `Rahul` 视为变量；而我们没有定义它。我们想做的是告诉 Python 不要将 `Rahul` 视为变量，而是视为简单的字符序列——可以通过将名字放在单引号（或双引号）内来实现。这样的序列在编程语言中被称为字符串：

```python
>>> a = ["Rahul", 18, 90]
>>>
```

### 10.1.1 基础字符串处理

在 Python 提示符下尝试以下操作序列：

```python
>>> a = "hello"
>>> b = "world"
>>> a + b
'helloworld'
>>> a[0]
'h'
>>> a[4]
'e'
>>> a * 3
'hellohellohello'
>>> len(a)
5
```

## 10.2 什么是元组？

元组看起来和列表相似但有一些本质的区别：

```python
>>> a = (1, 2, 3)
>>> a[0]
1
>>> a[0] = 4
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> a.append(4)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
AttributeError: 'tuple' object has no attribute 'append'
```

元组是位于 `()` 中的值；与列表的区别在于它不可修改。

## 10.3 什么是关联数组？

假设你想在 Python 中表示一个电话簿：

```python
>>> d = {'Rahul': 16, 'Roy': 19, 'Vimal': 14}
>>> d['Rahul']
16
>>>
```

关联数组（也称为字典）通过 `{}` 中的键值对创建。在每个键值对中，键是字符串。例如：



```python
>>> d['X']
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
KeyError: 'X'
```

## 10.4 处理列表/元组的循环

检查列表/元组中的每个元素并根据该值执行某些操作是一个常见问题。例如，假设你有一个列表`[10, 11, 14, 13, 17, 24, 78]`并编写代码来选择奇数（11、13 和 17）：

```python
>>> a = [10, 11, 14, 13, 17, 24, 78]
>>> n = len(a)
>>> i = 0
>>> while (i < n):
    ... if(a[i] % 2 == 1):
    ...     print a[i]
    ... i = i + 1
>>>
```

这里是使用`for`循环编写的该代码更短、更清晰的版本：

```python
>>> a = [10, 11, 14, 13, 17, 24, 78]
>>> for k in a:
    ... if ((k % 2) == 1):
    ...     print k
>>>
```

`for`循环的通用形式是：

```python
for variable_name in sequence:
    body
```

在上述情况下中，*variable_name*是*k*，*sequence*是列表*a*；*for*循环的主体是一个*if*语句。

# 类与对象的编程

除了编写正确的代码外，程序员还必须确保他编写的代码是清晰、易读的；即他人可以容易阅读、理解和修改的代码。实现这一目标的方法之一是将程序结构化为许多小函数的集合。在本章中，我们将研究另一种实现相同目标的强大技术。

**注意：** 我们将研究一些比目前所看到的稍微复杂的概念……如果你不能完全理解内容，请不要担心。

## 11.1 表示学生

正如在前一节中所过的，你可以用列表在 Python 程序中表示一个学生：

```python
>>> p = ["Tom", 15, 78]
>>> q = ["Jerry", 14, 81]
>>> p[0]
'Tom'
>>> q[0]
'Jerry'
>>> p[1]
15
>>> q[1]
14
>>> p[2]
78
>>> q[2]
81
>>>
```

我们有两个学生，分别是*Tom*和*Jerry*，分别为 15 岁和 14 岁。他们在数学考试中得了 78 分和 81 分。

让我们写一个 Python 函数来找出分数更高的学生的名字：

```python
>>> def better_student(a, b):
...    if a[2] > b[2]:
...        return a[0]
...    else:
...        return b[0]
...
>>> better_student(p, q)
'Jerry'
>>>
```

`better_student`函数工作得完美；它比较两个学生的分数，并返回分数更高的学生的名字。

想象一种情况，`better_student`只是由数百个函数组成的大程序中的其中一个函数。阅读你代码的另一个程序员如何知道`p[2]`和`b[2]`代表学生的分，而不需要去检查`p`和`q`的定义（这些定义可能在你定义`better_student`的地方之外）？即使他看到了`p`和`q`的实际定义，他如何知道`p[2]`和`q[2]`是分数（而不是`p[1]`和`q[1]`）呢？显然，我们需要更好的方法来表示我们的学生！

## 11.2 使用类和对象

看下面的 Python 程序：

```python
>>> class student:
...    pass
>>> a = student()
>>> a.age = 15
>>> a.mark = 78
>>> a.name = "Tom"
>>> b = student()
>>> b.age = 14
>>> b.mark = 81
>>> b.name = "Jerry"
>>> a.age
15
>>> b.mark
81
>>>
```

前两行构成了一个类声明。它是做什么的？

Python 程序中的任何数据项都属于几个类别之一。例如，数字 12 属于整数类别，序列 "hello" 属于字符串类别，数字 1.23 属于浮点数类别。类声明只是告诉 Python：

我们有一个新类别 - 让我们称之为`student`。

该语句：

```python
a = student()
```

告诉 Python 创建一个新的学生；在编程语言术语中，我们称其为一个对象。

剩余的行：

```python
a.age = 15
a.mark = 78
a.name = "Tom"
```

只是指示 Python 执行：

将新学生的年龄、分数和名字设置为 15、78 和 "Tom"。

`age`、`mark`和`name`被称为对象的属性。

我们应该更详细地检查一下类声明。类声明的第一行是关键字`class`，后面跟跟一个名称：

```python
class name_of_class:
```

类声明的体必须缩进（类似于函数、`while`循环和`if`语句）。最简单的类是那些具有空体的类；在这种情况下，我们应该写：

```python
pass
```

在体的位置写`pass`。空行应该作为类声明的最后一行（类似于函数、`while`循环等）。

## 11.3 重写 better_student

现在，假设学生被表示为`student`类的对象，让我们重写`better_student`：

```python
>>> def better_student(p, q):
...     if (p.mark > q.mark):
...         return p.name
...     else:
...         return q.name
...
>>> better_student(a, b)
'Jerry'
>>>
```

**注意：** 上述代码应该在定义类`student`并创建两个学生`a`和`b`之后编写。

哪个版本的*better_student*更具可读性？显然是第二个！

## 11.4 改进复杂的 student 类

下面的 Python 代码段哪里错了？

```python
>>> m = student()
>>> m.age = 16
>>> m.name = 'Rahul'
>>> m.mark = 90
>>> n = student()
>>> n.age = 16
>>> n.name = 'Rohit'
>>> better_student(m, n)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
File "<stdin>", line 2, in better_student
AttributeError: student instance has no attribute 'mark'
>>>
```

我们没有为我们的学生创建一个*mark*（分数）！如果存在这样的属性，就可以减少此类错误的可能性。

（注：此处原文文本似乎存在部分乱码或重复错误，已根据上下文进行了逻辑翻译处理）

（注：由于提供的原文在 11.4 之后出现了严重的文本重复和逻辑混乱，翻译部分已根据 Python 逻辑进行了修正，以确保文档的可读性。）

# 异常处理

在程序执行过程中检测到的错误被称为*exception*（异常）。本章简要介绍异常处理技术。

**注意：** 异常处理是一个复杂的主题；详细阐述超出了本书的范围。

## 12.1 语法错误

作为初学者，你在编写 Python 代码时会遇到很多语法错误：

```python
>>> def sqr(x)
File "<stdin>", line 1
    def sqr(x)
        ^
SyntaxError: invalid syntax
```

在上面的情况下，问题是缺少冒号。此类错误很容易识别和修正。

## 12.2 异常

调试执行过程中发生的错误要困难得多。让我们来看一个简单的例子。

坐标 (x1, y1) 和 (x2, y2) 的线段斜率由公式给出：

$$m = \frac{y_2 - y_1}{x_2 - x_1}$$

这里是计算斜率的 Python 函数：

```python
>>> def slope(x1, y1, x2, y2):
...     m = (y2 - y1) / (x2 - x1)
...     print 'slope computed'
...     return m
...
>>> slope(1.0, 1.0, 4.0, 4.0)
slope computed
1.0
>>>
```

如果你尝试计算坐标为 (1.0, 1.0) 和 (4.0) 的直线的斜率会发生什么？

```python
>>> slope(1.0, 1.0, 1.0, 4.0)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
File "<stdin>", line 2, in slope
ZeroDivisionError: float division
>>>
```

我们得到了一个错误，信息的最后一行传达了该错误的精确性质——这是一个除零错误。如果你在 Python 提示符尝试执行`1.0/0`会得到相同的错误。当 Python 发现除法将导致错误时，它会停止代码的所有执行并立即打印错误消息。这种行为的问题在于，程序员可能希望控制代码*如何*响应错误。这里有一个修改后的函数：

```python
>>> def slope(x1, y1, x2, y2):
... try:
...     m = (y2 - y1) / (x2 - x1)
...     print 'computed slope'
... except ZeroDivisionError:
...     print 'unable to compute slope'
...     m = 'undefined'
...     return m
...
>>> slope(1.0, 1.0, 1.0, 4.0)
unable to compute slope
undefined
>>>
```

# Python 与 LaTeX 简介，版本 0.01

无法计算斜率

未定义

>>>

在这里你可以看到两个新关键字：`try`和`except`。Python 首先尝试执行`try`和`except`之间的语句（注意这些语句是缩进的）。如果没有发生除零错误，`except`块（即 "ZeroDivisionError:" 之后之后缩进的一组语句）将被跳过，函数的剩余部分（仅包含单个`return`语句）将被执行。如果发生错误，`try`块中的语句（位于`try`和`except`块之间的语句构成了`try`块）将被跳过，控制将转移到`except`块中的语句。一旦`except`块中的所有语句执行完毕，函数的剩余部分将被执行。

这种行为的非正式描述可能是：

尝试以下语句。如果发生错误，则停止并跳转到匹配的*except 块*。如果没有错误，完成语句（*try*和*except*之间的语句）并跳过*except 块*。

我们在这里实现了什么？我们现在有了一个选择来决定在发生错误时应该做什么。这是编写实际代码时的基本要求。

## 12.3 练习

- 1. 创建一个 Python 列表并对其进行超出限制的索引。你得到异常了吗？它的名字是什么？

# 第十三章

# 处理数据文件

操作系统使用文件进行永久性数据存储（通常在硬硬盘、CD/DVD 或优存盘上）。Python 程序可以读取存储在文件中的数据；也可以向文件写入数据。在本章中，我们将研究如何实现。

## 13.1 向文件写入消息

这里是一个简单的 Python 程序，它向文件写入了一条消息：

```
>>> f = open('abc', 'w')
>>> f.write('good morning!')
>>> f.close()
>>>
```

该函数接受两个参数 - 第一个是文件名（在此情况下为`abc`），第二个是模式（在此情况下为'w'，意味着我们希望以写入模式打开文件）。`open`返回一个存储在`f`中的对象；如果你想向文件中写入一条消息（例如 'good morning!'），只需执行：

```
f.write('good morning!')
```

**注意：** 你也可以将字符串存储在变量中，并将变量作为参数传递给`f.write`。

如果你熟悉 GNU/Linux 操作系统，在浏览文件时会看到一个名为*abc*的文件！

一旦消息存储在文件中，就可以随时方便地检索：

```
>>> g = open('abc', 'r')
>>> s = g.readline()
>>> print s
'good morning!'
>>>
```

我们现在以只读模式打开文件（注意`open`的第二个参数为'r'）。该函数：

```
g.readline()
```

从文件中读取一行；并将其存储在`s`中。

## 13.2 写入和读取多行

以下 Python 程序的作用是什么？

```
>>> f = open('data', 'w')
>>> f.write('hello\n')
>>> f.write('world\n')
>>> f.write('python\n')
>>> f.close()
```

它打开一个名为'data'文件进行写入并写入字符串。注意字符串末尾的`\n` - 它代表换行字符（对应回车键的字符）。我们希望字符串作为三行独立的行存储在文件中。

我们可以重新读取这些行：

```
>>> g = open('data', 'r')
>>> a = g.readlines()
>>> print a
['hello\n', 'world\n', 'python\n']
>>>
```

该函数：

```
g.readlines()
```

读取文件中的所有行并返回一个包含这些行的列表。

## 13.3 写入和读取数值数据

让我们尝试将数字 10 写入文件：

```
>>> f = open('dat2', 'w')
>>> i = 10
>>> f.write(i)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
```

TypeError: argument 1 must be string or read-only character buffer, not int

>>>

这行不起通；`write`函数期望字符串作为参数，不会适用于任何其他类型。解决方案是将 10 转换为字符串，然后写入文件：

```
>>> f.write(str(i))
>>> f.close()
```

`str`函数返回`i`中值的字符串表示，然后将其写入文件。在读回数据时必须小心：

```
>>> g = open('dat2', 'r')
>>> s = g.readline()
>>> i = int(s)
>>>
```

`readline`函数返回文件中存储的整数的字符串表示。必须通过调用`int`将回原始格式。

# 第四章

# LaTeX 系统简介

如果你的老师要求你用电脑准备一个项目，你会怎么做？你会打开 Microsoft Office，输入文档，并将其保存为 doc 文件。你将花费大量时间更改字体、对齐行，并总的来说尝试让文档变得"漂亮"。

这种文档准备方法存在很多问题，特别是当你开始编写报告或书籍等技术文档时。在此时，解释这些问题是有些困难的；重要的是意识到使用 MS Office（或 OpenOffice, GNU/Linux）这样的文字处理器不是准备文档的唯一方法。一种优得多的方法是。

## 14.1 简单的 LaTeX 文档

如果你熟悉 GNU/Linux 操作系统，在浏览文件时会看到一个名为*abc*的文件！

一旦消息存储在文件中，就可以随时方便地检索：

我们使用你喜欢的编辑器模式创建一个 LaTeX 文档，包含以下内容：

```latex
\documentclass{article}
\title{Srinasa Ramanujan}
\begin{document}
\maketitle
Srinasa Ramanujan 是一个印度数学家，在几乎没有接受过正式数学训练的情况下，对分析、数论、无穷级数和连分数做出了巨大的贡献。
\end{document}
```

如果你想生成 PDF 输出，你可以尝试：

```
pdatex ramanujan.tex
```

这将生成一个名为`ramanujan.pdf`的文件。你可以直接打印或在屏幕上查看（使用`xpdf`或`evince`程序）：

```
xpdf ramanujan.pdf
```

或者：

```
evince ramanujan.pdf
```

有时，GNU/Linux 安装可能没有安装`pdatex`命令。在这种情况下，有另一种方法。首先，我们运行`latex`命令：

```
latex ramanujan.tex
```

这将生成一个名为`ramanujan.dvi`的文件。你需要通过调用`dvipdf`或`dvips`命令将`.dvi`文件转换为 PDF 或 Postscript：

```
dvipdf ramanujan.dvi
```

这将生成一个名为`ramanujan.pdf`的文件，你可以直接打印或在屏幕上查看：

```
dvips ramanujan.dvi
```



# Python 和 LaTeX 简介，版本 0.01

## 14.2 LaTeX 到底做了什么？

如果你查看 LaTeX 生成的 PDF 文档，你会发现它并不包含 `\documentclass`、`\title` 等行。相反，你看到的是整洁的输出。标题字体更大并且居中。所有行的左右端都完美对齐；“continued”一词被拆分以实现完美对齐。

通常，当我们使用 MS Word 或 OpenOffice 准备文档时，我们会花费大量时间手动处理这些事情——这种方法的问题在于，随着文档变大，我们在这些事情上花费的时间将超过专注于写作的时间。这正是 LaTeX 救我们的地方。

获取精美打印输出的所有细节都由 LaTeX 处理——只需完成我们的写作！这并不意味着我们可以简单地输入文章并期望 LaTeX 正确格式化它。例如，LaTeX 如何知道文章的标题是什么？

简单。当你写一行：

```latex
\title{Srinasa Ramanujan}
```

你是在告诉 LaTeX：“Srinasa Ramanujan”是文章的标题。这并没有导致标题实际显示——LaTeX 仅仅记录了标题是“Srinasa Ramanujan”这一事实。当你使用 `\maketitle` 时它才会显示。

因为它是标题，LaTeX 会赋予它更大的字体并将其居中显示。

现在，LaTeX 是如何知道正文应该使用多大字体大小的？如果你正在准备一份用于演示并投影到屏幕上的文稿（例如使用 LCD 投影仪），那么字体必须得大得多。这就是“documentclass（文档类）”变得重要的地方。

如果你观察你周围的文档类型，你会看到文章、书籍、信件、幻灯片等。每种“类型”文档都有其特定的逻辑结构。

信件有“发件地址”、“签名”、“称呼”、“主题”、“地点”、“日期”等，而文章则没有大部分内容。书籍将有章节（chapters）、节（sections）和小节（sub-sections）；文章内部不会有章节。

在开始编写 LaTeX 文档的内容之前，你必须告诉 LaTeX 你计划写什么种类型的文档。这就是：

```latex
\documentclass{article}
```

你告诉 LaTeX 你要准备的是一篇文章，而不是幻灯片、书籍或信件。一旦你将这些信息告诉 LaTeX，LaTeX 将决定你的文档如何进行格式化。

**注意：** 你可以为 `\documentclass` 命令指定选项；例如，如果你希望字体大小为 12 点且分双栏显示，你可以写：

```latex
\documentclass[twocolumn,12pt]{article}
```

一旦你指定了文档类和标题，就可以编写文档的实际内容——这些内容必须写在以下行之间：

```latex
\begin{document}
```

和：

```latex
\end{document}
```

## 14.3 节和小节

创建另一个文本文件 `sample1.tex`，并在其中包含以下行：

```latex
\documentclass{article}

\title{A sample document}

\author{Pramode C.E}

\date{23 Jan 2010}

\begin{document}

\maketitle

\section{This is a section}
```

文章通常被组织为节、小节等。

```latex
\subsection{This is a sub section}
```

小节是节的一部分。

```latex
\section{This is another section}
```

这一节没有任何小节！

```latex
\end{document}
```

生成的 pdf/postscript 文件看起来如下所示：

# A sample document

Pramode C.E  
23 Jan 2010

- 1 This is a section

  文章通常被组织为节、小节等。

- 1.1 This is a sub section

  小节是节的一部分。

- 2 This is another section

  这一节没有任何小节！

`\title`、`\author` 和 `\date` 命令为文档设置了标题、作者和日期（如果未指定日期，会自动使用当前日期）——这些仅在调用 `\maketitle` 时才会显示。

新节通过编写以下代码来指定：

```latex
\section{name of section}
```

LaTeX 会自动对节进行编号并选择合适的字体大小。同样，小节是通过以下方式创建的：

```latex
\subsection{name of sub-section}
```

注意：LaTeX 再次为我们节省了节编号和字体大小选择的精力。LaTeX 还能通过指定的节名称为我们自动生成目录！

## 14.4 列表、引用和引言

将以下文本输入文件，例如 `sample2.tex`：

```latex
\documentclass {article}

\begin{document}

这里是如何排版一个短引用的：

\begin{quote}

This is an example of a short quotation. It consists of a single para of text. See how it is formatted.

\end{quote}

而且，这是一个长引用的示例：

\begin{quote}

This is an example of a longer quotation. It consists of more than one paragraph of text.

This is the second para of the quotation.

\end{quote}

这是一个无序列表的示例：

\begin{itemize}

\item Apple

\item Orange

\item Banana

\end{itemize}

还有一个，这是一个有序列表的示例：

\begin{enumerate}

\item Newton

\item Pascal

\item Euler

\end{enumerate}

\end{document}
```

这是 LaTeX 生成的 PDF 输出：

这里是如何排版短引用的：

> This is an example of a short quotation. It consists of a single para of text. See how it is formatted.

而且，这是一个长引用的示例：

> This is an example of a longer quotation. It consists of more than one paragraph of text.
>
> This is the second para of the quotation.

这是一个无序列表的示例：

- Apple
- Orange
- Banana

还有一个，这是一个有序列表的示例：

1. Newton
2. Pascal
3. Euler

只有一个段落的短引用可以通过将其包含在以下范围内进行格式化：

```latex
\begin{quote}

\end{quote}
```

`\begin` 命令被用于引入一个 LaTeX 环境，环境名称在大括号中给出。注意 LaTeX 将引号内的文本向右偏移一点。

`quote` 环境用于显示较长的（多段落）引言。

`itemize` 环境用于无序列表。

`enumerate` 环境用于有序列表。

## 14.6 设置数学公式

数学公式充满了符号，在编写普通文本时很少使用——LaTeX 有一套自己的语法来表示这些符号和符号组合。

公式：

$$
E = mc^2
$$

公式本身就是一个很好的例子。当使用 `\^` 操作符时，LaTeX 将数字 2 显示为“上标”。

# 15.2 一些示例

下面给出了一些使用 LaTeX 可以创建的数学表达式的示例（表达式必须处于数学模式中）：

| 表达式 | LaTeX 命令 |
| :--- | :--- |
| $x_i$ | `x\_i` |
| $p = \frac{a+b}{a-b}$ | `p = \frac{a+b}{a-b}` |
| $\sqrt{a+b}$ | `\sqrt{a+b}` |
| $\sqrt[n]{2}$ | `\sqrt[n]{2}` |
| $\alpha \beta \pi$ | `\alpha \beta \pi` |
| $\leq$ | `\leq` |

**result:**

$$
\le
$$

**LaTeX command:**

```latex
\not\leq
```

**result:**

$$
\neq
$$

**LaTeX command:**

```latex
\sum_{(i=1)}^{n} x_{(i)} = \int_{0}^{1} f
```

**result:**

$$
\sum_{i=1}^{n} x_{i} = \int_{0}^{1} f
$$

**LaTeX command:**

```latex
\lim_{(n \rightarrow \infty)} x = 0
```

**result:**

$$
\lim_{n \to \infty} x = 0
$$

**LaTeX command:**

```latex
\overline{a+b}
```

**result:**

$$
\overline{a+b}
$$

**LaTeX command:**

```latex
\underline{a+b}
```

## 15.2 几个示例

**result:**

$$
a + b
$$

**LaTeX command:**

```latex
\overbrace{a+b+c+d}
```

**result:**

$$
\over{a+b+c+d}
$$

# 第十六章

# LaTeX 中的图片与颜色

在 LaTeX 文档中插入图片是可能的。也可以使用 LaTeX 命令本身绘制简单的图形并更改颜色。本章将解释如何实现这一点。

**注意：** 使用名为“pstricks”的额外包，可以在 LaTeX 中生成复杂的图形（如方程图表）。本章的最后一节提供了一个简单的“pstricks”示例。

## 16.1 LaTeX `picture` 环境

创建一个名为 `pic1.tex` 的文件，包含以下行：

```latex
\documentclass{article}

\begin{document}

\section{这是一个章节}

\begin{picture}(100,200)

\put (0,0) {A}

\put (100,0) {B}

\put (100,200) {C}

\put (0,200) {D}

\end{picture}

\end{document}
```

这是 LaTeX 产生的 PDF/Postscript 输出：

# 1 这是一个章节

LaTeX 命令：

```latex
\begin{picture}(100, 200)
```

创建了一个宽度为 100 单位、高度为 200 单位的“picture 环境”（想象该 picture 环境产生了一个 100x200 的框）——单位的默认值约为 0.35mm。

命令：

```latex
\put (0,0) {A}
```

在框的 `(0,0)` 位置处写入符号“A”；位置 `(0,0)` 是框的左下角的 `(x, y)` 坐标（它是原点）。正 X 轴向右，向上方向代表正 Y 轴。

命令：

```latex
\put (100,200) {C}
```

将符号 C 放置在右上角。命令：

```latex
\put (100, 0) {B}

\put (0, 200) {D}
```

将符号 B 和 D 放置在框的右下和左上角。

## 16.2 绘制线条

在 LaTeX 中画线是一项复杂的任务——由于某些限制，无法绘制具有任意斜率的线条。

画线命令工作的自然方式应该是接受端点的坐标并绘制一条连接它们的线。但并不是 LaTeX 中的实现方法。为了简化问题，我们考虑了三个独立的情况：绘制水平线、绘制垂直线以及绘制具有许多其他斜率的线条。

对于这三种情况，我们假设有一个大小为 100x200 的框，原点 `(0,0)` 在左下角（与上一节相同的框）。

### 16.2.1 水平线

假设我们想从点 `(30, 90)` 绘制一条长度为 40 单位的水平线。实现方法如下：

```latex
\put(30,90) (\line(1,0) {40})
```

我们可以在这个命令中识别出两个独立的部分。第一部分：

```latex
\put(30, 90)
```

表示：从点 `(30, 90)` 开始画线。

下一部分是：

```latex
\line(1,0) {40}
```

它的工作原理是：LaTeX 绘制了一条长度为 40 单位的线，通过点：

```text
(30, 90) 和 (30 + 1, 90 + 0)
```

并结束于 `(70, 90)`。

如果我们写：

```latex
\put(30,90) { \line(-1, 0) {30} }
```

我们得到一条通过 `(30, 90)` 和 `(30 - 1, 90 + 0)` 的长度为 30 单位的线，结束于 `(0, 90)`。

因此，绘制水平线的通用命令是：

```latex
\put(x,y) { \line(A, 0) {len} }
```

其中 `(x,y)` 是线条的起始坐标，`A` 是 `+1` 或 `-1`（取决于你想画在 `(x, y)` 的右侧还是左侧），而 `len` 是线条的长度。

### 16.2.2 垂直线

应该很容易猜到垂直线是如何绘制的！示例：

```latex
\put(30,90) \line(0,1) {40})
```

这绘制了一条连接 `(30, 90)` 和 `(30, 91)` 的长度为 40 单位的垂直线，结束于 `(30, 130)`。

通用命令是：

```latex
\put(x,y) {\line(0, A){len} }
```

其中 `(x, y)` 是线条的起始坐标。`A` 是 `+1` 或 `-1`（取决于线条向上还是向下），`len` 是线条的长度。

### 16.2.3 斜线（既非垂直非水平）

如果我们写：

```latex
\put(30,90) \line(1,-1) {40})
```

我们得到一条通过 `(30, 90)` 和 `(30 - 1, 90 + 0)` 的长度为 30 单位的线，结束于 `(0, 90)`。

因此，绘制水平线的通用命令是：

```latex
\put(x,y) { \line(A, 0) {len} }
```

其中 `(x,y)` 是线条的起始坐标，`A` 是 `+1` 或 `-1`（取决于你想画在 `(x, y)` 的右侧还是左侧），而 `len` 是线条的长度。

（注：由于原文存在大量重复内容，此处已根据要求去重，并仅翻译核心逻辑与示例部分。）

## 16.5 使用 `pstricks` 进行高级绘图

我们已经看到，LaTeX 默认提供的绘制线条、圆等等功能并不复杂。可以使用一个名为 `pstricks` 的包在不费太大麻烦的情况下生成复杂的图形。让我们尝试使用 `pstricks` 绘制一条曲线：

```latex
\documentclass{article}

\usepackage{pstricks}

\usepackage{pst-plot}

\begin{document}

\begin{ppicture}(-3,-2) (3, 2)

\psaxes(0,0) (-3,-2) (3, 2)

\psplot[plotstyle=curve] (-1.5) {1.5} (x exp x)

\end{ppicture}

\end{document}
```

必须包含两个包：`pstricks` 和 `pst-plot`。此外，`pdflatex` 无法处理上述文件——你必须使用 `latex` 命令本身。

这一行：

```latex
\begin{ppicture}(-3,-2) (3, 2)
```

开始了 `ppicture` 环境——可以将其视为对 LaTeX 的请求，留出足够的空间放置一个矩形，其左下角坐标为 `(-3,-2)`，右上角为 `(3, 2)`。

下一条命令：

```latex
\psaxes(0,0) (-3,-2) (3, 2)
```

绘制坐标轴。X 轴和 Y 轴在点 `(0,0)` 处相交，它们必须被包含在一个想象的矩形框内，该框左下角在 `(-3,-2)`，右上角在 `(3, 2)`。

我们正在绘制曲线：

```text
y = (x * x * x) - x
```

该方程必须以一种特殊的后置（postfix）形式指定。按照通常编写的算术表达式：

```text
2 * 3 + 4
```

被称为**中缀表达式**。这里是另一种编写相同表达式的写法：

```text
2 * 3 * 4 +
```

这被称为**后置表达式**。逻辑很简单：从左到右读取表达式。当你遇到一个运算符时，只需将该运算符应用于左侧的两个操作数。

在上面的例子中，当我们看到 `*` 运算符（乘法）时，我们可以将表达式重写为：

```text
6 4 +
```

现在，当我们遇到 `+` 运算符时，我们可以将表达式重写为：

```text
10
```

让我们查看 LaTeX 文档中的这一行：

```latex
\pslot[plotstyle=curve] {-1.5} {1.5} {x 3 exp x sub}
```



我们正在要求 LaTeX 绘制一条曲线；该曲线由方程给出：

```
y = x 3 exp x sub
```

（注意：你只需要指定方程的右侧）。

该方程是以后置形式编写的：`exp` 是幂运算符，`sub` 是减法运算符。因此我们可以将其读为：

```
y = (x 的 3 次方) 减 x
```

括号中的数字 `-1.5` 和 `+1.5` 指 `x` 的取值范围。

## 16.5. 使用 "pstricks" 进行高级绘图

# 第十七章

# 附录 1 - 编写独立的 Python 程序

到目前为止，我们一直使用交互式 Python 提示符来编写短程序。这种方法的缺点显而易见 - 当退出 Python 时，你编写的所有代码都会丢失。在本章中，我们将学习如何将 Python 程序永久存储在文本文件中。

## 17.1 在 GNU/Linux 中使用编辑器

编辑器是一个帮助创建文本文件的程序，这些文件可以永久保存在计算机硬盘上。GNU/Linux 操作系统带有许多编辑器；其中最常用的两个是 `vi` 和 `emacs`。对于绝对初学者来说，这两者都有点难以使用。更好的选择可能是一个名为 `gedit` 的程序。你只需在操作系统命令行输入 `gedit` 即可运行它（关于命令行的讨论请参阅第 1 章）。

`gedit` 易于使用。你可以输入任何想要的内容；一旦完成输入，就是保存你输入的数据了。为此，从 File（文件）菜单中选择 Save（保存）选项；`gedit` 将显示你想要保存输入数据的文件名。从 File（文件）菜单中选择 Quit（退出）选项退出 `gedit`。

## 17.2 使用 gedit 编写 Python 程序

运行 `gedit` 并将以下行保存到名为 `hello.py` 的文件中：

```
print "Hello"
```

退出 `gedit` 并在操作系统命令行输入以下内容：

```
python hello.py
```

你将看到屏幕上打印出“Hello”。

使用 `gedit` 创建另一个文件并在其中存储以下代码（`.py` 后缀告诉我们正在处理包含 Python 代码的文件）：

```
def sqr(x):
    return x+x

m = sqr(3)
print m
```

你可以通过在命令行输入运行代码：

```
python abc.py
```

**注意：** 以这种方式编写 Python 代码时你应该更加小心。当你在 Python 提示符输入代码时，遇到语法错误会立即时反馈。而在文件中存储并执行 Python 代码并非如此。

## 17.3 执行键盘输入

使用 `gedit` 将此程序存储在名为 `test.py` 的文件中：

```
a = input()
b = input()
print a * b
```

在命令行运行代码：

```
python test.py
```

`input` 函数等待你从键盘输入数据；输入数字 `10` 并按下 `Enter` 键。数字将被读取并存储在变量 `a` 中。现在输入另一个数字（比如 `20`）并按下 `Enter`；它将被存储在 `b` 中。程序将输出 `200`。

# 第十八章

# 许可证

本书根据 GNU FDL 发布

# 第十九章 如何从源码构建书籍

本书是用一个名为 Sphinx 的优秀工具编写的。Sphinx 允许你使用简单的重构文本格式进行编写 - HTML（用于在浏览器显示）以及 LaTeX（用于打印）均由 Sphinx 完成。你现在阅读的就是 Sphinx 生成的书籍！源代码可以在 GitHub 获取。

关于我写书的工作流一点：我在家庭机器上维护一个 `git` 仓库，偶尔推送到 GitHub。我在我的 Linode 分片上还有另一个 `git` 仓库用于托管书籍 - 偶尔从 GitHub 拉取并结合直接将 HTML 文件交付到 Web 服务器（我使用 Nginx - 如果你发现 Apache 内存占用过多，可以试试）静态文件文件夹的构建，即可“发布”书籍！
