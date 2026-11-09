

- b. 经常休息：我建议每 20–30 分钟休息一次。在休息间隙散散步。
- c. 饮食：保持健康的饮食，富含优质脂肪、蛋白质和复合碳水化合物。尽量减少简单碳水化合物和糖。
- d. 锻炼：保持规律的锻炼习惯或进行一项运动。每周至少锻炼 3–4 次（也许更多）很重要。
- e. 睡眠：每晚至少睡 7–8 小时。如果你无法入睡，请咨询有资质的医生，了解如何改善睡眠。

关于上述每个主题，都可以写成整本书；但这是一本编程书，所以我就此打住。只需记住，上述软技能非常重要，你在编程时也可以加以练习。

## 设置你的工作区

### 你需要什么

你需要一台可连接互联网并已安装网页浏览器的笔记本电脑/台式电脑。我推荐使用 Mozilla Firefox 或 Google Chrome。

### 下载/安装文本编辑软件

下载最新版本的文本编辑软件。我推荐下载 NotePad++。下载后，双击 Setup.exe 文件并按照安装提示操作。

[https://notepad-plus-plus.org/downloads/](https://notepad-plus-plus.org/downloads/)

### 开始使用 NotePad++

从桌面或开始菜单打开 Notepad++

![](img/443990a0ec620659ce8be783c0758bc6_229_0.png)

现在，点击 **文件 > 新建** 打开一个新文件。

现在，选择 **文件 > 另存为**，并将文件类型选择为 **.html**

![](img/443990a0ec620659ce8be783c0758bc6_231_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_231_1.png)

### 测试程序

现在，让我们测试程序是否能与浏览器连接。
只需在文件中随意输入一些文本。在我的文件里，我输入了 **“这是一条测试消息。”**
现在选择 **文件 > 保存。**
之后，根据你使用的浏览器，点击 **运行 > 在 Firefox/Chrome/IE 中启动**。
如果运行正常，你输入的文本应显示在浏览器窗口中。

![](img/443990a0ec620659ce8be783c0758bc6_232_0.png)

![](img/443990a0ec620659ce8be783c0758bc6_233_0.png)

- 运行... F5
- **在 Firefox 中启动** Ctrl+Alt+Shift+X
- 在 IE 中启动 Ctrl+Alt+Shift+I
- 在 Chrome 中启动 Ctrl+Alt+Shift+R
- 在 Safari 中启动 Ctrl+Alt+Shift+A
- 获取 PHP 帮助 Alt+F1
- 维基百科搜索 Alt+F3
- 在另一个实例中打开文件 Alt+F6
- 通过 Outlook 发送 Ctrl+Alt+Shift+O
- 修改快捷键/删除命令...

结果：

![](img/443990a0ec620659ce8be783c0758bc6_234_0.png)

这是一种很好的简单方法，可在继续之前确保程序正常运行。

### 附注：

一些学生遇到过的一个问题是，“在浏览器中运行”选项有时不起作用并报错。这是因为路径设置不正确。如果由于某种原因它不起作用，你仍然可以运行程序。

- 1. 只需将 Notepad++ 文件保存为 HTML 文档。
- 2. 关闭 Notepad++ 文件。
- 3. 转到 HTML 文档所在的文件夹。
- 4. 双击该 HTML 文件，它应该就能正常工作。

## 什么是 HTML？

HTML 代表超文本标记语言（Hyper Text Markup Language）。它是我们通过网页与互联网交互所使用的编程语言。所有网页的基本结构都由 HTML 定义。它足够简单，初学者程序员也能快速掌握。大多数 HTML 编程都是通过称为标签的元素完成的。这些标签以 `<>` 开始，以 `</>` 结束。例如，一个常见标签是段落标签，它以 `<p>` 开始，以 `</p>` 结束。

### 常见 HTML 标签

- **<html>** - 此标签用于每个网页的开头，表示 HTML 代码的开始
- **<head>** - 这段 HTML 代码会在程序其余部分之前执行
- **<title>** - 此标签用于设置网页标题。它会把文本写到网页顶部的标题栏上。
- **<body>** - 这是网页正文中的信息。
- **<h1>** - 用于表示标题标签。这是最大字号的标题标签。
- **<h2>,<h3>,<h4>,<h5>,<h6>** - 用于表示字号依次减小的副标题。
- **<p>** - 用于表示文本段落
- **<img>** - 在网页上显示图像。该图像可以链接到外部网页，也可以链接到内部文件。
- **<strong>** - 用于将文本加粗
- `<ul>` - 用于无序列表。例如项目符号形式的条目列表。
- `<li>` - 向无序列表添加一个项目符号条目。
- `<ol>` - 用于有序列表，例如从 1、2、3…… 开始的编号列表。
- `<div>` - 用于表示较大的文本区块；这些区块包含多个段落。
- `<a>` - 用于将网页中的项目链接到另一个网页。
- `<br>` - 在代码中添加换行，并移到下一行。

### HTML 代码示例

下面是基本 HTML 代码示例。它包含了上述所有 HTML 代码的示例。你可以把这些代码打出来，或者复制粘贴下面的示例。

![](img/443990a0ec620659ce8be783c0758bc6_237_0.png)

### 可复制粘贴的 HTML 代码版本

你可以将下面的代码复制粘贴到你的 HTML 浏览器中，看看它是否能运行

```html
<html>
<head>
<title>My first html website......</title>
</head>
<body>
<h1>Welcome to Programming in Javascript (this is a h1 tag)</h1>
<h2>Let’s get started (this is a h2 tag)</h2>
<h3>This is the start of bigger things (this is a h3 tag)</h3>
<p>We’re going over a few basic html tags here but you can feel free to
play around them and experiment.
There are 1000's of html tags that you can learn in the long run. Here's a list
of topics you can learn below (This is a paragraph tag)</p>

<ul> Below is the example of an unordered bulleted list
<li>Basics of html</li>
<li>CSS</li>
<li>JavaScript</li>
<li>Loops</li>
<li>Arrays</li>
<li>Canvas</li>
</ul>
<a href="https://www.google.com">Example of hyperlink to Google</a>
<br>
<a href="https://www.facebook.com">Example of hyperlink to Facebook</a><br>
<a href="https://www.amazon.com">Example of hyperlink to Amazon</a>
<br>
</body>
</html>
```

### 代码输出

![](img/443990a0ec620659ce8be783c0758bc6_238_0.png)

现在，让我们分解这些不同的元素：下面是 title 标签 `<title>`。

![](img/443990a0ec620659ce8be783c0758bc6_239_0.png)

下面是 heading 标签 `<h1>`、`<h2>`、`<h3>`

![](img/443990a0ec620659ce8be783c0758bc6_239_1.png)

下面是段落标签 `<p>`

![](img/443990a0ec620659ce8be783c0758bc6_239_2.png)

下面是一个无序项目符号列表 `<ul>` `<li>`

- HTML 基础
- CSS
- JavaScript
- 循环
- 数组
- 类

下面是三个指向三个热门网站的超链接标签 `<a href>`

- [指向 YouTube 的超链接示例](#)
- [指向 Facebook 的超链接示例](#)
- [指向 Instagram 的超链接示例](#)

### 练习题

- 1. 制作一个网站，使用标题标签，并在无序列表中列出杂货商品。使用段落标签说明你对特定商品可能有的任何特殊要求。在列表末尾，使用超链接标签链接到最近的杂货店网站。
- 2. 创建一个网站，列出你足球队的所有球员。使用 title 标签、heading 标签和段落标签来欢迎用户访问你的网站，并描述球队及球队理念。使用有序列表列出球员。
- 3. 制作一个网站，在无序列表中列出你所在地区所有你最喜欢的餐厅和咖啡店。使用 title 标签、heading 标签和段落标签介绍你自己以及你所在地区的餐饮体验。

## 示例 HTML 程序

### 这个项目做什么

这个 HTML 项目会创建两个按钮。这两个按钮在“白天”和“夜晚”的两张图像之间切换。两个按钮分别标记为“白天”和“夜晚”。

这是一个简单的 HTML 项目，它创建一个按钮，可以打开/关闭页面上的灯泡。我们将使用两张灯泡图像来实现这一点。按钮将在两张图像之间切换。

