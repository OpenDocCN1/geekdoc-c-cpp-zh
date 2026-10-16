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

```
public class SyntaxTokenViewModel
{
    public SyntaxTokenViewModel(SyntaxToken syntaxToken)
    {
        SyntaxToken = syntaxToken;
    }

    public SyntaxToken SyntaxToken { get; }
}
```