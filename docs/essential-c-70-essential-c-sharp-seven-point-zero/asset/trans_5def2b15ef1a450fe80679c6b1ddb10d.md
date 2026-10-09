

## 高级主题

### 以十六进制格式化数字

要在十六进制格式下显示数值，必须使用 x 或 X 数字格式化说明符。字母的大小写决定了十六进制字母是以小写还是大写形式出现。列表 2.8 展示了一个示例。

```
LISTING 2.8: Example of a Hexadecimal Format Specifier
// Displays "0x2A"
System.Console.WriteLine($"0x{42:X}");
```

输出 2.6 展示了结果。

![](img/ef6a8a417630b222bfb3f3b949facff0_88_0.png)

请注意，数字字面量 (42) 可以是十进制或十六进制形式。结果将是相同的。此外，为了实现十六进制格式化，我们依赖格式化说明符，它用冒号与字符串插值表达式分隔。

## 高级主题

### 往返格式化

默认情况下，`System.Console.WriteLine(1.618033988749895);` 显示 1.61803398874989，最后一位数字缺失。为了更准确地标识 double 值的字符串表示形式，可以使用格式字符串和往返格式化说明符 R（或 r）进行转换。例如，`string.Format("{0:R}", 1.618033988749895)` 将返回结果 1.6180339887498949。

往返格式化说明符返回的字符串，如果转换回数值，将始终产生原始值。列表 2.9 显示，如果没有使用往返格式，这些数字是不相等的。

### 列表 2.9：使用 R 格式化说明符进行格式化

```
/// ...
const double number = 1.618033988749895;
double result;
string text;

text = $"{number}";
result = double.Parse(text);
System.Console.WriteLine($"{result == number}: result == number");

text = string.Format("{0:R}", number);
result = double.Parse(text);
System.Console.WriteLine($"{result == number}: result == number");
/// ...
```

输出 2.7 显示了结果输出。

### 输出 2.7

```
False: result == number
True: result == number
```

在第一次分配给 `text` 时，没有使用往返格式化说明符；因此，`double.Parse(text)` 返回的值与原始数字值不同。相反，当使用往返格式化说明符时，`double.Parse(text)` 返回原始值。

对于不熟悉基于 C 的语言中 `==` 语法的读者，如果 `result` 等于 `number`，则 `result == number` 评估为 `true`，而 `result != number` 则相反。赋值和相等运算符将在下一章中讨论。

## 更多基本类型

迄今为止讨论的基本类型是数字类型。C# 还包括一些额外的类型：`bool`、`char` 和 `string`。

### 布尔类型 (bool)

C# 的另一种原始类型是布尔或条件类型，`bool`，它在条件语句和表达式中表示 `true` 或 `false`。允许的值是关键字 *true* 和 *false*。*bool* 的 BCL 名称是 `System.Boolean`。例如，要以不区分大小写的方式比较两个字符串，你调用 `string.Compare()` 方法并传递 *bool* 字面量 *true*（参见列表 2.10）。

### 列表 2.10：两个字符串的不区分大小写的比较

```
string option;
...
int comparison = string.Compare(option, "/Help", true);
```

在这种情况下，你对变量 *option* 的内容与字面文本 */Help* 进行不区分大小写的比较，并将结果赋值给 *comparison*。

虽然从理论上讲，单个位可以容纳布尔值，但 *bool* 的大小是 1 字节。

### 字符类型 (char)

*char* 类型表示 16 位字符，其可能值的集合取自 Unicode 字符集的 UTF-16 编码。*char* 的大小与 16 位无符号整数 (*ushort*) 相同，表示 0 到 65,535 之间的值。然而，*char* 是 C# 中的独特类型，代码应将其视为此类。

*char* 的 BCL 名称是 `System.Char`。

## 初学者主题

### Unicode 标准

Unicode 是表示大多数人类语言中找到的字符的国际标准。它为计算机系统提供构建**本地化**应用程序的功能——也就是说，为不同文化显示适当的语言和文化特征的应用程序。

## 高级主题

### 16 位对于所有 Unicode 字符来说太小了

不幸的是，并非所有 Unicode 字符都可以仅用单个 16 位 *char* 表示。最初的 Unicode 设计者认为 16 位足够了，但随着支持的语言越来越多，人们意识到这个假设是错误的。因此，一些（很少使用的）Unicode 字符由两个 char 值的“代理对”组成。

要构造字面量字符，请将字符放在单引号内，如 'A'。允许的字符包括键盘字符的完整范围，包括字母、数字和特殊符号。

某些字符无法直接放置在源代码中，而是需要特殊处理。这些字符以前缀反斜杠 (\) 开头，后跟一个特殊字符代码。组合起来，反斜杠和特殊字符代码构成一个**转义序列**。例如，\n 代表换行符，\t 代表制表符。由于反斜杠指示转义序列的开始，它不能再标识一个简单的反斜杠；相反，你需要使用 \\ 来表示单个反斜杠字符。

列表 2.11 写出一个单引号，因为由 \' 表示的字符对应于单引号。

### 列表 2.11：使用转义序列显示单引号

```
class SingleQuote
{
    static void Main()
    {
        System.Console.WriteLine('\'');
    }
}
```

除了显示转义序列外，表 2.4 还包括字符的 Unicode 表示。

### 表 2.4：转义字符

| 转义序列 | 字符名称 | Unicode 编码 |
| :--- | :--- | :--- |
| \' | 单引号 | \u0027 |
| \" | 双引号 | \u0022 |
| \\ | 反斜杠 | \u005C |
| \0 | 空字符 | \u0000 |
| \a | 警报（系统蜂鸣） | \u0007 |
| \b | 退格 | \u0008 |
| \f | 换页符 | \u000C |
| \n | 换行符（有时称为换行） | \u000A |
| \r | 回车 | \u000D |
| \t | 水平制表符 | \u0009 |
| \v | 垂直制表符 | \u000B |
| \uxxxx | 十六进制 Unicode 字符 | \u0029 |
| \x[n][n][n]n | 十六进制 Unicode 字符（前三个占位符是可选的）；\uxxxx 的可变长度版本 | \u3A |
| \uxxxxxxxx | 用于创建代理对的 Unicode 转义序列 | \UD840DC01 (弓) |

你可以使用 Unicode 编码表示任何字符。为此，请使用 \u 前缀 Unicode 值。你使用十六进制表示法表示 Unicode 字符。例如，字母 A 是十六进制值 0x41。列表 2.12 使用 Unicode 字符显示一个笑脸 (:)，输出 2.8 显示了结果。

### 列表 2.12：使用 Unicode 编码显示笑脸

```
System.Console.Write('\u003A');
System.Console.WriteLine('\u0029');
```

### 输出 2.8

:)

## 字符串

零个或多个字符的有限序列称为**字符串**。C# 中的字符串类型是 `string`，其 BCL 名称是 `System.String`。字符串类型包含一些特殊特性，对于熟悉其他编程语言的开发者来说可能出乎意料。除了第 1 章中讨论的字符串字面量格式外，字符串还包括“逐字字符串”前缀字符 `@`，支持带有 `$` 前缀字符的字符串插值，以及一个可能令人惊讶的事实，即字符串是不可变的。

### 字面量

你可以通过将文本放在双引号 (`"`) 中在代码中输入字面字符串，正如你在 `HelloWorld` 程序中所见。字符串由字符组成，因此，字符转义序列可以嵌入在字符串中。

例如，在列表 2.13 中，显示了两行文本。然而，代码列表没有使用 `System.Console.WriteLine()`，而是显示了带有换行符 `\n` 的 `System.Console.Write()`。输出 2.9 显示了结果。

### 列表 2.13：使用 \n 字符插入换行

```
class DuelOfWits
{
    static void Main()
    {
        System.Console.Write(
            "\"Truly, you have a dizzying intellect.\"");
        System.Console.Write("\n\"Wait 'til I get going!\"\n");
    }
}
```

### 输出 2.9

```
"Truly, you have a dizzying intellect."
Wait 'til I get going!
```

双引号的转义序列将打印的双引号与定义字符串开始和结束的双引号区分开来。

