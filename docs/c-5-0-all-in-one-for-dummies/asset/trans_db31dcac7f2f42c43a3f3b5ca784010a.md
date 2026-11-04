

![](img/80ff26f06fc9ab951e1cd4257b867366_92_0.png)

这些格式说明符可能看起来有点令人困惑。（我甚至还没有提到详细的货币和日期控制项。）请在“帮助索引”中浏览“格式说明符”主题以了解更多信息。为帮助你梳理这些选项，下面的 OutputFormatControls 程序让你能够输入一个浮点数，随后输入一个说明符序列。然后，程序使用指定的 Format() 控制显示该数字：

```csharp
// OutputFormatControls -- Allow the user to reformat input numbers
// using a variety of format specifiers input at run time.
namespace OutputFormatControls
{
    using System;
    public class Program
    {
        public static void Main(string[] args)
        {
            // Keep looping -- inputting numbers until the user
            // enters a blank line rather than a number.
            for(;;)
            {
                // First input a number -- terminate when the user
                // inputs nothing but a blank line.
                Console.WriteLine("Enter a double number:");
                string numberInput = Console.ReadLine();
                if (numberInput.Length == 0)
                {
                    break;
                }
                double number = Double.Parse(numberInput);
                // Now input the specifier codes; split them
                // using spaces as dividers.
                Console.WriteLine("Enter the format specifiers"
                    + " separated by a blank "
                    + "(Example: C E FI NO 000000.00000)");
                char[] separator = { ' ' };
                string formatString = Console.ReadLine();
                string[] formats = formatString.Split(separator);
                // Loop through the list of format specifiers.
                foreach(string s in formats)
                {
                    if (s.Length != 0)
                    {
                        // Create a complete format specifier
                        // from the letters entered earlier.
                        string formatCommand = "{0:" + s + "}";
                        // Output the number entered using the
                        // reconstructed format specifier.
                        Console.Write(
                            "The format specifier {0} results in ", formatCommand);
                        try
                        {
                            Console.WriteLine(formatCommand, number);
                        }
                        catch(Exception)
                        {
                            Console.WriteLine("<illegal controls>");
                        }
                        Console.WriteLine();
                    }
                }
            }
        }
    }
}
```

类似地，当应用于 `0.12345` 时，控制项 `00.0%` 会输出 `12.3%`。百分号会将数字乘以 100 并添加 `%`。`00.0` 表示输出应包含小数点左边至少两位数字，小数点后仅一位数字。使用相同的 `00.0%` 说明符时，数字 `0.01` 显示为 `01.0%`。

神秘的 `try . . . catch` 会捕获你输入非法格式命令（例如 `D`，代表十进制）时抛出的任何错误。（我在本小册第9章介绍异常。）

![](img/80ff26f06fc9ab951e1cd4257b867366_94_0.png)

### StringBuilder：更高效地操作字符串

用许多较短的字符串构建较长的字符串可能会让你付出高昂代价。因为字符串一旦创建就不能更改——正如我在本章开头所说，它是不可变的。这个示例并没有把 "ly" 附加到 `s1` 上：

```csharp
string s1 = "rapid";
string s2 = s1 + "ly";          // s2 = rapidly.
```

它会创建一个由组合而成的新字符串。（`s1` 保持不变。）类似地，其他看似修改字符串的操作（如 `Substring()` 和 `Replace()`）也会这样做。

结果是，对字符串的每次操作都会产生另一个字符串。假设你需要将 1000 个字符串连接成一个巨大的字符串。每次连接都会创建一个新字符串：

```csharp
string[] listOfNames = ...  // 1000 pet names
string s = string.Empty;
for(int i = 0; i < 1000; i++)
{
    s += listOfNames[i];
}
```

当你要对字符串进行大量修改时，为避免这种开销，请使用配套类 `StringBuilder`。务必在文件顶部添加以下行：

```csharp
using System.Text;  // Tells the compiler where to find StringBuilder.
```

![](img/80ff26f06fc9ab951e1cd4257b867366_94_1.png)

与 `String` 操作不同，对 `StringBuilder` 进行的操作会直接更改底层字符串。示例如下：

```csharp
StringBuilder builder = new StringBuilder("012");
builder.Append("34");
builder.Append("56");
string result = builder.ToString();  // result = 0123456
```

创建一个用现有字符串初始化的 `StringBuilder` 实例，如刚才所示。或者创建一个没有初始值的空 `StringBuilder`：

```csharp
StringBuilder builder = new StringBuilder(); // Defaults to 16 characters
```

你还可以按预期需要的容量创建 StringBuilder，这会减少频繁增加生成器容量带来的开销：

```csharp
StringBuilder builder = new StringBuilder(256); // 256 characters.
```

使用 Append() 方法将文本添加到当前内容的末尾。完成修改后，使用 ToString() 检索 StringBuilder 内的字符串。下面是刚才那个循环的 StringBuilder 版本，其中检索最终连接字符串的部分以粗体显示：

```csharp
StringBuilder sb = new StringBuilder(20000); // Allocate a bunch.
for(int i = 0; i < 1000; i++)
{
    sb.Append(listOfNames[i]);    // Same list of names as earlier
}
string result = sb.ToString();  // Retrieve the results.
```

StringBuilder 还有许多其他有用的字符串操作方法，包括 Insert()、Remove() 和 Replace()。不过，它缺少字符串的许多方法，例如 Substring()、CopyTo() 和 IndexOf()。

假设你只想将字符串的第一个字符改为大写，就像前面“将字符串转换为大写或小写”一节中那样。使用 StringBuilder 时，代码看起来比我之前给出的代码整洁得多。

```csharp
StringBuilder sb = new StringBuilder("jones");
sb[0] = char.ToUpper(sb[0]);
string fixedString = sb.ToString();
```

这段代码将小写字符串 "jones" 放入 StringBuilder，通过 sb[0] 直接访问 StringBuilder 底层字符串中的第一个字符，使用 char.ToUpper() 方法将该字符转为大写，并将大写后的字符重新赋给 sb[0]。最后，它从 StringBuilder 中提取改进后的字符串 "Jones"。

本章前面“所有字符串一律平等：Compare() 方法”一节中介绍的 BuildASentence 示例，使用 StringBuilder 会受益匪浅。我经常使用 StringBuilder。

本书网站上的 StringCaseChanging 和 VariousStringTechniques 示例展示了 StringBuilder 的实际应用。

第II部分介绍 C# 的一项称为扩展方法的功能。那里的示例向 String 类添加了几个方便的方法。在该小册的后面，我描述了如何在字符串、char 数组和 byte 数组之间转换。这些是你可能需要频繁执行的操作（并且本书网站上的 StringCaseChanging 示例中展示了这些操作）。

![](img/80ff26f06fc9ab951e1cd4257b867366_95_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_95_1.png)

## 第4章：流畅的运算符

### 本章内容

- 执行一些算术运算
- 进行一些逻辑运算
- 用复合逻辑运算符把事情复杂化

数学家创建变量并以各种方式操作它们：相加、相乘，以及——这里有个棘手之处——甚至对它们进行积分。本小册第2章描述了如何声明和定义变量。然而，它几乎没有说明在声明变量后如何使用变量来完成事情。本章探讨可对变量执行以完成一些工作的操作。操作需要运算符，例如 +、-、*、/、= 和 &。本章介绍算术、逻辑和其他类型的运算符。

![](img/80ff26f06fc9ab951e1cd4257b867366_96_0.png)

编写能完成工作的程序是好事。如果你的程序不做任何事，你就永远无法成为一名 C# 程序员——当然，除非你是顾问。

### 执行算术运算

算术运算符可分为几组：简单算术运算符、赋值运算符，以及一组编程特有的特殊运算符。消化完这些之后，你还需要消化另一组逻辑运算符。祝你好胃口！

### 简单运算符

你很可能在小学就学会了如何使用大多数简单运算符。表4-1列出了它们。注意：计算机使用星号（*）而不是乘号（×）来表示乘法。

