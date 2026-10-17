
`brothers` 中的结果是 "Chuck:Bob:Steve:Mike"，名字之间用冒号分隔。你可以在名字之间放置任何分隔字符串：`", \t"`、`". "`。第一个项目是逗号和空格。第二个是制表符。第三个是多个空格字符串。

### 手动控制输出

控制程序的输出是字符串处理的一个重要方面。面对吧：程序的输出是用户看到的内容。无论程序的内部逻辑有多优雅，如果输出看起来很糟糕，用户可能不会印象深刻。

## 手动控制输出 61

`String` 类为直接格式化输出提供了帮助。以下章节将检查 `Pad()`、`PadRight()`、`PadLeft()`、`Substring()` 和 `Concat()` 方法。

### 使用 Trim() 和 Pad() 方法

之前展示过使用 `Trim()` 及其专门变体 `TrimFront()` 和 `TrimEnd()`。在这里，我讨论了另一种格式化输出的常用方法。你可以使用 `Pad` 方法，它在字符串的末端添加字符以扩展字符串到某些长度。例如，你可以在字符串的左侧或右侧添加空格来实现左对齐或右对齐，或者可以在货币数字的左侧添加 `"` 等。

`AlignOutput` 程序使用 `Trim()` 和 `Pad()` 对一组名称进行修剪和对齐：

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_86_0.png)

```csharp
// AlignOutput -- 左对齐并对齐一组字符串
// 以改进程序输出的外。
namespace AlignOutput
{
    using System;
    using System.Collections.Generic;
    class Program
    {
        public static void Main(string[] args)
        {
            List<string> names = new List<string>{"Christa ",
                "Sarah",
                "Jonathan",
                "Dan",
                "Schmekowitz"};

            // 首先输出初始的名字。
            Console.WriteLine("The names are of " 
                + "different lengths");
            foreach (string s in names)
            {
                Console.WriteLine("This is the name " + s);
            }
            Console.WriteLine("");

            // 首先，修复字符串使它们
            // 左对齐且长度都相同。
            // 将源数组复制到你可以操作的数组中。
            List<string> stringsAlign = new List<string>();
            // 与此同时，从名称两端删除
            // 不必要的空格。
            for (int i = 0; i < names.Count; i++)
            {
                string trimmedName = names[i].Trim();
                stringsAlign.Add(trimmedName);
            }

            // 现在找到最字符串的长度，以便
            // 所有其他字符串与该字符串对齐。
            int maxLength = 0;
            foreach (string s in stringsAlign)
            {
            }
```
```

### 62 手动控制输出

`AlignOutput` 定义了一个 `List<string>`，包含长度不齐且未对齐的名称。（你可以轻松编写程序从控制台或文件中读取这些名称）。`Main()` 方法首先按原显示名称。然后 `Main()` 使用 `Trim()` 和 `PadRight()` 方法对名称进行对齐，并重新显示处理后的裁剪字符串：

以下是长度不同的名称：
This is the name 'Christa' before
This is the name 'Sarah' before
This is the name 'Jonathan' before
This is the name 'Sam' before
This is the name 'Schmemewitz' before

以下是相同的名称但已对齐到相同长度：
This is the name 'Christa' afterwards
This is the name 'Sarah' afterwards
This is the name 'Jonathan' afterwards
This is the name 'Sam' afterwards
This is the name 'Schmemewitz' afterwards

对齐过程从复制输入名称列表开始。

代码首先遍历列表，对每个元素调用 `Trim()` 以移除两端未使用的空格。该方法（此处指循环）再次遍历列表以找到最长的成员。代码最后循环一次，调用 `PadRight()` 将每个字符串扩展到列表中最长成员的长度。注意填充后的名称如何在输出中形成一列列。

`PadRight(10)` 将字符串扩展到至少十个字符长度。例如，`PadRight(10)` 在六个字符的字符串右侧添加四个空格。

最后，代码显示裁剪并填充后的字符串列表以输出。
Voilà（搞定）。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_87_0.png)

### 手动控制输出

### 63 使用 Concatenate() 方法

你经常遇到拆字符串或在另一个字符串中间插入子字符串的问题。用一个字符替换另一个最容易通过 `Replace()` 方法处理，如下：

```csharp
string s = "DangerNoSmoking";
s = s.Replace(' ', '!');
```
此示例将字符串转换为 "Danger!NoSmoking."。

将一个字符的所有出现（在本例中为空格）替换为另一个（感叹号），在生成便于解析的分隔符字符串时特别有用。然而，更常见且更困难的情况是将单个字符串拆分为子字符串，对它们进行操作，然后将其重新组合为一个修改后的单个字符串。

以下 `RemoveWhitespace` 示例程序使用 `Replace()` 方法从字符串移除空白（空格、制表符和换行符——一组字符的所有实例）：

```csharp
// RemoveWhitespace -- 从给定字符串移除一组字符中的任意字符。
// 使用此方法移除空白
namespace RemoveWhitespace
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // 定义空白字符。
            char[] whitespace = {' ', '\n', '\t' };
            // 从包含空白的字符串开始。
            string s = "this is almost string"; // 包含空格和换行。
            Console.WriteLine("before:" + s);
            // 输出缺少空白的字符串。
            Console.WriteLine("after:" + s);
            // 寻找空格字符的偏移量。
            while (true)
            {
                // 找到字符的偏移量；退出循环
                int offset = s.IndexOfAny(whitespace);
                if (offset == -1)
                    break;
                // 将字符串拆分为字符之前的部分
                // 和字符之后的部分。
                string before = s.Substring(0, offset);
                string after = s.Substring(offset + 1);
                // 现在将两个子字符串放在一起，
                // 中间缺少该字符。
                s = String.Concat(before, after);
                // 回到寻找下一个空白字符
            }
        }
    }
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_88_0.png)

第一卷
第三章
处理字符串

### 64 手动控制输出

```csharp
Console.WriteLine(s);
// 等待用户确认结果。
Console.WriteLine('Press Enter to terminate...');
Console.Read();
```

该程序的关键在于**粗体字体循环**。该循环不断精炼由输入字符串组成的字符串，移除 `whitespace` 数组中包含的一组字符中的每一个字符。

循环使用 `IndexOfAny()` 来寻找 `whiteSpace` 数组中任何字符的首次出现处。它不会返回所有已移除的这些字符的实例。`IndexOfAny()` 方法返回数组中能找到的第一个空白字符的索引。值为 -1 表示未在数组中找到任何成员。

循环的第一次通过移除了目标字符串开头的空白。`IndexOfAny()` 找到索引 0 处的空白。第一次 `String()` 调用返回一个空字符串，第二次调用返回空白后的整个字符串。然后用 `Concat()` 将它们拼接，产生一个挤掉空白的字符串。

循环的第二次通过找到 "this" 中的空格并以同样的方式将其挤掉，拼接字符串 "this" 和 "is a\nstring"。在此通过之后，`s` 变为了 "thisis a\nstring"。

第三次通过找到 `\n` 字符并将其挤掉。在第四次通过中，`IndexOfAny()` 没有更多空白字符可以寻找，并返回 -1（未找到）。这结束了循环。

`RemoveWhiteSpace` 程序打印包含多种形式空白的字符串。该程序剥离了空白字符。该程序的输出如下：

```
before: is a
string
after:thisastring
Press Enter to terminate...
```

## 让我们用 Split() 拆分那个拼接程序

`RemoveWhiteSpace` 程序演示了 `Concat` 和 `IndexOf()` 方法的使用；然而，它并没有使用最高效的方法。如往常，稍微检查一下就能发现一种使用我们老朋友 `Split()` 的更高效的方法。你可以在 RemoveWhiteSpaceSplit 网站找到包含此代码的程序——现在在另一个方法示例中。执行该工作的方法在此处：

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_90_0.png)

```csharp
// RemoveWhiteSpace -- RemoveSpecialChars 移除字符串中
// 指定字符的每处出现处。
// 注意：程序的其他部分未显示。
public static string RemoveChars(string input, char[] targets)
{
    // 使用字符作为分隔符
    // 分割输入字符串。
    string[] substrings = input.Split(targets);
    // output 将包含最终输出。
    string output = "";
    // 遍历子字符串。
    foreach(string subString in substrings)
    {
        output = String.Concat(output, subString);
    }
    return output;
}
```

此版本使用 `Split()` 方法将输入字符串拆分为一组子字符串，使用要移除的字符作为分隔符。分隔符不包含在创建的子字符串中，这实现了移除字符的效果。这里的逻辑要简单得多，且不易出错。

程序后半部分的 `foreach` 循环使用 `Concat()` 将碎片重新组合。程序的输出不变。

将代码封装成方法进一步简化了它并使其更清晰。

## 精确格式化你的字符串

`String` 类还提供了用于格式化输出的 `Format()` 方法，特别是数字输出。在简单形式，`Format()` 允许在字符串格式中间插入字符串、数值或布尔输入。例如，考虑此调用：

```csharp
string myString = String.Format("{0} times {1} equals ({2})", 2, 5, 2);
```

`Format()` 的第一个参数被称为格式字符串——即你看到的引号字符串。格式字符串中间的 `{n}` 项表示将格式字符串之后的第 n 个参数插入到该处。`{0}` 指向第一个参数（在本例中为 2），`{1}` 指向下一个（即 5），依此类推。

这返回一个字符串 `myString`。结果字符串是

```
"2 times 5 equals 10"
```

除非另有指示，`Format()` 为每个参数类型使用默认输出格式。`Format()` 允许你通过包含来影响输出格式
占位符中的格式指定符（修饰符或控制符）。参见表 3-1 的其中一些指定符列表。例如，{0:E6} 的意思是“以指数形式输出数字，小数部分使用六个空格。”

# 表 3-1 使用 String.Format() 的格式指定符

| 控制符 | 示例 | 结果 | Note |
| --- | --- | --- | --- |
| C — 货币 | {0:C} of 123456 | $123.45 | 货币符号取决于区域（Region）设置。 |
| | {0:C} of -123456 | ($123.45) | (在 Windows 控制面板中指定区域)。 |
| D — 十进制 | {0:D5} of 123 | 00123 | 仅整数。 |
| E — 指数 | {0:E} of 12345 | 1.2345E+002 | 也称为科学计数法。 |
| F — 固定值 | {0:F2} of 123456 | 123.46 | F 之后的数字表示小数点后的位数。 |
| N — 数字 | {0:N} of 12345678 | 12,345.79 | 添加逗号并四舍入到最接近的十分位。 |
| | {0:N1} of 12345678 | 123,456.8 | 控制小数点后的位数。 |
| | {0:N0} of 12345678 | 123,457 | |
| X — 十六进制 | {0:X} of 123 | 07B | 7B = 十进制 123（仅整数）。 |
| {0:...} | {0:.000} of 12.3 | 012.30 | 如果数字不存在，则强制补 0。 |
| {0:...} | {0:#.##} of 12.3 | 12 | 强制留空空格；任何其他字段都不能侵占小数点左侧的三位和右侧的两位，这有助于保持点的对齐。 |
| | {0:##.0} of 0 | 0.0 | 结合 # 和零，由 # 分配空间，并强制至少显示一个数字，即使数字为 0。 |
| {0:# 或 0%} | {0:##.%} of .1234 | 12.3% | % 号将数字以百分比形式显示（乘以 100 并添加 % 号）。 |
| | {0:##.%} of .0234 | 2.3% | |

# 精确格式化你的字符串 67

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_92_0.png)

`Console.WriteLine()` 方法相同的占位符符。第一个占位符 {} 获取语句中格式字符串之后列出的第一个变量或值，依此类推。鉴于早期 `Format()` 调用中提供的精确参数，`Console.WriteLine()` 将向控制台写入相同的字符串。你也可以使用格式指定符。从现在开始，大部分时间使用 `WriteLine()` 的格式化形式，而不是使用 + 运算符将其连接到最终输出中。

第一卷第 3 章

这些格式指定符可能会让人有些困惑。（我甚至没有提到详细的货币和日期控制）。请在索引中查找“format specifiers”（格式指定符）以获取更多信息。为了帮助你处理这些选项，下面的 `OutputFormatControls` 程序允许你使用一个浮点数后跟一个指定的序列。该程序使用指定的 `Format()` 控制显示数字：

### 提取字符串

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_92_1.png)

```csharp
// OutputFormatControls -- 允许用户使用运行时输入的
// 格式指定符重新格式化输入数字。
namespace OutputFormatControls
{
    using System;
    public class Program
    {
