

## 步骤 5 为你的代码输入一个名称，例如 'print hello'，然后点击保存按钮。Python 代码将被保存，如果执行，结果将在 IDLE Shell 中详细显示。在这种情况下，显示的内容为 'Hello everyone!'。

## 步骤 8 让我们扩展代码，并输入上一个教程中的几个示例：

```
a=2
b=2
name="David"
surname="Hayward"
print(a+b)
```

![](img/588364e02a77f179099fae91a1713f0a_26_0.png)

如果你按下 F5，它将保存代码，因为它已经从以下内容进行了修改：

![](img/588364e02a77f179099fae91a1713f0a_26_1.png)

## 步骤 6 这是你大部分 Python 代码的运行方式。将其输入编辑器编辑器，按下 F5，保存代码并查看 Shell 中的输出。有时输出会有所不同，取决于你是否请求了独立窗口，但本质上就是这个过程。除非另有说明，否则我们将全程使用这个过程。

如果你点击 OK 按钮，文件将被新的代码条目覆盖并执行，输出将在 Shell 中。对于这几行代码这不是问题，但如果你编辑了一个较大的文件，覆盖可能会成为问题。使用编辑器中的“File > Save As”来创建一个副本。

![](img/588364e02a77f179099fae91a1713f0a_26_2.png)

## 步骤 7 如果你打开保存 Python 代码的位置，你会发现它是 .py 扩展名。这是 Python 文件的默认文件名。你创建的任何代码可以是任意名称，从互联网下载的任何代码也是。只需确保代码是为 Python 3 编写的。

## 步骤 10 创建一个新文件。关闭编辑器并打开一个新实例（File > New File from the Shell）。输入以下并保存为 hello：

```
a="Python"
b=15
c="cool!"
print(a, b, c)
```

你将在教程中使用这段代码。

![](img/588364e02a77f179099fae91a1713f0a_26_3.png)

![](img/588364e02a77f179099fae91a1713f0a_26_4.png)

## 从命令行执行代码

尽管我们在本书中一直使用 GUI（图形界面），但查看一眼 Python 的命令行处理也是值得的。我们已经知道有一个命令行版本的 Python，它也被用于执行代码。

## 命令行执行代码

使用我们在上一个教程中创建的代码（即命名为 hello.py 的代码），看看如何在命令行级别运行在 GUI 中创建的代码。

- 步骤 1 在 Linux 中，Python 有两种通过命令行执行代码的方法。其中一种方法是使用 Python 2，而另一种是使用 Python 3 库等。首先，进入你操作系统的命令行或终端（Terminal）。

- 步骤 3 现在你已处于命令行界面，我们可以开始运行 Python。对于 Python 3，你需要输入命令并按回车键。这将你进入命令行版本的 Shell，并带有熟悉的三个右箭头作为光标 (>>)。

![](img/588364e02a77f179099fae91a1713f0a_27_0.png)

- 步骤 2 像之前一样，我们使用的树莓派：Windows 需要点击开始按钮并搜索 CMD，然后点击搜索结果中的 Command Line；macOS 用户可以通过点击 Go > Utilities > Terminal 来访问他们的命令行。

- 步骤 4 从这里你可以输入我们之前看过的代码，例如：

```
a=2
print(a)
```

你可以发现它的工作原理完全一样。

![](img/588364e02a77f179099fae91a1713f0a_27_1.png)

## 从命令行执行代码

**步骤 5** 现在输入：exit() 以退出命令行会话并返回命令提示符。进入你从上一个教程保存的文件夹，并列出其中的可用文件；希望你能看到 hello.py。

**步骤 8** 从 Python 2 代码运行 Python 3 代码的结果是非常显而易见的。虽然由于 Python 3 处理 Print 的方式与 Python 2 不同，它并没有报错，但结果并不是我们预期的。使用 Sublime 打开 hello.py：

```
hello.py
python 2.7 (default Oct 19 2014, 12:31:11)
print('copyright', 'credits' or 'license' for more information.
print('hello, world')

exit()
C:\Documents\rasberrypi~/Documents/Python Code
python hello.py
rasberrypi~/Documents/Python Code $
python3 hello.py
rasberrypi~/Documents/Python Code $
```
```
hello.py
python 2.7 (default Oct 19 2014, 12:31:11)
print('copyright', 'credits' or 'license' for more information.
print('hello, world')

exit()
C:\Documents\rasberrypi~/Documents/Python Code
python hello.py
rasberrypi~/Documents/Python Code $
python3 hello.py
rasberrypi~/Documents/Python Code $
```

**步骤 6** 在你要运行的代码所在的文件夹内，输入 python3 hello.py 将执行该代码，提醒你：

**步骤 9** 由于树莓派上没有 Sublime Text，暂时离开树莓派并使用 Python IDLE。打开 hello.py 文件，包含以下内容：

```
a="Python"
b="cool"
print(a, b, c)

name=input("What is your name?")
print("hello", name)
```
```
hello.py
python 2.7 (default Oct 19 2014, 12:31:11)
print('copyright', 'credits' or 'license' for more information.
print('hello, world')

exit()
C:\Documents\rasberrypi~/Documents/Python Code
python hello.py
rasberrypi~/Documents/Python Code $
python3 hello.py
rasberrypi~/Documents/Python Code $
```
```
hello.py
python 2.7 (default Oct 19 2014, 12:31:11)
print('copyright', 'credits' or 'license' for more information.
print('hello, world')

exit()
C:\Documents\rasberrypi~/Documents/Python Code
python hello.py
rasberrypi~/Documents/Python Code $
python3 hello.py
rasberrypi~/Documents/Python Code $
```

**步骤 7** 自然地，既然你正在使用 Python 3，如果你尝试用 Python 2 输入语法和布局是 Python 3 特有的：

**步骤 10** 保存 hello.py 文件并回到命令行。现在新保存的 python3 hello.py hello.py 结果将是原始代码！在你的代码中添加 input 并在窗口中显示。

```
hello.py
python 2.7 (default Oct 19 2014, 12:31:11)
print('copyright', 'credits' or 'license' for more information.
print('hello, world')

exit()
C:\Documents\rasberrypi~/Documents/Python Code
python hello.py
rasberrypi~/Documents/Python Code $
python3 hello.py
rasberrypi~/Documents/Python Code $
```
```
hello.py
python 2.7 (default Oct 19 2014, 12:31:11)
print('copyright', 'credits' or 'license' for more information.
print('hello, world')

exit()
C:\Documents\rasberrypi~/Documents/Python Code
python hello.py
rasberrypi~/Documents/Python Code $
python3 hello.py
rasberrypi~/Documents/Python Code $
```

## 数字与表达式

我们已经看到了 Python 的一些基础数学表达式，简单的加法等。现在让我们扩展一下，看看 Python 作为计算器有多强大。你可以在 IDLE Shell 或编辑器中工作，随你喜欢。

## 全都是数学

你可以利用 Python 的数学能力获得一些令人惊讶的结果；正如大多数（并非所有）编程语言一样，数学是大脑后部的小器官

- 步骤 1 如上所述打开 Python 3 GUI 版本。下次当你准备使用 Shell 或编辑器来活跃大脑后部（或不在）的小器官时：

- 步骤 3 你可以使用所有的数学操作：除法、乘法、括号等。练习几个，例如：

```
1/2
6/2
2*3
(1+2)+(3*4)
```

```
Python 3.4.2 Shell
File Edit Shell Debug Options windows help
Python 3.4.2 (default. Oct 19 2014, 13:31:11)
(GCC 4.9.0) on Linux
>>> print("copyright "credits" or "license") for more information.
>>> 1/2
0.5
>>> 54356+3553245
3607601
>>> 986734*2734484421
269807102281179024
```

- 步骤 2 在 Shell 中输入：
2*2
54356+3553245
986734*2734484421

- 步骤 4 你没有注意到，除法产生的是小数。在 Python 中这些被称为浮点数（floats）或浮点运算。然而，如果你需要将整数转换为小数，可以使用双斜杠：

你可以看到 Python 可以轻松处理大数字。

```
1/2
6/2
2*3
(1+2)*(3*4)
```

等等如此。

```
Python 3.4.2 Shell
File Edit Shell Debug Options windows help
Python 3.4.2 (default. Oct 19 2014, 13:31:11)
(GCC 4.9.0) on Linux
>>> print("copyright "credits" or "license") for more information.
>>> 1/2
0.5
>>> 54356+3553245
3607601
>>> 986734*2734484421
269807102281179024
```

