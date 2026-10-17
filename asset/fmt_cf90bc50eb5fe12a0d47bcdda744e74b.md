
然后，在调用 `AppendFormat` 方法时，剩余文本被放置在空白空间中，无需分配更多内存。然而，使用 `StringBuilder` 的真正效率提升是在你进行重复文本替换时实现的。例如，如果你尝试以与之前相同的方式加密文本，你可以在不分配任何更多内存的情况下执行整个加密：

```
var greetingBuilder =
    new StringBuilder("Hello from all the guys at Wrox Press.", 150);
greetingBuilder.AppendFormat("We do hope you enjoy this book as much" +
    "as we enjoyed writing it");

WriteLine("Not Encoded:\n" + greetingBuilder);

for(int i = 'z'; i>='a'; i--)
{
    char old1 = (char)i;
    char new1 = (char)(i+1);
    greetingBuilder = greetingBuilder.Replace(old1, new1);
}

for(int i = 'Z'; i>='A'; i--)
{
    char old1 = (char)i;
    char new1 = (char)(i+1);
    greetingBuilder = greetingBuilder.Replace(old1, new1);
}

WriteLine("Encoded:\n" + greetingBuilder);
```

这段代码使用了 `StringBuilder.Replace` 方法，它执行与 `String.Replace` 相同的操作，但在此过程中不会复制字符串。在前面的代码中，为保存字符串而分配的总内存包括：`StringBuilder` 实例的 150 个字符，以及在最终 `WriteLine` 语句内部执行的字符串操作期间分配的内存。

通常，你会希望使用 `StringBuilder` 来执行任何字符串操作，并使用 `String` 来存储或显示最终结果。

### StringBuilder 成员

你已经看到了 `StringBuilder` 的一个构造函数演示，该构造函数将初始字符串和容量作为参数。还有其他构造函数。例如，你可以只提供字符串：

```
var sb = new StringBuilder("Hello");
```

或者你可以创建一个具有给定容量的空 `StringBuilder`：

```
var sb = new StringBuilder(20);
```

除了 `Length` 和 `Capacity` 属性之外，还有一个只读的 `MaxCapacity` 属性，它指示给定 `StringBuilder` 实例允许增长到的限制。默认情况下，此值由 `int.MaxValue` 指定（如前所述，大约二十亿），但你可以在构造 `StringBuilder` 对象时将此值设置为较小的值：

```
// This will set the initial capacity to 100, but the max will be 500.
// Hence, this StringBuilder can never grow to more than 500 characters,
// otherwise it will raise an exception if you try to do that.
var sb = new StringBuilder(100, 500);
```

你也可以随时显式设置容量，不过如果你将容量设置为小于字符串当前长度的值或超过最大容量的值，则会引发异常：

```
var sb = new StringBuilder("Hello");
sb.Capacity = 100;
```

下表列出了主要的 `StringBuilder` 方法。

| 方法 | 描述 |
| --- | --- |
| `Append` | 将一个字符串追加到当前字符串。 |
| `AppendFormat` | 追加一个已根据格式说明符格式化的字符串。 |
| `Insert` | 在当前字符串中插入一个子字符串。 |
| `Remove` | 从当前字符串中移除字符。 |
| `Replace` | 将当前字符串中所有出现的某个字符替换为另一个字符，或将某个子字符串替换为另一个子字符串。 |
| `ToString` | 返回当前字符串，转换为 `System.String` 对象（从 `System.Object` 重写）。 |

这些方法中有许多存在多个重载。

> **注意** 实际上，当你调用 `Console.WriteLine` 时，最终调用的方法就是 `AppendFormat`，它负责确定所有格式表达式（如 `{0:D}`）应替换为的内容。下一节将介绍此方法。

不存在从 `StringBuilder` 到 `String` 的转换（无论是隐式还是显式）。如果你想将 `StringBuilder` 的内容作为 `String` 输出，则必须使用 `ToString` 方法。

既然你已经了解了 `StringBuilder` 类，并学会了使用它来提高性能的一些方法，那么请注意，这个类并不总能带来你所追求的性能提升。基本上，当你在操作多个字符串时，应该使用 `StringBuilder` 类。然而，如果你只是做连接两个字符串这样简单的事情，你会发现 `System.String` 的性能更好。

### 字符串格式

在前面的章节中，你已经看到了使用 `$` 前缀将变量传递给字符串。本章探讨 C# 6 这个新特性背后的内容，并涵盖格式字符串提供的所有其他功能。

#### 字符串插值

C# 6 通过为字符串使用 `$` 前缀引入了字符串插值。下面的示例使用 `$` 前缀创建字符串 `s2`。此前缀允许在花括号中使用占位符来引用代码中的结果。`{s1}` 是字符串中的一个占位符，编译器将变量 `s1` 的值放入字符串 `s2` 中（代码文件 `StringFormats/Program.cs`）：

```csharp
string s1 = "World";
string s2 = $"Hello, {s1}";
```

实际上，这仅仅是语法糖。对于带有 `$` 前缀的字符串，编译器会生成对 `String.Format` 方法的调用。因此，前面的代码片段会被转换成这样：

```csharp
string s1 = "World";
string s2 = String.Format("Hello, {0}", s1);
```

这里使用的 `String.Format` 方法，其第一个参数接受一个格式字符串，其中有从 0 开始编号的占位符，随后是用于填充字符串孔洞的参数。

新的字符串格式要方便得多，也不需要编写那么多代码。

你不仅可以使用变量来填充字符串的孔洞。任何返回值的方法都可以使用：

```csharp
string s2 = $"Hello, {s1.ToUpper()}";
```

这会转换为类似的语句：

```csharp
string s2 = String.Format("Hello, {0}", s1.ToUpper());
```

字符串中也可以有多个孔洞，就像这样：

```csharp
int x = 3, y = 4;
string s3 = $"The result of {x} + {y} is {x + y}";
```

它会被转换为：

```csharp
string s3 = String.Format("The result of {0} + {1} is {2}", x, y, x + y);
```

#### FormattableString

通过将内插字符串赋值给 `FormattableString`，可以很容易地看出它会被转换为怎样的形式。内插字符串可以直接赋值给它，因为 `FormattableString` 是比普通字符串更好的匹配。这个类型定义了一个 `Format` 属性，返回结果格式字符串；一个 `ArgumentCount` 属性；以及用于返回值的 `GetArgument` 方法：

```csharp
int x = 3, y = 4;
FormattableString s = $"The result of {x} + {y} is {x + y}";
WriteLine($"format: {s.Format}");
for (int i = 0; i < s.ArgumentCount; i++)
{
    WriteLine($"argument {i}: {s.GetArgument(i)}");
}
```

运行这段代码会产生如下输出：

```
format: The result of {0} + {1} is {2}
argument 0: 3
argument 1: 4
argument 2: 7
```

> **注意** *`FormattableString` 类定义在 `System` 命名空间中，但需要 .NET 4.6。如果你希望将 `FormattableString` 用于更早的 .NET 版本，你可以自己创建这个类型，或者使用 `StringInterpolationBridge` NuGet 包。*

#### 使用其他区域性进行字符串内插

默认情况下，内插字符串使用当前区域性。这可以很容易地被更改。辅助方法 `Invariant` 将内插字符串改为使用固定区域性而不是当前区域性。由于内插字符串可以赋值给 `FormattableString` 类型，所以可以将它们传递给这个方法。`FormattableString` 定义了一个允许传递 `IFormatProvider` 的 `ToString` 方法。`IFormatProvider` 接口由 `CultureInfo` 类实现。将 `CultureInfo.InvariantCulture` 传递给 `IFormatProvider` 参数，可以将字符串改为使用固定区域性：

```csharp
private string Invariant(FormattableString s) =>
    s.ToString(CultureInfo.InvariantCulture);
```

> **注意** *第28章“本地化”讨论了格式字符串的语言特定问题，以及区域性和固定区域性。*

在下面的代码片段中，`Invariant` 方法被用来将一个字符串传递给第二个 `WriteLine` 方法。第一次调用 `WriteLine` 使用当前区域性，而第二次调用使用固定区域性：

```csharp
var day = new DateTime(2025, 2, 14);
WriteLine($"{day:d}");
WriteLine(Invariant($"{day:d}"));
```

如果你的区域性设置为英语（美国），结果如下所示。如果你的系统配置了不同的区域性，第一个结果会有所不同。无论如何，你都会看到与固定区域性之间的差异：

```
2/14/2025
02/14/2025
```

要使用固定区域性，你不需要实现自己的方法；你可以直接使用 `FormattableString` 类的静态 `Invariant` 方法：

```csharp
WriteLine(FormattableString.Invariant($"{day:d}"));
```

#### 转义花括号

如果你希望在内插字符串中使用花括号，可以使用双花括号进行转义：

```csharp
string s = "Hello";
WriteLine($"{{s}} displays the value of s: {s}");
```

`WriteLine` 方法会被转换为如下实现：

```csharp
WriteLine(String.Format("{s} displays the value of s: {0}", s));
```

因此输出是：

```
{s} displays the value of s: Hello
```

你还可以通过转义花括号，从格式字符串构建一个新的格式字符串。让我们看看下面的代码片段：

```csharp
string formatString = $"{s}, {{ {0} }}";
string s2 = "World";
WriteLine(formatString, s2);
```

使用字符串变量 `formatString` 时，编译器通过放入一个占位符 0 来插入变量 `s`，从而创建对 `String.Format` 的调用：

```csharp
string formatString = String.Format("{0}, {{ {0} }}", s);
```

这反过来会产生如下格式字符串，其中变量 `s` 被替换为值 `Hello`，并且第二个格式的最外层花括号被移除：

```csharp
string formatString = "Hello, {0}";
```

在最后一行使用 `WriteLine` 方法时，使用变量 `s2` 的值将字符串 `World` 插入到新的占位符 0 中：

```csharp
WriteLine("Hello, World");
```

#### DateTime 和数字格式

除了在占位符中使用字符串格式之外，还可以根据数据类型使用特定格式。我们先从日期开始。格式字符串跟在占位符内的表达式之后，用冒号分隔。这里展示的例子是 `DateTime` 类型的 `D` 和 `d` 格式：

```csharp
var day = new DateTime(2025, 2, 14);
WriteLine($"{day:D}");
WriteLine($"{day:d}");
```

结果显示，大写 `D` 对应长日期格式字符串，小写 `d` 对应短日期字符串：

```
Friday, February 14, 2025
2/14/2025
```

`DateTime` 类型会根据使用大写还是小写字符串而产生不同的输出。根据系统的语言设置，输出可能会有所不同。日期和时间是语言相关的。

`DateTime` 类型支持许多不同的标准格式字符串，以表示所有的日期和时间形式——例如，`t` 表示短时间格式，`T` 表示长时间格式，`g` 和 `G` 用于显示日期和时间。这里不讨论所有其他选项，因为可以在 MSDN 文档中找到 `DateTime` 类型的 `ToString` 方法的全部内容。

> **注意** 需要提到的一点是，为 `DateTime` 构建自定义格式字符串。自定义日期和时间格式字符串可以组合格式说明符，例如 `dd-MMM-yyyy`：

```csharp
WriteLine($"{day:dd-MMM-yyyy}");
```

> 结果如下所示：

```
14-Feb-2025
```

> 这个自定义格式字符串使用 `dd` 显示两位数的日期（如果日期在 10 号之前，这一点很重要；这里可以看到 `d` 和 `dd` 的区别），使用 `MMM` 显示月份的缩写名称（注意大写，`mm` 表示分钟），以及使用 `yyyy` 显示四位数的年份。同样，你可以在 MSDN 文档中找到自定义日期和时间格式字符串的所有其他格式说明符。

数字的格式字符串不区分大小写。让我们看看 `n`、`e`、`x` 和 `c` 标准数字格式字符串：

```csharp
int i = 2477;
WriteLine($"{i:n} {i:e} {i:x} {i:c}");
```

`n` 格式字符串定义了一种数字格式，显示带有组分隔符的整数和小数位；`e` 使用指数表示法；`x` 转换为十六进制；`c` 显示货币：

```
2,477.00 2.477000e+003 9ad $2,477.00
```

对于数字表示，你也可以使用自定义格式字符串。`#` 格式说明符是一个数字占位符，如果有数字则显示数字，否则不显示任何数字。`0` 格式说明符是一个零占位符，显示相应数字；如果不存在数字，则显示零。

```csharp
double d = 3.1415;
WriteLine($"{d:###.###}");
WriteLine($"{d:000.000}");
```

对于示例代码中的 `double` 值，第一个结果将逗号后的值四舍五入到三位数字；第二个结果还会显示逗号前的三位数字：

```
3.142
003.142
```

MSDN 文档提供了关于所有标准数字格式字符串的信息，涵盖百分比、往返和定点显示，以及用于指数值显示、小数点、组分隔符等不同外观的自定义格式字符串。

#### 自定义字符串格式

格式字符串不仅限于内置类型；你可以为自定义类型创建自己的格式字符串。只需实现 `IFormattable` 接口。

从一个简单的 `Person` 类开始，该类包含 `FirstName` 和 `LastName` 属性（代码文件 `StringFormats/Person.cs`）：

```
public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

为了对该类进行简单的字符串表示，需要重写基类的 `ToString` 方法。该方法返回由 `FirstName` 和 `LastName` 组成的字符串：

```
public override string ToString() => FirstName + " " + LastName;
```

除了简单的字符串表示之外，`Person` 类还应支持格式字符串 `F`（仅返回名字）、`L`（返回姓氏）以及 `A`（代表“all”，与 `ToString` 方法返回相同的字符串表示）。要实现自定义字符串，接口 `IFormattable` 定义了带有两个参数的 `ToString` 方法：一个用于格式的字符串参数和一个 `IFormatProvider` 参数。示例代码中未使用 `IFormatProvider` 参数。你可以根据区域性使用该参数实现不同的表示，因为 `CultureInfo` 类实现了此接口。
