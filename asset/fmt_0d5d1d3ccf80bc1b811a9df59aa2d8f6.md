
```
class Program
{
    static void Main()
    {
        // ...
        string fullName;
        string driveLetter = "C:";
        string folderPath  = "Data";
        string fileName    = "index.html";

        fullName = Combine(driveLetter, folderPath, fileName);

        Console.WriteLine(fullName);
        // ...
    }

    static string Combine(
        string driveLetter, string folderPath, string fileName)
    {
        string path;
        path = string.Format("{1}{0}{2}{0}{3}",
            System.IO.Path.DirectorySeparatorChar,
            driveLetter, folderPath, fileName);
        return path;
    }
}
```

## OUTPUT 4.5

```
C:\Data\index.html
```

即使 `Combine()` 方法在返回前将 `driveLetter`、`folderPath` 和 `fileName` 分配为 `null`，`Main()` 中的相应变量仍将保持其原始值，因为在调用方法时变量会被复制。当调用栈在调用结束时展开时，被复制的数据会被丢弃。

## BEGINNER TOPIC

### Matching Caller Variables with Parameter Names

在清单 4.12 中，调用者的变量名与被调用方法的参数名完全匹配。这种匹配仅为可读性目的而提供；名称是否匹配与方法调用的行为完全无关。被调用方法的参数和调用方法的局部变量位于不同的声明空间中，彼此无关。

## ADVANCED TOPIC

### Reference Types versus Value Types

就本节目的而言，传递的参数是值类型还是引用类型并不重要。更重要的是，被调用方法是否可以向调用者的原始变量写入值。由于调用者变量的值会被复制，因此调用者的变量无法被重新赋值。尽管如此，了解包含值类型的变量与包含引用类型的变量之间的区别仍然很有帮助。

引用类型变量的值，如其名称所示，是对与对象关联的数据存储位置的引用。运行时选择如何表示引用类型变量的值是运行时的实现细节；通常它表示为对象数据存储的内存位置的地址，但不一定如此。

如果引用类型变量按值传递，则引用本身会从调用者复制到方法参数。因此，目标方法无法更新调用者变量的值，但它可以更新引用所指向的数据。

相反，如果方法参数是值类型，则值本身会被复制到参数中，并且在被调用方法中更改参数不会影响原始调用者的变量。

## Reference Parameters (ref)

请考虑清单 4.13，其中调用了一个函数来交换两个值，以及显示结果的输出 4.6。

### LISTING 4.13: Passing Variables by Reference

```
class Program
{
    static void Main()
    {
        // ...
        string first = "hello";
        string second = "goodbye";
        Swap(ref first, ref second);

        Console.WriteLine(
            $@"first = "{ first }", second = "{ second }"" );
        // ...
    }

    static void Swap(ref string x, ref string y)
    {
        string temp = x;
        x = y;
        y = temp;
    }
}
```

## OUTPUT 4.6

```
first = "goodbye", second = "hello"
```

分配给 `first` 和 `second` 的值已成功交换。为此，变量是**按引用传递**的。调用 `Swap()` 与清单 4.12 中调用 `Combine()` 的明显区别在于参数数据类型前包含关键字 `ref`。该关键字更改调用方式，使得用作参数的变量按引用传递，因此被调用方法可以更新原始调用者的变量的新值。

当被调用方法将参数指定为 `ref` 时，调用者必须提供一个变量而不是一个值作为参数，并且要在传递的变量前加上 `ref`。这样做时，调用者明确承认目标方法可能会重新分配与接收到的任何 `ref` 参数关联的变量的值。此外，必须初始化作为 `ref` 传递的任何局部变量，因为目标方法可能在不先为其赋值的情况下从 `ref` 参数读取数据。例如，在清单 4.13 中，`temp` 被赋值为 `first` 的值，假设调用者在 `first` 中传递的变量已被初始化。有效地，ref 参数是传递变量的别名。换句话说，它本质上是为现有变量提供一个参数名，而不是创建一个新变量并将参数的值复制到其中。

## Output Parameters (out)

如前所述，使用作 `ref` 参数的变量必须在传递给被调用方法之前被赋值，因为被调用方法可能会从该变量读取。前面给出的“交换”示例必须从传递给它的两个变量中读取和写入。然而，通常情况下，一个接受变量引用的方法打算向该变量写入，但不从中读取。在这种情况下，显然可以安全地按引用传递未初始化的局部变量。

为此，代码需要在参数类型上加上关键字 `out`。这在清单 4.14 中的 `TryGetPhoneButton()` 方法中得到了演示，该方法返回与字符对应的电话按钮。

```csharp
class ConvertToPhoneNumber
{
    static int Main(string[] args)
    {
        char button;
        if(args.Length == 0)
```
```
{
    Console.WriteLine(
        "ConvertToPhoneNumber.exe <phrase>");
    Console.WriteLine(
        "'_' indicates no standard phone button");
    return 1;
}
foreach(string word in args)
{
    foreach(char character in word)
    {
        if(TryGetPhoneButton(character, out button))
        {
            Console.Write(button);
        }
        else
        {
            Console.Write('_');
        }
    }
    Console.WriteLine();
    return 0;
}

static bool TryGetPhoneButton(char character, out char button)
{
    bool success = true;
    switch( char.ToLower(character) )
    {
        case '1':
            button = '1';
            break;
        case '2': case 'a': case 'b': case 'c':
            button = '2';
            break;

        // ...

        case '-':
            button = '-';
            break;
        default:
            // Set the button to indicate an invalid value
            button = '_';
            success = false;
            break;
    }
    return success;
}
```

## OUTPUT 4.7

```
>ConvertToPhoneNumber.exe CSharpIsGood
274277474663
```

在此示例中，`TryGetPhoneButton()` 方法在成功确定字符对应的电话按钮时返回 `true`。函数还通过使用带有 `out` 装饰的 `button` 参数返回对应的按钮。

`out` 参数在功能上与 `ref` 参数完全相同；唯一的区别是语言对别名变量的读取和写入如何强制执行的要求。每当参数标记为 `out` 时，编译器都会检查方法中所有正常返回的代码路径是否都为参数赋值（即不抛出异常的代码路径）。例如，如果代码在某些代码路径中未为 `button` 赋值，编译器将发出错误，指出代码未初始化 `button`。清单 4.14 将 `button` 分配为下划线字符，因为即使它无法确定正确的电话按钮，仍有必要为其赋值。

方法开发者可以声明一个或多个 `out` 参数，以规避方法只能有一个返回类型的限制；一个需要返回两个值的方法可以通过正常返回一个值作为方法的返回值，并通过将第二个值写入作为 `out` 参数传递的别名变量来返回第二个值。尽管这种模式很常见且合法，但通常有更好的方法来实现该目标。例如，如果你考虑从方法返回两个或更多值，你可能最好编写两个方法，每个值一个。如果方法必须返回两个值，使用元组类型（表示多个值）或可空值类型（表示可能“无效”的值，如前面的示例）可以消除按引用传递变量的需要。

> NOTE
> 每个且每个正常的代码路径都必须导致所有 `out` 参数的赋值。

# 参数数组 (params)

在迄今为止的示例中，必须传递的参数数量由目标方法声明中声明的参数数量决定。然而，有时如果参数数量可以变化会更方便。考虑来自列表 4.12 的 `Combine()` 方法。在该方法中，你传递了驱动器号、文件夹路径和文件名。如果路径包含多个文件夹，并且调用者希望方法将额外的文件夹连接起来形成完整路径怎么办？也许最好的选择是为文件夹传递一个字符串数组。然而，这会使调用代码稍微复杂一些，因为需要构造一个数组作为参数传递。

为了让此类方法的调用者更轻松，C# 提供了一个关键字，使参数数量在调用代码中可以变化，而不是由目标方法设定。在讨论方法声明之前，先观察在 `Main()` 中声明的调用代码，如列表 4.15 所示。

### LISTING 4.15: Passing a Variable Parameter List

```
using System;
using System.IO;
class PathEx
{
    static void Main()
    {
        string fullName;

        // ...

        // Call Combine() with four arguments
        fullName = Combine(
            Directory.GetCurrentDirectory(),
            "bin", "config", "index.html");
        Console.WriteLine(fullName);

        // ...

        // Call Combine() with only three arguments
        fullName = Combine(
            Environment.SystemDirectory,
            "Temp", "index.html");
        Console.WriteLine(fullName);

        // ...

        // Call Combine() with an array
        fullName = Combine(
new string[] {
    "C:\\", "Data",
    "HomeDir", "index.html" });
Console.WriteLine(fullName);
// ...
}
```

```
static string Combine(params string[] paths)
{
    string result = string.Empty;
    foreach (string path in paths)
    {
        result = System.IO.Path.Combine(result, path);
    }
    return result;
}
}
```

## OUTPUT 4.8

```
C:\Data\mark\bin\config\index.html
C:\WINDOWS\system32\Temp\index.html
C:\Data\HomeDir\index.html
```

在第一次调用 `Combine()` 时，指定了四个参数。第二次调用只包含三个参数。在最后一次调用中，使用一个数组传递了单个参数。换句话说，`Combine()` 方法接受可变数量的参数——以逗号分隔的任意数量的字符串参数呈现，或作为单个字符串数组。前一种语法称为方法调用的“展开”形式，第二种形式称为“常规”形式。

为了允许这一点，`Combine()` 方法执行以下操作：

+   1. 在方法声明中将 `params` 放在最后一个参数之前
+   2. 将最后一个参数声明为数组

使用 **参数数组** 声明，可以将每个对应参数作为 `params` 数组的成员访问。在 `Combine()` 方法实现中，你遍历 `paths` 数组的元素并调用 `System.IO.Path.Combine()`。此方法自动组合路径的各部分，适当使用特定于平台的目录分隔符。请注意 `PathEx.Combine()` 与 `Path.Combine()` 相同，只是 `PathEx.Combine()` 处理可变数量的参数，而不是仅仅两个。

参数数组有几个值得注意的特征：

+   - 参数数组不一定是方法上的唯一参数。参数数组必须是方法声明中的最后一个参数。由于只有最后一个参数可以是参数数组，因此方法不能有多个参数数组。
+   - 调用者可以指定与参数数组参数对应的零个参数，这将导致传递一个零项的数组作为参数数组。
+   - 参数数组是类型安全的。给定的参数必须与参数数组的元素类型兼容。
+   - 调用者可以使用显式数组而不是逗号分隔的参数列表。生成的 IL 代码是相同的。
+     - 如果目标方法实现需要最少数量的参数，则这些参数应显式出现在方法声明中，从而强制编译错误，而不是依赖于运行时错误处理，如果缺少必需参数。例如，如果你有一个需要一个或多个整数参数的方法，请声明方法 `int Max(int first, params int[] operands)` 而不是 `int Max(params int[] operands)`，以便至少有一个值传递给 `Max()`。

使用参数数组，你可以将相同类型的可变数量参数传递给方法。本章后面出现的“方法重载”部分讨论了一种支持可变数量参数的方法，这些参数不一定是相同类型。

## Guidelines

DO use parameter arrays when a method can handle any number—including zero—of additional arguments.

# Recursion

调用方法 **recursively** 或使用 **recursion** 实现方法是指使用调用自身的 方法。递归有时是实现特定算法的最简单方法。列表 4.16 计算目录及其子目录中所有 C# 源文件 (*.cs) 的行数。

### Listing 4.16: Counting the Lines within *.cs Files, Given a Directory

```csharp
using System.IO;

public static class LineCounter
{
    // Use the first argument as the directory
    // to search, or default to the current directory.
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
