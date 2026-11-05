
```csharp
{
    Console.WriteLine("Enter the path of the root directory:");
    var rootDirectorypath = Console.ReadLine();

    Console.WriteLine(
        $"Getting directory tree of '{rootDirectorypath}'");

    PrintDirectoryTree(rootDirectorypath);
    Console.WriteLine("Press 'Enter' to quit...");
    Console.ReadLine();
}

internal static void PrintDirectoryTree(string rootDirectoryPath)
{
    try
    {
        if (!Directory.Exists(rootDirectoryPath))
        {
            throw new DirectoryNotFoundException(
                $"Directory '{rootDirectoryPath}' not found.");
        }

        var rootDirectory = new DirectoryInfo(rootDirectoryPath);
        PrintDirectoryTree(rootDirectory, RootLevel);
    }
    catch (DirectoryNotFoundException e)
    {
        Console.WriteLine(e.Message);
    }
}

private static void PrintDirectoryTree(
    DirectoryInfo directory, int currentLevel)
{
    var indentation = string.Empty;
    for (var i = RootLevel; i < currentLevel; i++)
    {
        indentation += Tab;
    }

    Console.WriteLine($"{indentation}--{directory.Name}");
    var nextLevel = currentLevel + 1;
    try
    {
        foreach (var subDirectory in directory.GetDirectories())
        {
            PrintDirectoryTree(subDirectory, nextLevel);
        }
    }
    catch (UnauthorizedAccessException e)
    {
        Console.WriteLine($"{indentation}--{e.Message}");
    }
}
```

这段代码比完成此任务所需的最低限度代码稍复杂一些，因为它包含异常检查，以处理获取目录时可能出现的任何问题。下面你会看到将代码分解成更小片段并逐一解释的内容。

### Main：

主方法从用户处接收一个字符串输入，该字符串将用作根目录的路径。然后，它调用 PrintDirectoryTree 方法，并将此字符串作为参数。

### PrintDirectoryTree(string)：

这是处理实际目录树打印的两个方法中的第一个。此方法接收一个表示根目录路径的字符串作为参数。它会检查该路径是否为实际目录；如果不是，则抛出 DirectoryNotFoundException，随后在 catch 块中处理。如果路径是真实目录，则从该路径创建 DirectoryInfo 对象 rootDirectory，并使用 rootDirectory 对象和 RootLevel（一个值为零的整数常量）调用第二个 PrintDirectoryTree 方法。

### PrintDirectoryTree(DirectoryInfo, int)：

第二个方法承担了大部分工作。它接收 DirectoryInfo 和整数作为参数。DirectoryInfo 是当前目录，整数是当前目录相对于根目录的深度。为便于阅读，输出会根据当前目录的深度级别逐级缩进，因此输出看起来像这样：

```
-Root
  -Child 1
  -Child 2
    -Grandchild 2.1
  -Child 3
```

打印当前目录后，会检索其子目录，然后对每个子目录调用此方法，并将深度级别值设为比当前值大 1。这部分就是递归：方法调用自身。程序将以这种方式运行，直到访问完树中的每个目录。当到达一个没有子目录的目录时，方法会自动返回。

此方法还会捕获 UnauthorizedAccessException；如果当前目录的任何子目录受系统保护，就会抛出该异常。为保持一致，错误消息会按当前缩进级别打印。

下面的方法为此问题提供了一种更基本的方法：

```csharp
internal static void PrintDirectoryTree(string directoryName)
{
    try
    {
        if (!Directory.Exists(directoryName)) return;
        Console.WriteLine(directoryName);
        foreach (var d in Directory.GetDirectories(directoryName))
        {
            PrintDirectoryTree(d);
        }
    }
    catch (Exception e)
    {
        Console.WriteLine(e.Message);
    }
}
```

它不包含第一种方法中的特定错误检查或输出格式，但有效实现了相同的功能。由于它只使用字符串而不是 DirectoryInfo，因此无法访问其他目录属性（如权限）。

## 第 54.6 节：阶乘计算

数字的阶乘（用 ! 表示，例如 9!）是该数字与比它小 1 的数字的阶乘相乘。因此，例如，9! = 9 x 8! = 9 x 8 x 7! = 9 x 8 x 7 x 6 x 5 x 4 x 3 x 2 x 1。

因此在代码中，使用递归可写成：

```csharp
long Factorial(long x)
{
    if (x < 1)
    {
        throw new OutOfRangeException("Factorial can only be used with positive numbers.");
    }

    if (x == 1)
    {
        return 1;
    } else {
        return x * Factorial(x - 1);
    }
}
```

## 第 55 章：命名约定

本主题概述编写 C# 语言时使用的一些基本命名约定。与所有约定一样，它们不由编译器强制执行，但可确保开发者之间的可读性。

有关全面的 .NET 框架设计指南，请参阅 docs.microsoft.com/dotnet/standard/design-guidelines。

### 第 55.1 节：大小写约定

以下术语描述标识符大小写的不同方式。

### Pascal 命名法

标识符的第一个字母以及每个后续连接单词的第一个字母都大写。对于三个或更多字符的标识符，可以使用 Pascal 命名法。例如：BackColor

### Camel 命名法

标识符的第一个字母小写，每个后续连接单词的第一个字母大写。例如：backColor

### 全大写

标识符中的所有字母都大写。例如：IO

### 规则

当标识符由多个单词组成时，不要在单词之间使用分隔符，例如下划线（"_"）或连字符（"-"）。而应使用大小写形式来表示每个单词的开头。

下表总结了标识符的大小写规则，并提供了不同类型标识符的示例：

| 标识符 | 大小写 | 示例 |
|---|---|---|
| 局部变量 | Camel | carName |
| 类 | Pascal | AppDomain |
| 枚举类型 | Pascal | ErrorLevel |
| 枚举值 | Pascal | FatalError |
| 事件 | Pascal | ValueChanged |
| 异常类 | Pascal | WebException |
| 只读静态字段 | Pascal | RedValue |
| 接口 | Pascal | IDisposable |
| 方法 | Pascal | ToString |
| 命名空间 | Pascal | System.Drawing |
| 参数 | Camel | typeName |
| 属性 | Pascal | BackColor |

更多信息可在 MSDN 上找到。

### 第 55.2 节：枚举

### 大多数枚举使用单数名称

```csharp
public enum Volume
{
    Low,
    Medium,
    High
}
```

### 位字段枚举类型使用复数名称

```csharp
[Flags]
public enum MyColors
{
    Yellow = 1,
    Green = 2,
    Red = 4,
    Blue = 8
}
```

注意：始终为位字段枚举类型添加 FlagsAttribute。

### 不要添加 'enum' 作为后缀

```csharp
public enum VolumeEnum // Incorrect
```

### 不要在每一项中使用枚举名称

```csharp
public enum Color
{
    ColorBlue, // Remove Color, unnecessary
    ColorGreen,
}
```

### 第 55.3 节：接口

接口应使用名词或名词短语，或描述行为的形容词来命名。例如，IComponent 使用描述性名词，ICustomAttributeProvider 使用名词短语，IPersistable 使用形容词。

接口名称应以字母 I 为前缀，以表明该类型是接口，并且应使用 Pascal 命名法。

以下是命名正确的接口：

```csharp
public interface IServiceProvider
public interface IFormattable
```

### 第 55.4 节：异常

### 添加 'exception' 作为后缀

自定义异常名称应以“-Exception”作为后缀。

以下是命名正确的异常：

```csharp
public class MyCustomException : Exception
public class FooException : Exception
```

### 第 55.5 节：私有字段

私有字段有两种常见约定：camelCase 和 _camelCaseWithLeadingUnderscore。

### 驼峰式大小写

```csharp
public class Rational
{
    private readonly int numerator;
    private readonly int denominator;

    public Rational(int numerator, int denominator)
    {
        // "this" keyword is required to refer to the class-scope field
        this.numerator = numerator;
        this.denominator = denominator;
    }
}
```

### 带下划线的驼峰式大小写

```csharp
public class Rational
{
    private readonly int _numerator;
    private readonly int _denominator;

    public Rational(int numerator, int denominator)
    {
        // Names are unique, so "this" keyword is not required
        _numerator = numerator;
        _denominator = denominator;
    }
}
```

### 第 55.6 节：命名空间

命名空间的一般格式为：

```
<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>].
```

示例包括：

```
Fabrikam.Math
Litware.Security
```

在命名空间名称前加上公司名称，可以防止不同公司的命名空间具有相同名称。
