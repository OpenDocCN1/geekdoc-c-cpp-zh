
If you're planning to go even further and structure a longer course around this book, the practice exercises make particularly good lecture-specific homework to keep students abreast of the skills in R and statistics as they're developed. The main points of the sections making up each chapter are relatively easy to translate into slides that can be initially structured with help from the Contents in Detail.

## PART I

## THE LANGUAGE

## GETTING STARTED

![](img/b2cfc85cbb129f60fe595a2bae074fe4_36_0.png)

R provides a wonderfully flexible programming environment favored by the many researchers who do some form of data analysis as part of their work. In this chapter, I'll lay the groundwork for learning and using R, and I'll cover the basics of installing R and certain other things useful to know before you begin.

### 1.1 Obtaining and Installing R from CRAN

R is available for Windows, OS X, and Linux/Unix platforms. You can find the main collection of R resources online at the Comprehensive R Archive Network (`CRAN`). If you go to the R project website at `http://www.r-project.org/`, you can navigate to your local `CRAN` mirror and download the installer relevant to your operating system. Section `A.1` provides step-by-step instructions for installing the base distribution of R.

### 1.2 Opening R for the First Time

R is an interpreted language that's strictly case- and character-sensitive, which means that you enter instructions that follow the specific syntactic rules of the language into a console or command-line interface. The softare interprets and executes your code and returns any results.

R is what's known as a high-level programming language. Level refers to the level of abstraction away from the fundamental details of computer execution. That is, a low-level language will require you to do things such as manually manage the machine's memory allotments, but with a high-level language like R, you're fortunately spared these technicalities.

When you open the R application, you are presented with the R console; Figure 1-1 shows a Windows instance, and the left image of Figure 1-2 shows an example on OS X. This represents R's naturally graphical user interface (`GUI`) and is the typical way R is used.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_37_0.png)

The functional, "no-frills" appearance of the interpreter, in which my experience has struck fear into the heart of many an undergraduate, stays true to the very nature of the software—a blank canvas that can be used for any number of tasks. Note that OS X versions use separate windows for the console and editor, though behavior in Windows is to contain these panes in one overall R window.

![](img/b2cfc85cbb129f60fe595a2bae074fe4_38_0.png)

The functional, "no-frills" appearance of the interpreter, in which my experience has struck fear into the heart of many an undergraduate, stays true to the very nature of the software—a blank canvas that can be used for any number of tasks. Note that OS X versions use separate windows for the console and editor, though behavior in Windows is to contain these panes in one overall R window.

#### 1.2.1 Console and Editor

There are two main window types used for R: the console and the editor.

The console is where you enter commands and see the output. The editor is where you write your scripts. It is often better to write your code in the editor and then send it to the console, which allows you to save your work and organize it better.

#### 1.2.2 Comments

In R, you can annotate your code with comments. Just preface the line with a hash mark (`#`), and anything that comes thereafter will be ignored by the interpreter. For example, executing the following in the console does not return you to the prompt:

```
R > # This is a comment in R...
```

Comments can also appear after value commands.

```
R > 1+1 # This works out the result of one pulse!
[1] 2
```

#### 1.2.3 工作目录

R 会话始终与其关联一个工作目录。除非你在保存或导入数据文件时明确指定文件路径，否则 R 会默认使用此工作目录。要检查工作目录的位置，请使用 `getwd` 函数。

```R
R getwd()
[1] "/Users/davies"
```

文件路径始终用双引号括起来，并且 R 在指定文件夹位置时使用正斜杠，而不是反斜杠。

你可以使用 `setwd` 函数更改默认工作目录，如下所示：

```R
R setwd("/folder1/folder2/folder3")
```

你可以提供相对于当前工作目录的文件路径，或提供完整路径（换句话说，从系统根驱动器开始）。无论哪种方式，都必须记住 R 的区分大小写特性；你必须完全匹配任何文件夹名称的名称和标点，否则会抛出错误。

也就是说，如果你在每次读取或写入文件时指定完整且正确的文件路径感到困难（第 8 章中有进一步的细节），那么感兴趣的文件可以位于计算机上的任何位置。

#### 1.2.4 安装和加载 R 包

R 的基础安装已准备好大量用于数值计算、常见统计分析和绘图与可视化的内置命令。这些命令可以从一开始就直接使用，并且无需以任何方式加载或导入。如果你在本文中将它们称为内置或即用型。

稍微更专业的技巧和数据集包含在代码包（也称为库）中。使用贡献的包很常见，你将在本书中全程使用它们，因此熟悉安装和加载所需库非常重要。

第 `A.2` 节涵盖了从 `CRAN` 下载和安装包的相关细节，但我在此提供一个简要概述。

##### 加载包

有一小部分推荐的包包含在 R 的基础发行版中（列在第 `A.2.2` 节）。它们不需要单独安装，但要使用它们，你需要通过调用 `library` 来加载它们。本书中你使用的一个包名为 `MASS`（Venables and Ripley, 2002）。要加载它（或任何其他已安装的包）并获得访问其函数和数据集的权限，只需在提示符下执行 `library` 即可，如下所示：

```R
R library("MASS")
```

注意，调用 `library` 仅为当前运行的 R 会话提供对包功能的访问。当你关闭 R 并重新打开一个新实例时，你需要重新加载想要使用的任何包。

##### 安装包

有数千个贡献的包未包含在典型的 R 安装中；要使它们在 R 中可加载，你必须首先从存储库（通常是 `CRAN`）下载并安装它们。最简单的方法是直接从 R 提示符使用 `install.packages` 函数（为此你需要互联网连接）。

例如，其中一个包是 `ks`（Duong, 2007），你将在第 26 章中使用它。执行以下操作将尝试连接到你的本地 `CRAN` 镜像并下载并安装 `ks`，以及它所依赖的几个包（称为依赖项）：

```R
R install.packages("ks")
```

控制台将在过程完成时显示运行输出。你只需安装一次包；此后它将可用于你的 R 安装。你可以通过调用 `library` 以与你对 `M65` 所做的相同方式，在任何新打开的 R 实例中加载已安装的包（如 `ks`）。

第 `A.2.3` 节提供了有关包安装的更多详细信息。

##### 更新包

贡献包的维护人员会定期提供版本更新以修复错误并添加功能。时不时地，你可能想要检查已安装包集合的更新。

从 R 提示符，简单执行以下操作将尝试连接到你设置的包存储库（默认为 `CRAN`），查找所有已安装包的版本，这些版本晚于你当前拥有的版本

```R
R update.packages()
```

第 `A.3` 节提供了有关更新包的更多详细信息，第 `A.4` 节讨论了替代的 `CRAN` 镜像和存储库。

#### 1.2.5 帮助文件和函数文档

R 附带一套帮助文件，你可以使用它来搜索特定功能、寻求有关如何精确使用给定函数及其参数的信息（换句话说，当你执行它时提供给函数的数值或对象）、澄清参数在操作中的作用、了解任何返回对象的形式、提供使用该函数的可能示例，以及获取有关如何引用任何软件或数据集的详细信息。

##### 要访问命令或其他对象的帮助文件，请在控制台提示符下使用 `help` 函数或使用方便的快捷方式 `?`。例如，考虑即用型的算术平均函数 `mean`。

```R
R> ?mean
```

这会在图 1-4 的顶部图像中显示。

![](img/b2cfc85cbb129f60fe595a2bae074fe4_42_0.png)

图 1-4：OS X 中函数 `mean` 的 R 文件 [顶部] 和对字符串 "mean" 的搜索结果 [底部]

如果你不确定所需函数的确切名称，你可以使用传递给 `help.search` 的字符字符串（双引号中的语句）在所有已安装包的文档中搜索文档，也可以使用 `??` 作为快捷方式：

```R
R> ??"mean"
```

此搜索会列出一个函数列表，其中包含其宿主包和描述，其帮助文件包含感兴趣的字符串，如图 1-4 的底部图像所示（突出显示的条目是算术平均值）。

所有帮助文件都遵循图 1-4 顶部图像所示的通用格式，文件中的长度和详细程度通常反映函数所执行操作的复杂性。大多数帮助文件包括此处列出的前三项；其他项是常见但可选的：

- Description 部分提供关于所执行操作的简短说明。
- Usage 部分指定函数的形式，即应如何传递给 R 控制台，包括参数的自然顺序和任何默认值（这些是显示使用 `=` 的参数）。
- Arguments 部分，更详细地说明了每个参数的作用以及它们允许取的值。
- 函数返回的对象（如果有）的性质在 Value 下指定。
- References 部分为命令或函数背后的方法提供相关引用。
- 相关函数的帮助文件在 *See Also* 下链接。
- Examples 提供可执行代码，可复制并粘贴到控制台，演示函数的使用。

帮助文件中有几个字段——初学者常犯的错误，我鼓励你熟悉布局和解释——即使你已经知道如何工作，也是成为熟练 R 用户的重要组成部分。

#### 1.2.6 第三方编辑器

R 的流行导致了几个第三方编辑器的开发，或现有编辑软件的兼容插件，可以增强编码体验。

一个值得注意的例子是 `RStudio`（RStudio Team, 2015）。这是一个集成开发环境（IDE），可在 Windows、OS X 和 Linux/Unix 平台上使用，网址为 `http://www.rstudio.com/`。

`RStudio` 包括直接提交的代码编辑器；用于文件、对象和项目管理等事项的单独点按式窗格；以及使用 R 创建 markdown 文档。附录 B 详细讨论了 `RStudio` 及其功能。

使用任何第三方编辑器，包括 `RStudio`，在很大程度上是个人选择。在本书中，我只是假设使用典型的 R 应用程序。
