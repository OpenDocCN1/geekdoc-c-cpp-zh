
因为它现在只需考虑两个选项，而不是一长串选项：QUIT 或 EXIT 的任意拼写变体。

## 如果我想切换大小写呢？

你可能想知道字符串中的所有字符（或仅一个字符）是大写还是小写字符。而且你可能需要从一种形式转换为另一种形式。

### 区分全大写字符串和全小写字符串

我几乎不想提这件事，但你可以使用 switch 命令（见本迷你书的第 5 章）来查找特定字符串。通常，你使用 switch 命令将计数数字与一组可能值进行比较；不过，switch 也确实可以用于字符串对象。BuildASentence 中终止部分的这个版本使用了 switch 结构：

```
switch(line)
{
    case "EXIT":
    case "exit":
    case "QUIT":
    case "quit":
    return true;
}
return false;
```

这种方法可行，因为你只比较有限数量的字符串。for 循环为搜索字符串值提供了灵活得多的方法。使用上一节中不区分大小写的 Compare()，可以让程序在理解用户输入方面具有更大的灵活性。

### 将字符串转换为大写或小写

假设你有一个小写字符串，需要将其转换为大写。可以使用 ToUpper() 方法：

```
string lowercase = "armadillo";
string uppercase = lowercase.ToUpper();  // ARMADILLO.
```

同样，你可以使用 ToLower() 将大写转换为小写。

如果你只想将字符串中的第一个字符转换为大写，该怎么办？下面这段相当绕的代码可以做到（但本章最后一节会给出更好的方法）：

正如上一节关于切换大小写的最后一个示例所示，你也可以使用数组索引表示法访问字符串中的单个字符。

![](img/80ff26f06fc9ab951e1cd4257b867366_79_0.png)

数组从零开始，所以如果你想获取第一个字符，就请求 `[0]`。如果你想获取第三个字符，就请求 `[2]`：

```
char thirdChar = favoriteFood[2];   // First 'e' in "cheeseburgers"
```

## 搜索字符串

如果你需要在字符串中查找某个特定的单词或字符，该怎么办？也许你需要它的索引，以便对它使用 `Substring()`、`Replace()`、`Remove()` 或其他方法。本节将介绍如何查找单个字符或子字符串。（我仍在使用上一节中的 `favoriteFood` 变量。）

### 我能找到它吗？

最简单的是使用 `IndexOf()` 查找单个字符：

```
int indexOfLetterS = favoriteFood.IndexOf('s');   // 4.
```

`String` 类还有其他用于查找内容的方法，可以查找单个字符或子字符串：

- `IndexOfAny()` 接收一个 `char` 数组，并在字符串中搜索其中任意字符，返回找到的第一个字符的索引。

```
char[] charsToLookFor = { 'a', 'b', 'c' };
int indexOfFirstFound = favoriteFood.IndexOfAny(charsToLookFor);  // 0.
```

这种调用通常更简短地写成这样：

```
int index = name.IndexOfAny(new char[] { 'a', 'b', 'c' });
```

- `LastIndexOf()` 查找的不是字符的第一次出现，而是最后一次出现。

- `LastIndexOfAny()` 的工作方式与 `IndexOfAny()` 类似，但从字符串末尾开始。

- 如果能在目标字符串中找到给定子字符串，`Contains()` 就返回 `true`：

```
if(favoriteFood.Contains("ee")) ...       // True
```

- 而 `Substring()` 会返回该字符串（如果存在），或返回空字符串（如果不存在）：

```
string sub = favoriteFood.Substring(6, favoriteFood.Length - 6);
```

### 我的字符串是空的吗？

如何判断目标字符串是空字符串（""）还是值为 null？（null 表示尚未分配任何值，甚至不是空字符串。）使用 `IsNullOrEmpty()` 方法，如下所示：

```csharp
bool notHere = string.IsNullOrEmpty(favoriteFood);  // False
```

注意调用 `IsNullOrEmpty()` 的方式：`string.IsNullOrEmpty(s)`。

可以通过以下两种方式将字符串设置为空字符串：

```
string name = "";
string name = string.Empty;
```

## 从命令行获取输入

控制台应用程序中的一项常见任务是获取用户在你提示后输入的信息，比如利率或姓名。你需要读取以字符串形式传入的信息。（来自命令行的所有内容都以字符串形式传入。）然后，有时你需要解析输入以从中提取数字。有时你还需要处理大量输入数字。

### 修剪多余的空白字符

首先，请考虑在某些情况下，你不想处理字符串两端的任何空白字符。术语 *空白字符* 指的是通常不会显示在屏幕上的字符——例如空格、换行符（或 \n）和制表符（\t）。有时你可能还会遇到回车字符 \r。

你可以使用 `Trim()` 方法修剪字符串的边缘，如下所示：

```
// Get rid of any extra spaces on either end of the string.
random = random.Trim();
```

`String` 类还提供了 `TrimStart()` 和 `TrimEnd()` 方法，以便进行更精细的控制；你可以传入一个字符数组，让这些字符连同空白字符一起被修剪。例如，你可能会修剪开头的货币符号，比如 '$'。清理字符串可以让解析更容易。这些修剪方法会返回一个新字符串。

### 解析数值输入

程序可以一次从键盘读取一个字符，但你必须处理换行符等。更简单的方法是读取一个字符串，然后从字符串中解析出字符。

// No nondigits found; it's probably okay.
return true;
}

IsAllDigits() 方法首先移除字符串两端任何无害的空白字符。如果什么都不剩，说明该字符串是空白的，不可能是整数。然后，该方法遍历字符串中的每个字符。如果其中任何字符不是数字，该方法就返回 false，表示该字符串很可能不是数字。如果该方法返回 true，那么该字符串很有可能成功转换为整数。

下面的代码示例从键盘输入一个数字，并将其打印回控制台。（为了节省篇幅，我从代码清单中省略了 IsAllDigits() 方法，但已将程序调用它的位置加粗。）

![](img/80ff26f06fc9ab951e1cd4257b867366_82_0.png)

```
// IsAllDigits -- Demonstrate the IsAllDigits method.
using System;
namespace IsAllDigits
{
    class Program
    {
        public static void Main(string[] args)
        {
            // Input a string from the keyboard.
            Console.WriteLine("Enter an integer number");
            string s = Console.ReadLine();
            // First check to see if this could be a number.
            if (!IsAllDigits(s)) // Call the special method.
            {
                Console.WriteLine("Hey! That isn't a number");
            }
            else
            {
                // Convert the string into an integer.
                int n = Int32.Parse(s);
                // Now write out the number times 2.
                Console.WriteLine("2 * " + n + " = " + (2 * n));
            }
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}
// IsAllDigits here.
```

程序从控制台键盘读取一行输入。如果 IsAllDigits() 返回 false，程序会提醒用户。否则，程序使用 Convert.ToInt32(aString) 的替代方法——调用 Int32.Parse(aString)——将字符串转换为数字。最后，程序输出该数字以及该数字的两倍（后者是为了证明程序确实按所称那样转换了字符串）。

该程序一次示例运行的输出如下：

```
Enter an integer number
1A3
Hey! That isn't a number
Press Enter to terminate...
```

你可以让 Convert 尝试转换垃圾数据，并处理它可能决定抛出的任何异常。然而，很有可能它不会抛出异常，而只是返回错误结果——例如，遇到 1A3 时返回 1。你应该自己验证输入数据。

![](img/80ff26f06fc9ab951e1cd4257b867366_83_0.png)

你也可以改用 Int32.TryParse(s, n)，如果解析失败则返回 false，如果成功则返回 true。如果确实成功，转换后的数字会放在第二个参数中，也就是我命名为 n 的 int。这不会抛出异常。示例见下一节。

![](img/80ff26f06fc9ab951e1cd4257b867366_83_1.png)

## 处理一系列数字

程序经常从键盘的一行中接收一系列数字。使用 String.Split() 方法，你可以轻松地将字符串拆分成若干子字符串，每个数字对应一个子字符串，然后分别解析它们。

Split() 方法使用某个分隔符将单个字符串切分成一个由较小字符串组成的数组。例如，如果你让 Split() 使用逗号（,）作为分隔符来划分字符串，"1,2,3" 就会变成三个字符串："1"、"2" 和 "3"。（分隔符就是你用来拆分集合的那个字符。）

下面的程序使用 Split() 方法输入一系列要求和的数字。（同样，为了节约纸张，我省略了 IsAllDigits() 方法。）

![](img/80ff26f06fc9ab951e1cd4257b867366_83_2.png)

```
// ParseSequenceWithSplit -- Input a series of numbers separated by
commas,
// parse them into integers and output the sum.
// namespace ParseSequenceWithSplit
{
using System;
class Program
{
public static void Main(string[] args)
{
// Prompt the user to input a sequence of numbers.
Console.WriteLine
"Input a series of numbers separated by commas:";
// Read a line of text.
string input = Console.ReadLine();
Console.WriteLine();
// Now convert the line into individual segments
// based upon either commas or spaces.
char[] dividers = {',', ' '};
string[] segments = input.Split(dividers);
// Convert each segment into a number.
int sum = 0;
foreach(string s in segments)
{
// Skip any empty segments.

