

## 18 .NET 编译器平台

### 本章内容

- 编译器管道概述
- 语法分析
- 语义分析
- 代码转换
- 代码重构

### 本章 Wrox.com 代码下载

本章的 wrox.com 代码下载可在 www.wrox.com/go/professionalcsharp6 的 Download Code 选项卡上找到。
本章的代码分为以下主要示例：

- WPFSyntaxTree
- SyntaxQuery
- SyntaxWalker
- SemanticsCompilation
- TransformMethods
- SyntaxRewriter
- PropertyCodeRefactoring

### 引言

C# 6 最重要的变化是 C# 有了一个由 .NET 编译器平台提供的全新编译器（代号 Roslyn）。
最初，C# 编译器是用 C++ 编写的。现在它的主要部分是用 C# 和 .NET 创建的。编译器平台可在 http://github.com/dotnet/Roslyn 以开源形式获得。

这次更新的一个优势是，Microsoft 清理了过去 20 年内编写的大量遗留代码。借助新的代码库，使用 C# 实现新功能变得容易得多；新代码更易于维护。这就是为什么在版本 6 中你会看到许多小的 C# 语言改进的原因。这不仅仅是 Microsoft 面临的情况；对于维护多年的项目，使用源代码进行更新变得困难。到了某个阶段，从头开始项目会更好。

重写 C# 编译器的一个更大的优势是，现在可以利用编译器管道，在编译器管道的每一步添加功能，并且还可以分析和转换源代码。

大多数开发人员只会通过使用 Visual Studio 中利用 .NET 编译器平台本身的工具来受益，但对于许多人来说，创建自定义代码分析器（可在团队内使用）以及代码转换——例如，将遗留代码迁移并转换为新技术——将非常有用。

你可以在 Visual Studio 的哪里看到 .NET 编译器平台的使用？一个例子是代码编辑器，在你输入时 API 不断被使用。当你使用智能标记实现接口时，Visual Studio 2015 与以前版本之间有一个有趣的区别：当你实现接口 IDisposable 并单击智能标记时，你不仅可以看到 Implement Interface 和 Implement Interface Explicitly 选项，还可以看到 Implement Interface with Dispose Pattern 和 Implement Interface Explicitly with Dispose Pattern 选项（见图 18.1）。在 Visual Studio 的早期版本中，实现接口的唯一自动方式是自动生成接口中定义的方法和属性的方法存根和属性存根，其中接口的实现会抛出 NotImplementedException。现在你可以根据接口类型拥有不同的实现。对于接口 IDisposable，实现的不仅仅是 Dispose 方法：为此接口所需完整模式，例如带布尔参数的 Dispose 方法；检查对象是否已被释放但仍被调用；以及可选的终结器也被实现。

![](img/3d365b72b289213a91ade7eb366b8f35_663_0.png)

图 18.1

本章描述了 .NET 编译器平台的功能以及如何分析和转换源代码。使用调试器了解类型和成员对本书的所有章节都有帮助。对于本章，使用调试器极其有帮助。.NET 编译器平台 SDK 包含数千种类型和一个

让我们从一个简单的任务开始：使用 Syntax API 进行语法分析。使用 Syntax API，你可以从 C# 源代码构建语法节点树。示例应用程序是一个 WPF 应用程序，你可以在其中加载任何 C# 源文件，并在树视图中显示源文件的层次结构。

> 注意 XAML 和 WPF 的详细说明从第 29 章“Core XAML”开始，并在其后的章节中继续。你可以在第 34 章“Windows Desktop Applications with WPF”中阅读有关树视图控件的更多信息。

示例应用程序定义了一个用户界面，其中包含一个用于加载 C# 源文件的按钮控件、一个 TreeView 控件，以及一些用于显示文档大纲（见图 18.2）和 XAML 设计器（见图 18.3）中节点的详细信息的 TextBlock 和 ListBox 控件。数据绑定用于将信息内容绑定到 UI 元素。

![](img/3d365b72b289213a91ade7eb366b8f35_665_0.png)

图 18.2

![](img/3d365b72b289213a91ade7eb366b8f35_666_0.png)

图 18.3

当你运行应用程序后，单击 Load 按钮后，会在 OpenFileDialog 类的帮助下提示你选择一个 C# 文件。单击此对话框中的 OK 后，文件将被加载到语法树中（代码文件 WPFSyntaxTree/MainWindow.xaml.cs）：

```csharp
private async void OnLoad(object sender, RoutedEventArgs e)
{
    var dlg = new OpenFileDialog();
    dlg.Filter ="C# Code (.cs)|*.cs";

    if (dlg.ShowDialog() == true)
    {
        string code = File.ReadAllText(dlg.FileName);
        // load the syntax tree
    }
}
```

> 注意 文件输入/输出（I/O）在第 23 章“Files and Streams”中讨论。

Syntax API 的核心是 SyntaxTree 类。SyntaxTree 对象是通过使用 CSharpSyntaxTree.ParseText 解析 C# 文件内容创建的。要从树中获取节点，GetRootAsync（或 GetRoot）方法返回根节点。所有节点都是派生自基类 SyntaxNode 的类的实例。为了在用户界面中显示根节点，SyntaxNode 在添加到 Nodes 属性之前会被 SyntaxNodeViewModel 类包装：

```csharp
private async void OnLoad(object sender, RoutedEventArgs e)
{
    // etc.

    SyntaxTree tree = CSharpSyntaxTree.ParseText(code);
    SyntaxNode node = await tree.GetRootAsync();

    Nodes.Add(new SyntaxNodeViewModel(node));
}
}
```

Nodes 属性的类型为 ObservableCollection<SyntaxNodeViewModel>。当集合更改时，它会更新用户界面。

```csharp
public ObservableCollection<SyntaxNodeViewModel> Nodes { get; }
= new ObservableCollection<SyntaxNodeViewModel>();
```

SyntaxNodeViewModel 类将 SyntaxNode 包装以在用户界面中显示。它定义了 Children 属性以递归显示所有子节点。Children 属性通过调用 ChildNodes 方法从语法树访问所有子节点，并将 SyntaxNode 对象的集合转换为 SyntaxNodeViewModel。此类还定义了稍后在本节中讨论的 Tokens 和 Trivia 属性。TypeName 属性返回由 SyntaxNodeViewModel 类包装的真实类型的名称。这应该是派生自基类 SyntaxNode 的类型（代码文件 WPFSyntaxTree/ViewModels/SyntaxNodeViewModel.cs）：

```csharp
public class SyntaxNodeViewModel
{
    public SyntaxNodeViewModel(SyntaxNode syntaxNode)
    {
        SyntaxNode = syntaxNode;
    }

    public SyntaxNode SyntaxNode { get; }

    public IEnumerable<SyntaxNodeViewModel> Children =>
        SyntaxNode.ChildNodes().Select(n => new SyntaxNodeViewModel(n));

    public IEnumerable<SyntaxTokenViewModel> Tokens =>
        SyntaxNode.ChildTokens().Select(t => new SyntaxTokenViewModel(t));

    public string TypeName => SyntaxNode.GetType().Name;

    public IEnumerable<SyntaxTriviaViewModel> Trivia
    {
        get
        {
            var leadingTrivia = SyntaxNode.GetLeadingTrivia().Select(
                t => new SyntaxTriviaViewModel(TriviaKind.Leading, t));
            var trailingTrivia =
            SyntaxNode.GetTrailingTrivia().Select(
                t => new SyntaxTriviaViewModel(TriviaKind.Trailing, t));
            return leadingTrivia.Union(trailingTrivia);
        }
    }
}
```

