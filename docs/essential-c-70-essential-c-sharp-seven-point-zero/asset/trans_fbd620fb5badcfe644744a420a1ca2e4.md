
```csharp
static int DirectoryCountLines()
{
    return DirectoryCountLines(
        Directory.GetCurrentDirectory());
}

static int DirectoryCountLines(string directory)
{
    return DirectoryCountLines(directory, "*.cs");
}

static int DirectoryCountLines(
    string directory, string extension)
{
    int lineCount = 0;
    foreach (string file in
        Directory.GetFiles(directory, extension))
    {
        lineCount += CountLines(file);
    }

    foreach (string subdirectory in
        Directory.GetDirectories(directory))
    {
        lineCount += DirectoryCountLines(subdirectory);
    }

    return lineCount;
}

private static int CountLines(string file)
{
    int lineCount = 0;
    string line;
    FileStream stream =
        new FileStream(file, FileMode.Open);
    StreamReader reader = new StreamReader(stream);
    line = reader.ReadLine();
    while(line != null)
    {
        if (line.Trim() != "")
        {
            lineCount++;
        }
        line = reader.ReadLine();
    }
    reader.Close(); // Automatically closes the stream
    return lineCount;
}
```

*   这段代码可以通过使用 using 语句进行改进，这是一种我们之前回避使用的结构，因为该结构尚未在文中介绍。

## 输出 5.10

```bash
>LineCounter.exe .\*.cs
28
```

方法重载的效果是提供调用方法的可选方式。如在 Main() 中所示，你可以调用 DirectoryCountLines() 方法，无论是否传递要搜索的目录和文件扩展名。

请注意，DirectoryCountLines() 的无参数实现已被更改为调用单参数版本 (int DirectoryCountLines (string directory))。这是在实现重载方法时的一种常见模式。其思想是开发人员仅在一个方法中实现核心逻辑，所有其他重载方法都将调用该单一方法。如果核心实现发生变更，只需在一个位置进行修改，而不是在每个实现中修改。当使用方法重载来启用可选参数时，这种模式尤其普遍，因为这些参数没有编译时确定的值，因此无法使用可选参数指定。

> **注意**
>
> 将核心功能放在一个被所有其他重载方法调用的单一方法中，意味着你可以在核心方法中进行更改，其他方法将自动从中受益。

## 可选参数

从 C# 4.0 开始，语言设计人员添加了对**可选参数**的支持。通过允许在方法声明中将参数与常量值相关联，可以在不传递方法每个参数的参数的情况下调用该方法（参见列表 5.20）。

```csharp
using System.IO;

public static class LineCounter
{
    public static void Main(string[] args)
    {
        int totalLineCount;

        if (args.Length > 1)
        {
            totalLineCount =
                DirectoryCountLines(args[0], args[1]);
        }
        else if (args.Length > 0)
        {
            totalLineCount = DirectoryCountLines(args[0]);
        }
        else
        {
            totalLineCount = DirectoryCountLines();
        }

        System.Console.WriteLine(totalLineCount);
    }

    static int DirectoryCountLines()
    {
        // ... 
    }

    /*
    static int DirectoryCountLines(string directory)
    { ... }
    */

    static int DirectoryCountLines(
        string directory, string extension = "*.cs")
    {
        int lineCount = 0;
        foreach (string file in
            Directory.GetFiles(directory, extension))
        {
            lineCount += CountLines(file);
        }

        foreach (string subdirectory in
            Directory.GetDirectories(directory))
        {
            lineCount += DirectoryCountLines(subdirectory);
        }

        return lineCount;
    }

    private static int CountLines(string file)
    {
        // ...
    }
}
```

在列表 5.20 中，单参数的 DirectoryCountLines() 方法声明已被移除（被注释掉），但从 Main() 的调用（指定一个参数）仍然存在。当调用中未指定扩展名参数时，将使用声明中分配给 extension 的值（在这种情况下是 \*.cs）。这允许调用代码在需要时不指定值，并且消除了在 C# 3.0 及更早版本中所需的额外重载。请注意，可选参数必须出现在所有必需参数（那些没有默认值的参数）之后。此外，默认值必须是一个常量、在编译时解析的值，这一事实相当严格。例如，你不能声明像下面的方法：

```csharp
DirectoryCountLines(
    string directory = Environment.CurrentDirectory,
    string extension = "*.cs")
```

因为 Environment.CurrentDirectory 不是一个常量。相比之下，由于 \*.cs 是一个常量，C# 允许将其用作可选参数的默认值。

> **准则**
>
> - **务必**在可能的情况下为所有参数提供好的默认值。
> - **务必**提供具有少量必需参数的简单方法重载。
> - **考虑**将重载从最简单的到最复杂的进行组织。

C# 4.0 提供的第二个方法调用特性是使用命名参数。通过命名参数，调用者可以显式标识要分配值的参数名称，而不仅仅依赖于参数和参数的顺序来关联它们（参见列表 5.21）。

## 列表 5.21：按名称指定参数

```csharp
class Program
{
    static void Main()
    {
        DisplayGreeting(
            firstName: "Inigo", lastName: "Montoya");
    }

    public static void DisplayGreeting(
        string firstName,
        string middleName = default(string),
        string lastName = default(string))
    {
        // ...
    }
}
```

在列表 5.21 中，从 Main() 内部对 DisplayGreeting() 的调用通过名称将值分配给参数。在两个可选参数（middleName 和 lastName）中，只有 lastName 被作为参数提供。对于拥有许多参数且其中许多是可选的情况（在访问 Microsoft COM 库时很常见），使用命名参数语法确实是一种便利。然而，随着便利而来的是对方法接口灵活性的影响。过去，更改参数名称不会导致调用该方法的 C# 代码不再编译。随着命名参数的添加，参数名称成为接口的一部分，因为更改名称会导致使用命名参数的代码不再编译。

> **准则**
>
> - **务必**将参数名称视为 API 的一部分，如果 API 之间的版本兼容性很重要，则避免更改名称。

对于许多有经验的 C# 开发人员来说，这是一个令人惊讶的限制。然而，自 .NET 1.0 以来，这一限制就作为通用语言规范的一部分被强制执行。此外，Visual Basic 一直支持使用命名参数调用方法。因此，库开发人员应该已经遵循不更改参数名称的做法，以成功地在版本之间与其他 .NET 语言互操作。从本质上讲，C# 4.0 现在对更改参数名称施加了与其他许多 .NET 语言已经要求的相同的限制。

鉴于方法重载、可选参数和命名参数的组合，确定调用哪个方法变得不那么明显。如果所有参数都有恰好一个对应的参数（通过名称或位置）且类型兼容，除非参数是可选的（或参数数组），否则调用与方法是**适用的**（兼容的）。虽然这限制了可能被调用的方法数量，但它并没有确定唯一的方法。为了进一步区分将调用哪个特定方法，编译器仅使用调用者中明确标识的参数，忽略调用者中未指定的所有可选参数。因此，如果两个方法适用，因为其中一个具有可选参数，编译器将解析为没有可选参数的方法。

## 高级主题

### 方法解析

当编译器必须从多个适用方法中选择最适合特定调用的方法时，将选择具有*最具体*参数类型的方法。假设有两个适用方法，每个方法都需要从参数到参数类型的隐式转换，将使用参数类型为更派生类型的方法。

例如，如果调用者传递类型为 `int` 的参数，将选择接受 `double` 参数的方法，而不是接受 `object` 参数的方法。这是因为 `double` 比 `object` 更具体。有一些对象不是 double，但没有 double 不是对象，所以 double 必须更具体。

如果多个方法适用且无法确定唯一的最佳方法，编译器将发出错误，指示调用是模棱两可的。

例如，给定以下方法：

```csharp
static void Method(object thing){}
static void Method(double thing){}
static void Method(long thing){}
static void Method(int thing){}
```

