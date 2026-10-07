
在 Visual Studio 中，如果你按下 `Ctrl+`，将打开 Visual Studio 终端。

> 提示：` ` 位于 `~` 所在的键上。这也是 Visual Studio Code 中使用的相同按键。这使得 `Ctrl+` 非常方便，单手按键即可打开 Visual Studio 内部的终端。

启动终端会打开集成的 PowerShell 实例，如图 12 所示。

![](img/49b3596025cc7ecebab509ce03bfac_62_0.png)

图 12：Developer PowerShell

如果你不习惯使用 PowerShell，可以像图 13 所示切换到 Developer Command Prompt。

![](img/49b3596025cc7ecebab509ce03bfac_63_0.png)

图 13：Developer Command Prompt

你可以轻松地从下拉菜单中选择任何所需的终端，如图 14 所示。

| Developer Command Prompt | Developer PowerShell | Developer Command Prompt |

|---|---|---|

图 14：选择不同的终端

你不再需要离开 Visual Studio 即可使用终端窗口。这绝对非常节省时间。

## Studio Git 窗口

Visual Studio 现在将包含一个新的 Git 窗口。该窗口目前在 Visual Studio 2019 的预览版可用。

![](img/49b3596025cc7ecebab509ce03bfac_64_0.png)

图 15：Git 窗口

如图 15 所示，新的 Git 窗口布局非常漂亮，包含了你预期看到的所有内容。你可以从分支旁边的下拉菜单中操作。

![](img/49b3596025cc7ecebab509ce03bfac_65_0.png)

图 16：分支

如图 16 所示，该窗口显示了分支。你可以指定分支并选择你想要基于的基础的分支。

![](img/49b3596025cc7ecebab509ce03bfac_66_0.png)

图 17：创建新分支

管理分支也可以从下拉菜单轻松完成，如图 17 所示。

![](img/49b3596025cc7ecebab509ce03bfac_66_1.png)

图 18：Git 窗口中的分支

![](49b3596025cc7ecebab509ce03bfac_67_0.png)

图 19：管理分支

在这里你可以检出（checkout）、合并（merge）、变基（rebase）、重命名、删除或查看分支历史。

双击文件将在编辑器内显示代码差异，如图 20 所示。

![](img/49b3596025cc7ecebab509ce03bfac_68_0.png)

图 20：查看代码更改

Git 窗口还允许你执行常规任务，如储存（stashing）、暂存（staging）、撤销更改、获取（fetching）、推送（pushing）和同步（syncing）。根据 .NET 和 Visual Studio 程序经理 Mika Dumont 的说法，窗口 的目的是简化变得复杂的 Git 用户界面。

## 通过拖拽项目添加引用

在图 21 中，你会注意到解决方案中有两个项目。它们是：

- CSharpPreview
- CSharpPreview.Core

如果我想从 `CSharpPreview` 项目为 `CSharpPreview.Core` 添加引用，我只需点击并将 `CSharpPreview.Core` 项目拖到 `CSharpPreview` 项目上。

![](img/49b3596025cc7ecebab509ce03bfac_69_0.png)

图 21：添加项目引用

`CSharpPreview.Core` 的引用将被添加，如图 22 所示。

![](img/49b3596025cc7ecebab509ce03bfac_69_1.png)

图 22：项目引用已添加

不需要右键点击添加引用。你也可以从文件资源管理器将文件拖到解决方案管理器并将其到项目内部。该文件将被复制到你的源文件中。真棒！

## 搜索 Visual Studio

Visual Studio 中的另一个很棒的功能是 `Ctrl+Q`，这是一个非常棒的快捷键，它可以让 Visual Studio 中的搜索文本框获得焦点，让你立即开始输入（图 23）。

![](img/49b3596025cc7ecebab509ce03bfac_70_0.png)

图 23：搜索 Visual Studio

你可以进一步过滤你的搜索结果，只查看 Visual Studio 中的结果或代码中的结果（图 24）。

![](img/49b3596025cc7ecebab509ce03bfac_70_1.png)

图 24：通过驼峰命名法搜索代码

有趣的是，在 Visual Studio 中，你只需要输入驼峰命名（camel case）即可搜索代码，如图 24 所示。这非常棒，特别是当团队中有人决定创建一个 `SalesOrderFunctionalPreprocessor` 类时。

![](img/49b3596025ccb7ecebab509ce03bfac6_71_0.png)

图 25：部分驼峰字符搜索

在此实例中，能够输入 `SOF`（图 25）可以让代码搜索变得快速又简单。

![](img/49b3596025ccb7ecebab509ce03bfac6_71_1.png)

图 26：要运行的搜索命令

搜索还允许你运行命令（图 26）。这让你能够运行测试等，并且包含了键盘快捷键，这非常有帮助。

## 代码分析器

代码分析器可以确保你的代码具有更好的可读性，并在你编写过程中为你提供建议。请图 27。

![](img/49b3596025ccb7ecebab509ce03bfac6_72_0.png)

图 27：灯泡代码建议

灯泡会在你编写代码时对代码提出改进建议。然而，某些建议可能会被遗漏。请图 28。

```
var factorCount = intFactors.Count > 0 ? intFactors[intFactors.Count - 1] : 0;
```

图 28：代码修复建议

如果你仔细观察 `intFactors.Count - 1`，你会注意到变量 `intFactors` 的 "in" 部分下方有一个省略号（三个点）。

如果你点击省略号，你将看到代码修复建议（图 29）。在示例示例中，建议是使用索引操作符。关于索引操作符的更多信息，请查看代码列表 41。

intactors[intFactors.Count - 1] : 0;

![](img/49b3596025ccb7ecebab509ce03bfac6_73_0.png)

图 29：使用索引操作符的建议

你还可以通过应用代码修复的同一位置更改严重程度，来更改此代码修复建议的严重性（图 30）。

intFactors[intFactors.Count - 1] : 0;

![](img/49b3596025ccb7ecebab509ce03bfac6_73_1.png)

图 30：配置严重性

将此代码修复更改为警告将在被分析的代码下方显示一条波浪线，如图 31 所示。

```
var factorCount = intFactors.Count > 0 ? intFactors[intFactors.Count..1] : 0;
```

图 31：严重性提升为警告

代码分析器是 Visual Studio 的一项极功能，它们帮助开发人员和团队维护良好的编码规范。

## .editorconfig 中的文件头支持

`.editorconfig` 文件是在跨团队范围内强制执行特定代码风格或代码质量选项的通用方法（图 32）。

![](img/49b3596025ccb7ecebab509ce03bfac6_74_0.png)

图 32：`.editorconfig` 文件

该文件可以提交到版本控制中，并随你的解决方案传递给新的团队成员。

如果你打开 `.editorconfig` 文件（图 33），你会注意到我们在图 30 中为索引操作符添加的警告。`.editorconfig` 包含了文件头支持。现在我可以使用 `.editorconfig` 为解决方案中的文件添加文件头。要执行此操作，请如图 33 所示，在 `file_header_template` 中添加你想要的文本，并保存你的 `.editorconfig`。

![](img/49b3596025ccb7ecebab509ce03bfac6_75_0.png)

图 33：修改 `.editorconfig` 文件

在代码文件中，将光标置于第一个 `using` 语句之前的最顶部，并点击显示的灯泡（图 34）。

![](img/49b3596025ccb7ecebab509ce03bfac6_75_1.png)

图 34：添加文件头

你现在可以在代码文件中包含此文件头。你也可以选择将其添加到文档、项目或解决方案中。

## C# 语言资源

微软为开发人员提供了许多资源。网络上有丰富的代码库，还有各种社区让开发人员在需要时找到帮助。以下是一些你可能会觉得有用的资源。

### C# 语言参考

这份[引言]() 文档可能是你读得最多的文档。

### C# 语言提案

[语言提案]() 应该被视为动态文档，是查看围绕特定语言特性的当前想法的地方。

### C# 语言设计会议

语言设计会议（也称为 LDM）是 C# 团队研究、设计并决定添加到 C# 语言中的功能的场所。你可以在[此处查看会议记录]()()

### C# 语言设计设计

这是 [C# 语言的官方仓库]()()
