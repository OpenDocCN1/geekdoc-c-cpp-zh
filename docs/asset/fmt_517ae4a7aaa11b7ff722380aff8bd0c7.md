

> 注意 文件输入/输出（I/O）在第 23 章“Files and Streams”中讨论。

## Syntax API 核心

Syntax API 的核心是 `SyntaxTree` 类。`SyntaxTree` 对象是通过使用 `CSharpSyntaxTree.ParseText` 解析 C# 文件内容创建的。要从树中获取节点，`GetRootAsync`（或 `GetRoot`）方法返回根节点。所有节点都是派生自基类 `SyntaxNode` 的类的实例。为了在用户界面中显示根节点，`SyntaxNode` 在添加到 `Nodes` 属性之前会被 `SyntaxNodeViewModel` 类包装：

```csharp
private async void OnLoad(object sender, RoutedEventArgs e)
{
    // etc.

    SyntaxTree tree = CSharpSyntaxTree.ParseText(code);

    SyntaxNode node = await tree.GetRootAsync();

    Nodes.Add(new SyntaxNodeViewModel(node));
}
```

`Nodes` 属性的类型为 `ObservableCollection<SyntaxNodeViewModel>`。当集合更改时，它会更新用户界面。

```csharp
public ObservableCollection<SyntaxNodeViewModel> Nodes { get; }
= new ObservableCollection<SyntaxNodeViewModel>();
```

`SyntaxNodeViewModel` 类将 `SyntaxNode` 包装以在用户界面中显示。它定义了 `Children` 属性以递归显示所有子节点。`Children` 属性通过调用 `ChildNodes` 方法从语法树访问所有子节点，并将 `SyntaxNode` 对象的集合转换为 `SyntaxNodeViewModel`。此类还定义了稍后在本节中讨论的 `Tokens` 和 `Trivia` 属性。`TypeName` 属性返回由 `SyntaxNodeViewModel` 类包装的真实类型的名称。这应该是派生自基类 `SyntaxNode` 的类型（代码文件 `WPFSyntaxTree/ViewModels/SyntaxNodeViewModel.cs`）：

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

在用户界面中，`TreeView` 控件绑定到 `Nodes` 属性。`HierarchicalDataTemplate` 定义了树视图中项目的外观。通过此数据模板，`TypeName` 属性的值会显示在 `TextBlock` 中。为了显示所有子节点，`HierarchicalDataTemplate` 的 `ItemsSource` 属性绑定到 `Children` 属性（代码文件 `WPFSyntaxTree/MainWindow.xaml`）：

```xml
<TreeView x:Name="treeView" ItemsSource="{Binding Nodes, Mode=OneTime}" SelectedItemChanged="OnSelectSyntaxNode" Grid.Row="1" Grid.Column="0">
    <TreeView.ItemTemplate>
        <HierarchicalDataTemplate ItemsSource="{Binding Children}">
            <StackPanel>
                <TextBlock Text="{Binding TypeName}" />
            </StackPanel>
        </HierarchicalDataTemplate>
    </TreeView.ItemTemplate>
</TreeView>
```

使用示例应用程序打开的代码文件是一个简单的 Hello, World! 代码文件，其中还包含一些注释：

```csharp
using static System.Console;

namespace SyntaxTreeSample
{
    // Hello World! Sample Program
    public class Program
    {
        // Hello World! Sample Method
        public void Hello()
        {
            WriteLine("Hello, World!");
        }
    }
}
```

运行应用程序时，可以看到以下表格中显示的语法节点类型的树。`SyntaxNode` 使你能够遍历层次结构并访问父节点、祖先节点和后代节点。当使用返回 `TextSpan` 结构体的 `Span` 属性时，会返回源代码中的位置信息。以下表格第一列显示层次级别（2 是 1 的子节点；3 是 2 的子节点）；第二列给出节点类的类型；第三列列出节点的内容（如果内容较长，则显示省略号）；第四列给出 `Span` 属性的 `Start` 和 `End` 位置。通过此树，可以看到跨越完整源代码的 `CompilationUnitSyntax`。此节点的子节点是 `UsingDirectiveSyntax` 和 `NamespaceDeclarationSyntax`。`UsingDirectiveSyntax` 由用于导入静态 `System.Console` 类的 `using` 声明组成。`UsingDirectiveSyntax` 的子节点是 `QualifiedNameSyntax`，它本身包含两个 `IdentifierNameSyntax` 节点：

| Hierarchy Level | Syntax Node Type | Content | Span Start/End |
|---:|---|---|---:|
| 1 | `CompilationUnitSyntax` | `using static System.Console; ...` | `0.27...` |
| 2 | `UsingDirectiveSyntax` | `using static System.Console;` | `0.28...` |
| 3 | `QualifiedNameSyntax` | `System.Console` | `13.2...` |
| 4 | `IdentifierNameSyntax` | `System` | `13.1...` |
| 4 | `IdentifierNameSyntax` | `Console` | `20.2...` |
| 2 | `NamespaceDeclarationSyntax` | `namespace SyntaxTreeSample...` | `32.2...` |
| 3 | `IdentifierNameSyntax` | `SyntaxTreeSample` | `42.5...` |
| 3 | `ClassDeclarationSyntax` | `public class Program ...` | `103...` |
| 4 | `MethodDeclarationSyntax` | `public void Hello...` | `179...` |
| 5 | `PredefinedTypeSyntax` | `void` | `186...` |
| 5 | `ParameterListSyntax` | `()` | `196...` |
| 5 | `BlockSyntax` | `{ WriteLine(...` | `208...` |
| 6 | `ExpressionStatementSyntax` | `WriteLine("Hello,...` | `223` |
| 7 | `InvocationExpressionSyntax` | `WriteLine("Hello...` | `223` |
| 8 | `IdentifierNameSyntax` | `WriteLine` | `223` |
| 8 | `ArgumentListSyntax` | `("Hello, World!")` | `232` |
| 9 | `ArgumentSyntax` | `"Hello, World!"` | `233` |
| 10 | `LiteralExpressionSyntax` | `"Hello, World!"` | `233` |

语法节点并不是程序所需的一切。程序还需要标记。例如，示例程序的 `NamespaceDeclarationSyntax` 包含三个标记：`namespace`、`{` 和 `}`。`NamespaceDeclarationSyntax` 的子节点 `IdentifierNameSyntax` 具有值为 `SyntaxTreeSample` 的标记，即命名空间的名称。访问修饰符也是用标记定义的。`ClassDeclarationSyntax` 定义了五个标记：`public`、`class`、`Program`、`{` 和 `}`。

要在 WPF 应用程序中显示标记，定义了 `SyntaxTokenViewModel` 类来包装 `SyntaxToken`（代码文件 `WPFSyntaxTree/ViewModels/SyntaxTokenViewModel.cs`）：

```csharp
public class SyntaxTokenViewModel
{
    public SyntaxTokenViewModel(SyntaxToken syntaxToken)
    {
        SyntaxToken = syntaxToken;
    }

    public SyntaxToken SyntaxToken { get; }

    public string TypeName => SyntaxToken.GetType().Name;

    public override string ToString() => SyntaxToken.ToString();
}
```

为了编译程序，你需要节点和标记。要重建源文件，你需要更多内容：trivia。Trivia 定义空白字符和注释。为了显示 trivia，定义了 `SyntaxTriviaViewModel`（代码文件 `WPFSyntaxTree/ViewModels/SyntaxTriviaViewModel.cs`）：

```csharp
public enum TriviaKind
{
    Leading,
    Trailing,
    Structured,
    Annotated
}

public class SyntaxTriviaViewModel
{
    public SyntaxTriviaViewModel(TriviaKind kind, SyntaxTrivia syntaxTrivia)
    {
        TriviaKind = kind;
        SyntaxTrivia = syntaxTrivia;
    }

    public SyntaxTrivia SyntaxTrivia { get; }

    public TriviaKind TriviaKind { get; }

    public override string ToString() =>
        $"{{TriviaKind}, Start: {SyntaxTrivia.Span.Start}, " +
        $"Length: {SyntaxTrivia.Span.Length}: {SyntaxTrivia}";
}
```

运行应用程序并打开文件 `HelloWorld.cs` 时，可以看到带有标记和 trivia 的节点树，如图 18.4 所示。通过 trivia 你经常会看到空白字符，但也会看到注释。

```csharp
}

public int bar { get; set; }
```

与之前使用 Syntax API 的方式类似，使用类 `CSharpSyntaxTree` 和 `SyntaxTree` 获取根节点：

```csharp
static async Task CheckLowercaseMembers()
{
    string code = File.ReadAllText("../../Program.cs");

    SyntaxTree tree = CSharpSyntaxTree.ParseText(code);

    SyntaxNode root = await tree.GetRootAsync();

    // etc.
}
```

要获取树中遵循根节点的所有节点，`SyntaxNode` 类定义了方法 `DescendantNodes`。它返回节点的全部子节点以及子节点的子节点。之前示例中使用的方法 `ChildNodes` 只返回直接子节点。结果节点使用 `OfType` 方法进行过滤，以仅返回类型为 `MethodDeclarationSyntax` 的节点。`MethodDeclarationSyntax` 是一个派生自 `SyntaxNode` 的类，表示树中为方法的节点。你可以使用之前的示例 `WPFSyntaxTree` 查看现有源代码的所有节点类型。第一个 `Where` 方法定义了下一个过滤器。在这里，获取方法标识符（即方法名），并只获取第一个字符。使用方法 `char.IsLower` 确定第一个字符是否为小写。过滤器仅在该表达式为 true 时返回方法节点。对小写字符的此检查并不能满足我们所有的要求。还应仅返回公共成员。此过滤器由下一个 `Where` 方法定义。要检查公共访问修饰符，`MethodDeclarationSyntax` 定义了 `Modifiers` 属性。此属性返回方法的所有修饰符。`Where` 方法检查 `public` 修饰符是否属于修饰符列表。满足所有条件的方法会写入控制台。

```csharp
// etc.

    var methods = root.DescendantNodes()
        .OfType<MethodDeclarationSyntax>()
        .Where(m => char.IsLower(m.Identifier.ValueText.First()))
        .Where(m => m.Modifiers.Select(t => t.Value).Contains("public"));

    WriteLine("Public methods with lowercase first character:");

    foreach (var m in methods)
    {
        WriteLine(m.Identifier.ValueText);
    }

    // etc.
```

检索子元素和父元素的其他方法如下：

- `DescendantNodesAndSelf` 返回调用该方法的节点以及所有后代。
- `DescendantTokens` 返回所有后代标记
- `DescendantTrivia` 返回 trivia 信息
- `Ancestors` 检索父节点和父节点的父节点

若干方法是对前面列出方法的组合，例如 `DescendantNodesAndTokensAndSelf`。你可以在树中的每个 `SyntaxNode` 上使用这些方法。

要检索具有相同条件的属性，语法类似。你只需要获取类型为 `PropertyDeclarationSyntax` 的语法节点：

```csharp
// etc.

var properties = root.DescendantNodes()
    .OfType<PropertyDeclarationSyntax>()
```

