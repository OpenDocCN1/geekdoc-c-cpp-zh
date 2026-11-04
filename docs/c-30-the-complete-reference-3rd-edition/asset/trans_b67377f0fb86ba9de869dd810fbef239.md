
## 字符串的填充与修剪

有时你会想要从字符串中移除前导和尾随空格。这种操作称为修剪，通常由命令处理器需要。例如，数据库可能识别单词 "print。" 然而，用户可能会带有一个或多个前导或尾随空格输入此命令。在字符串被数据库识别之前，必须移除此类空格。相反，有时你会想要用空格填充字符串，使其达到最小长度。例如，如果你正在准备格式化的输出，你可能需要确保每行的长度为一定值以保持对齐。幸运的是，C# 包含使这些操作变得容易的方法。

要修剪字符串，请使用以下 Trim() 方法之一：

```
public string Trim()
public string Trim(params char[] chrs)
```

第一种形式会从调用字符串中移除前导和尾随空白。第二种形式会移除由 chrs 指定的字符的前导和尾随出现。在这两种情况下，都会返回结果字符串。

你可以通过在字符串的左侧或右侧添加字符来填充字符串。

要在左侧填充字符串，请使用此处显示的方法之一：

```
public string PadLeft(int len)
public string PadLeft(int len, char ch)
```

第一种形式在需要时在调用字符串左侧添加空格，使其总长度等于 len。第二种形式在需要时在调用字符串中添加由 ch 指定的字符，使其总长度等于 len。在这两种情况下，都会返回结果字符串。如果 len 小于调用字符串的长度，则返回未更改的调用字符串的副本。

要在右侧填充字符串，请使用以下方法之一：

```
public string PadRight(int len)
public string PadRight(int len, char ch)
```

第一种形式在需要时在调用字符串右侧添加空格，使其总长度等于 len。第二种形式在需要时在调用字符串中添加由 ch 指定的字符，使其总长度等于 len。在这两种情况下，都会返回结果字符串。如果 len 小于调用字符串的长度，则返回未更改的调用字符串的副本。

以下程序演示了修剪和填充：

```
// Trimming and padding.

using System;

class TrimPadDemo {
    static void Main() {
        string str = "test";

        Console.WriteLine("Original string: " + str);

        // Pad on left with spaces.
        str = str.PadLeft(10);
        Console.WriteLine("|" + str + "|");

        // Pad on right with spaces.
        str = str.PadRight(20);
        Console.WriteLine("|" + str + "|");

        // Trim spaces.
        str = str.Trim();
        Console.WriteLine("|" + str + "|");

        // Pad on left with #s.
        str = str.PadLeft(10, '#');
        Console.WriteLine("|" + str + "|");

        // Pad on right with #s.
        str = str.PadRight(20, '#');
        Console.WriteLine("|" + str + "|");

        // Trim #s.
        str = str.Trim('#');
        Console.WriteLine("|" + str + "|");
    }
}
```

输出如下所示：

```
Original string: test
|      test|
|test      |
|test|
|######test|
|##########test##########|
|test|
```

## 插入、删除和替换

你可以使用此处所示的 Insert() 方法将一个字符串插入到另一个字符串中：

```
public string Insert(int start, string str)
```

这里，str 被插入到调用字符串中 start 指定的索引处。返回结果字符串。

你可以使用 Remove() 删除字符串的一部分，如下所示：

```
public string Remove(int start)
public string Remove(int start, int count)
```

第一种形式从 start 指定的索引开始并删除字符串中剩余的所有字符。第二种形式从 start 开始并删除 count 个字符。在这两种情况下，都会返回结果字符串。

你可以使用 Replace() 替换字符串的一部分。它有以下形式：

```
public string Replace(char ch1, char ch2)
public string Replace(string str1, string str2)
```

第一种形式用 ch2 替换调用字符串中 ch1 的所有出现。第二种形式用 str2 替换调用字符串中 str1 的所有出现。在这两种情况下，都会返回结果字符串。

这里有一个演示 Insert()、Remove() 和 Replace() 的示例：

```
// Inserting, replacing, and removing.
using System;

class InsRepRevDemo {
    static void Main() {
        string str = "This test";

        Console.WriteLine("Original string: " + str);

        // Insert
        str = str.Insert(5, "is a ");
        Console.WriteLine(str);

        // Replace string
        str = str.Replace("is", "was");
        Console.WriteLine(str);

        // Replace characters
        str = str.Replace('a', 'X');
        Console.WriteLine(str);

        // Remove
        str = str.Remove(4, 5);
        Console.WriteLine(str);
    }
}
```

输出如下所示：

```
Original string: This test
This is a test
Thwas was a test
ThwXs wXs X test
ThwX X test
```

## 更改大小写

String 提供了两个方便的方法，可以更改字符串中字母的大小写。它们称为 ToUpper() 和 ToLower()。

以下是它们最简单的形式：

```
public string ToLower()
public string ToUpper()
```

ToLower() 将调用字符串中的所有字母小写。ToUpper() 将调用字符串中的所有字母大写。返回结果字符串。这些方法还有允许你指定文化设置的版本。

还提供了此处所示的 ToUpperInvariant() 和 ToLowerInvariant() 方法：

```
public string ToUpperInvariant()
public string ToLowerInvariant()
```

它们的工作方式与 ToUpper() 和 ToLower() 类似，只是它们使用不变文化来执行大小写转换。

## 使用 Substring() 方法

你可以使用 Substring() 方法获取字符串的一部分。它有以下两种形式：

```
public string Substring(int idx)
public string Substring(int idx, int count)
```

在第一种形式中，子字符串从 idx 指定的索引开始并运行到调用字符串的末尾。在第二种形式中，子字符串从 idx 开始并运行 count 个字符。在每种情况下，都会返回子字符串。

以下程序演示了 Substring() 方法：

```
// Use Substring().

using System;

class SubstringDemo {
    static void Main() {
        string str = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

        Console.WriteLine("str: " + str);

        Console.Write("str.Substring(15): ");
        string substr = str.Substring(15);
        Console.WriteLine(substr);

        Console.Write("str.Substring(0, 15): ");
        substr = str.Substring(0, 15);
        Console.WriteLine(substr);
    }
}
```

以下是产生的输出：

```
str: ABCDEFGHIJKLMNOPQRSTUVWXYZ
str.Substring(15): PQRSTUVWXYZ
str.Substring(0, 15): ABCDEFGHIJKLMNO
```

## 字符串扩展方法

如前所述，String 实现了 IEnumerable<T>。这意味着从 C# 3.0 开始，String 对象可以调用 Enumerable 和 Queryable 定义的扩展方法，两者都在 System.Linq 命名空间中。这些扩展方法主要为 LINQ 提供支持，但其中一些也可以用于其他目的，例如某些类型的字符串处理。有关扩展方法的讨论，请参阅第 19 章。

## 格式化

当需要内置类型（如 int 或 double）的人类可读形式时，必须创建字符串表示形式。

尽管 C# 自动为此表示提供默认格式，但也可以指定你自己的格式。例如，正如你在第一部分所看到的，可以使用美元和美分格式输出数字数据。若干方法可格式化数据，包括 Console.WriteLine()、String.Format() 以及为数值结构类型定义的 ToString() 方法。三者都使用相同的格式化方法；一旦你学会为其中一个格式化数据，就可将其应用于其他方法。

## 格式化概述

格式化由两个组件控制：格式说明符和格式提供程序。

值的字符串表示形式通过使用格式说明符来控制。因此，是格式说明符决定数据的可读形式的外观。例如，要使用科学记数法输出数值，将使用 E 格式说明符。

在许多情况下，值的精确格式会受到程序运行的文化和语言的影响。例如，在美国，货币以美元表示。在欧洲，货币以欧元表示。为处理文化和语言差异，C# 使用格式提供程序。格式提供程序定义格式说明符的解释方式。格式提供程序通过实现定义 GetFormat() 方法的 IFormatProvider 接口来创建。格式提供程序已为 .NET Framework 中的内置数值类型和许多其他类型预定义。一般来说，你可以在不担心指定格式提供程序的情况下格式化数据，并且本书不再进一步探讨格式提供程序。

要格式化数据，请在支持格式化的方法的调用中包含格式说明符。格式说明符的使用已在第 3 章中介绍，但在此回顾是有价值的。以下讨论使用 Console.WriteLine()，但相同的基本方法适用于其他支持格式化的 方法。

要使用 WriteLine() 格式化数据，请使用此处所示的 WriteLine() 版本：

```
WriteLine("format string", arg0, arg1, ..., argN);
```

在此版本中，WriteLine() 的参数由逗号分隔，而不是 + 号。格式字符串包含两项：常规打印字符，按原样显示，以及格式命令。

格式命令采用以下通用形式：

```
{argnum, width:.fmt}
```

这里，argnum 指定要显示的参数编号（从零开始）。字段的最小宽度由 width 指定，格式说明符由 fmt 表示。width 和 fmt 都是可选的。因此，在最简单的形式中，格式命令仅指示要显示哪个参数。例如，{0} 表示 arg0，{1} 指定 arg1，以此类推。

在执行期间，当在格式字符串中遇到格式命令时，按 argnum 指定的相应参数被替换并显示。因此，格式说明符在格式字符串中的位置决定了其匹配数据将被显示的位置。参数编号决定了将格式化哪个参数。

如果存在 fmt，则数据将使用指定的格式显示。否则，使用默认格式。如果存在 width，则输出会用空格填充以确保达到最小字段宽度。如果 width 为正，输出右对齐。如果 width 为负，输出左对齐。

本章的其余部分详细探讨格式化和格式说明符。
