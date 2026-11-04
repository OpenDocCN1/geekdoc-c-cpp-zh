
```csharp
public string FixNamespaceLine(string line)
{
    const string COMPANY_PREFIX = "CMSCo";
    int spaceIndex = line.IndexOf(' ');
    int nameStart = GetNameStartAfterNamespaceKeyword(line, spaceIndex);
    string newline = string.Empty;
    newline = PlugInNamespaceCompanyQualifier(line, COMPANY_PREFIX, nameStart);
    return newline.Trim();
}
```

给定一个 C# 文件，此方法属于旨在查找文件中的 namespace 关键字并在命名空间名称上作为前缀插入代表公司名称（我们其中之一的字符串）的某些代码的一部分。（有关命名空间的信息，请参阅第 II 书第 10 章。）以下示例说明了 namespace 关键字在 C# 文件中可能出现的位置：

```csharp
using System;
namespace SomeName
{
    // Code within the namespace . . .
}
```

结果运行 FixNamespaceLine() 方法对此类文件应将第一行转换为第二行：

```
namespace SomeName
namespace CmsCo.SomeName
```

整体程序读取 .CS 文件。然后逐行遍历，将每一行传递给 FixNamespaceLine() 方法。给定一行代码，该方法调用 String.IndexOf() 来查找命名空间名称的索引（通常为 10）。然后它调用 GetNameStartAfterNamespaceKeyword() 来定位命名空间名称的开头。最后，它调用另一个方法 PlugInNamespaceCompanyQualifier() 将公司名称插入到行中的正确位置，然后返回。大部分工作由从属方法完成。

首先，即使不知道这段代码的用途或两个被调用方法的作用，也要考虑输入。line 参数对于对 String.IndexOf() 的调用可能至少存在一个问题。如果 line 为 null，则 IndexOf() 调用会产生 ArgumentNullException。你不能对空对象调用方法。此外，乍一看，对空字符串调用 IndexOf() 会工作吗？事实证明它会工作，因此不会发生异常，但如果将空行传递给那些名称很长的方法之一会怎样？我们建议在 FixNamespaceLine() 中的第一行代码之前添加（如果有必要）一个保护子句——至少检查 null：

```csharp
if(String.IsNullOrEmpty(name))  // A handy string method
{
    return name;  // You can get away with a reasonable return value here
    // instead of throwing an exception.
}
```

第二，在安全通过 `IndexOf()` 调用之后，即使事先仔细检查了 `line`，其中一个方法调用仍可能抛出异常。如果 `spaceIndex` turns out 为 -1（未找到）——因为传入的行通常不包含 `namespace` 关键字而可能发生这种情况——将其传递给第一个方法可能会有问题。当然，你可以像这样防范这种情况：

```
if (spaceIndex > -1) ...
```

如果 `spaceIndex` 为负数，则该行不包含 `namespace` 关键字。这不是错误。你只需通过返回原始行来跳过该行，然后继续下一行。无论如何，不要调用从属方法。

方法中的方法调用需要探索每一个，以查看它可能抛出哪些异常，然后深入研究这些方法调用的任何方法，依此类推，直到到达此特定调用链的底部。

考虑到这种可能性，并且鉴于 `FixNamespaceLine()` 首先需要额外的防弹保护子句，你可能会在哪里放置异常处理程序？

你可能想把 `FixNamespaceLine()` 的大部分内容放在 `try` 块中。但你必须考虑这是否是最佳位置。此方法属于低级方法，因此应根据需要抛出异常——或只是传递在它调用的方法中发生的任何异常。我们建议向上查找调用链，看看哪个方法可能是处理程序的合适位置。

随着你向上移动调用链，请自问前面“Some questions to guide your planning”部分中的问题。如果 `FixNamespaceLine()` 抛出异常会怎样？这取决于其结果在链中更高层如何使用。此外，结果需要多么严重？如果无法为当前文件“修复”命名空间行，用户会失去什么重要东西吗？也许偶尔未修复的文件是可以接受的，在这种情况下，你可能会选择在调用链的某个级别“吞掉”异常，只通知用户未处理的文件。也许不是。你明白了。我们在 csharp102.info 上的文章“Responding to an Exception”中讨论了这些和其他异常处理选项。

寓意是，正确设置异常处理程序需要一些分析和思考。

然而，请记住任何方法调用都可能抛出异常——例如，应用程序可能内存不足，或者它所在的程序集可能找不到并加载。你对此无能为力。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_227_0.png)

## 如何找出哪些方法抛出哪些异常

要确定是否调用 .NET 类库中的特定方法，例如 String.IndexOf()——甚至是你自己的方法之一——会抛出异常，请考虑以下指南：

- Visual Studio 提供即时帮助，带有工具提示。当你在 Visual Studio 编辑器中将鼠标指针悬停在方法名称上时，一个黄色工具提示窗口不仅列出方法参数和返回类型，还列出它可能抛出的异常。
- 如果你使用 XML 注释来注释自己的方法。Visual Studio 会在 IntelliSense 工具提示中显示这些注释中的信息，就像对 .NET 方法一样。如果你记录了方法可能抛出的异常（参见上一节），你会在工具提示中看到它们。csharp102.info 上的文章“Getting Help in Visual Studio”展示了如何使用 XML 注释，而 FactorialException 示例说明了如何使用 XML 注释记录 Factorial()。在 <summary> 注释内插入 <exception> 行以使其在工具提示中显示。
- 帮助文件提供更多信息。当你在帮助中查找 .NET 方法时，你会找到方法可能抛出的异常列表，以及黄色 Visual Studio 工具提示中未提供的额外描述。要打开给定方法的帮助页面，请在代码中单击方法名称并按 F1。你也可以为自己的类和方法提供类似的帮助。

你应该查看列出的每个异常，判断其发生的可能性，并（如果对你的程序有必要）使用本章其余部分介绍的技术对其进行防护。

## 抓住捕获异常的最后机会

前面“Can I Get an Exceptional Example?” 部分中的 FactorialException 示例将 Main() 的所有内容（除最后的控制台调用外）包装在外部的“最后机会”异常处理程序中。

如果你正在编写应用程序，始终将 Main() 的内容夹在 try 块中，因为 Main() 是程序的起点，也是终点。（如果你正在编写打算重用的类库，不必担心未处理的异常——使用你的库的人需要知道所有异常，因此让它们通过你的方法冒泡。）

任何其他地方未捕获的异常都会渗透到 `Main()`。这是你在错误返回到 Windows 之前抓住它的最后机会，在那里错误消息更难解释，可能会让程序用户感到沮丧——甚至吓坏——。

`FactorialException` 的 `Main()` 中的所有重要代码都在 `try` 块内。关联的 `catch` 块捕获任何异常并向控制台输出消息，应用程序退出。

这个 `catch` 块通过拦截其他地方未处理的异常来防止硬崩溃。而且这是你解释应用程序为何退出机会。

实验一下。为了了解为什么需要这个最后机会处理程序，故意在一个小程序中抛出异常而不处理它。你会看到用户在你没有努力使着陆更柔和时会看到什么。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_229_0.png)

在开发期间，你 *希望* 在测试代码时看到发生的异常，在其自然环境中——因此你想要所有极客术语。在你发布的版本中，将程序员式的细节转换为普通英语，向用户显示消息，包括，如果可能的话，他下次成功运行可能需要做什么，并优雅退出。让这个纯英语版本的异常处理程序成为你在将程序发布到野外之前完成的最后任务之一。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_229_1.png)

你的最后机会处理程序当然应该以某种方式记录异常信息，以便日后进行取证分析。

## 更多信息

|  |
|---|
| 我们希望能够说我们告诉你关于异常的全部故事。我们非常希望如此。但我们没有，而且这是一个相当长的故事。<br><br>要追踪故事的其余部分，我们建议你前往网站 `csharp102.info`，在那里你可以找到有关以下主题的文章：<br><br>- **创建你自己的异常类：** .NET Framework 类库开发人员并不是唯一可以为类 `Exception` 扩展新异常子类的人。你也可以自己扩展 `Exception`。有关原因和如何操作，请参阅本书网站上的文章“Creating Your Own Exception Class”。<br><br>- **响应异常——当代码抛出异常时你可以做什么：** 你的选项是修复问题并重试，部分修复问题并将其交给可能能够修复其余部分的更高级别异常处理程序，将异常转换为不同异常类型，或什么都不做。本书网站上的文章“Responding to an Exception”通过几个示例探讨了这些选项。 |
