
"""

  Mama said, "Life was just a box of chocolates..."

"""

# 76 第 2 章：数据类型（续）

## 表 2.6：string 静态方法

| 语句 | 示例 |
| --- | --- |
| static string string.Concat(string str0, string str1) | `string` `text`, `firstName`, `lastName`; // ...\n `text` = `string.Concat(firstName, lastName)`; // 显示 "firstName<lastName>", 注意 // 名字之间没有空格\n `Console.WriteLine(text)`; |
| static int string.Compare(string str0, string str1) | // 1.\n `string` `option`; // ...\n // 区分大小写的比较\n `int` `result` = `string.Compare(option, "/help")`; // 显示:\n // 如果相等则为 0\n 如果 option < /help 则为负数\n // 如果 option > /help 则大于 0\n `Console.WriteLine(result)`;\n // 2.\n `string` `option`; // ...\n // 不区分大小写的字符串比较\n `int` `result` = `string.Compare(option, "Help", true)`; // 显示:\n // 如果相等则为 0\n 如果 option < /help 则小于 0\n 如果 option > /help 则大于 0\n `Console.WriteLine(result)`; |

## 表 2.7：string 方法

| 语句 | 示例 |
| --- | --- |
| bool StartsWith(string value) | `string` `lastName` // ...\n `bool` `isPhd` = `lastName.EndsWith("Ph.D.")`;\n `bool` `isDr` = `lastName.StartsWith("Dr.")`; |
| string ToLower() string ToUpper() | `string` `severity` = "warning"; // 以大写形式显示级别\n `Console.WriteLine(severity.ToUpper())`; |

## 表 2.7：string 方法（续）

| 语句 | 示例 |
| --- | --- |
| string Trim() string Trim(...) stringEnd() string TrimStart() | // 1. // 从开头和结尾移除任何空白字符\n `username` = `username.Trim()`; // 2. `string` `text` = "indiscriminate bullet:"; // 从文本的开头或结尾移除 'i' 和 'n'\n `text` = `text.Trim("in").ToCharArray()`; // 显示: discriminate bullet \n `Console.WriteLine(text)`; |
| string Replace() string oldValue, string newValue() | `string` `filename`; //... // 从字符串的任何位置移除 '?'\n `filename` = `filename.Replace("?", "")`; |

## 字符串格式化

无论你使用 `string.Format()` 还是字符串插值来构建复杂的格式化字符串，都可以使用丰富且复杂的复合格式模式来显示数字、日期、时间、跨度等。例如，如果 `price` 是 `decimal` 类型的值，`string.Format("{0,20:C2}", price)` 和等效的插值 `"${price,20:C2}"` 都会使用默认货币格式规则将小数值转换为字符串，保留两位小数，并在 20 个字符宽的字符串中右对齐。空间限制不允许详细讨论所有可能的格式化字符串；请咨询有关复合格式的 MSDN 文档（http://itl.tc/CompositeFormatting）以获取完整的列表。

## 换行符

在编写换行时，换行的确切字符取决于你执行代码的操作系统。在 Microsoft Windows 操作系统上，换行是回车符 (`\r`) 和换行符 (`\n`) 字符的组合，而 UNIX 使用单行行符。克服操作系统之间差异的一种简单方法是直接使用 `Console.WriteLine()` 输出空行。另一种方法（对于在多个操作系统上使用同一代码库处理换行符几乎是必须的）是使用 `System.Environment.NewLine`。换句话说，`Console.WriteLine("Hello World")` 和 `Console.Write($"Hello World{Environment.NewLine}")` 是等的。然而，在 Windows 上，`WriteLine()` 和 `Console.Write(Environment.NewLine)` 等于 `Console.Write("\r\n")` ——而不是 `Console.Write("\n")`。总之，应依赖 `WriteLine()` 和 `Environment.NewLine` 而不是 `\n`，以适应运行相同代码的 Windows 特定操作系统的特性。

# 82 第2 章：数据类型

`null` 也可以用作一种“字面量”类型。`null` 值表示变量被设置为空。将变量设置为 `null` 的代码会显式地分配一个“空”值。事实上，甚至可以检查一个变量是否引用了 `null` 值。

赋值 `null` 值并不等同于将其赋值为所有（all）。换句话说，一个被赋值为 `null` 的变量仍然被设置过，而一个没有赋值的变量则未被设置，因此在赋值之前使用它时，通常会导致编译错误。

请注意，将 `null` 赋值给字符串变量与赋值空字符串 `""` 是有区别的。使用 `null` 表示该变量没有值，而 `" "` 则表示有一个值——即一个空字符串。这种区别可能非常有用。例如，编程逻辑可以将将名为 `homePhone` 的字符串设为 `null` 解释为家庭电话号码值为 " "，而 " " 则可能表示没有家庭电话号码。

![](img/ffe0f34eac7523830420733690014d17_116_0.png)

## 高级修饰符

## 可空修饰符

列表 2.25 展示了通过在类型声明中添加可空修饰符——问号（?）——为整数变量赋值 `null`。

列表 2.25：给 String 赋值 null

```csharp
public static void Main() {
    int? age;
    //...
    // 清空 age 的值
    age = null;
    // ...
}
```

在引入可空修饰符之前，除了 `string`（它是一种引用类型）之外，我们目前为止介绍的任何类型（值类型）都没有种方法可以向变量分配 `null` 6。（有关值类型和引用类型的更多信息，请参阅第 3 章。）

此外，在 C# 8.0 之前，引用类型（如 `string`）默认支持 `null` 赋值，因此你不能为引用类型装饰可空修饰符。由于 `null` 无论如何都可以隐式地赋值，所以为它装饰可空修饰符是多余的。

## 高级引用类型

在 C# 8.0 之前，由于所有引用类型默认都是可空的，因此没有“可空引用类型”的概念——所有引用类型本身就是可空的。但在 C# 8.0 中，行为变得可配置，使得引用类型可以声明为可空修饰符，否则默认为 `null`。这样做，C# 8.0 引入了可空引用类型的概念。带有可空修饰符的引用类型变量就是可空引用类型。而且，当启用可空引用类型时，向没有可空修饰符的引用类型变量赋值 `null` 会警告。

书中目前涵盖唯一的引用类型是 `string`。如果配置为支持引用类型的可空修饰符，你可以声明这样的字符串变量：

```csharp
string? homeNumber = null;
```

为了支持可空性，请确保 `.csproj` 文件中的 `Nullable` 元素设置为 `enable`。

- 6 C# 2.0 中添加了对可空修饰符的支持。

# 第 2 章：数据类型

## void "类型"

有时 C# 语法需要指定一个数据类型，但没有传递任何数据。例如，如果方法不需要返回值，C# 允许你将 `void` 指定为数据类型。HelloWorld 程序（列表 1.1）中 `Main` 的声明就是一个例子。将 `void` 作为返回类型表示该方法不返回任何数据，并告诉编译器不要期待值。`void` 并不是一个数据类型，而是表示没有返回数据的指示。

## 语言对比：C++

在 C++ 和 C# 中，`void` 都有两个含义：作为方法不返回任何数据的标记，以及表示指向未知类型存储位置的指针。在 C++ 程序中，看到 `void*` 指针类型非常常见。C 也可以使用相同的语法表示指向未知类型存储位置的指针，但这种用法在 C# 中相对少见，通常在编写与未托管代码库交互的程序时遇到。

## 数据类型之间的转换

考虑到 .NET 中预定义的数千种类型以及可以定义的无限数量类型，让类型在合理的情况下支持从一种类型到另一种类型的转换是非常重要的。导致转换的最常见操作是强制转换（casting）。

考虑两个数值类型之间的转换：将 `long` 类型的变量转换为 `int` 类型的变量。`long` 类型可以包含高达 9,223,372,036,854,778 的值；然而，`int` 的最大值是 2,147,483,647。因此，如果 `long` 变量包含的值大于 `int` 的最大值，该转换可能会导致数据丢失。任何导致数据丢失（如数量或精度）或抛出异常的转换都需要显式转换。相反，数值转换不会丢失数量且不会抛出异常，前提是隐式转换。

## 数据类型之间的转换

### 强制转换

在 C# 中，你使用强制转换运算符。通过在括号内指定类型，你承认如果发生强制转换，可能会丢失精度和数据，或者可能会产生异常。列表 2.26 中的代码将 `long` 转换为 `int` 并显式地告诉系统尝试该操作。

- 列表 2.26：强制转换示例

```csharp
long longNumber = 9223372036854778;
int intNumber = (int)longNumber;
```

通过强制转换运算符，程序员实际上是对编译器说：“相信我，我知道我在做什么。我知道这个值放得下。”然而，通过强制转换，仍有转换失败的可能性。

## 高级主题

## 检查与未检查转换

C# 提供了特殊的关键字来标记当目标类型太小时应该发生什么。默认情况下，这是未检查的（unchecked），如列表 2.27 所示。

- 列表 2.27：整数溢出

```csharp
long longNumber = 2147483647;
int intNumber = (int)longNumber;
```

# 86 第2 章：数据类型

- 2147483647

- 2.28：检查示例

```csharp
checked {
    long longNumber = 2147483647;
    int intNumber = (int)longNumber;
}
```

- 2147483648

- 2.29：未检查示例

```csharp
unchecked {
    long longNumber = 2147483647;
    int intNumber = (int)longNumber;
}
```

- 2147483648

## 第 2 章：数据类型

## 隐式转换

在其他情况下，例如从 `int` 类型转到 `long` 类型，精度不会丢失，类型类型的值也不会发生根本性变化。在这些情况下，代码只需要指定赋值运算符；转换是隐式的。换句话说，编译器可以确定此类转换将正常工作。列表 2.30 中的代码通过简单地使用赋值运算符将 `int` 转换为 `long`。

列表 2.30：对隐式转换不使用强制转换运算符

```c
int intNumber = 31416;
long longNumber = intNumber;
```

即使不需要显式强制转换运算符（因为允许隐式转换），仍然可以使用强制转换运算符（参见列表 2.31）。

列表 2.31：对隐式转换使用强制转换运算符

```c
int intNumber = 31416;
long longNumber = (long)intNumber;
```

## 无强制转换的类型转换

没有定义从字符串到数值类型的转换，因此需要如 `Parse()` 等方法。每个数值数据类型都包含一个 `Parse()` 函数，允许从字符串转换为相应的数值类型。列表 2.32 演示了此调用。

列表 2.32：使用 `float.Parse()` 将字符串转换为数值数据类型

```csharp
string text = $"9.11E-31";
float kgElectronMass = float.Parse(text);
```

还有另一种特殊类型用于将一种类型转换为另一种类型。该类型是 `System.Convert`，其用法示例出现在列表 2.33 中。

## 数据类型之间的转换

列表 2.33：使用 System.Convert 进行类型转换

```csharp
string middleCText = "261.626";
double middleCText = Convert.ToDouble(middleCText);
bool boolean = Convert.ToBoolean(middleCText);
```

`System.Convert` 仅支持少数类型且不可扩展。它允许将 `bool`、`char`、`sbyte`、`short`、`int`、`long`、`ushort`、`uint`、`ulong`、`float`、`double`、`decimal`、`DateTime` 和 `string` 中的任何类型转换为其他任何类型。

所有类型都支持 `ToString()` 方法，该方法可以提供类型的字符串表示。列表 2.34 演示了如何使用此方法。输出结果见输出 2.18。

列表 2.34：使用 `ToString()` 转换为字符串

```csharp
bool boolean = true;
string text = boolean.ToString();
// 显示 "True"
Console.WriteLine(text);
```

输出 2.18

| True |

对于大多数类型，`ToString()` 方法返回数据类型的名称，而不是数据的字符串表示。只有当类型显式实现了 `ToString()` 时，才会返回字符串表示。最后一点是，可以编写自定义的转换方法，运行时中的许多类都有许多此类方法可用。

## 第 2 章：数据类型

## 进阶主题

### TryParse()

所有数值原始类型都包含一个静态 `TryParse()` 方法。所有数值原始类型都包含一个静态 `TryParse()` 方法。此方法与 `Parse()` 方法类似，不同之处在于，如果转换失败，`TryParse()` 方法返回 `false` 而抛出异常，如列表 2.35 和输出 2.19 所示。

列表 2.35：使用 TryParse() 代替无效异常

```csharp
double number;
string input;
Console.Write("Enter a number: ");
input = Console.ReadLine();
if (double.TryParse(input, out number))
{
    // 转换正确，现在使用 number
    // ...
}
else{
    Console.WriteLine("The text entered was not a valid number.");
}
```

# 输出 2.19

输入一个数字：十二
输入的文本不是有效的字符串

在这种情况下，代码从输入字符串解析出的结果值通过 `out` 参数返回（参见第 5 章中的[输出参数 (out)](https://essentialcsharp.com/output-parameters-out))），在此处为 `number`。

除了各种数字类型外，`TryParse()` 方法也适用于枚举。

- 7. 从 C# 2.0 开始。

从 C# 7.0 开始，不再需要在使用变量作为 `out` 参数之前对其进行声明。通过使用此功能，列表 2.36 显示了 `number` 的声明。

# 列表 2.36：C# 7.0 中带有内联声明的 TryParse()

```csharp
// double number;
string input;
Console.Write("Enter a number: ");
input = Console.ReadLine();
if (double.TryParse(input, out double number))
{
    Console.WriteLine($"{input 已成功解析为 {number}.");
}
else
{
    // 注意：number 的作用域在这里（尽管未赋值）
    Console.WriteLine("The text entered was not a valid number.");
}
Console.WriteLine($"{number} 当前的值为: {number}");
```
