

## 58 从命令行获取输入

```csharp
// 现在输出数字的 2 倍。
Console.WriteLine("2 * " + n + " = " + (2 * n));

// 等待用户确认结果。
Console.WriteLine("Press Enter to terminate...");
Console.Read();

// 在此处检查 IsAllDigits。
```

程序从控制台键盘读取一行输入。如果 `IsAllDigits()` 返回 `false`，程序会警告用户。如果程序使用 `Convert.ToInt32(aString)` 的替代方案——`Int32.Parse(aString)` 调用——它会将字符串转换为数字。最后，程序会输出该数字以及该数字的两倍（后者是为了证明程序确实如宣传的那样转换了字符串）。

程序示例运行的输出如下：

```
An integer number
IA3
Hey! That isn't a number
Press Enter to terminate...
```

你可以让 `Convert` 尝试转换 `gradle` 并处理它可能抛出的任何异常。然而，有一种较大的概率它不会抛出异常，但返回了错误的结果——例如，在遇到 `IA3` 时返回 `I1`。你应该自己验证输入数据。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_83_0.png)

你可以改用 `Int32.TryParse(s, n)`，它如果解析失败则返回 `false`，如果成功则返回 `true`。如果执行成功，转换后的数字位于第二个参数中，这是一个我命名为 `n` 的 `int` 类型。这不会抛出异常。示例请参见下一节。

## 处理系列数字

通常，程序会从键盘的一行接收一系列数字。使用 `String.Split()` 方法，你可以轻松地将字符串拆分为若干子字符串，并对每个数字分别进行解析。

`Split()` 方法使用某些分隔符将单个字符串切分为一个较小字符串的数组。例如，如果你告诉 `Split()` 使用逗号分割字符串，"1,2,3" 将产生三个字符串："1"、"2" 和 "3"。分隔符就是你用于分割集合的任何字符。

以下程序使用 `Split()` 方法输入一组数字并进行求和。（再次提醒，使用 `IsAllDigits()` 方法可以节省资源。）

## 从命令行获取输入 59

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_84_0.png)

第一卷
第 3 章

```csharp
// ParseSequenceWithSplit -- 输入一组由逗号分隔的系列数字，
// 将它们解析为整数并输出和。
namespace ParseSequenceWithSplit
{
    using System;
    class Program
    {
        public static void Main(string[] args)
        {
            // 提示用户输入一组数字。
            Console.WriteLine();
            // 读取一行文本。
            string input = Console.ReadLine();
            Console.WriteLine();
            // 根据字符或空格
            // 将行拆分成独立的段。
            char[] dividers = {',', ' ' };
            string[] segments = input.Split(dividers);
            // 将每个段转换为数字。
            int sum = 0;
            foreach (string s in segments)
            {
                // 跳过空段。
                // （这由连续的两个分隔符产生。）
                if (s.Length > 0)
                {
                    // 跳过不是数字的字符串。
                    // （例如，如果你输入带有额外非数字非分隔字符的 .3。）
                    if (IsAllDigits(s))
                    {
                        // 将字符串转换为32位int。
                        int num = 0;
                        if (int.TryParse(s, out num))
                        {
                            // 将此数字加到和。
                            sum += num;
                        }
                    }
                }
                // 如果解析失败，移动下一个数字。
            }
            // 输出和。
            Console.WriteLine("Sum = " + sum);
            // 等待用户确认结果。
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
        bool IsAllDigits(string s)
        {```

### 字符串填充

`ParseSequenceWithSplit` 程序首先从键盘读取一个字符串。程序将 `char` 类型的 `dividers` 数组传递给 `Split()` 方法，表示逗号和空格是用于分隔单个数字的字符。任何字符都会在该处分割。

程序使用 `foreach` 循环控制遍历 `Split()` 创建的每个较小子数组。程序跳过任何长度为零的子数组。（由连续两个分隔符产生。）程序接着使用 `IsAllDigits()` 方法确保字符串包含数字。（例如，如果你输入了带有额外非数字非分隔字符的 `.3`）。有效数字被转换为整数，然后加到累加器 `sum` 中。无效数字被忽略了。（为了保持简洁，我选择不生成错误消息。）

以下是典型运行的输出：

```
Input a series of numbers separated by commas:
1, a 3 4
Next number = 1
Next number = 2
Next number = 3
Next number = 4
Sum = 10
Press Enter to terminate...
```

程序分割了列表，接受逗号、空格或两者都作为分隔符。它成功地跳过了 `a` 并生成了 10 的结果。然而，在现实世界的程序中，你可能不想在没有任何注释的情况下跳过错误的输入。你几乎总是希望用户注意输入流中的垃圾数据。

## 将字符串数组合并为一个字符串

`String` 类有一个 `Join()` 方法。如果你有一个字符串数组，可以使用 `Join()` 拼接所有字符串。你可以告诉它在数组中的每个项目和下一个项目之间放置一个特定的字符：

```csharp
string[] brothers = {"Chuck", "Bob", "Steve", "Mike" };
string brothers = String.Join(":", brothers);
```

`brothers` 中的结果是 "Chuck:Bob:Steve:Mike"，名字之间用冒号分隔。你可以在名字之间放置任何分隔字符串：`", \t"`、`". "`。第一个项目是逗号和空格。第二个是制表符。第三个是多个空格字符串。

## 手动控制输出

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

