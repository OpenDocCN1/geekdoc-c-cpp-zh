
错误并不是源于你的代码编写，而是一个 HTTP 错误。具体来说，它是 403 Forbidden（禁止）错误。URL 已发送给 Google，但它回复：“抱歉，你可以从这里搜索我们的网站，但不能通过这样的 Python 代码（Sorry, you can search our site from your, but not from Python code like that）。”

好消息是，那些不允许你直接使用 Python 或其他编程语言发布内容的网站，通常允许你通过它们的 API（应用程序编程接口）发布内容。你仍然可以使用 Python 作为你的编程语言，你只需要遵守它们的规则。

## 使用 Python 爬取网页

当你从网络请求页面时，它通常以网页的形式交付给你，通常由 HTML 和内容组成。HTML 是一种标记代码，配合另一种名为 CSS 的语言，告诉浏览器如何根据尺寸、位置、字体、图像以及所有其他视觉和样式问题显示内容。在网页浏览器中，你看不到 HTML 或 CSS 代码。你只能看到内容，而这些内容通常包含在页面 HTML 代码块中。

即使你在网页上看到的大部分数据来自数据库，你也没有权限直接访问数据库。但是，你可以使用一种名为“网页爬取”（web scraping）的技术从网页中提取数据并用于其他用途。Python 具有强大的网页爬取能力，这是大多数人想要学习的热门话题。因此，我们将使用图 12-5 中的示例页面作为工作示例，开始学习网页爬取。

## Python 3 速查表

![](img/be36b4e9a8416f1ae2a353bd745f71cb_166_0.png)

网页爬取示例。告诉浏览器如何显示该页面内容的代码在浏览器中是不可见的，除非你查看源代码。在大多数浏览器中，你可以通过按下 F12 键或在页面空白处点击右键并选择“查看源代码”或“检查”或其他选项来实现。在大多数页面上，真实内容——你在浏览器中看到的内容——是 `<body>` ... `</body>` 标签。在页面主体内，可能会有头部、导航栏、页脚、可能的广告等部分。在该特定页面中，内容的精华位于 `<article>` ... `</article>` 标签之间。你在网页上看到的每个方块 [图 12-5] 都被称为“卡片”（card），每个卡片都定义在 `<a>` ... `</a>` 标签中。

[图 12-6] 显示了页面 [图 12-5] 的部分 HTML 代码。我们展示了页面中前两个链接的代码，但所有的链接都遵循相同的结构，并且它们都包含在由 `<article>` ... `</article>` 标签指定的区域内。

在 Python 代码中，你需要三个模块：来自 `urllib` 的 `request` 模块，允许你向网络请求资源并读取网络返回的内容。这是 Python 自带的标准模块之一，因此你不需要获取任何新东西。

对于网页爬取，你还需要 BeautifulSoup（它的名字来源于《爱丽丝梦游仙》书中的歌）。该模块提供了解析检索网页的工具，用于提取感兴趣的特定数据项。Python 已经可用，但你必须使用 `pip` 安装它。在 VS Code 中，进入“终端”（Terminal）面板。如果你使用的是 Windows，输入此命令：

```bash
pip install beautifulsoup4
```

![](img/be36b4e9a8416f1ae2a353bd745f71cb_167_0.png)

你应该会在屏幕上看到一些反馈，表示 BeautifulSoup 已找到并安装。或者，如果你之前安装过，你会看到一条消息，显示要求已满足。无需担心。

你还需要一个 HTML5 解析器。你可以使用 `html5lib`，这是另一个你现在就可以安装的模块。如果你使用的是 Windows，在 VS Code 的终端面板中输入此命令：

```bash
pip install html5lib
```

如果你在 Mac 上遇到错误，请在 VS Code 的终端面板中使用此命令：

```bash
pip3 install html5lib
```

要尝试代码，请在 VS Code 中创建一个 .py 文件并输入以下代码：

```python
# 从 url 库获取 request 模块
from urllib import request

## 这个具有爬取网页的方便工具
from bs4 import BeautifulSoup
```

接下来，你需要告诉 Python 所感兴趣的页面在互联网上的位置。在这种情况下，URL 是：

```python
https://freeasy.ai/scrape_sample.html
```

要查看页面，像往常一样将 URL 输入浏览器的地址栏。在浏览器中，页面看起来就像任何带有图片的普通网页。这是因为浏览器显示的是渲染后的页面，而不是原始的 HTML 和 CSS 代码。要爬取页面，你需要将其放入 Python 代码中。你可以给它起一个短名称，如 `page_url`：

```python
page_url = 'https://freeasy.ai/scrape_sample.html'
```

```python
links_list.append({'url' : url, 'img': img, 'text': text})
```

如果数据缺失，我们更希望 Python 直接跳过错误行并继续运行，而不是崩溃并导致我们没有任何任何数据。我们应该将获取各个部分的整个操作放在一个 `try:` 块中，如果执行失败，它允许 Python 直接跳过该行并移动到下一行：

```python
## Try to get the href(href), image url, and text.
try:
    url = link.get('href')
    img = link.img.get('src')
    text = link.span.text
    links_list.append({'url' : url, 'img': img, 'text': text})
# 如果该行缺少任何内容...
except AttributeError:
    #.. 跳过它，不要让崩溃。
pass
```

**图 12-7** 显示了目前所有的代码。如果你按照所示运行它，`link_list` 将填充你爬取的所有数据，但这对你来说并没有太大帮助。很有可能，你想要保存这些数据以备在其他地方使用。你可以通过将数据保存到 JSON 文件、CSV 文件或两者，取决于对你来说最方便。在接下来的章节中，我们将向你展示这两种方法。

```python
## 从 url 库导入 request 模块。
from urllib import request

## 这个包含了方便的工具。
from bs4 import BeautifulSoup

## 用于练习的示例页面。
page_url = 'https://freeasy.ai/scrape_sample.html'

## 打开该页面
raw_page = request.urlopen(page_url)

## 从 html 页面创建一个 BeautifulSoup 对象。
soup = BeautifulSoup(raw_page, 'html5lib')

## 隔离主内容块。
content = soup.article

links_list = []

## 遍历文章中所有的链接。
for link in content.find_all('a'):
    # 尝试获取 href、图像 url 和文本。
    try:
        url = link.get('href')
        img = link.img.get('src')
        text = link.span.text
        links_list.append({'url': url, 'img': img, 'text': text})
    # 如果该行缺少任何内容...
    except AttributeError:
        # ... 跳过它，不要让崩溃。
        pass
```

图 12-7：网络爬虫代码完成。

通过编程访问网络为获取和组织知识开辟了新的可能性，事实上，它是一个被称为数据科学领域的一部分。

# 第 13 章

## 库、包和模块

## 本章内容

- 理解标准库
- 概览 Python 包
- 查看如何导入 Python 模块

在大多数情况下，在这一章之前的所有章节都集中在 Python 核心语言上，即根据你打算如何使用 Python 所需要的语言元素。但正如你所看到的，许多程序都是从导入一个或多个模块开始的。每个模块本质上都是预写代码的集合，你可以在自己的代码中使用它们，而无必重新发明轮子。所有这些预写专门代码的“祖师”被称为 Python 标准库。

## 理解 Python 标准库

Python 标准库基本上是你在获取 Python 语言时获得的所有内容，包括所有的 Python 数据类型，如字符串、整数、浮点数和布尔值。这些数据类型的每个实例都是标准库中定义的类的实例。由于由于原因，type（类型）、instance（实例）和 object（对象）这些术语经常互换使用。整数是一个整数；它在 Python 中也是一种数据类型。但它的存在是因为标准库包含一个整数类，而你创建的每个整数都是该类的实例，因此是一个对象（因为类是被称为对象的物的模板）。

Python 中的 `type()` 函数通常识别一段数据的类型。例如，在 Python 提示符、Jupyter notebook 或 .py 文件中运行这两行代码：

```python
x = 3
print(type(x))
```

输出为：

```
<class 'int'>
```

输出告诉你 `x` 是一个整数，是标准库中 `int` 类的实例。运行这段代码：

```python
x = 'howdy'
print(type(x))
```

产生此输出：

```
<class 'str'>
```

也就是说，`x` 包含的是字符串数据类型的数据，由 Python `str` 类创建。`type()` 函数也适用于浮点数（带有小数点的数值，例如 3.14）和布尔值（True 或 False）。

## 使用 dir() 函数

Python 标准库提供了一个 `dir()` 方法，它可以显示与类型相关的所有属性的列表。例如，在前面的示例中，结果 `<class 'str'>` 告诉你 `str` 数据类型。所以你知道这是一个类型，因此是一个名为 `str`（代表字符串）的类的实例。如果你输入此命令：

```python
dir(str)
```

会显示类似这里的内容：

| '__add__', '__class__', '__contains__', '__delattr__', '__dir__', |
| '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', |
| '__getitem__', '__getnamed__', '__hash__', '__init__', |
| '__subclass__', '__iter__', '__len__', '__lt__', |
| '__mod__', '__mul__', '__new__', '__reduce__', |

python `capitalize` 链接了许多不同的资源，用于学习 `str` 对象的 `capitalize` 函数，包括用法示例。如果你正在使用 AI（无论是 Copilot、Bard、ChatGPT 还是其他工具），你都可以寻求帮助和示例。例如，尝试输入“告诉我关于 Python str.capitalize()”或类似的内容。

Python 标准库的一个很好的（尽管是技术性的）资源是标准库文档本身。这些信息始终可以在 [https://docs.python.org/](https://docs.python.org/) 获取，通常位于“Library Reference”链接下。尽管措辞可能会发生，如果有疑问，只需在网上搜索 python standard library 即可。注意，该库非常庞大且技术性强，因此不要期望上手就能理解它。相反，将其作为一个持续的资源，随着你对 Python 知识的积累，学习你感兴趣的内容。

## 探索内置函数

`dir()` 和 `help()` 都是 Python 内置函数的示例，在 Python 中、你创建的任何应用程序以及 Python 命令行提示符中始终可以使用它们。这些内置函数也是标准库的一部分。事实上，如果你在网上搜索 built-in functions，某些搜索结果将直接指向 Python 文档。点击这些结果中的一个将打开标准库文档的一个章节，并显示所有内置函数的表格，如图 13-1 所示。在该上，你可以点击任何函数的名称以了解更多信息。

## 内置函数

Python 解释器内置了许多始终可用的函数和类型。它们按字母顺序在这里列出。

| A | L | R |
|---|---|---|
| abs() | enumerate() | range() |
| iter() | list() | repr() |
| eval() | locals() | reversed() |
| any() | | |()() |
| ascii() | map() | set() |
| float() | memoryview() | setattr() |
| bin() | min() | slice() |
| bool() | | hex() |

## 探索 Python 包

Python 语言支持模块化编程，在这种情况下，程序被分解为更小、更于管理的组件和模块。其中某些组件可能由其他人创建，并可以重复使用。

任何大型项目，无论你是独立工作还是团队成员，如果某些组件可以使用 Python 编程社区成员已经编写、测试、调试并认为可靠的代码，就可以被简化和精简。你听到的关于 Python 的包是某种代码——经过开发和培养、值得信赖，且足够通用，可以作为大型项目组件使用的代码。

Python 有数以万计的包。寻找包的一个很好的资源是 PyPI，这是一个聪明且易于记忆的名字，是 Python Package Index（Python 包索引）的缩写。你可以查看它 [https://pypi.org/](https://pypi.org/)。

此外，一个名为 `pip`（Pip Install Packages 的含义，另一个聪明的名字）的程序是一个包管理器，你可以用它来探索、更新和删除系统中的现有包。

![](img/be36b4e9a8416f1ae2a353bd745f71cb_178_0.png)

要使用 `pip`，你必须进入操作系统的命令行提示符，在 Mac 上是 Terminal，Windows 上是 cmd.exe 或 PowerShell。如果你使用 VS Code，进入命令行提示符最简单的方法是打开 VS Code 并选择 ⇒ Terminal。

如果你已经安装了 `pip`，在命令行提示符中输入此命令将告诉你是安装了哪个版本的 `pip`：

```
pip --version
```

如果你使用的是 Mac 并收到“command not found”错误，你需要在所有命令中使用 `pip3` 替换 `pip`。例如，使用：

```bash
pip3 --version
```

结果看起来真的像这样（但会显示你的版本号，以及 Python 的路径代替省略号 `[...]`）：

```
pip 23.1.2 from ...
```

要查看你已经安装了哪些包，在 Windows 的操作系统命令行提示符或 VS Code 的 Terminal 面板中输入：

```bash
pip list
```

或者在 Mac 上，如果使用 `pip` 报错，请使用 `pip3` 替换 `pip`：

```bash
pip3 list
```

## 导入 Python 模块

你会听到模块在 Python 中的用法。

Python 语言支持模块化编程，在这种情况下，程序被分解为更小、更易管理的组件和模块。

要使用 `pip`，你必须进入操作系统的命令行提示符，在 Mac 上是 Terminal，Windows 上是 cmd.exe 或 PowerShell。如果你使用 VS Code，最简单的方法是选择 ⇒ Terminal。

如果你已经安装了 `pip`，在命令行提示符中输入此命令将告诉你是安装了哪个版本的 `pip`：

```bash
pip --version
```

如果你使用的是 Mac 并收到“command not found”错误，你需要在所有命令中使用 `pip3` 替换 `pip`。例如，使用：

```bash
pip3 --version
```

结果看起来真的像这样（但会显示你的版本号，以及 Python 的路径代替省略号 `[...]`）：

```
pip 23.1.2 from ...
```
