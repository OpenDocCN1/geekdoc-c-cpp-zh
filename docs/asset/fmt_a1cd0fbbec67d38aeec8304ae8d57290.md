
选择“文件：保存”（`File:Save`）显示“另存为”对话框，如图 4-14 所示。编辑窗口会自动选择 `Python33` 文件夹来保存你的应用程序。然而，这是 Python 代码所在的地方，将应用程序代码保存在同一个文件夹中是一个坏主意。

书中的示例代码包含在一个名为 `BP4D`（Beginning Python For Dummies）的文件夹中。本章的代码可以在下载源代码的 `\BP4D\Chapter4` 子文件夹中找到（请参见“引言”部分查看在线源代码的位置）。如果你愿意，可以在跟随书籍学习时，使用适用于你平台的方法创建一个具有相似名称的目录结构。你也可以打开书籍的可下载源码文件，避免输入示例代码。

70 第一部分：开始学习 Python

在“另存为”对话框的文件名字段中输入 `FirstFit.py` 并点击保存。你的应用程序代码现在已保存到磁盘上，你可以随地访问它。

![](img/ec69aa1535cd82c735ee14abfc05048f_85_0.png)

图 4-14：“另存为”对话框提供了保存你应用程序的手段。

当你回到编辑窗口时，标题栏的文本发生了变化，如图 4-15 所示。注意标题栏包含了应用程序的完整路径。

![](img/ec69aa1535cd82c735ee14abfc05048f_85_1.png)

图 4-15：磁盘上的应用程序在标题栏中显示其名称和路径。

## 运行应用程序

如果你不能运行应用程序，它们就没用。Python 提供了多种方法运行你创建的任何应用程序。本节探索了在创建应用程序后运行它的最简单的方法。你将在本章的“加载和运行应用程序”部分看到其他方法。需要记住的重要点是，Python 提供了一个极其灵活的环境，因此如果执行某任务的方法不起，另一种方法几乎一定会成功。

要运行这第一个应用程序，选择“运行-模块”（`Run-Module`）。你会看到一个新的 Python Shell 窗口打开，然后你的应用程序的输出将如图 4-16 所示。

```
Python 3.3.4 Shell
File Edit Debug Options Windows Help
Python 3.3.4(v3.3.4:7ff621e426, Feb 20 2014, 18:13:51) [MSC v.1600 64 bit (AM-D4)] on win32
>>> Type "copyright", "credits" or "license()" for more information.
===============================================================
>>> RESTART ==================================================
>>> This is a simple Python application.
>>> |
```

图 4-16 中的两行输出你现在应该很熟悉了——它们是启动 shell 时总是出现的信息。接下来是一条消息。你会看到这条消息，每当你运行应用程序时都会看到它。要亲眼看到，回到编辑窗口并选择“运行-模块”。Python Shell 显示了输出，如图 4-17 所示。

72 第一部分：开始学习 Python

```
Python 3.3.4 Shell
File Edit Debug Options Windows Help
Python 3.3.4(v3.3.4:7ff621e426, Feb 20 2014, 18:13:51) [MSC v.1600 64 bit (AM-D4)] on win32
>>> Type "copyright", "credits" or "license()" for more information.
===============================================================
>>> RESTART ==================================================
>>> This is a simple Python application.
>>> |
```

图 4-17：Python Shell 显示了它的名称和路径。

## 缩进

如果你不能运行应用程序，它们就没用。Python 提供了多种方法运行你创建的任何应用程序。本节探索了在创建应用程序后运行它的最简单方法。你将在本章的“加载和运行应用程序”部分看到其他方法。

缩缩。

图 4-16 中的两行输出你现在应该很熟悉了——它们是启动 shell 时总是出现的信息。接下来是一条消息，每当你运行应用程序时都会看到它。。亲亲看到看到，回到窗口窗口并运行-。

图 4-17：Python Shell 显示了输出。

```
Python 3.3.4 Shell
File Edit Debug Options Windows Help
Python 3.3.4(v3.3.4:7ff621e426,. 20 2014, 18:13:51) [
..1600 64. (AM-D4.. on32
 "
. ".
 or "
 for for.
。
```

## 第 4 章：编写你的第一个应用程序

尽管单行注释和多行注释都是注释，但 IDLE 编辑器可以让你轻松地区分两者。当你使用默认配色方案时，单行注释显示为红色文本，Python 并不关心颜色；这些颜色只是为了帮助你这个开发者。

## 使用注释给自己留点提醒

许多人并不真正理解注释——他们不知道在代码中该如何处理注释。请记住，你可能今天写了一段代码，但在好几年之后才再看它。你需要唤醒记忆，以便记住这段代码的功能以及你为什么要写它。事实上，在代码中使用注释有以下几个理由：

- 提醒自己代码的作用以及你写这段代码的原因
- 告诉他人如何维护你的代码
- 让其他开发者能够阅读你的代码
- 列出未来更新的想法
- 提供你编写代码时使用的文档来源列表
- 维护一份你所做的改进列表

你也可以以许多其他方式使用注释，但这些是最常见的方法。看看书中的示例是如何使用注释的，特别是当你进入后面的章节，代码变得更加复杂时。随着代码变得复杂，你需要添加更多的注释，并让注释与你需要记忆的内容密切相关。

## 使用注释防止代码执行

开发者有时会使用注释功能来防止某些行代码执行（被称为“注释掉”）。你需要这样做来确定某行代码是否导致了你的应用程序失败。事实上，这是处理代码的一种非常常见且有效的方法，以至于添加此类注释的技术已直接内置在 IDLE 中。这里是该功能工作原理的示例。假设你有一个像图 4-20 所示的应用程序（位于下载源码包提供的 `Comments.py` 文件中）。

图 4-20：有时开发者需要注释掉代码行。

你可能想注释掉显示“This code is commented out.”的行。要这样做，请将插入点置于行首，或简单地选择整行，然后选择 `Format>Comment Out Region`（格式>注释区域）。IDLE 随后会在代码中添加单行注释，如图 4-21 所示。注意，这个单行注释使用了两个井号（`##`），以与手动创建的单行注释区分开来。

```
Python 3.3.4: Comments.py - C:\BBP4D\Chapter04\Comments.py

File Edit Format Run Options Windows Help

***

Application: Comments.py

Written by: John

Purpose: Shows how to use comments.

***

## This is a comment.

print("Hello from Python!") #This is also a comment.

##print("This code is commented out.")
```

图 4-21：注释掉任何不想让 Python 执行的代码。

## 第 4 章：编写你的第一个应用程序

当然，你还不知道注释已经生效。将文件保存到磁盘，然后运行 `Run:Run Module`（运行：运行模块）。你看到一个新的 Python 窗口打开，只有一行输出，如图 4-22 所示。因此，第一个没有被注释掉的 `print()` 命令执行了该行，但第二个没有执行。

```
Python 3.3.4 Shell

File Edit Shell Debug Options Windows Help

Python3.3.4 (v3.3.4:7ff6241e526, Feb 10 2014, 18:13:51) [MSC v.1600 64 bit (AMD D64)] on win32

>>> "copyright", "credit" or "license" for more information.

>>> RESTART =================

>>> Hello from Python!

>>>

Ln: 6:Col 4
```

图 4-22：注释掉的代码行不会执行。

要将代码重新加入应用程序，将插入点置于行首，或高亮整行，然后选择 `Format>Uncomment Region`（格式>取消注释）。IDLE 将将移除它之前添加的注释。保存文件并选择 `Run Module`，你会看到两个 `print()` 命令，如图 4-23 所示。

```
Python 3.3.4 Shell

File Edit Shell Debug Options Windows Help

Python3.3.4 (v3.3.4:7ff6241e526, Feb 10 2014, 18:13:51) [MSC v.1600 64 bit (AMD D64)] on win32

>>> "copyright", "credit" or "license" for more information.

>>> RESTART =================

>>> Hello from Python!

>>> This code is commented out.

>>>

Ln: 10:Col 4
```

图 4-23：当两者都没有被注释时，两个命令。

你可以通过高亮所有行并选择 `Format:Comment Out Region` 来注释多行代码。同样，你可以通过高亮行并选择 `Format:Uncomment Region` 来取消注释多行代码。你不需要逐行注释，除非你只有一行代码需要检查。

![](img/ec69aa1535cd82c735ee14abfc05048f_92.png)

## 加载和运行应用程序

编写完成后，你需要运行它来查看是否有效。有几种方法可以实现，但常见的是使用 `Run:Run Module` 命令。

## 使用编辑器

当你编写代码时，你使用的是编辑器。这是你输入 Python 命令的地方。编辑器具有许多帮助你编写更好代码的功能，例如语法高亮和代码补全。

## 使用 Shell 窗口

当你运行代码时，输出出现在 Shell 窗口中。这是你查看代码结果的地方。Shell 窗口也是交互式的，你可以直接在其中输入命令并获得结果。

## 使用命令行

命令行是运行 Python 代码的另一种方法。这在运行已经编写好的脚本时特别有用。运行脚本时，你使用 `python` 命令后跟文件名。

![](img/ec69aa1535cd82c735ee14abfc05048f_93.png)

## 第二部分

## 话术

```python

Python 3.3.4 (v3.3.4:Tff62415e426, Feb 10 2014, 18:13:51) [MSC v1600 64 bit (AM-D64)] on win32

Type "copyright","credits" or "license()" for more information.

>>> def Hello():

    print("This is my first Python function!")

>>>

>>> Hello()

This is my first Python function!

>>> |
```
