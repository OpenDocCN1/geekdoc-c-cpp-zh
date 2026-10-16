```
public IEnumerable<UsingDirectiveSyntax> UsingDirectives =>
    _usingDirectives;

public override void VisitUsingDirective(UsingDirectiveSyntax node)
{
    _usingDirectives.Add(node);
}
}
```

The class `CSharpSyntaxWalker` defines virtual methods for many different kind of nodes that can be overwritten. You can use `VisitToken` and `VisitTrivia` to retrieve token and trivia information. You can also collect information about specific source code statements, such as `VisitWhileStatement`, `VisitWhereClause`, `VisitTryStatement`, `VisitThrowStatement`, `VisitThisExpression`, `VisitSwitchStatement`, and many more.

The `Main` method checks for a program argument that contains the directory for the C# source files that should be checked for the using declarations (code file `SyntaxWalker/Program.cs`):

```
static void Main(string[] args)
{
    if (args.Length != 1)
    {
        ShowUsage();
        return;
    }

    string path = args[0];
    if (!Directory.Exists(path))
    {
        ShowUsage();
        return;
    }
}
```

```
static void ShowUsage()
{
    WriteLine("Usage: SyntaxWalker directory");
}
```

The method `ProcessUsingsAsync` does all the processing. First, a `UsingCollector` instance is created. To iterate through all the files from the passed directory, the `Directory.EnumerateFiles` method is used with the search pattern `*.cs` to retrieve all C# files. However, automatically generated C# files should be excluded—that’s why files with the file extensions `.g.i.cs` and `.g.cs` are filtered out using the `Where` method. Within the following `foreach` statement, the syntax tree is built and passed to the `Visit` method of the `UsingCollector` instance:

```
static async Task ProcessUsingsAsync(string path)
{
    const string searchPattern = "*.cs";
    var collector = new UsingCollector();

    IEnumerable<string> fileNames =
        Directory.EnumerateFiles(path, searchPattern,
```