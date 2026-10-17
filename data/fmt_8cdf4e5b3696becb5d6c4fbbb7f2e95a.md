
```csharp
using System.IO;

public static class LineCounter
{
    // 使用第一个参数作为目录
    // 进行搜索
    return lineCount;
}
private static int CountLines(string file)
{
    string? line;
    int lineCount = 0;
    // 此处可以使用 using 语句进行改进，
    // 目前尚未描述。
    FileStream stream = new(file, FileMode.Open);
    StreamReader reader = new(stream);
    line = reader.ReadLine();

    while (line != null)
    {
        if (line.Trim() != "")
        {
            lineCount++;
        }
        line = reader.ReadLine();
    }

    reader.Dispose(); // 自动关闭流
    return lineCount;
}
```

输出 5.8 显示了列表 22 的结果。

**输出 5.8**

104

程序通过将命令行参数传递给 `DirectoryCountLines()` 或在未提供参数时使用当前目录开始运行。该方法首先遍历目录中的所有文件并汇总每个文件的行数。处理目录中的每个文件后，通过将子目录传回 `DirectoryCountLines()` 方法递归地处理每个子目录。该过程重复，直到没有剩余的目录。

不熟悉递归的读者起可能会感到困惑。无论如何，对于文件系统等分级数据，这通常是代码简单的模式。然而，尽管这种方法可能最具可读性，但它通常不是最快的实现。如果性能成为问题，开发者应该寻找递归实现的替代方案。

# 初学者错误

递归实现的选择通常取决于可读性与性能的平衡。递归方法中常见的编程错误以程序执行期间栈溢出的形式出现。这通常由于无限递归导致，方法不断调用自身，从未触发递归的结束。对于使用递归的方法，验证调用是有限的是一个良好的习惯。

递归的常用伪代码如下：

```text
M(x)
{
  if x is trivial
    return result
  else
    a. 执行一些工作使问题变小
    b. 递归调用 M 来解决问题
    c. 根据 a 和 b 计算结果
  return result
```

不遵循此模式时就会出错。例如，如果不让问题变小，或者如果不处理所有可能的边界情况，递归永远不会终止。

# 方法重载

列表 22 调用了 `DirectoryCountLines()`，它统计了 `*.cs` 文件。然而，如果你想统计 `*.h`/`*.cpp` 或 `*.vb` 文件的代码，`DirectoryCountLines()` 将无法工作。相反，你需要一个接受文件扩展名的方法，但保留现有方法定义以处理 `*.cs` 文件。

类中的所有方法必须具有唯一的签名。C# 通过方法名、参数类型或参数数量的变化来定义唯一性。即使返回类型不同，定义两个返回类型相同的方法也会导致编译错误。当类具有两个或多个同名但参数数量或数据类型不同的方法时，就会发生方法重载。

> 注意：只要方法名、参数类型或参数数量存在差异，方法就被认为是唯一的。

方法重载是操作多态的一种类型。当相同的逻辑操作由于数据的不同而采取多种（poly）形式（morphs）时，就发生了多态现象。例如，调用 `WriteLine()` 并传递带有某些参数的字符串与调用 `WriteLine()` 指定整数的实现方式不同。对于调用者来说，方法负责写入数据，内部如何实现并不重要。列表 23 提供了一个示例，输出 5.9 显示了结果。

**列表 23：使用重载统计 *.cs 文件中的行数**

```csharp
public static class LineCounter
{
    public static void Main(string[] args)
    {
        int totalLineCount;
        if(args.Length > 1)
        {
            totalLineCount = DirectoryCountLines(args[0], args[1]);
        }
        else if (args.Length > 0)
        {
            totalLineCount = DirectoryCountLines(args[0]);
        }
        else
        {
            totalLineCount = DirectoryCountLines();
        }

        Console.WriteLine(totalLineCount);
    }

    static int DirectoryCountLines()
    {
        return DirectoryCountLines(Directory.GetCurrentDirectory());
    }

    static int DirectoryCountLines(string directory)
    {
        return DirectoryCountLines(directory, "*.cs");
    }

    static int DirectoryCountLines(string directory, string extension)
    {
        int lineCount = 0;
        foreach(string file in Directory.GetFiles(directory, extension))
        {
            lineCount += CountLines(file);
        }

        foreach(string subdirectory in Directory.GetDirectories(directory))
        {
            lineCount += DirectoryCountLines(subdirectory);
        }

        return lineCount;
    }

    private static int CountLines(string file)
    {
        int lineCount = 0;
        string? line;
        // 此处可以使用 using 语句进行改进，
        // 目前尚未描述。
        FileStream stream = new(file, FileMode.Open);
        StreamReader reader = new(stream);
        line = reader.ReadLine();
        while(line is not null)
        {
            if(line.Trim() != "")
            {
                lineCount++;
            }
            line = reader.ReadLine();
        }
        reader.Dispose(); // 自动关闭流
        return lineCount;
    }
}
```

**输出 5.9**

>LineCounter.exe \ *.cs

28

方法重载的作用是提供调用方法的可选方式。如 `Main()` 内部所示，你可以在传递或不传递搜索目录和文件扩展名的情况下调用 `DirectoryCountLines()` 方法。

注意 `DirectoryCountLines()` 的无参数实现调用了 `DirectoryCountLines(string directory)`。这是实现重载方法时的一种常用模式。其核心思想是开发者只在一个方法中实现核心逻辑，所有其他重载方法都调用该单一方法。如果核心实现发生变化，只需要在一处进行修改，而不是在每个实现中进行修改。这种模式在通过方法重载启用无法在编译时确定值的可选参数时尤为常见。

> **注意**

将核心功能放置在单一方法中，所有其他重载方法都调用该方法，这样你只需要在核心方法中进行更改，其他方法将自动从中获益。

# 可选参数

C# 语言设计人员还添加了对可选参数的支持。通过允许在方法声明中将参数与常量值关联，可以在调用方法时无需为该方法的每个参数都传递参数（见列表 5.24）。

列表 5.24：带有可选参数的方法

```csharp
public static class LineCounter
{
    public static void Main(string[] args)
    {
        if(args.Length > 1)
        {
            totalLineCount = DirectoryCountLines(args[0], args[1]);
        }
        else if(args.Length > 0)
        {
            totalLineCount = DirectoryCountLines(args[0]);
        }
        else
        {
            totalLineCount = DirectoryCountLines();
        }
        Console.WriteLine(totalLineCount);
    }
}
```

7. 在 C# 4.0 中引入。

```csharp
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
    foreach(string file in
        Directory.GetFiles(directory, extension))
    {
        lineCount += CountLines(file);
    }
    foreach(string subdirectory in
        Directory.GetDirectories(directory))
    {
        lineCount += DirectoryCountLines(subdirectory);
    }
    return lineCount;
}
```

在列表 5.24 中，带有单个参数的 `DirectoryCountLines()` 方法声明已被移除（注释掉了），但来自 `Main()` 的调用（指定了一个参数）仍然存在。当调用时未指定 `extension` 参数时，将使用声明中赋值给 `extension` 的值（在此情况下为 `*.cs`）。这允许调用代码根据需要不指定值，并消除了原本可能需要的额外重载。注意，可选参数必须出现在所有必需参数（那些没有默认值的参数）之后。此外，默认值必须是常量（编译时解析的值）这一事实相当具有限制性。例如，你不能声明如下方法：

```csharp
DirectoryCountLines(
string directory = Environment.CurrentDirectory,
string extension = "*.cs")
```

因为 `Environment.CurrentDirectory` 不是常量。相比之下，由于 `"*.cs"` 是常量，C# 允许其作为可选参数的默认值。

## 指南

- **应当** 尽可能为所有参数提供良好的默认值。
- **应当** 提供具有少量必需参数的简单方法重载。
- **考虑** 从简单到复杂的顺序来组织重载。

第二个方法可以采用命名参数的使用。通过使用命名参数，调用者可以显式地识别要为哪个参数名称赋值值，而不是仅仅依赖参数和参数的顺序来将它们关联起来（见列表 5.25）。

列表 5.25：通过名称指定参数

```csharp
public static void Main()
{
    DisplayGreeting(
firstName: "Inigo", lastName: "Montoya");
}
```

```csharp
public static void DisplayGreeting(
string firstName,
string? middleName = null,
string? lastName = null
)
```

8. 在 C# 4.0 中引入。

```csharp
{
  // ...
}
```

在列表 5.25 中，从 `Main()` 内部对 `DisplayGreeting()` 的调用通过名称为参数赋值。在两个可选参数（`middleName` 和 `lastName`）中，只有 `lastName` 被作为参数传递。对于方法拥有大量参数且许多参数是可选的情况，使用命名参数语法无疑是一种便利。然而，伴随便利而来的还有对方法接口灵活性的影响。在过去，更改参数名称不会导致调用该方法的 C# 代码无法编译。随着命名参数的加入，参数名称变成了接口的一部分，因为更改名称将导致使用命名参数的代码不再能够编译。

## 指南

> **应当将参数名称视为 API 的一部分，如果 API 之间的版本兼容性很重要，请避免更改名称。**

对于许多丰富的 C# 开发者来说，这是一个意料之外的限制。然而，自 .NET 1.0 以来，该限制作为通用语言规范（CLS）的一部分一直存在。此外，Visual Basic 一直支持使用命名参数调用方法。因此，库开发人员应该遵循不更改参数名称的习惯，以便在不同版本之间与其他 .NET 语言顺利协作。本质上，命名参数现在对更改参数名称施加了许多其他 .NET 语言已经要求的相同限制。

由于方法重载、可选参数和命名参数的结合，解析调用哪个方法变得不再那么直观。如果所有参数恰好有一个类型兼容的对应参数（通过名称或位置），则与该方法是适（可解析的），除非该参数是可选的（或是参数数组）。尽管这限制了可能调用的方法数量，但它并不能确定唯一的方法。为了进一步区分将调用哪个特定方法，编译器仅使用调用者中显式识别的参数，忽略调用者处未指定的所有可选参数。因此，如果两个方法都适用，且其中一个有一个可选参数，编译器将解析为没有可选参数的方法。

9. 访问 Microsoft Word 或 Microsoft Excel 等 Microsoft COM 库时的常见现象。

## 高级主题

# 方法解析

当编译器必须在多个适用的方法中选择一个最适合特定调用者的方法时，将选择参数类型最具体的那一个。假设有两个适用的方法，每个方法都需要从参数到参数类型隐式转换，将使用参数类型为更派生类型的方法。

例如，如果调用者传递一个 `int` 类型的参数，则选择接受 `double` 参数的方法而不是接受 `object` 参数的方法。这是因为 `double` 比 `object` 具体。存在不是 `double` 的对象，但不存在不是 `object` 的 `double`，所以 `double` 必须更具体。

如果有多个方法且无法确定唯一的最佳方法，编译器将发出错误，指示调用存在义。

例如，给定以下方法：

```csharp
static void Method(object thing){}
static void Method(double thing){}
static void Method(long thing){}
static void Method(int thing){}
```

形式为 `Method(42)` 的调用解析为 `Method(int thing)`，因为这是参数类型到参数类型的精确匹配。如果该方法被移除，重载解析将选择 `long` 版本，因为 `long` 比 `double` 或 `object` 都具体。

# 第 5 章：参数与方法

C# 规范包含了关于 `byte`、`ushort`、`uint`、`ulong` 以及其他数值类型之间隐式转换的额外规则。尽管如此，通常使用强制转换使预期的目标方法更易识别更好。

# 使用异常的基础错误处理

本节研究了如何通过称为异常处理的机制来处理错误报告。通过异常处理，方法可以向调用方法传递有关错误的信息，而无需显式地提供任何参数来实现此。带有输出 5.10 的列表 5.26 对列表 1.16 进行了微调——即来自第 1 章的 `HeyYou` 程序。它不再请求用户的姓，而是提示用户输入年龄。

列表 5.26：将字符串转换为 int

```csharp
public static void Main()
{
    string? firstName;
    string ageText;
    int age;

    Console.WriteLine("Enter your first name: ");
    firstName = Console.ReadLine();

    Console.WriteLine("Enter your age: ");
    // 假设不为空以清晰清晰
    ageText = Console.ReadLine()!;
    age = int.Parse(ageText);

    Console.WriteLine(
        "$Hi {firstName}! You are {age * 12} months old.");

}
```

# 输出 5.10

Hey you!
