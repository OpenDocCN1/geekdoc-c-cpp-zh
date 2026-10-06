
这以处理复合字符串的方式为本地化留下了空间，并且不会通过字符串引入任何编译后的代码注入。

## 字符串方法

字符串类型类似于 `System.Console` 类型，包含了几个方法。例如，有用于格式化、拼接和比较字符串的方法。

表 2.5 中的 `Format()` 方法的行为与 `Console.Write()` 和 `Console.WriteLine()` 方法类似，不同之处在于不是在控制窗口中显示结果，而是 `string.Format()` 将值返回给调用者。不过，通过使用字符串插值，对 `Format()` 的需求显著减少（本地化支持除外）。但是，字符串插值编译为常量加上 `string.Concat()` 和 `string.Format()` 调用的 CIL 。

表 2.5 中的所有方法都是静态的。这意味着，要调用该方法，必须在方法名（例如 `string`）之前加上包含该方法的类型。然而，如本章后文所示，string 类中的某些方法是实例方法。实例方法不是在方法名前前加上类型，而是使用变量名（或其他对实例的引用）。表 2.6 显示了这些方法的几个及其用法示例。

## 表 2.5：string 静态方法

| 语句 | 示例 |
| --- | --- |
| static string string.Format(string format, ...) | `string text, firstName, lastName; // text = string.Format("Your full name is {0} {1}", firstName, lastName); // Display // "Your full name is <firstName><lastName>". System.Console.WriteLine(text);` |
| static string string.Concat(string str0, string str1) | `string text, firstName, lastName; // text = string.Concat(firstName, lastName); // Display "<firstName><lastName>", notice // that there is no space between names System.Console.WriteLine(text);` |
| static int string.Compare(string str0, string str1) | `string option; //... // 分写敏感的字符串比较 int result = string.Compare(option, "")); // Display: ` |

## 表 2.6：string 方法

| 语句 | 示例 |
| --- | --- |
| bool StartsWith(string value) | `string option; //... // 分写敏感的字符串比较 int result = string.Compare(option, "")); // Display: ` |
| bool EndsWith(string value) | `severity = "warning"; // 显示大写的严重程度` |
| string ToLower() | `severity.ToLower()` |
| string ToUpper() | `severity.ToUpper()` |
| string Trim() | `username = username.Trim()` |
| string Trim(...) | `text = text.Trim()` |
| string TrimEnd() | `text = text.TrimEnd()` |
| string TrimStart() | `text = text.TrimStart()` |
| string Replace(string old, string newValue) | `filename = filename.Replace("?", "");` |

## 高级主题

### using 指令和 static 指令

我们目前为止使用的静态方法调用总是涉及命名空间前缀后跟类型名称。例如，在调用 `System.Console.WriteLine` 时，尽管上下文中没有该名称的方法，但仍然需要在方法名前加上命名空间（System）。在情况下，你可能希望有一个快捷方式来避免显式写法。这样做，你可以利用 C# 6.0 的 `static` 指令，如列表 2.15 所示。

`static` 指令需要出现在文件顶部。每当我们使用 `System.Console` 类时，就不再需要使用 `System.Console` 前缀。相反，我们可以直接编写方法名。关于 `static` 指令的一个重要点是，它仅适用于静态方法和属性，而不适用于实例成员。

## 列表 2.15：using static

```csharp
// static 指令允许你省略命名空间

using static System.Console;

class HeyYou
{
    static void Main()
    {
        string firstName;
        string lastName;
    }
}
```

```csharp
WriteLine("Hey you!");
Write("Enter your first name: ");
firstName = ReadLine();
Write("Enter your last name: ");
lastName = ReadLine();
WriteLine($"Your full name is {firstName}{lastName}");
```

## 字符串格式化

无论我们使用 `string.Format()` 还是 C# 6 的字符串插值功能来构建复杂的格式字符串，都有一套丰富的复合格式模式可显示数字、日期、时间、范围等。例如，如果 `price` 是 `decimal` 类型，`string.Format("{0,20:C2}", price)` 和等效的插值 `"{price,20:C2}"` 都会使用默认货币格式规则将小数值转换为字符串，保留小数点后两位数字，并在 20 个字符宽的字符串中右对齐。空间不允许对所有可能的格式字符串进行详细讨论；请参阅关于复合格式的 MSDN 文档获取完整的列表。

# 第 2 章：数据类型

如果你想在插值字符串内部包含真正的左或右大括号，可以双写括号来表示字符串或格式化字符串。例如，插值字符串 `"${{{{{price:C2}}}"` 可能会产生字符串 "{ $1,234.56}"。

# 换行

在编写换行时，换行的确切字符取决于你执行的操作系统。在 Microsoft 操作系统，换行是回车符（`\r`）和换行符（`\n`）字符的组合，而 UNIX 系统则使用单个换行符。克服操作系统之间差异的一种方法是使用 `System.Console.WriteLine()` 输出空行。另一种方法（对于在多个操作系统上从同一代码库处理换行来说至关重要）是使用 `System.Environment.NewLine`。换句话说，`System.Console.WriteLine("Hello World")` 和 `System.Console.Write("System.Environment.NewLine")` 是等价的。然而，在 Windows 上，`System.Console.WriteLine()` 和 `System.Console.Write(System.Environment.NewLine)` 等同于 `System.Console.Write("\r\n")`——而不是 `System.Console.Write("\n")`。总之，请依赖 `System.WriteLine()` 和 `System.Environment.NewLine` 而不是 `\n`，以便让可以在 Linux 和 iOS 上运行的相同代码适应 Windows 特有的操作系统特性。

> 指南
> 请依赖 `System.WriteLine()` 和 `System.Environment.NewLine` 而不是 `\n`，以便让可以在 Linux 和 iOS 上运行的相同代码适应 Windows 特有的操作系统特性。

## 高级主题

## C# 属性

下节中提到的 `Length` 成员实际上并不是一个方法，这一点从其调用后没有括号可以判断出来。`Length` 是字符串的一个属性，C# 语法允许像访问成员变量一样访问属性（在 C# 中称为字段）。换句话说，属性具有称为设置器（setters）和取值器（getters）的特殊方法的行为，但访问该行为的语法是字段的语法。检查属性的底层 CIL 实现可以发现，它被编译为两个方法：`set_<PropertyName>` 和 `get_<PropertyName>`。然而，这两个方法都无法直接从 C# 代码访问，除非通过 C# 属性结构进行访问。有关属性的更多详细信息，请参见第 6 章。

## 字符串长度

要确定字符串的长度，使用名为 `Length` 的字符串成员。这个特定成员被称为只读属性。正如你可能知道的，它无法被设置，调用它也不任何参数。列表 2.16 展示了如何使用 `Length` 属性，输出 2.11 显示了结果。

# 2.16：使用字符串的 Length 成员

输出 2.11
输入一个回文：Never odd or even
回文 "Never odd or even" 有 17 个字符。

字符串的长度不能直接设置；它是根据字符串中的字符数计算的。此外，字符串的长度不能改变，因为字符串是不可变的。

# 字符串是不可变的

字符串类型的一个关键特性是它是不可变的。字符串变量可以分配一个全新的值，但没有修改字符串内容的机制。因此，无法将字符串转换为所有大写字母。创建一个由旧字符串的大写版本组成的新字符串是轻而易见的，但在过程中旧字符串并没有被修改。以列表 2.17 为例。

列表 2.17：错误；字符串是不可变的

```c
class Uppercase
{
    static void Main()
    {
        string text;
        System.Console.Write("Enter text: ");
        text = System.Console.ReadLine();
        // 意外之外：没有将文本转换为大写
        text.ToUpper();
        System.Console.WriteLine(text);
    }
}
```

输出 2.12 显示了列表 2.17 的结果。

输出 2.12
输入文本：This is a test of the broadcast system.
This is a test of the broadcast system.

乍看，`text.ToUpper()` 似乎应该将 text 中的字符转换为大写。然而，字符串是不可变的，因此 `text.ToUpper()` 不会任何修改。相反，`text.ToUpper()` 返回一个新的字符串，需要将其保存到变量或直接传递给 `System.Console.WriteLine()`。修正后的代码见列表 2.18，其输出见输出 2.13。

列表 2.18：处理字符串

```c
class Uppercase
{
    static void Main()
    {
        string text, uppercase;
        System.Console.Write("Enter text: ");
        text = System.Console.ReadLine();
        // 返回一个大写的新字符串
        uppercase = text.ToUpper();
        System.Console.WriteLine(uppercase);
    }
}
```

# 输出 2.13

输入：This is a test of the broadcast system.
THIS IS A TEST OF THE EMERGENCY BROADCAST SYSTEM.

如果忽略了字符串的不可变性，像列表 2.17 所示的错误也会出现在其他字符串方法中。
要实际更改 `text` 的值，可以将 `ToUpper()` 的值赋值回 `text`，如下所示：

```csharp
text = text.ToUpper();
```

## System.Text.StringBuilder

如果需要大量的字符串修改（例如在构建字符串时），请使用 `System.Text.StringBuilder`。`StringBuilder` 类允许你修改字符串而无需每次都创建一个新对象，这对于频繁修改要高效得多。

# 第 2 章：数据类型

## 语言对比：Visual Basic——返回 void 相当于定义一个子程序

在 C# 中返回 `void` 的 Visual Basic 等效方法是定义一个子程序（Sub/End Sub），而不是一个返回值的函数。

## 数据类型之间的转换

鉴于 .NET 框架中预定义的数千种类型，以及代码可以定义的无限数量的类型，因此让类型在合理的情况下支持从一种类型到另一种类型的转换是非常关重要的。导致转换的最常见操作是强制类型转换（casting）。

考虑两种数值类型之间的转换：将 `long` 类型的变量转换为 `int` 类型的变量。`long` 类型可以包含大达 `9,223,372,036,854,775,808` 的值；然而，`int` 的最大大小为 `2,147,483,647`。因此，该转换可能会导致数据丢失——例如，如果 `long` 类型变量包含的值大于 `int` 的最大值。任何可能导致数据丢失（如数量级和/或精度）或因转换失败而导致异常的转换都需要显式强制转换（explicit cast）。相反，一种不会丢失数量级且无论操作数类型如何都不会抛出异常的转换操作是——

## 显式强制转换

在 C# 中，使用强制转换运算符。通过在括号内指定你想要转换变量的类型，你承认了如果发生显式强制转换，可能会导致精度和数据的丢失，或者可能会产生异常。列表 2.20 中的代码将 `long` 转换为 `int`，并显式地告诉系统尝试该操作。

### 列表 2.20：显式强制转换示例

```cs
long longNumber = 50918309109;
int intNumber = (int) longNumber;
```

使用强制转换运算符，程序员本质上是在对编译器说：“相信我，我知道我在做什么。我知道该值可以放入目标类型中。” 做出这种选择将导致编译器允许转换。然而，通过显式转换，如果数据没有被成功转换，在执行期间仍可能以异常的形式发生错误。因此，确保数据成功转换，或在转换失败时提供必要的错误处理代码，是程序员的责任。

## 高级主题

## 检查（Checked）与未检查（Unchecked）转换

C# 提供了特殊的关键字来标记代码块，以指示如果目标数据类型小到无法包含分配的数据会发生什么。默认情况下，如果目标数据类型无法包含分配的数据，数据将在赋值期间被截断。例如列表 2.21所示。

### 列表 2.21：整数值溢出

```cs
class Program
{
    static void Main()
    {
        // int.MaxValue 等于 2147483647
        int n = int.MaxValue;
        n = n + 1;
        System.Console.WriteLine(n);
    }
}
```

输出 2.14

```
-2147483648
```

列表 2.21 将值 -2147483648 写入控制。然而，将代码放在 `checked` 块中，或在运行编译器时使用 `checked` 选项，会导致运行时抛出 `System.OverflowException` 异常。`checked` 块的语法使用 `checked` 关键字，如列表 2.22 所示。

### 列表 2.22：Checked 块示例

```cs
class Program
{
    static void Main()
    {
        checked
        {
            // int.MaxValue 等于 2147483647
            int n = int.MaxValue;
            n = n + 1;
            System.Console.WriteLine(n);
        }
    }
}
```

此外，所有类型都支持 `ToString()` 方法，该方法可提供类型的字符串表示。列表 2.28 展示了如何使用此方法。结果如输出 2.17 所示。

# 列表 2.28：使用 ToString() 转换为字符串

```c
bool boolean = true;
string text = boolean.ToString();
// Display "True"
System.Console.WriteLine(text);
```
