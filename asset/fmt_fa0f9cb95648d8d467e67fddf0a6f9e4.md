
| | |
| --- | --- |
| Accept | text/html,application/xml+xml,application;q=0.9,image/webp,image/*,*q=0.8 |
| Accept-Encoding | gzip, deflate, br |
| Accept-Language | en-US;q=0.9 |
| Referer | https://alansimpson.me/python/cheats/ |
| Upgrade-Insecure-Requests | 1 |
| User-Agent | Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome |
| Response Headers | |

大多数时候，你可能会经常用到 `request` 模块，因为它允许你从互联网打开资源。从库中访问单个包的语法如下：

```python
from library import module
```

其中 `library` 是较大库的名称，`module` 是模块的名称。要访问 `urllib` 中 `response` 模块的功能，请在代码顶部使用以下语法（注释行是可选的）：

```python
# 从 urllib 库导入 request 模块
from urllib import request
```

要打开网页，请使用此语法：

```
variablename = request.urlopen(url)
```

将 `variablename` 替换为你自定义的变量名。将 `url` 替换为你想要访问的资源的 URL，并用单引号或双引号（除非它存储在变量中）。

运行代码时，结果将是一个 `HttpResponse` 对象。

例如，你可以在 `.py` 文件中运行以下代码，以访问 Alan 为此目的添加到其网站的示例 HTML 页面：

```python
# 从 urllib 库导入 request 模块
from urllib import request

# 目标页面的 URL（地址）。
sample_url = 'https://freeasy.ai/sample.html'

# 请求页面并将其放入名为 the_page 的变量中
the_page = request.urlopen(sample_url)

# 将响应状态码放入名为 status 的变量中
status = the_page.code

# 页面的数据类型是什么？
print(type(the_page))

# 状态码是什么？
print(status)
```

运行此代码将显示此输出：

```
<class 'http.client.HttpResponse'
200
```

名为 `the_page` 的变量包含一个 `http.client.HttpResponse` 对象，它包含了服务器响应请求返回的所有内容。`200` 是状态码，告诉你是一切正常。

## 使用 Python 向网页发布内容

并不是所有访问网络资源的尝试都能像前面的示例那样顺利。例如，在你的浏览器的地址栏中输入以下 URL 并按回车键：

```
https://www.google.com/search?q=python web scraping tutorial
```

Google 返回了许多包含“python web scraping tutorial”关键词的搜索结果页面和视频。如果你查看地址栏，可能会发现你输入的 URL 发生了细微变化。空格已全部替换为 `%20`，如下行代码所示：

```
https://www.google.com/search?q=python%20web%20scraping%20tutorial
```

`%20` 是空格的十六进制 ASCII 编码。我们可能熟悉 `%20`，因为 HTTP 不支持在 URL 中使用字面空格。如果需要，传输完成后可以将 `%20` 回空格。

现在看看如果使用 Google URL 而不是原始 URL 运行代码会发生什么。以下是该代码：

```python
from urllib import request

# 目标页面的 URL（地址）。
sample_url = 'https://www.google.com/search?q=python%20web%20scraping%20tutorial'

# 请求页面并将其放入名为 tpage 的变量中
the_page = request.urlopen(sample_url)

# 将响应状态码放入名为 status 的变量中
status = the_page.code

# 页面的数据类型是什么？
print(type(the_page))

# 状态码是什么？
print(status)
```

运行这段代码时，事情并不顺利。你可能会看到几个错误信息，但最重要的信息是：

`HTTPError: HTTP Error 403: Forbidden`

错误并不是你的代码出的问题，而是一个 HTTP 错误。具体来说，它是错误代码 403 `Forbidden`（禁止访问）。URL 已发送给 Google，它回答说：“抱歉，你可以通过浏览器搜索我们的网站，但不能通过像这样的 Python 代码。”

好消息是，那些不允许你直接使用 Python 或其他编程语言发布内容的网站，允许你通过它们的 API（应用程序编程接口）来发布内容。你仍然可以使用 Python 作为你的编程语言，你只需要遵守它们的规则即可。

## 使用 Python 爬取网页

每当你从网络请求页面时，它交付给你的的是一个通常由 HTML 和内容组成的页面。HTML 是一种标记语言，配合另一种名为 CSS 的语言，告诉浏览器根据大小、位置、字体、图像以及所有此类视觉、样式标记来显示内容。在浏览器中，你看不到 HTML 或 CSS 代码。你只能看到内容，这些内容通常包含在页面 HTML 代码块中。

尽管你在网页上看到的大部分数据来自数据库，但你没有权限直接访问数据库。不过，你可以使用名为“网络爬虫”（web scraping）的技术从网页中提取数据，供其他方式使用。Python 具有强大的网络爬取能力，这是大多数人想学习的热门话题。因此，我们将从图 12-5 中的示例页面作为工作示例开始学习网络爬虫。

Python 3 速表

![](img/ca342ce31cd39db62dca2143d5fa4229_164_0.png)

图 12-5：用于网络爬取的示例页面。

告诉浏览器如何显示页面内容的代码在浏览器中不可见的，除非你查看源代码。在大多数浏览器中，你可以通过按 F12 键或在页面空白处点击右键并选择“查看源代码”或其他选项来实现这一点。在大多数网页上，真实内容——你在浏览器中看到的内容——位于 `<body>` ... `</body>` 标签之间。在页面主体内，可能会有头部、导航栏、页脚、可能还有广告等部分。在该特定页面中，内容的实质位于 `<article>` ... `</article>` 标签之间。你在图 12-5 页面上看到的每个方块被称为*卡片*（card），并且每个卡片都被定义为 `<a>` ... `</a>` 标签中的链接。

图 12-6 显示了图 12-5 页面的一些 HTML 代码。我们展示了页面中前两个链接的代码，但所有链接都遵循相同的结构，并且它们都包含在由 `<article>` ... `</article>` 标签标记的部分中。

在 Python 代码中，你需要三个模块。其中一个是 `urllib` 模块，它允许你向网络发送资源请求并读取网络提供的内容。这是 Python 自带的标准模块之一，所以你不需要获取任何新东西。

对于网络爬虫，你还需要 `BeautifulSoup`（其模块名源自《爱丽丝梦仙游》书中的一首歌）。该模块提供了工具用于解析你检索的网页，以获取你感兴趣的特定数据项。Python 本身没有自带 BeautifulSoup，所以你必须使用 `pip` 安装它。在 VS Code 中，转到终端（Terminal）面板。如果你使用的是 Windows，输入你的命令行：

`pip install beautifulsoup4`

```html
<body>
60 &lt;Python-3 Cheat Sheets/html&gt;
61 &lt;div class="cards256"&gt;
62 &lt;a href="http://www.datascienceresearch.com/python"&gt;
63 &lt;img src="images/basics256.jpg" alt="Python Cheat Sheet"&gt;
64 &lt;/a&gt;
65 &lt;span&gt;
67 &lt;a href="https://alansomon.me/datascience/beginner/"&gt;
68 &lt;img src="Images/Begin256.jpg" alt="Python Cheat Sheet"&gt;
69 &lt;/a&gt;
70 &lt;span&gt;
71 &lt;a href="https://alansomon.me/datascience/python/justbasics/"&gt;
72 &lt;img src="images/justBasics256.jpg" alt="Python Just the Cheat Sheet"&gt;
73 &lt;/a&gt;
74 &lt;span&gt;
76 &lt;a href="https://alansomon.me/datascience/python/cheatography/"&gt;
77 &lt;img src="images/cheatography256.jpg" alt="Python Cheat Sheet"&gt;
78 &lt;/a&gt;
79 &lt;span&gt;
81 &lt;a href="https://alansomon.me/datascience/dataquest/"&gt;
82 &lt;img src="images/dataquest256.jpg" alt="Dataquest Python Cheat Sheet"&gt;
83 &lt;/a&gt;
84 &lt;span&gt;
</body>
```

图 12-6- 一些代码在屏幕上提供了反馈，表明 BeautifulSoup 已安装。

接下来，你需要告诉 Python 你感兴趣的页面在互联网上的位置。在这种情况下，URL 是：

```
https://freeeasy.ai/scrape_sample.html
```

要查看该页面，只需像往常一样将 URL 输入浏览器的地址栏即可。在浏览器中，该页面看起来就像任何带有某些图片的普通网页。这是因为网络浏览器显示的是渲染后的页面，而不是原始的 HTML 和 CSS 代码。为了抓取该页面，你需要将该 URL 放入你的 Python 代码中。你可以通过将其赋值变量来给它起一个短名称，例如 `page_url`：

```python
# 用于练习的页面。
page_url = 'https://freeeasy.ai/scrape_sample.html'
```

要将该处的网页引入你的 Python 应用，创建一个另一个变量（我们称之为 `raw_page`），并使用 `request` 方法的 url 读取页面：

```python
# 打开该页面。
raw_page = request.urlopen(page_url)
```

为了方便在后续代码中进行解析，将其复制到 BeautifulSoup 对象中。我们在代码中为该对象命名了名。你还需要告诉 BeautifulSoup 你希望如何解析该页面。你可以使用 `html5lib`，如下所示：

```python
# 从 html 页面创建一个 BeautifulSoup 对象。
soup = BeautifulSoup(raw_page, 'html5lib')
```

生成式 AI 可以为你创建通用的网页抓取代码，因此你不需要记忆这些语法。只需要求 Copilot 或 Claude ai 编写使用 BeautifulSoup 抓取网站的 Python 代码即可。这将为你提供抓取页面的基础代码。然后，你需要指定 URL 并调整代码以从页面检索你需要的任何内容。

在接下来的代码中，我们将该代码块赋值给名为 `content` 的变量。页面中的后续代码将只解析页面的该部分，这可以提高速度和效率。

```python
# 隔离主内容块。
content = soup.article
```

![](img/ca342ce31cd39db62dca2143d5fa4229_166_0.png)

## 存储解析后的内容

在抓取网页时，你的目标通常是收集特定的感兴趣数据。在这种情况下，我们只需要许多链接的 URL、图像源和文本。我们知道会有多行。存储这些内容的一种简单方法是将它们放入列表中，因此在下面的代码中，我们创建了一个空列表 `links_list`：

```python
# 创建一个空列表来存放字典项。
links_list = []
```

接下来，代码需要遍历页面内容中的每个标签。每个链接都以 `<a>` 标签开始，以 `</a>` 标签结束。要让 Python 逐个遍历每个链接，请在循环中使用 BeautifulSoup 的 `find_all` 方法。在下面的代码中，当我们遍历链接时，将当前链接赋值给名为如下的变量：

```python
# 遍历文章中的所有链接。
for link in content.find_all('a'):
```

每个链接的代码将看起来像这样，尽管每个链接将有唯一的 URL、图像源和文本：

我们想要的三项数据如下：

- 链接 URL：包含在 `<a>` 标签中 `href=` 之后的引号内。
- 图像源：包含在 `<img>` 标签中 `src=` 之后的引号内。
- 链接文本：包含在 `<span>` ... `</span>` 标签中。

以下代码使用 BeautifulSoup 的 `.get()` 方法提取每个组件，以隔离链接内部的内容（即标记链接开始和结束的 `<a>` 和 `</a>` 标签之间）。以下获取链接的 URL 部分并将其放入名为 `url` 的变量中：

```python
url = link.get('href')
```

将该代码缩进循环下方以便对每个链接执行。以下代码获取图像源并将其放入名为 `img` 的变量中：

```python
img = link.img.get('src')
```

文本位于链接底部附近的 `<span>` ... `</span>` 标签之间。要获取该文本并放入变量 `text` 中，请添加此行代码：

```python
text = link.span.text
```

你不需要使用 .get() 来获取文本，因为文本不在 `href=` 或 `src=` 等 HTML 属性中。它只是 `<span>` ... `</span>` 标签之间的文本。

最后，在跳转到页面上的下一个链接之前你需要保存它。实现此点的简单方法是使用以下代码将三项数据追加到 `links_list`：

```python
links_list.append({'url': url, 'img': img, 'text': text})
```

如果数据缺失，我们更倾向于让 Python 跳过坏行并继续运行，而不是崩溃导致我们没有任何数据。因此，我们应该将获取部分的整个操作放在 `try:` 块中，如果失败，将允许 Python 跳过该链接并移动到下一个：

```python
# 尝试获取 href、图像 url 和文本。
try:
  url = link.get('href')
  img = link.img.get('src')
  text = link.span.text
  links_list.append({'url': url, 'img': img, 'text': text})
# 如果该行缺少任何内容...
except AttributeError:
  #... 跳过它，不要让程序崩溃
  pass
```

157 与互联网交互

## 第 13 章 库、包和模块

158 Python 基础

## 理解 Python 标准库

在抓取网页时，你的目标通常是收集特定的感兴趣数据。在这种情况下，我们只需要许多链接的 URL、图像源和文本。我们知道会有多行。存储这些内容的一种简单方法是将它们放入列表中，因此在下面的代码中，我们创建了一个空列表 `links_list`：

```python
# 创建一个空列表来存放字典项。
links_list = []
```

接下来，代码需要遍历页面内容中的每个标签。每个链接都以 `<a>` 标签开始，以 `</a>` 标签结束。要让 Python 逐个遍历每个链接，请在循环中使用 BeautifulSoup 的 `find_all` 方法。在下面的代码中，当我们遍历链接时，将当前链接赋值给名为如下的变量：

```python
# 遍历文章中的所有链接。
for link in content.find_all('a'):
```

每个链接的代码将看起来像这样，尽管每个链接将有唯一的 URL、图像源和文本：

我们想要的三项数据如下：

- 链接 URL：包含在 `<a>` 标签中 `href=` 之后的引号内。
- 图像源：包含在 `<img>` 标签中 `src=` 之后的引号内。
- 链接文本：包含在 `<span>` ... `</span>` 标签中。

以下代码使用 BeautifulSoup 的 `.get()` 方法提取每个组件，以隔离链接内部的内容（即标记链接开始和结束的 `<a>` 和 `</a>` 标签之间）。以下获取链接的 URL 部分并将其放入名为 `url` 的变量中：
