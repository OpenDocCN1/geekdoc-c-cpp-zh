
In the user interface, the TreeView control binds to the Nodes property. The HierarchicalDataTemplate defines the look of the items in the tree view. With this data template, the value of the TypeName property is shown in a TextBlock. For showing all the child nodes, the ItemsSource property of the HierarchicalDataTemplate is bound to the Children property (code file `WPFSyntaxTree/MainWindow.xaml`):

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

The code file that is opened with the sample application is a simple Hello, World! code file that also includes some comments:

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

When you run the application, you can see a tree of the syntax node types shown in the following table. A SyntaxNode enables you to walk through the hierarchy and also access the parent node, ancestors, and descendants. When you use the Span property, which returns a TextSpan struct, the position information within the source code is returned. The following table shows the hierarchy level in the first column (2 is a child node of 1; 3 is a child node of 2); the second column gives the type of the node class; the third column lists the content of the node (if the content is longer, an ellipsis is shown); and the fourth column gives the Start and End positions of the Span property. With this tree, you can see the CompilationUnitSyntax that spans the complete source code. Child nodes of this node are the UsingDirectiveSyntax and the NamespaceDeclarationSyntax. The UsingDirectiveSyntax consists of the using declaration to import the static System.Console class. The child node of the UsingDirectiveSyntax is the QualifiedNameSyntax that itself contains two IdentifierNameSyntax nodes:

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

The syntax nodes are not all that’s needed for a program. A program also needs tokens. For example, the `NamespaceDeclarationSyntax` of the sample program contains three tokens: `namespace`, `{`, and `}`. The child node of the `NamespaceDeclarationSyntax`, the `IdentifierNameSyntax`, has a token with the value `SyntaxTreeSample`, the name of the namespace. Access modifiers are also defined with tokens. The `ClassDeclarationSyntax` defines five tokens: `public`, `class`, `Program`, `{`, and `}`.

To show the tokens in the WPF application, the `SyntaxTokenViewModel` class is defined that wraps a `SyntaxToken` (code file `WPFSyntaxTree/ViewModels/SyntaxTokenViewModel.cs`):

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

For compiling the program, you need nodes and tokens. To rebuild the source file, you need something more: trivia. Trivia defines whitespace and also comments. To show the trivia, the `SyntaxTriviaViewModel` is defined (code file `WPFSyntaxTree/ViewModels/SyntaxTriviaViewModel.cs`):

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

When you run the application and open the file `HelloWorld.cs`, you can see the node tree with tokens and trivia as shown in Figure 18.4. With trivia you often see white space, but you also see comments.

```csharp
}

public int bar { get; set; }
```

Similar to the way the Syntax API was used before, the root node is retrieved using the classes `CSharpSyntaxTree` and `SyntaxTree`:

```csharp
static async Task CheckLowercaseMembers()
{
    string code = File.ReadAllText("../../Program.cs");
    SyntaxTree tree = CSharpSyntaxTree.ParseText(code);
    SyntaxNode root = await tree.GetRootAsync();
    // etc.
```

To get all the nodes in the tree that follow the root node, the `SyntaxNode` class defines the method `DescendantNodes`. This returns all the children of the node and the children’s children. The method `ChildNodes` that has been used in the earlier example returns only the direct children. The resulting nodes are filtered with the `OfType` method to return only the nodes of type `MethodDeclarationSyntax`. `MethodDeclarationSyntax` is a class that derives from `SyntaxNode` and represents a node that is a method in the tree. You can use the previous sample `WPFSyntaxTree` to see all the node types for existing source code. The first `Where` method defines the next filter. Here, the identifier of the method (that’s the method name) is taken, and just the first character is retrieved. The method `char.IsLower` is used to determine whether the first character is lowercase. The filter returns the method node only if this expression is true. This check for lowercase characters doesn’t fulfill all the requirements we have. Also, only public members should be returned. This filter is defined by the next `Where` method. To check the public access modifier, the `MethodDeclarationSyntax` defines a `Modifiers` property. This property returns all the modifiers of the method. The `Where` method checks whether the `public` modifier belongs to the list of modifiers. The methods where all the conditions apply are written to the console.

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

Other methods to retrieve children and parent elements are the following:

- `DescendantNodesAndSelf` returns the node invoking the method in addition to all descendants.
- `DescendantTokens` returns all the descendant tokens
- `DescendantTrivia` returns trivia information
- `Ancestors` retrieves the parent and parent’s parent nodes

Several methods are a combination of the previously listed methods, such as `DescendantNodesAndTokensAndSelf`. You can use these methods with every `SyntaxNode` in the tree.

To retrieve the properties with the same conditions, the syntax is similar. You just need to get the syntax nodes of type `PropertyDeclarationSyntax`:

```csharp
// etc.
var properties = root.DescendantNodes()
    .OfType<PropertyDeclarationSyntax>()
    .Where(p => char.IsLower(p.Identifier.ValueText.First()))
    .Where(p => p.Modifiers.Select(t => t.Value).Contains("public"));

WriteLine("Public properties with lowercase first character:");
foreach (var p in properties)
{
    WriteLine(p.Identifier.ValueText);
}
```

When you run the application, you see the following result and change the source files accordingly to fulfill the guidelines:

```text
Public methods with lowercase first character:
foo
Public properties with lowercase first character:
bar
```

## Walking Through Nodes

Besides doing queries, there’s another way to efficiently filter source code trees based on specific node types: syntax walkers. A syntax walker visits all nodes within a syntax tree. This means while parsing the syntax tree, different `VisitXXX` methods of the syntax walker are invoked.

The next sample defines a syntax walker that retrieves all using directives to show a list of all needed imports for all C# files from a specified directory.

You create a syntax walker by creating a class that derives from `CSharpSyntaxWalker`. The class `UsingCollector` overrides the method `VisitUsingDirective` to collect all using directives from a syntax tree. The `UsingDirectiveSyntax` node that is passed to this method is added to a collection (code file `SyntaxWalker/UsingCollector.cs`):

```csharp
class UsingCollector: CSharpSyntaxWalker
{
    private readonly List<UsingDirectiveSyntax> _usingDirectives =
        new List<UsingDirectiveSyntax>();
```
