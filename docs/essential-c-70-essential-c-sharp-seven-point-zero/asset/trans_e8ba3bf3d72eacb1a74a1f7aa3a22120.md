

在方法实现中，你遍历 paths 数组的元素并调用 `System.IO.Path.Combine()`。该方法会自动组合路径的各部分，并使用特定于平台的目录分隔符。请注意，`PathEx.Combine()` 与 `Path.Combine()` 的唯一区别在于，`PathEx.Combine()` 可以处理可变数量的参数，而不仅仅是两个。

参数数组具有几个显著特性：

- 参数数组不一定是方法中唯一的参数。
- 参数数组必须是方法声明中的最后一个参数。由于只有最后一个参数可以是参数数组，因此一个方法不能拥有多个参数数组。
- 调用者可以指定与参数数组参数对应的零个参数，这将导致传递一个包含零个项的数组作为参数数组。
- 参数数组是类型安全的：所提供的参数必须与参数数组的元素类型兼容。
- 调用者可以使用显式数组，而不是逗号分隔的参数列表。生成的 CIL 代码是相同的。
- 如果目标方法实现要求最小参数数量，这些参数应显式地出现在方法声明中，这样当缺少必需参数时会引发编译错误，而不是依赖运行时错误处理。例如，如果你有一个方法需要至少一个整数参数，应将其声明为 `int Max(int first, params int[] operands)` 而不是 `int Max(params int[] operands)`，以确保至少传递一个值给 `Max()`。

使用参数数组，你可以将可变数量的同类型参数传递给方法。本章稍后出现的“方法重载”部分讨论了支持可变数量参数的方法，这些参数不一定具有相同的类型。

## 指南

**必须**在方法可以处理任意数量（包括零个）附加参数时使用参数数组。

### 递归

以**递归**方式调用方法或采用递归方式实现方法，指的是使用自身调用的方法。递归有时是实现特定算法最简单的方式。列表 5.18 统计了目录及其子目录中所有 C# 源文件（*.cs）的行数。

```
Listing 5.18: 统计指定目录中 *.cs 文件的行数

using System.IO;

public static class LineCounter
{
    // 使用第一个参数作为要搜索的目录，
    // 或者默认为当前目录
    public static void Main(string[] args)
    {
        int totalLineCount = 0;
        string directory;
        if (args.Length > 0)
        {
            directory = args[0];
        }
        else
        {
            directory = Directory.GetCurrentDirectory();
        }
        totalLineCount = DirectoryCountLines(directory);
        System.Console.WriteLine(totalLineCount);
    }

    static int DirectoryCountLines(string directory)
    {
        int lineCount = 0;
        foreach (string file in
                 Directory.GetFiles(directory, "*.cs"))
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
        string line;
        int lineCount = 0;
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

        reader.Close();  // 自动关闭流
        return lineCount;
    }
}
```

输出 5.9 展示了列表 5.18 的结果。

### 输出 5.9

104

程序首先将第一个命令行参数传递给 DirectoryCountLines()，如果没有提供参数，则使用当前目录。该方法首先遍历当前目录中的所有文件，并统计每个文件的源代码行数。在处理完目录中的每个文件后，代码通过将子目录传回 DirectoryCountLines() 方法，对每个子目录进行处理，并使用该子目录重新运行该方法。相同的递归过程在每个子目录中重复，直到没有剩余的目录需要处理为止。

对递归不熟悉的读者起初可能会感到困惑。尽管如此，它通常是最简单的编码模式，特别是对于像文件系统这样的分层类型数据。然而，尽管这可能是最易读的编程方式，但它通常不是最快的实现方式。如果性能成为问题，开发者应寻求替代递归实现的方案。选择通常取决于在可读性与性能之间取得平衡。

1. 如果代码使用 using 语句，可能会得到改进，这是一种我们之前避免使用的结构，因为尚未引入该概念。

### 初学者主题

### 无限递归错误

递归方法实现中常见的编程错误表现为程序执行期间的栈溢出。这通常是由于**无限递归**造成的，即方法持续地回调自身，始终无法达到触发递归终止的条件。良好的做法是程序员审阅任何使用递归的方法，并验证递归调用是有限的。

使用伪代码的递归常见模式如下：

```
M(x)
{
    如果 x 是平凡情况
        返回结果
    否则
        a. 进行一些操作以减小问题规模
        b. 递归调用 M 以解决较小的问题
        c. 根据 a. 和 b. 计算结果
        返回结果
}
```

当未遵循此模式时，问题就会发生。例如，如果你没有减小问题规模，或者没有处理所有可能的“最小”情况，递归将永远不会终止。

### 方法重载

列表 5.18 调用了 *DirectoryCountLines()*，用于统计 `*.cs` 文件的行数。然而，如果你想统计 `*.h`/`.cpp` 文件 or `*.vb` 文件中的代码行数，*DirectoryCountLines()* 将不起作用。相反，你需要一个可以接受文件扩展名的方法，同时保留现有的方法定义，使其默认处理 `*.cs` 文件。

类中的所有方法必须具有唯一的签名，C# 通过方法名、参数数据类型或参数数量上的变化来定义唯一性。这不包括方法返回数据类型；定义两个仅返回数据类型不同的方法会导致编译错误。即使返回类型是两个不同的元组，这也是成立的。**方法重载**发生在类中存在两个或更多同名方法，并且这些重载方法之间参数数量和数据类型有变化时。

![](img/ef6a8a417630b222bfb3f3b949facff0_254_0.png)

方法重载是**操作多态性**的一种形式。当相同逻辑操作因数据差异而呈现多种（“poly”）形式（“morphs”）时，就会发生多态性。调用 WriteLine() 并传递格式字符串及一些参数，与调用 WriteLine() 并指定整数的实现方式不同。然而，逻辑上，对于调用者而言，该方法负责写入数据，内部实现方式相对无关紧要。列表 5.19 提供了一个示例，输出 5.10 显示了结果。

### 列表 5.19: 使用重载统计 .cs 文件中的行数

```
using System.IO;

public static class LineCounter
{
public static void Main(string[] args)
{
int totalLinesCount;
if (args.Length > 1)
{
totalLinesCount =
DirectoryCountLines(args[0], args[1]);
}
if (args.Length > 0)
{
totalLinesCount = DirectoryCountLines(args[0]);
}
else
{
totalLinesCount = DirectoryCountLines();
}
System.Console.WriteLine(totalLinesCount);
}
}
```

