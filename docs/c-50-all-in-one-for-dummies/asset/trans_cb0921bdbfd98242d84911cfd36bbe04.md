
从字符串中解析字符是另一个我不喜欢提到的话题，因为我担心程序员会滥用这种技术。在某些情况下，程序员太急于跳到字符串中间并开始提取他们在那里发现的内容。这对于 C++ 程序员来说尤为如此，因为那是他们处理字符串的唯一方法——直到 `string` 类的加入。

用于从控制台读取的 `ReadLine()` 方法返回一个字符串对象。期望数值型输入的程序必须转换此字符串。C# 在 `Convert` 类中提供了你需要的转换工具。该类提供了从字符串到每种内置变量类型的转换方法。因此，这段代码段从键盘读取一个数字并存储在 `int` 变量中：

```
string s = Console.ReadLine();  // 键盘输入是字符串数据
int n = Convert.ToInt32(s);     // 但你知道它应该是一个数字。
```

其他的转换方法要直观得多：`ToDouble()`、`ToFloat()` 和 `ToBoolean()`。

`ToInt32()` 指的是一个 32 位有符号整数（32 位是普通 `int` 的大小），所以这是 `int` 的转换方法。`ToInt64()` 处理 `long` 的大小。

当 `Convert()` 遇到意外之外的字符类型时，它可能会产生意外的结果。因此，你必须确定你正在处理的是什么类型的数据，并确保没有多余的字符。

虽然我还没有充分讨论方法（参见第二本书），但这里还是有一个。以下方法如果传递给它的字符串仅由数字组成，则返回 `true`。你可以在将其转换为整数类型之前调用此方法，假设仅由数字组成的序列可能是一个合法的数字。

为了做到真正的完整，你需要为浮点型变量包含小数点，并为负数包含前导负号——但嘿，你明白意思了。

这里是该方法：

```
// IsAllDigits -- 如果字符串中的所有字符
//   都是数字，则返回 true。
public static bool IsAllDigits(string raw)
{
    // 首先去掉两端的任何无害字符；
    // 如果什么都不剩，说明你没有数字。
    string s = raw.Trim();  // 忽略两侧的空格。
    if (s.Length == 0) return false;
    // 遍历字符串。
    for(int index = 0; index < s.Length; index++)
    {
        // 非数字表示该字符串可能不是数字。
        if (Char.IsDigit(s[index]) == false) return false;
    }
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_81_0.png)

![](img/6df7bb88e9302e98442acc219cfbd7fc_81_1.png)

```
// 没有找到非数字；可能没问题。
return true;
}
```

`IsAllDigits()` 方法首先移除字符串两端的任何无害空格。如果空无一物，则该字符串为空，且不能转换为整数。该方法随后遍历字符串中的每个字符。如果这些字符中的任何一个证明是非数字，该方法将返回 `false`，表示字符串可能不是数字。如果此方法返回 `true`，则该字符串成功转换为整数的概率很高。

下面的代码示例从键盘输入一个数字并将其打印回控制台。（为了节省空间，我在列表中省略了 `IsAllDigits()` 方法，但我用加粗标记了该程序调用它的地方。）

![](img/6df7bb88e9302e98442acc219cfbd7fc_82_0.png)

```
// IsAllDigits -- 演示 IsAllDigits 方法。
using System;
namespace IsAllDigits
{
class Program
{
public static void Main(string[] args)
{
// 从键盘输入一个字符串。
Console.WriteLine("Enter an integer number");
string s = Console.ReadLine();
// 首先检查这是否是一个数字。
if (!IsAllDigits(s)) // 调用特殊方法。
{
Console.WriteLine("Hey! That isn't a number");
}
else
{
// 将字符串转换为整数。
int n = Int32.Parse(s);
// 现在输出数字乘以2 的结果。
Console.WriteLine(2 * " " + n + " = " + (2 * n));
}
// 等待用户确认结果。
Console.WriteLine("Press Enter to terminate...");
Console.Read();
}
// IsAllDigits 在这里。
}
}
```

该程序从控制台键盘读取一行输入。如果 `IsAllDigits()` 返回 `false`，程序会警告用户。如果不是，程序将使用 `Convert.ToInt32(aString)` 的替代方案——`Int32.Parse(aString)` 调用将字符串转换为数字。最后，程序输出该数字以及数字的两倍（后者是为了证明程序确实如广告的那样转换了字符串）。

程序示例运行的输出如下：

```
Enter an integer number
1A3
Hey! That isn't a number
Press Enter to terminate...
```

你可以让 `Convert` 尝试转换垃圾数据，并处理它可能决定抛出的任何异常。然而，有超过半数的概率它不会抛出异常，而是直接返回错误的结果。你可以使用 `Int32.TryParse(s, out n)`，它不会抛出异常，在失败时返回 `false`，成功时返回 `true` 并将结果赋值给 `n`。这种方法通常更健壮，因为它不需要处理异常的开销。

处理一系列的数字

通常，程序从键盘接收一系列数字。使用 `Split()` 方法，你可以轻松将字符串拆分成数字，例如。

```
// ParseWithSplit -- 处理一系列数字的示例。
using System;
namespace ParseWithSplit
{
    class Program
    {
        public static void Main(string[] args)
        {
            // 提示用户输入一系列数字。
            Console.WriteLine("Input a series of numbers:");
            string input = Console.ReadLine();
            // 使用逗号或空格分割。
            char[] dividers = {',', ' '};
            string[] segments = input.Split(dividers);
            int sum = 0;

            foreach(string s in segments)
            {
                // 跳过空段。
                if (s.Length > 0)
                {
                    // 跳过不是数字的字符串。
                    if (IsAllDigits(s))
                    {
                        // 32位整数。
                        int num = 0;
                        if (Int32.TryParse(s, out num))
                        {
                            // 输出数字
                            Console.WriteLine("Next number = {0}", num);
                            // 将此数字加到总和中。
                            sum += num;
                        }
                    }
                }
            }
            // 输出总和。
            Console.WriteLine("Sum = {0}", sum);
            // 等待用户确认结果。
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }

        // IsAllDigits 在这里。
        public static bool IsAllDigits(string raw)
        {
            // 首先去掉两端的任何无害字符；
            // 如果什么都不剩，说明你没有数字。
            string s = raw.Trim();  // 忽略两侧的空格。
            if (s.Length == 0) return false;
            // 遍历字符串。
            for(int index = 0; index < s.Length; index++)
            {
                // 非数字表示该字符串可能不是数字。
                if (Char.IsDigit(s[index]) == false) return false;
            }
            // 没有找到非数字；可能没问题。
            return true;
        }
    }
}
```

典型运行的输出如下：

```
Input a series of numbers:
1,2, a, 3 4

Next number = 1
Next number = 2
Next number = 3
Next number = 4
Sum = 10
Press Enter to terminate...
```

程序分割了列表，接受逗号、空格或两者作为分隔符。它成功地跳过了 a 以生成 10 的结果。然而，在现实世界的程序中，你可能不想跳过错误的