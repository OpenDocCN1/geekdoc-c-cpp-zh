
```
Enter temp in degrees Fahrenheit:100
Temperature in degrees Celsius = 37.777777777778
Press Enter to terminate...
```

## 检查浮点变量的一些局限性

你可能想一直一直使用浮点变量，因为它们很好地解决了截断问题。诚然，它们会多消耗一点内存。但现在的内存很便宜，所以为什么不用呢？但浮点变量也有局限性，我在接下来的章节中讨论。

## 计数

你不能将浮点变量作为计数数字。某些 C# 结构需要计数（例如 1, 2, 3 等）。你认为 1.0、2.0 和 3.0 和 1, 2, 和 3 一样是计数数字，但 C# 并不这么认为。例如，考虑到浮点的精度限制，C# 如何知道你并不是在说 1.000001 呢？

无论你觉得这个论点是否有说服力，计数时都不能使用浮点变量。

![](img/6df7bb88e9302e98442acc219cfbd7fc_57_0.png)

## 比较数字

在比较浮点数时必须小心。例如，12.5 可能被表示为 12.500001。大多数人不在乎末尾那个小额外部分。然而，计算机处理得非常死板。

然而，小数（`decimal`）变量类型有两个非常重大的局限性。首先，小数不被视为计数数字，因为它可能包含分数值。因此，你不能在流程控制循环中使用它们，我将在本微教程的第 5 章中解释这一点。

小数变量的第二个问题同样严重，甚至更严重。涉及小数值的计算速度比涉及简单整数或浮点值的计算慢得多——我说的确实是慢得多。在一项针对 300,000,000 次加减法的粗略基准测试中，涉及小数变量的操作比涉及简单 `int` 变量的操作慢了大约 50 倍。对于更复杂的操作，相对计算速度会变得更糟。此外，大多数计算函数（如计算正弦或指数）都不适用于小数类型。

显然，小数变量类型最适用于银行等应用，在这些应用中，准确性极其重要，但计算次数相对较少。

## 检查 bool 类型：它是逻辑性的吗？

![](img/6df7bb88e9302e98442acc219cfbd7fc_59_0.png)

最后是逻辑变量类型。除了这种情况下，我真的是指“逻辑”类型。布尔类型 `bool` 可以有两个取值：`true`（真）或 `false`（假）。我不是在开玩笑——一个整个变量类型只有两个值。甚至没有“可能”。

以前的 C 和 C++ 程序员习惯于使用 `int` 值 0（零）表示 `false`，使用非零值表示 `true`。这在 C# 中是行不通的。

你这样声明一个 `bool` 变量：

```
bool thisIsABool = true;
```

`bool` 变量与任何其他类型之间不存在转换路径。换句话说，你不能将 `bool` 直接转换为其他东西。（即使你可以这样做，也不应该这样做，因为这没有意义。）特地，你不能将 `bool` 转换为 `int`（例如将 `false` 变为 0）或字符串（例如将 `false` 变为单词“false”）。

## 了解字符类型

一个只会吐出数字的程序对于数学家、会计师、拥有死亡率数字的保险代理人以及计算大炮弹道轨迹的人们来说可能没问题。（别笑，最初的计算机造出来是为了生成大炮弹道轨迹表来帮助炮兵的。）然而，对于大多数应用程序，程序必须处理字母，也要处理数字。

C# 以两种截然不同的方式处理字母：`char` 类型的单个字符（通常读作 char，就像 singe 或 burn 中的读音）和字符字符串——很巧的是，这种类型被称为 `string`。

### char 变量类型

`char` 变量是一个能够容纳单个字符的盒子。字符常量表现为被一对单引号包围的字符，如下例所示：

```
char c = 'a';
```

你可以存储来自罗马字母、希伯来字母、阿拉伯字母、西里字母以及大多数其他字母表中的任何单个字符。你还可以存储日语片假名和平假名字符，以及许多日语和中文汉字。

此外，`char` 被认为是一种计数类型。这意味着你可以使用 `char` 类型来控制我在微教程第 5 章中描述的循环结构。字符变量不会遇到舍入问题。

字符变量不包含字体信息。因此，你可能在 `char` 变量中存储你认为是完美的汉字（它很可能确实完美），但当你查看该字符时，如果你不是通过正确的字体来看它，它看起来可能像乱码。

### 特殊字符

给定字体中的某些字符是不可打印的，从某种意义上说，当你从计算机屏幕或打印机查看它们时，什么也看不到。这最明显的例子是空格，它由字符 `' '`（单引号、空格、单引号）表示。其他字符没有对应的字母——例如制表符。C# 使用反斜杠来标记这些字符，如表 2-3 所示。

| 表 2-3 | 特殊字符 |
|---|---|
| 字符常量 | 值 |
| `'\n'` | 换行 |
| `'\t'` | 制表符 |
| `'\0'` | 空字符 |
| `'\r'` | 回车 |
| `'\\'` | 反斜杠 |

![](img/6df7bb88e9302e98442acc219cfbd7fc_60_0.png)

### string 类型

另一个常见的变量类型是 `string`。以下显示了如何声明和初始化字符串：

```
string some1 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some2 = "this is string";
```

以下显示了如何使用字符串：

```csharp
string some3 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some4 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some5 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some6 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some7 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some8 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some9 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some10 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some11 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some12 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some13 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some14 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some15 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some16 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some17 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some18 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some19 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some20 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some21 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some22 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some23 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some24 = "this is a string";
```

以下显示了如何使用字符串：

```csharp
string some25 = "this is a string";
```

## 什么是值类型？

![](img/6df7bb88e9302e98442acc219cfbd7fc_62_0)

我在本章中描述的变量类型都是固定长度的，`string` 除外。固定长度变量总是占据相同的内存。因此当你赋值 `a = b` 时，C# 不需要采取额外措施来处理变长类型。这种特性使得这些类型被称为*值类型*。

![](img/6df7bb88e9302e98442acc219cfbd7fc_62_1)

`int`、`double` 和 `bool` 类型以及它们的派生类型（如无符号 int）是内置的变量类型。这些内置类型加上 `decimal` 也被称为值类型，因为变量存储的是实际数据。`string` 类型则不是两者——因为变量实际上存储的是指向字符串数据的“指针”，称为*引用*。字符串数据实际上位于另一个位置。

我在本微教程第 8 章中解释的程序员定义类型被称为引用类型，既不是值类型也不是内置类型。`string` 类型是引用类型，尽管 C# 编译器对其特殊处理。

### 比较 string 和 char

虽然字符串处理字符，但 `string` 类型与 `char` 非常不同。当然，存在某些细微的差异。你用单引号包含字符，如下例：

```
'a'
```

相反，你用双引号包围字符串：

```
"this is a string"
"a"  // 如此——看到双引号了吗？
```

字符串的规则与字符的规则不同。首先，你明确知道 `char` 是单个字符，仅此而已。例如，以下代码无论是加法还是拼接都没有意义：

```
char c1 = 'a';
char c2 = 'b';
char c3 = c1 + c2
```

顺便说一下，本章中的所有其他数据类型都是*值类型*。然而，`string` 类型不是值类型，正如我在下一节中所解释的那样。本微教程的第 3 章将对 `string` 类型进行更多介绍。

## 命名规范

编程本身已经足够困难了，不需要程序员再让它变得更复杂。为了让你的 C# 源代码更易读，请采用一种命名规范并坚持遵守。尽可能地，你的命名规范应该遵循其他 C# 程序员所采用的规范：

变量之外的对象名称以大写字母开头，而变量以小写字母开头。让这些名称尽可能具有描述性这通常意味着一个名称由多个单词组成。这些单词应该大大写，但紧挨在一起，中间不加下划线——例如，`ThisIsALongName`。大写字母开头的命名被称为 Pascal 命名法（Pascal-cased），这源于 20 世纪 70 年代名为 Pascal 的语言命名方式。（我的第一本书就是关于 Pascal 的。）

变量名以小写字母开头。一个典型的变量名看起来像这样：`thisIsALongVariableName`。这种变量命名风格被称为驼峰命名法（camel-casing），因为它中间有“驼峰”。

在 .NET 时代之前，Windows 程序员中通常使用一种约定，即变量名的首字母表示变量的类型。这些字母大部分是直观的：`f` 代表 `float`，`d` 代表 `double`，`s` 代表 `string`，以此此类推。唯一稍有不同的是 `n` 代表 `int`。该规则有一个例外：由于追溯到 20 世纪 60 年代的 Fortran 编程语言，单个字母 `i`、`j` 和 `k` 也被用作 `int` 的常用名称，在 C# 中仍然在使用。这种变量命名风格被称为“匈牙利符号”（Hungarian notation），是以 Charles Simonyi 命名的，他是一位著名的微软员工，最近作为太空游客前往国际空间站。（Martha Stewart 为他准备了便餐。）

匈牙利符号已不再流行，至少在 .NET 编程圈中是如此。在最近的 Visual Studio 版本中，你只需将光标停在调试器中的变量上，即可在工具提示框中显示其数据类型。这使得匈牙利前缀变得不那么有用，尽管仍少数人坚持使用匈牙利符号。

实际上，这段代码几乎可以编译——但其含义与意图完全不同。这些语句将 `c1` 转换为一个由 `c1` 数值组成的 `int`。C# 还会将 `c2` 转换为 `int`，然后将两个整数相加。在尝试将结果存回 `c3` 时发生错误——将 `int` 存储到较小的 `char` 中可能会丢失数值数据。在任何情况下，该操作都没有意义。

另一方面，字符串可以是任何长度。因此，像这里这样连接两个字符串确实是有意义的：

```
string s1 = "a";
string s2 = "b";
string s3 = s1 + s2;  // 结果 "ab"
```

## 计算闰年：DateTime

如果你必须编写一个程序来计算今年是否为闰年该怎么办？

算法如下：

```
如果满足以下条件则是闰年
  年份能被 4 整除
  并且，如果恰好能被 100 整除，
    它也能被 400 整除
```

你还没有足够的工具在 C# 中解决这个问题问题。但你可以直接询问 `DateTime` 类型（它是一个值类型，类似于 `int`）：

```
DateTime thisYear = new DateTime(2011, 1, 1);
bool isLeapYear = DateTime.IsLeapYear(thisYear.Year);
```

2011 年的结果是 `false`，但对于 2012 年，它是 `true`。（现在，不用担心第一行代码，它使用了一些你尚未接触的内容。）

使用 `DateTime` 数据类型，你可以执行大约 80 种不同的操作，例如只提取月份；获取星期；给给定日期添加天、小时、分钟、秒、毫秒、月份或年份；获取给定月份的天数；相减两个日期。

以下示例代码行使用了 `DateTime` 的一个方便属性 `Now` 来获取当前的日期和时间，并使用了允许你将一个时间转换为另一个许多 `DateTime` 方法之一：

```
DateTime thisMoment = DateTime.Now;
DateTime anHourFromNow = thisMoment.AddHours(1);
```

你还可以提取 `DateTime` 的特定部分：

```
int year = DateTime.Now.Year;            // 例如，2007
DayOfWeek dayOfWeek = DateTime.Now.DayOfWeek;  // 例如，星期日
```

如果你打印该 `DayOfWeek` 对象，它会输出类似“Sunday”的内容。你还可以对 `DateTime` 进行其他方便的操控：

```
DateTime date = DateTime.Today;                // 只获取日期部分。
TimeSpan time = thisMoment.TimeOfDay;           // 只获取时间部分。
TimeSpan duration = new TimeSpan(3, 0, 0, 0);  // 指定持续天数。
DateTime threeDaysFromNow = thisMoment.Add(duration);
```

前两行只是提取 `DateTime` 中信息的部分。接下来的两行给 `DateTime` 添加了持续时间。持续时间（或时间量）与时间点不同；你用 `TimeSpan` 类指定持续时间，用 `DateTime` 指定时刻。因此，第三行设置了一个持续时间三天、零小时、零分钟和零秒的 `TimeSpan`。第四行将这三天的持续时间加到代表现在的 `DateTime` 上，产生一个新的 `DateTime`，其天数部分比 `thisMoment` 的天部分部分三。

从一个 `DateTime` 减去另一个 `DateTime`（或从 `DateTime` 减去 `TimeSpan`）返回一个 `DateTime`：

```
TimeSpan duration1 = new TimeSpan(1, 0, 0); // 一小时后。
// 由于 Today 给出 12:00:00 AM，接下来的操作得到 1:00:00 AM：
DateTime anHourAfterMidnight = DateTime.Today.Add(duration1);
Console.WriteLine("An hour after midnight will be {0}", anHourAfterMidnight);
DateTime midnight = anHourAfterMidnight.Subtract(duration1);
Console.WriteLine("An hour before 1 AM is {0}", midnight);
```

上述代码的第一行创建了一个小时的 `TimeSpan`。下一行获取日期（实际上是今天早上的午夜）并加上一小时的跨度，得到一个代表该时间的 `DateTime`。最后一行将其减去一个小时得到午夜。

![midnight](img/6dfbb88e9302e984421ac7fc_65_0.png)

## 声明数值常量

生活中很少有绝对的事；然而，我要告诉你 C#：每个表达式都有值和类型。人类并不以不同方式处理不同类型的数字。例如，一个普通人（区别于 C# 程序员）不会考虑数字 1 是有符号还是无符号、是短还是长。尽管 C# 认为这些类型是不同的，但 C# 也意识到它们之间存在关系。例如，这段代码将 `int` 转换为 `long`：在这样的声明中，你可以很容易看到类型是 `int`。此外，描述符的大小并不重要；`1U` 和 `1u` 是等价的。

### 表 2-4 带有特定类型的声明常量

| 常量 | 类型 |
|---|---|
| `1` | `int` |
| `1U` | `unsigned int` |
| `1L` | `long int`（避免小写 l；它太像数字 1 了） |
| `1.0` | `double` |
