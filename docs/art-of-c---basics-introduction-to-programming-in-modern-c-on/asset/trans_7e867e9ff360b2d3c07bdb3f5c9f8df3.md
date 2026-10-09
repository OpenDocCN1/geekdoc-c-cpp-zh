
或者，

```csharp
private static char ConvertIntToChar(int n) {
    if (n < 10) {
        return (char)(n + '0');
    } else {
        return (char)(n - 10 + 'a');
    }
}
```

> 简洁性与冗长性之间往往存在权衡。请选择你感觉最舒适的风格。

为了计算 32 进制数，我们使用了“递归”。在这个特定的实现中，方法 *DivideAndAggregate()* 调用了自身。

递归函数需要一个基本情况（base case）。在本例中，如果给定的数字小于 32，我们就简单地返回对应的“数字”作为字符串。

```csharp
if (n < BASE) {
    return ConvertIntToChar(n).ToString();
}
```

*ToString()* 是 C# 中基类 *object* 中声明的“虚方法”，或者是 .NET 中对应的基类 *System.Object*。在这种情况下，它只是将 ConvertIntToChar() 返回的 char 转换为单字符字符串。

递归依赖于以下观察：

![](img/25af69ec45b3c0b589a8dccd0c2a88be_150_0.png)

数字 1234（十进制）等同于 (123 * 10) + 4。同样，123 等同于 (12 * 10) + 3。12 又等同于 (1 * 10) + 2。最后，1 等同于 (0) + 1。

因此，如果我们知道 1 在十进制中的值，就可以轻松地计算 12 的十进制值。如果我们知道 12 在十进制中的值，就可以利用公式 (12 * 10) + 3 计算出 123 的十进制值。以此类推。

基于相同的推理，32 进制中的数字 xyzw 等同于 (xyz * 32) + w，而 xyz 等同于 (xy * 32) + z，等等。

DivideAndAggregate() 静态方法使用这种逻辑来计算给定数字在 32 进制下的字符串表示。

如果我们重写该方法如下，则更容易理解。我们可以轻松地将 xyzw、xyz 和 w 与方法定义中对应的部分匹配起来。

```csharp
private static string DivideAndAggregate(int n) {
// ...
return DivideAndAggregate(n / 32) + ConvertIntToChar(n % 32).ToString();
}
```

内部 API ToBase32() 除了处理负数的负号外，只是调用了私有的 DivideAndAggregate() 方法。

如果这种方式能提高你的可读性，该方法也可以用更冗长的方式编写。

```csharp
internal static string ToBase32(int num) {
    var flipped = false;

    if (num < 0) {
        num *= -1;
        flipped = true;
    }

    var base32Str = DivideAndAggregate(num);

    if (flipped) {
        base32Str = "-" + base32Str;
    }

    return base32Str;
}
```

## 总结

我们查看了将字符串转换为数字的几种不同方法。特别是，为所有数字类型（整数或浮点数）以及 Boolean 类型定义的 `Parse()` 和 `TryParse()` 静态方法，可用于类型转换。

在本课中，我们还简要查看了 C# 中的异常处理。

## 8.3. 练习

- 1. 编写一个静态方法，将给定的（十进制）整数转换为二进制数。编写一个程序，将作为命令行参数给定的十进制整数转换为二进制数表示，并打印结果。

## 第 9 课。出生日期

### 9.1. *议程 - 枚举类型，while 和 do while 循环，switch 语句，char 类型*

处理日期和时间是编程中最常见的任务之一。我们将查看 .NET `DateTime` 类（来自 `System` 命名空间）中的一些简单 API。

我们还将复习 C# 中的字符和字符串类型。

![](img/25af69ec45b3c0b589a8dccd0c2a88be_152_0.png)

### 9.2. 代码阅读 - 日期和时间

你出生至今*有多少天？多少小时和分钟？* ☺ 你出生那天是星期几？

下面的程序为你做了简单的数学计算来回答这些问题。该程序的主要逻辑全部在主要的 "Program.cs" 文件中：

birth-date/Program.cs

```csharp
using Example;

// ... (OCR noise omitted, assuming standard context)

var smiley = char.ConvertFromUtf32(0x1F642);

while (true) {
    Console.WriteLine("What is your birth date? (mm/dd/yyyy)");
    var input = Console.ReadLine();

    if (DateTime.TryParse(input, out DateTime date)) {
        var weekday = BirthDate.Weekday(date);
        Console.WriteLine($"You are a {weekday} child.");

        var days = BirthDate.AgeInDays(date);
        Console.WriteLine($"You are {days} days old as of today.");

        var (hours, mins) = BirthDate.AgeInHours(date);
        Console.WriteLine($"😀You are {hours} hours and {mins} minutes old as of right now. {smiley}");

        break;
    } else {
        Console.WriteLine("Invalid date. Try again? Yes (Y) or No (N)");

        var ans = Console.ReadLine() ?? "";
        var firstLetter = (ans.Length > 0) ? ans.Substring(0, 1).ToUpper() : "";
        switch (firstLetter) {
            case "Y":
                continue;
            case "N":
            default:
                Console.WriteLine($"Your loss! {smiley}");
                return;
        }
    }
}
```

**BirthDate** 静态类*内部*导出了一些围绕某些 System.DateTime API 的简单包装方法。（注："Internal" 指程序集内部。）

*birth-date/BirthDate.cs*

```csharp
namespace Example;

static class BirthDate {
    internal static string Weekday(DateTime date) =>
        Enum.GetName(date.DayOfWeek) ?? "";
    internal static int AgeInDays(DateTime date) => (DateTime.Now -
        date).Days;
    internal static (int, int) AgeInHours(DateTime date) {
        var age = DateTime.Now - date;
        return ((int)age.TotalHours, age.Minutes);
    }
}
```

### 9.2.1. 解释

如果我们使用 dotnet CLI 工具运行该程序，它首先会询问日期。如果提供了日期，则程序会在控制台打印出一些（趣味）信息。

## 9.3. 语法

```
$ dotnet run

What is your birth date? (mm/dd/yyyy)   (1)
1/1/2000
You are a Saturday child.
You are 7846 days old as of today.
You are 188312 hours and 50 minutes old as of right now.
```

- (1) 用户输入。

这是另一个示例运行：

```
$ dotnet run

What is your birth date? (mm/dd/yyyy)   (1)
january 50th 30000
Invalid date. Try again? Yes (Y) or No (N)   (2)
Yes
What is your birth date? (mm/dd/yyyy)   (3)
jan 1 2020
You are a Wednesday child.
You are 541 days old as of today.
You are 12993 hours and 35 minutes old as of right now.
```

- (1) 无效的用户输入。
- (2) 用户输入 "yes" 并按下回车键。
- (3) 一个新的有效日期输入。

C# 和 .NET 使用 Unicode 字符来表示 char 和 string。Unicode 使用 2 或 4 个字节来表示（已知）宇宙中所有（已知）语言中的所有字符。☺

我们使用某些编码方案在计算机上表示 Unicode 字符（例如，用于存储和传输）。Unicode 最流行的两种编码方法是 UTF-8 和 UTF-16。英语字母和大多数拉丁字母只需要 1 个字节。而且，在传输或存储 Unicode 字符数据时，UTF-8 是最流行且相当高效的编码方法。

不深入细节，C# 内部使用一个或两个 `char` 类型（2 字节）的值，使用 UTF-16 来存储单个 Unicode 字符。在许多情况下，C# 中的单个 `char` 对应于单个 Unicode 字符（例如，来自“基本多文种平面”（BMP））。然而，在某些情况下，单个 `char` 不足以表示某些 Unicode 字符（例如，需要来自“代理平面”额外的 2 个字节字符）。

在这个示例代码中，我们使用函数 `char.ConvertFromUtf32()` 来获取某个笑脸字符 (😀)。来自 .NET 中 `System.Char` 的这个静态方法返回的是一个 `string`，而不是 `char`，因为有些 Unicode 字符无法由单个 `char` 表示。

通常，任何来自 BMP 的 Unicode 字符（只需要 2 个字节）都可以通过在 C# 中使用 "\u" 字符转义语法来表示。

例如，`\u0041` 表示字符 `'A'`。（十六进制数 `0x41` 在十进制中是 65。注意，在这种表示法中，无论字符的整数值如何，我们都使用*四个*十六进制数字来表示两个字节。）

对于其他任何字符，我们将需要依赖 .NET 提供的一些 API 方法。请注意，`string? ConvertFromUtf32(int)` 方法接受的是 `int` 参数，而不是 `char`。

在这个特定示例中，整数 `0x1F642` 不适合 `char` 类型。显式转换为 `char` 将导致编译时错误。

