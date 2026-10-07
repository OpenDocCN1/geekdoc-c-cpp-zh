
[图 2-2](Figure-2-2) 中的提示符之一提到，你可以在 Python 解释器中输入 `help` 作为命令。注意你不要输入引号，只需使用 `help`（然后始终按回车）。这次你看到

```
help() 用于交互式帮助，或使用 help(object) 获取关于对象的帮助。
```

现在解释器正在要求你输入 `help` 后跟一个空括号，或者在括号中输入特定单词后输入 `help`（object 是给出的示例）。确保你在输入命令后按了回车。请继续输入以下内容：

注意该行没有空格。按下回车键后，屏幕提供了了关于使用 Python 交互式帮助的信息。

在窗口底部看到 `help>` 表明你不再处于操作系统 shell 或 Python 解释器中（后者始终显示 `>>>`），而是处于一个提供帮助的新区域。正如屏幕所示，你可以输入任何模块、关键字或主题名称来获取关于该术语的帮助。作为初学者，你现在可能不需要这些具体内容。但知道在需要时帮助就在那里是好的。

例如，Python 使用了一些在语言中具有特殊含义的关键字。要获取这些关键字的列表，只需在 `help>` 提示符下输入以下内容：

```
keywords
```

按下回车后，你将看到一个关键字列表，如图 2-3 所示。

| 问题 | 输出 | 终端 |
| :--- | :--- | :--- |
| False | class |  |
| None | continue |  |
| True | for |  |
| and | global |  |
| as | def |  |
| assert | elif |  |
| break | else |  |
| except | if |  |
| finally | is |  |
| with | yield |  |

图 2-3: 关键字帮助。

要退出 解释器并返回操作系统，输入 `exit()` 并按回车。

> TIP 如果你在文本底部看到 --More--，可以使用 Space (Mac) 或 Space (Windows) 滚动。

当你看到终端末尾出现系统提示符时，你就知道你退出了解释器。

Python 的内置帮助在你想要查找具体的术语和概念很有用。但对于初学者来说这通常很难。当你在线时，搜索可能更好。如果你在寻找视频，从 www.youtube.com 开始；如果没有，https://stackoverflow.com 是提问和搜索帮助的好地方。当然，还有 Google、Bing。

无论你使用什么搜索，记住在搜索时带有 python 这个词。许多编程语言共享相似的概念和关键字，如果你不在搜索请求中指定 Python 语言，无法预测得到什么样的结果。

## 为代码创建文件夹

在本节中，你创建一个文件夹来存储你在书中编写的所有 Python 代码，以便它们集中在一起并在需要时易找到。你可以将此文件夹放在任何地方并随意命名。

在 Windows 中，你可以导航到包含新文件夹的文件夹。（Alan 使用 OneDrive，你可以使用桌面、文档或任何文件夹。）在文件夹空白处点击右键，然后选择新建文件夹（Mac）或新建文件夹（Windows）。输入文件夹名称并按回车。为了跟随本章的示例，将你的文件夹命名为 Python Essentials。

## 输入、编辑和调试 Python 代码

由于人们倾向于将代码组织成文件夹（正如我们建议你对本章示例所做的那样），第一步是打开文件夹

在编辑器中包含你的代码。有几种方法可以实现。如果你是第一次尝试，请按照以下步骤操作：

+   1. **使用 Windows 的开始菜单或 Mac 的启动台打开 VS Code。**

+   2. **从 VS Code 的菜单栏点击文件（File）⇒ 打开文件夹（Open Folder），找到文件夹所在，点击你想要打开的文件夹名称，然后点击选择文件夹（Select Folder）。**

当前打开的文件夹名称显示在 VS Code 窗口左侧资源管理器面板顶部。

![](img/be36b4e9a8416f1ae2a353bd745f71cb_29_0.png)

> 你创建的每个 Python 代码文件都将是 `.py` 扩展名的纯文本文件。我们建议将你为本书创建的任何文件放在 Python Essentials 文件夹中（请参见上一节如何创建文件夹）。只要 VS Code 和你的 Python 3 工作区打开着，你就应该能够随时看到你的 Python Essentials。

要随时创建一个 `.py` 文件，请按照以下步骤操作：

+   1. **如果你还没有这样做，请打开 VS Code 和你的 Python Essentials 文件夹。**

+   2. **如果资源管理器面板没有打开，点击 VS Code 左上角附近的资源管理器图标。**

+   3. **要在你的 Python Essentials 文件夹中创建文件，点击文件夹名称右侧的新建文件（New File）。**

+   4. **输入带有 `.py` 扩展的文件名（第一个文件输入 `hello.py`）并按回车。**

新文件将打开，你可以在右侧的标签页中看到它的名称。标签下方较大的区域是编辑器，你可以在那里输入 Python 代码。文件名也会显示在资源管理器中 Python Essentials 文件夹名称下方，因为它是存储在那里的。

现在你已经打开了一个 `.py` 文件，可以用它来编写一些 Python 代码了。就像学习新编程语言时通常一样，你将从输入一个简单的 Hello World 程序开始。以下是步骤：

+   1. 点击编辑区域第 1 行的右侧。

+2. 输入以下内容：

```
print("Hello World")
```

在你输入时，你可能会注意到屏幕上出现文本。那些文本是 IntelliSense 文字，它会检测你输入的内容并向你显示关于该关键字的一些信息。具体显示多少信息取决于你是否在使用 GitHub Copilot。但你不需要对它做任何操作——继续输入即可。

+   3. 输入该行后按回车。

新行代码将显示在屏幕上。你可能还会注意到其他几个变化，如图 2-4 所示：

> >> 资源管理器图标上有一个点，或者可能是一个圆圈的数字 1，表示你当前有一个未保存的更改。

> >> 标签页中的 `hello.py` 名称显示有一个点，表示该文件有未保存的更改。

你在 VS Code 中输入的代码不会自动保存。有两种方法来处理这个问题。一种是记住每当你进行了值得保存的更改时就进行保存。这样做最简单的方法是从 VS Code 的菜单栏中选择文件（File）⇒ 保存（Save），或者在 Windows 上按 `Ctrl+S`，或者在 Mac 上按 `⌘+S`。

![](img/be36b4e9a8416f1ae2a353bd745f71cb_31_0.png)

图 2-4：`hello.py` 文件包含一些 Python 代码并有未保存的更改。

我们更喜欢第二种方法，即使用自动保存（AutoSave）自动保存我们做的更改。要启用自动保存，从 VS Code 的菜单栏选择文件（File）⇒ 自动保存（Auto Save）。下次你打开文件菜单时，你会看到自动保存旁边有一个勾选，这告诉你自动保存已开启。要关闭自动保存，只需再次选择文件（File）⇒ 自动保存。当你进行更改时，文件会自动保存。

若要在 VS Code 中测试你的 Python 代码，你需要运行它。运行它最简单的方法是右键点击文件名（此例为 `hello.py`）并选择在终端运行 Python（Run Python in Terminal）。

如果提示选择 Python 解释器，只需选择你在第 1 章下载并安装的那个。通常情况下，它会被标记为“推荐”（Recommended）。如果你遇到困难，从 VS Code 的菜单栏选择视图（View）⇒ 命令面板（Command Palette）。输入 `python` 然后点击 Python：选择解释器（Python: Select Interpreter）。选择推荐选项。然后像上段描述的那样尝试运行 `hello.py`。

终端面板在 VS Code 窗口底部打开。你将看到一个命令提示符，后面跟着在 Python 解释器中运行代码的注释（`python.exe`）。在下方，你将看到程序的输出：在本例中为 Hello World 字，然后是另一个提示符，如图 2-5 所示。这个应用并不是世界上最令人兴奋的，但至少你知道了如何在 VS Code 中编写、保存和执行 Python 程序，在你继续阅读这本书以及整个 Python 编程职业中，你将经常使用这项技能。

| 问题 | 输出 | 调试控制台 | 终端 |
|---|---|---|---|
| C:\Users\Alan\OneDrive\AIO Python> & C:/Users/Alan/AppData/L | | | |
| Hello World | | | |
| C:\Users\Alan\OneDrive\AIO Python> | | | |

**图 2-5：** `hello.py` 的输出。

记住，当你学习某些代码时，你不可避免会犯错。这个应用并不是世界上最令人兴奋的，但至少你知道了如何在 VS Code 中编写、保存和执行 Python 程序，在你继续阅读这本书以及整个 Python 编程职业中，你将经常使用这项技能。

在尝试运行某些代码之前，你可能会看到几个迹象：

- 资源管理器图标上有一个点，或者可能是一个圆圈的数字 1，表示你当前有一个未保存的更改。

- 标签页中的 `hello.py` 名称显示有一个点，表示该文件有未保存的更改。

- 错误的代码会有波浪线底部。

Python 对大小写敏感，正确的命令是小写的。在图 2-6 中，我们输入了大写的 `PRINT`，这在 Python 中是不允许的。若要在终端运行该文件，你必须修复错误，我们将 `PRINT` 替换为 `print`（除非我们开启了自动保存）。然后我们右键并选择在终端运行 Python。

![](img/be36b4e9a8416f1ae2a353bd745f71cb_33_0.png)

**图 2-6：** `PRINT` 输入错误。

当你完成对 VS Code 中某个程序或文件的操作时，可以轻松关闭它。只需点击标签页中文件名旁边的 X，或者选择文件（File）。只要资源管理器打开着，文件的名称仍然可见。当你需要重新打开文件时，只需点击文件名即可。

如果你还没有 Python Essentials 文件夹，请参阅第 2 章关于如何创建它的信息。

- 2. 如果终端（Terminal）面板未打开，从 VS Code 菜单栏中选择 View ⇒ Terminal。

- 3. 输入 `python` 并按回车进入 Python 提示符 (`>>>`)。如果出现错误，在 Mac 上输入 `python3`，在 Windows 上输入 `py`。

- 4. 在 `>>>` 提示符处，输入 `import this` 并按回车。

格言列表将会出现。你可能需要向上或向下滚动或增大终端面板以看到所有内容。这些格言在哲学修辞上带有些幽默，但其核心思想始终是让代码对人类可读，而非机器可读。

```
PROBLEMS DEBUG CONSOLE TERMINAL
PS C:\Users\Alan\OneDrive\Python> python
Python 3.11.4 (tags/v3.11.4, d432bef, Jun 7 2023, 05:45:37) [MSC v.1934 64 bit (AMD64)] on win32
type "help", "copyright", "credits" or "license" for more information.
>>> import this
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't enough to break the rules.
Although explicit beats purity.
Errors never pass silently.
Unless silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be -- and preferably one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than "right" now.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one great idea -- let's use more of those!
>>> 
```

图 3-1：Python 之禅（The Zen of Python）。

Python 之禅有时被称为 PEP 20；PEP 是 Python 增强提案（Python enhancement proposals）的缩写。20 可能指的是 20 条 Python 之禅准则，但只有 19 条被记录了下来。我们都会对此好奇，或者构出自己的最后一个准则。

这里冒着变得技术化或计算机科学化的风险，我们应该提到，设计语言有不同的方法。也许最成功且应用最广泛的模型是面向对象编程（或 OOP），这种设计哲学试图模拟真实世界，因为它由具有属性以及这些对象所执行的方法（动作）的对象组成。

Python 是一门非常面向对象的语言。核心语言由控制语句（单词形式）组成，允许你控制你自己以及他人程序中的所有不同对象。然而，你需要先学习核心语言，这样当你准备好使用他人的对象时，你知道如何操作。同样，当你学会开一辆车后，基本上你就都会开所有的车。你不需要担心租了车才发现加速踏板在屋顶上，方向盘在地上，而你必须使用语音指令而不是刹车来减速。驾驶的基本技能适用于所有的汽车。

## 探索为什么缩进至关重要

在代码编写的基本风格方面，真正让 Python 于许多其他语言不同的特征是，它使用缩进而不是括号、大括号等来表示代码块（或代码段）。我们不假设你熟悉其他语言，所以如果这句话对你来说毫无意义，请不要担心。

Python 的规则是相反的，因为它不使用大括号或任何其他特殊字符来标记代码块的开始和结束。缩进本身标记了这些内容。这些缩进不是可选的——它们是强制性的，并且对代码的运行方式有相当大的影响。因此，当你阅读代码时（作为人类而非计算机），可以相对容易地看出发生了什么，而且你不会被大量的额外引号所分散注意力。

```python
import random
question = input("Ask Magic 8 Ball a question")
answer = random.randint(1, 8)
if answer == 1:
    print("It is certain")
elif answer == 2:
    print("Outlook good")
elif answer == 3:
    print("You may rely on it")
elif answer == 4:
    print("Ask again later")
elif answer == 5:
    print("Concentrate and ask again")
elif answer == 6:
    print("Reply hazy, try again")
elif answer == 7:
    print("My reply is no")
elif answer == 8:
    print("My sources say no")
else:
    print("That's not a question")
print("The end")
```

![](img/be36b4e9a8416f1ae2a353bd745f71cb_37_0.png)

你可能已经注意到 Python 代码开头以 `import` 开头的行。以 `import` 开头的行在 Python 中很常见，你将在下一节看到原因。

以 `import` 开头的行在 Python 中很常见，你将在下一节看到原因。Python 的秘密之一在于它有许多内置模块。要使用它们，必须先导入它们。例如：

```python
import random
```

一旦导入了模块，就可以使用它的函数。例如，要生成随机数，你可以使用：

```python
answer = random.randint(1, 8)
```

上一节中的 Magic 8 Ball 程序展示了如何使用 `random` 模块为问题提供答案。代码简单易懂。

你将在本书中使用广受欢迎的 Visual Studio Code (VS Code) 编辑器来学习 Python 并创建 Python 应用程序。我们假设你已经按照前面的章节设置好了学习和开发环境，并知道如何打开 VS Code。要跟上本章的内容，请按照以下步骤操作：

- 1. 在 Mac 上使用 Launchpad 或 Windows 上使用开始菜单打开 VS Code，并在 VS Code 中选择文件 ⇒ 打开文件夹或使用资源管理器窗格，打开你在[第 2 章](#)中创建的 Python Essentials 文件夹。

你可能会注意到在其他文件旁边有一个名为 `.vscode` 的新文件夹。别担心，这只是 VS Code 使用的信息，你现在可以忽略它。

- 2. 如果你已经按照[第 2 章](#)所述创建了 `hello.py` 文件，请点击它；否则，现在创建一个然后回到这里。

- 3. 选择第一行的所有文本并将其删除，这样你就可以从零开始。
