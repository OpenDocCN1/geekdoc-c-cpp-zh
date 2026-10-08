
代码片段可以组成分级文件夹结构。例如，Visual C# 代码片段包含以下文件夹：

- NetFX3 — 这些是针对 .NET 3.0 新特性的代码片段。
- OfficeDevelopment — 这些是帮助完成 Microsoft Office 开发任务的代码片段。
- other — 这是存放其他代码片段的文件夹。目前，在此处可以找到几个 WF 代码片段。
- Refactoring — 这些是由 C# 语言服务用于重构函数的代码片段。
- Visual C# — 这些是与 C# 语言相关的通用代码片段（属性、事件、类等）。

系统文件夹拥有所谓的索引文件来列出代码片段。这些文件确实存在，其名称在 Visual Basic 中为 `SnippetIndex.xml`，对于其他语言为 `SnippetsIndex.xml`。这些索引文件的格式超出了本书的范围，但你可以自由地打开并查看它们。

## 添加和删除代码片段

代码片段管理器（Code Snippets Manager）允许你添加包含代码片段的自定义文件夹。如前文所述，代码片段管理器仅存储文件夹的路径。通过使用“添加”按钮，你可以仅为所选语言添加顶级文件夹。当你点击“添加”按钮时，会弹出一个带有代码片段目录的文件夹选择对话框，让你指定要添加的文件夹。在你将文件夹添加到目录后，它将显示在文件夹列表中。你可以立即浏览其内容。

当你在列表中选择一个文件夹并点击“删除”按钮时，你可以将其从代码库中移除。当然，此操作不会删除文件夹的内容；它只是将其从代码片段管理器处理的列表中剔除掉。你只能移除顶级文件夹。当你选择子文件夹或代码片段时，“删除”按钮将被禁用。

请小心删除系统文件夹。代码片段管理器允许你删除它们，且不会进行任何确认。如果你不小心删除了系统文件夹，稍后可以通过选择你移除的物理文件夹来重新添加它。在再次添加后，Visual Studio 会将其识别为系统文件夹并进行正确处理。

## 导入代码片段

如果你有一个组织良好的文件夹，包含大量代码片段，可以使用代码片段管理器将该文件夹添加到相应的语言中。然而，如果你有尚未组织在任何文件夹中的 `.snippet` 文件，可以对其进行导入，并将其中的代码片段成为你库的一部分。

在选择了一个或多个 `.snippet` 文件后，点击“导入”按钮开始导入代码片段。图 3-19 显示的“导入代码片段”对话框将弹出，让你为每个文件选择导入文件夹。

![](img/b5597c749e848b27b0d305153ae16106_96_0.png)

**图 3-19：** 使用导入代码片段对话框

窗口的左格显示代码片段文件夹，右格列出要导入的用户文件夹。当导入代码片段文件时，文件会被物理复制到所选文件夹中。如图 3-19 所示，你可以为每个单独的文件设置导入文件夹。一个文件可以复制到一个或多个文件夹中。图 3-19 展示了这样的情况：选定的代码片段都要导入到“My Code Snippets”文件夹中，而其中仅有一个准备放入“My Special Snippets”。

代码代码片段管理器允许你仅将代码片段导入到顶级用户文件夹。

你可以选择支持不同语言的代码片段文件夹。“导入代码片段”对话框会根据其宿主语言对其进行分组。你可以点击“上一个”和“下一个”按钮在语言之间翻页，并选择合适的文件夹。对话框左侧代码片段面板上方的标签会告诉你面板列出的文件的宿主语言。

当你点击“完成”按钮时，代码片段文件将立即导入到所选文件夹并准备就绪。

## 高级代码片段功能

到本章为止，你已经学习了代码片段的概念、`.snippet` 文件格式以及代码片段管理器的作用。让我们看看代码片段的高级功能。

## 一个文件中的多个代码片段

`.snippet` 文件的设计初衷就是允许包含多个 `<Snippet>` 元素，如代码段 4 所示。

代码段 4：一个文件中的多个代码片段

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeSnippet xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">

<!-- 第一个代码片段 -->
<Snippet>
  <Declarations>
    <Literal>
      <ID>condition</ID>
      <ToolTip>评估的条件</ToolTip>
      <Default>true</Default>
    </Literal>
  </Declarations>
  <Code Language="C#">
    <![CDATA[if ($condition$) {Console.WriteLine("xxx")}]]>
  </Code>
</Snippet>

<!-- 第二个代码片段 -->
<Snippet>
  <Declarations>
    <Literal>
      <ID>value</ID>
      <ToolTip>要比较的值</ToolTip>
      <Default>someVal</Default>
    </Literal>
  </Declarations>
  <Code Language="C#">
    <![CDATA[if (condVar > $value$) {Console.WriteLine("xxx")}}]]>
  </Code>
</Snippet>

<!-- 第三个代码片段 -->
<Snippet>
  <Declarations>
    <Literal>
      <ID>methodName</ID>
      <ToolTip>要重构的方法名</ToolTip>
      <Default>TestMethod</Default>
    </Literal>
  </Declarations>
  <Code Language="C#">
    <![CDATA[void $methodName$() { // 重构后的代码 }]]>
  </Code>
</Snippet>
</CodeSnippet>
```

当你导入文件时，你将看到所有代码片段显示在管理器中，如图 3-20 所示。将具有共同行为的两个片段放在一个文件中是易于管理的。然而，如果你将更多片段放入一个文件，管理性将变得困难，而且可能导致复杂化。

![](img/b5597c749e848b27b0d305153ae16106_98_0.png)

图 3-20：导入包含多个片段的文件

## 其他语言中的代码片段

如前文所述，Visual Studio 2010 开箱支持 HTML、JScript、Visual Basic、C# 和 SQL 的代码片段。然而，代码片段的基础适用于任何其他语言。Visual Studio 允许创建语言服务来实现其他语言，这些语言可以使用代码片段的基础来创建自己的支持。

语言服务可以进行自定义，以确定它们如何使用代码片段，以及在代码编辑器中针对特定语言提供何种支持。你可以想象，Visual Basic 实现与其他语言在处理代码片段类型（例如类型声明、方法声明、方法体等）以及提供环境代码片段方面存在巨大差异。

语言提供程序可以决定是否实现代码片段，如果实现，则决定支持哪些功能。例如，你可以为 Visual Studio 2008 安装 IronPython，它为 IronPython 语言提供了语言服务，并且确实实现了代码片段。图 3-21 显示了带有 Python 语言过滤器并已安装 Python 代码片段的代码片段管理器。

当你查看 Python 代码片段文件时，你会发现它们使用了标准的代码片段基础。你可以从 `<code>` 元素明确识别出这些片段属于 Python 语言：

```xml
<Snippet>
  <Declarations>
    <Literal>
      <ID>Expression</ID>
      <ToolTip>要评估的表达式</ToolTip>
      <Default>true</Default>
    </Literal>
  </Declarations>
  <Code Language="python">
    <![CDATA[while $expression$:
      $selected$end
    ]]>
  </Code>
</Snippet>
```
