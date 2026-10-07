
`def get_dirlist(path):`

```
    """

    返回 path 中所有条目的排序列表。

    返回的是名称，而不是名称的完整路径。

    """

    dirlist = os.listdir(path)

    dirlist.sort()

    return dirlist
```

`def print_files(path, prefix=""):` 

```
    """打印 path 内容的递归列表，打印标题

    """

    if prefix == "":

        # 检测最外层调用

        print("Folder listing for, " + path)

        prefix = " | "

    dirlist = get_dirlist(path)

    for f in dirlist:

        print(prefix+f) # 打印行

        fullname = os.path.join(path, f) # 将名称转换为完整路径

        if os.path.isdir(fullname):

            # 如果是目录，则递归。

            print_files(fullname, prefix + " | ")
```

调用函数 `print_files` 并传入文件夹名将产生类似下面的输出：

- __init__.py
- aacircle.py
- aliens.py
- arraydemo.py
- blend_fill.py
- blit_blends.py
- camera.py
- chimp.py
- cursors.py
- data
- alien1.png
- alien2.png
- alien3.png
..>

## 18.6 术语表

**base case (基础情况)** 递归函数中条件语句的一个分支，不会产生进一步的递归调用。

**infinite recursion (无限递归)** 一个函数不断递归地调用自己，而永远不会到达任何基础情况。最终，无限递归会导致运行时错误。

**recursion (递归)** 调用一个正在执行的函数的过程。

**recursive call (递归调用)** 调用已执行中的函数的语句。递归也可以是间接的——函数 $f$ 调用 $g$，$g$ 调用 $h$，而 $h$ 可能会调回 $f$。

**recursive definition (递归定义)** 一种通过自身来定义某些事物的定义。为了使其有用，它必须包含非递归的 *base cases*。通过这种方式，它区别于 *circular definition*（循环定义）。递归定义通常提供了一种表达复杂结构的优雅方式，例如包含其他目录的目录，或者包含其他菜单的菜单。

## 18.7 练习

1. 修改科赫分形，使其绘制出雪花，如下：(img/ddd769225b55d8f3b97c0d284_0.png)
2. (a) 根据用户给定的阶数绘制一条塞萨罗线。我们展示了四条阶数分别为 0,1,2,3 的不同线。在这个例子中，折叠角为 10 度。(img/ddd769225b55d8f3b97c0d284_0.png)
This model通过“兔子永远不死”的简化假设来解释兔子的繁殖。科学家经常做出（不切实际的）简化假设和限制，以便更好地理解解决问题。
如果我们使用从 0 开始的数列术语，可以递归地描述每一项为前两项之和：
```python
fib(0) = 0
fib(1) = 1
fib(n) = fib(n-1) + fib(n-2) for n >= 2
```
这直接翻译为一些 Python：
```python
def fib(n):
    if n <= 1:
        return n
    t = fib(n-1) + fib(n-2)
    return t
```
这是一个特别低效的算法，当我们学习字典时，我们将展示一种修复它的方法：
```python
import time
t0 = time.clock()
n = 35
result = fib(n)
t1 = time.clock()
print("fib({0}) = ({1}, ({2:.2f} secs)".format(n, result, t1-t0))
```
我们得到了正确的结果，但工作量是爆炸性的！
fib(35) = 9227465, (10.54 secs)

## 18.5 递归目录和文件的示例

以下程序列出了目录及其子目录的内容。
```python
import os
def get_dirlist(path):
    """
    返回 path 中所有条目的排序列表。
    返回的是名称，而不是名称的完整路径。
    """
    dirlist = os.listdir(path)
    dirlist.sort()
    return dirlist
def print_files(path, prefix=""):
    """打印 path 内容的递归列表，打印标题
    """
    if prefix == "":
        # 检测最外层调用
        print("Folder listing for, " + path)
        prefix = " | "
    dirlist = get_dirlist(path)
    for f in dirlist:
        print(prefix+f) # 打印行
        fullname = os.path.join(path, f) # 将名称转换为完整路径
        if os.path.isdir(fullname):
            # 如果是目录，则递归。
            print_files(fullname, prefix + " | ")
```

调用函数 `print_files` 并传入文件夹名将产生类似下面的输出：
- __init__.py
- aacircle.py
- aliens.py
- arraydemo.py
- blend_fill.py
- blit_blends.py
- camera.py
- chimp.py
- cursors.py
- data
- alien1.png
- alien2.png
- alien3.png
..>

## 18.6 术语表

# 如何像计算机科学家一样思考：使用 Python 3 学习
文档，第3版

```
"C:\Python31\Lib\site-packages\pygame\docs\ref\mask.html",
"C:\Python31\Lib\site-packages\pygame\docs\ref\midi.html",
"C:\Python31\Lib\site-packages\pygame\examples\aliens.py",
"C:\Python31\Lib\site-packages\pygame\examples\data\boom.wav",
..
```

- 11. 写一个名为 `litter.py` 的程序，以目录树的根作为参数（默认为当前目录），在目录树的每个子目录下创建一个名为 `trash.txt` 的空文件。现在写一个名为 `cleanup.py` 的程序来删除所有这些文件。

**提示 #1：** 以本章最后一节的示例作为这两个递归程序的基础。因为你将要删除磁盘上的文件，最好确保万无一失否则可能会丢失你关心的文件。一个非常好的建议是，最初你应该模拟删除文件——只需打印你打算删除的每个文件的完整路径名。一旦你确认逻辑正确，就可以将 `print` 语句替换为真实操作。

**提示 #2：** 在 `os` 模块中查找删除文件的函数。

## 18.7 练习题

# 第十九章
# 异常

## 19.1 捕获异常

当发生运行时错误时，会创建一个异常对象。程序在此处停止运行，Python 会打印出回溯（traceback），其以一条描述所发生异常的消息结束。

例如，除以零会导致异常：
```python
>>> print(5/0)
Traceback (most recent call last):
File "<interactive>", line 1, in <module>
ZeroDivisionError: integer division or modulo by zero
```

访问不存在的列表项也是：
```python
>>> a = []
>>> print(a[5])
Traceback (most recent call last):
File "<interactive>", line 1, in <module>
IndexError: list index out of range
```

或者尝试对元组进行项赋值：
```python
>>> tuple = ("a", "b", "d", "d")
>>> tuple[2] = "c"
Traceback (most recent call last):
File "<interactive>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

在每种情况下，冒号所在的消息包含两个部分：冒号之前的错误类型，以及冒号后面的错误细节。

有时我们想要执行一个可能会引发异常的操作，但我们不希望程序停止。我们使用 `try` 语句来“包裹”一段代码并处理异常。

例如，我们可能会提示用户输入文件名然后打开它。如果文件不存在，我们不希望程序崩溃；我们想要处理异常：
```python
filename = input("Enter a file name: ")
try:
    f = open(filename, "r")
except:
    print("There is no file named", filename)
```

`try` 语句有三个子句（或部分），由 `try ... except ... finally` 关键字引入。`except` 或 `finally` 子句可以省略，因此上面的代码显示了 `try` 语句最常见的版本。

`try` 语句执行并监控第一个块中的语句。如果没有发生异常，它将跳过 `except` 子句下的块。如果发生任何异常，它将执行 `except` 子句中的语句然后继续执行。

我们可以将此功能封装在一个函数 `exists` 中，它接收一个文件名，如果文件存在则返回真，不存在则返回假：
```python
def exists(filename):
    try:
        f = open(filename)
        f.close()
        return True
    except:
        return False
```

## 不使用异常来测试文件是否存在

我们刚刚展示的函数并不是我们推荐的。它打开并关闭文件，这在语义上不同于询问“它是否存在？”

这里有一个检查文件存在的更好方法：
```python
import os
def exists(filename):
    return os.path.exists(filename)
```

`os.path.exists()` 函数在路径存在时返回 True，否则返回 False。这比尝试打开文件高效得多。

# 如何像计算机科学家一样思考：使用 Python 3 学习
文档，第3版

## 19.2 抛出我们的异常

有时即使没有发生错误，我们也自己抛出异常。例如，我们可能想要确保一个数字是正数：
```python
def check_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
try:
    check_age(-5)
except ValueError as e:
    print(e)
```

`raise` 关键字用于触发异常。

## 19.3 回顾之前的示例

使用异常处理，我们现在可以修改 `recursion_depth` 示例，使其在达到最大递归深度时停止：
```python
def recursion_depth(number):
    print("Recursion depth", number)
    try:
        recursion_depth(number + 1)
    except:
        print("I cannot go deeper into this wormhole.")
recursion_depth(0)
```

## 19.4 try语句的 finally 子句

一种编程模式是获取某种资源——例如我们为绘画创建一个窗口，处理与互联网服务商的连接，或者打开一个文件进行写入。我们执行可能会引发异常的计算，或者顺利地运行。

无论发生什么，我们都想要“清理”收集到的资源——例如关闭窗口、断开拨号连接或关闭文件。`try` 语句的 `finally` 子句就是执行此操作的方法。考虑这个（有些为了的）示例：
```python
import turtle
import time
def show_poly():
    try:
        win = turtle.Screen() # 获取/创建资源，例如一个窗口
        tess = turtle.Turtle()
        # 这个对话框可能会被取消，
        # 或者转换为 int 可能会失败，或者 n 可能为零。
        n = int(input("How sides do you want in your polygon?"))
        angle = 360 / n
        for i in range(n): # 绘制多边形
            tess.forward(10)
            tess.left(angle)
            time.sleep(3) # 让程序等待几秒
    finally:
        win.bye() # 关闭乌龟窗口
show_poly()
show_poly()
show_poly()
```

# 如何像计算机科学家一样思考：Python 3 学习文档，第三版

在第 20–22 行中，`show_poly` 被调用了三次。每次调用都会为它的乌龟创建一个窗口，并根据用户输入的边数绘制一个多边形。但如果用户输入了一个无法转换为 `int` 的字符串怎么办？如果他们关闭了对话框呢？我们会得到一个异常，即使发生了异常，我们仍然希望关闭乌龟的窗口。第 17–18 行为我们完成了此工作。无论 `try` 子句中的语句是否成功完成，`finally` 块始终会被执行。

注意，该异常仍然未被处理——只有 `except` 子句可以处理异常，因此我们的程序仍然会崩溃。但至少在崩溃之前，它的乌龟窗口会被关闭！

## 19.5 术语表

**exception**（异常）运行时发生的错误。

**handle an exception**（处理异常）通过将代码块封装在 `try-except` 结构中，防止异常导致程序崩溃。

**raise**（抛出）使用 `raise` 语句创建一个人为的异常。

## 19.6 练习

+ 1. 写一个名为 `readposint` 的函数，使用 `input` 对话框提示用户输入正整数，然后检查输入以确认其符合要求。它能够能够无法转换为 `int` 的输入、负整数 `ints` 以及边缘情况（例如，用户关闭了对话框或没有输入任何内容）。

# 第二章
# 字典

我们目前为止详细学习的所有复合类型——字符串、列表和元组——都是序列类型，它们使用整数作为索引来访问其中包含的值。

字典是另一种复合类型。其值是 Python 的映射类型。它们将键（可以是任何不可变对象）映射到值（可以是任何类型，异构的），就像列表或元组的元素一样。在其他语言中，它们被称为关联数组，因为它们将键与值关联在一起。

例如，我们将创建一个字典将英语单词翻译成西班牙语。对于这个字典，键是字符串。

创建字典的一种方法是从空字典开始并添加键:值对。
空字典表示为 `{}`：
```python
>>> eng2sp = {}
>>> eng2sp["one"] = "uno"
>>> eng2sp["two"] = "dos"
```

第一次赋值创建了字典 `eng2sp`；其他赋值添加了新的键:值对。我们可以用通常的方法打印字典的当前值：
```python
>>> print(eng2sp)
('two': 'dos', 'one': 'uno')
```

字典的键:值对由逗号分隔。每对包含一个键和一个值。

# 哈希

值对的顺序可能与预期的不同。Python 使用复杂的算法（旨在极快速访问）来确定键:值对存储在字典中的位置。对于我们的目的，可以将其看作是不可预测的排序。

你可能会奇怪，为什么还要使用字典，因为将键映射到值的相同概念可以使用元组的列表来实现：
```python
>>> [('apples', 430), ('bananas', 312), ('orange', 525), ('pears', 217)]
{'pears': 217, 'apples': 430, 'orange': 525, 'bananas': 312}
```
